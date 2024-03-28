### Low-01 Unnecessary code - `_amount` input argument is redundant
**Instances(1)**
In L1ERC20Bridge::`tranferTokenToSharedBridge` . `_amount` input argument is unnecessary because the function is intended to always transfer the entire balance of a token. 

The require statement `require(amount == _amount, "Incorrect amount");` can be removed as well.

```solidity
//code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol
    function tranferTokenToSharedBridge(
        address _token,
|>      uint256 _amount //@audit unnecessary code
    ) external {
        require(msg.sender == address(sharedBridge), "Not shared bridge");
        uint256 amount = IERC20(_token).balanceOf(address(this));
        require(amount == _amount, "Incorrect amount"); //@audit unnecessary code
        IERC20(_token).safeTransfer(address(sharedBridge), amount);
    }
```
(https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L66)

Recommendations:
Consider remove `_amount` argument and require `amount == _amount` to simply transfer the balance of `_token` if balance is non-zero.

### Low-02 Users cannot claim a failed deposit if they deposited in old L1ERC20Bridge with an l2batchnumber equal to or greater than `eraFirstPostUpgradeBatch`
**Instances(1)**
There is an edge case where a user might not be able to claim a failed deposit.

Scenario: The user has deposited an ERC20 token through the old L1ERC20Bridge.sol right before or during the migration process. 

The l2batchNumber of the user deposit might equal (or exceed) `eraFirstPostUpgradeBatch`. Note [eraFirstPostUpgradeBatch](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L111) is a pre-determined batch number to be used to initialize L1ShareBridge.sol. Because (1) `eraFirstPostUpgradeBatch` is pre-determined, (2)and the entire migration process might not finish within an atomic transaction (due to various contracts deployment, ERA-upgrade tx, and roughly 300 different erc20 funds migration process,etc), a deposit on the legacy L1ERC20Bridge.sol may be included in a batch number >= `eraFirstPostUpgradeBatch`.

In the above case, if the user's deposit fails on L2 for any reason. They are not able to claim the deposit on L1 post-migration. 

This is because the new L1ERC20Brdige.sol will pass the claimFailedDeposit control flow to L1SharedBridge::`claimFailedDeposit`. In `_claimFailedDeposit()`, `_isEraLegacyWithdrawal` will evaluate to false (if `_l2BatchNumber` >= `eraFirstPostUpgradeBatch`), this will cause `bool notCheckedInLegacyBridgeOrWeCanCheckDeposit` evaluates to true. In the if-body, `depositHappened[_chainId][_l2TxHash]` will be checked. However, because the user made the deposit in the old L1ERC20Bridge.sol (before [the last step of Migration](https://github.com/code-423n4/2024-03-zksync/blob/main/docs/Protocol%20Section/Migration%20process.md#introduction)), there is no record of this deposit in L1SharedBridge. User's `claimFailedDeposit()` will revert. The user cannot claim.
```solidity
//code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
    function _claimFailedDeposit(
        bool _checkedInLegacyBridge,
        uint256 _chainId, //@audit-info note: this is ERA_CHAIN_ID
        address _depositSender,
        address _l1Token,
        uint256 _amount,
        bytes32 _l2TxHash,
        uint256 _l2BatchNumber,
        uint256 _l2MessageIndex,
        uint16 _l2TxNumberInBatch,
        bytes32[] calldata _merkleProof
    ) internal nonReentrant {
...
        {
            bool notCheckedInLegacyBridgeOrWeCanCheckDeposit;
            {
                  //@audit if user 's made deposit through old L1ERC20Bridge, but the _l2BatchNumber >= eraFirstPostUpgradeBatch, notCheckedInLegacyBridgeOrWeCanCheckDeposit will return true
|>                bool weCanCheckDepositHere = !_isEraLegacyWithdrawal(
                    _chainId,
                    _l2BatchNumber
                );
                  //@audit even if the legacy bridge already checked the deposit, this might check the deposit in share bridge again. 
|>                notCheckedInLegacyBridgeOrWeCanCheckDeposit =
                    (!_checkedInLegacyBridge) ||
                    weCanCheckDepositHere;
            }
            if (notCheckedInLegacyBridgeOrWeCanCheckDeposit) {
                bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
                bytes32 txDataHash = keccak256(
                    abi.encode(_depositSender, _l1Token, _amount)
                );
                 //@audit in the above scenario, this check will fail because user's deposit has no record in L1SharedBridge if deposited in the old ERC20Bridge
 |>               require(dataHash == txDataHash, "ShB: d.it not hap");
                delete depositHappened[_chainId][_l2TxHash];
            }
}
```
(https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L333)
Edge case above will result in claiming failed deposit impossible on L1. 

Recommendations:
In L1SharedBridge::`_claimFaiedDeposit`, instead of `bool notCheckedInLegacyBridgeOrWeCanCheckDeposit`, consider refactoring the if control flow based on `bool _checkedInLegacyBridge`. 
(1) if `_checkedInLegacyBridge` is true, `depositAmount` record is already checked and deleted in L1ERC20Bridge, which means deposit is made through L1ERC20Bridge (either oldERC20 bridge or newERC20 bridge). We only need to delete `depositHappened[_chainId][_l2TxHash]` to prevent double claiming.
(2) if `_checkedInLegacyBridge` is false. Either deposit is made through new L1ERC20Bridge or made directly through L1SharedBridge. We check `depositHappened[_chainId][_l2TxHash]`  first, a) if dataHash matches, we confirm and delete `depositHappened[_chainId][_l2TxHash]` to prevent double claiming. b) if dataHash doesn't match or doesn't exist, we reject the claim. Either the deposit is made with old L1ERC20Bridge, which can be claimed from new L1ERC20Bridge (same as (1) flow), Or deposit already claimed, OR the deposit doesn't exist. 

### Low-03 Add checks to ensure that resetting admin-controlled parameters will not set the same old value (Not included in Bot report)
**Instances(3)**
In some instances, resetting admin-controlled parameters lacks checks to ensure the new value will not be the old value. Consider adding a check to ensure the state is only written when the new value differs.

(1)
```solidity
//code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol
    function setPendingAdmin(
        address _newPendingAdmin
    ) external onlyOwnerOrAdmin {
        // Save previous value into the stack to put it into the event later
        address oldPendingAdmin = pendingAdmin;
        // Change pending admin
        //@audit Add check to ensure newPendingAdmin is different from oldPendingAdmin before writing to storage
|>      pendingAdmin = _newPendingAdmin;
        emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
    }
```
(https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55)
(2)
```solidity
//code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
    function setPendingAdmin(
        address _newPendingAdmin
    ) external onlyOwnerOrAdmin {
        // Save previous value into the stack to put it into the event later
        address oldPendingAdmin = pendingAdmin;
        // Change pending admin
        //@audit Add check to ensure newPendingAdmin is different from oldPendingAdmin before writing to storage
|>      pendingAdmin = _newPendingAdmin;
        emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
    }
```
(https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L114)

(3)
```solidity
//code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
    function setNewVersionUpgrade(
        Diamond.DiamondCutData calldata _cutData,
        uint256 _oldProtocolVersion,
        uint256 _newProtocolVersion
    ) external onlyOwner {

        upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
        //@audit-info note: it didn't check the _newProtocolVersion is different from _oldProtocolVersion, only overwrite protocolVerision when _newProtocolVersion is different from current protocolVersion
 |>     protocolVersion = _newProtocolVersion;
    }
```
(https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L148)

Recommendations:
Consider adding if-condition to only overwrite state parameter when the new value differs from the current value.

### Low-04 Remove code that is intended for only testing purpose (Not included in bot report)
**Instances(1)**
The code below is intended only for testing purposes. Consider removing code that is only intended for testing.

```solidity
//code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
    function initialize(
        StateTransitionManagerInitializeData calldata _initializeData
    ) external reentrancyGuardInitializer {
...
        // While this does not provide a protection in the production, it is needed for local testing
        // Length of the L2Log encoding should not be equal to the length of other L2Logs' tree nodes preimages
|>      assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
...
```
(https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L106)

Recommendations:
Removing code intended only for testing.

### Low-05 State transition cannot be `unfreeze` by StateTransitionManager after `freeze` due to an error.
**Instances(1)**
A state transition (ST)'s `freezeDiamond()` or `unfreezeDiamond` is intended to be called by either StateTransitionManger or the admin of the state transition. However, there is an error in `unfreezeChain` on StateTransitionManager.sol that will prevent StateTransitionManger from unfreezing a chain when needed.

```solidity
//code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
    function unfreezeChain(uint256 _chainId) external onlyOwner {
          //@audit this should be `unfreezeDiamond()`. This error prevents StateTransitionManager from freezing a chain(ST) when needed.
|>        IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();
    }
```
(https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L166)

A state transition(ST) can be malicious. The hyperchain implementation is based on the assumption that StateTransitionManager(STM) is [the main point of trust](https://github.com/code-423n4/2024-03-zksync/blob/main/docs/Smart%20contract%20Section/L1%20ecosystem%20contracts.md#state-transition-manager-stm). This error prevents STM to exercise key control over ST to unfreeze an ST. If the ST admin is malicious and intends to freeze the chain for longer, STM won't be able to exercise intended control of the malicious ST.

```solidity
//code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol
      //@audit Due to error in StateTransitionManger, only ST admin can unfreeze the chain
|>    function unfreezeDiamond() external onlyAdminOrStateTransitionManager {
        Diamond.DiamondStorage storage diamondStorage = Diamond
            .getDiamondStorage();
        require(diamondStorage.isFrozen, "a7"); // diamond proxy is not frozen
        diamondStorage.isFrozen = false;
        emit Unfreeze();
    }
```
(https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L143) 

Recommendations:
In `unfreezeChain`, change to call `unfreezeDiamond()`.

### Low-06 Outdated comments - Change 'ETH' to base token
**Instances(1)**
The the hyperchain setup baseToken is used instead of `ETH`. However, in some cases, outdated comments are left. 
(1)
```solidity
//code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
    //@audit It should be L2 gas in baseToken, not ETH, because ST can have a non-eth baseToken, and this function to convert ETH price to baseToken denomination.
|>  /// @notice Derives the price for L2 gas in ETH to be paid.
    /// @param _l1GasPrice The gas price on L1
    /// @param _gasPerPubdata The price for each pubdata byte in L2 gas
    /// @return The price of L2 gas in ETH
    function _deriveL2GasPrice(
        uint256 _l1GasPrice,
        uint256 _gasPerPubdata
    ) internal view returns (uint256) {
...
```
(https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L152)

Recommendations:
Change 'ETH' to baseToken.

### Low-07 If an ST has a baseToken with a different decimal from ETH, `_deriveL2GasPrice` might return incorrect value due to rounding, causing gas incorrectly paid
**Instances(1)**
If an ST chain has a baseToken with a different decimal from ETH. The implementation in `_deriveL2GasPrice` might cause rounding errors.

For example, suppose 1 ETH = 0.1 baseToken (8 decimals), and current `_l1GasPrice` is 36 gwei/gas.

Current implementation: ` uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) / s.baseTokenGasPriceMultiplierDenominator;`

`l1GasPriceConverted` = 36e9 * 0.1*1e6/1e18 = 36e-4 -> 0 baseToken/gas
Note: the resulting `l1GasPriceConverted` will not be scaled and has to be in baseToken decimal because it is used directly to [multiply gas](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L271) for baseToken amount transfer.

In `_deriveL2GasPrice`, when `l1GasPriceConverted` round to 0. `batchOverheadBaseToken` and `pubdataPriceBaseToken` will return 0, L2 gas will be underestimated and underpaid.

```solidity
//code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
    function _deriveL2GasPrice(uint256 _l1GasPrice, uint256 _gasPerPubdata) internal view returns (uint256) {
...
|>      uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
            s.baseTokenGasPriceMultiplierDenominator;
        uint256 pubdataPriceBaseToken;
        if (feeParams.pubdataPricingMode == PubdataPricingMode.Rollup) {
            pubdataPriceBaseToken = L1_GAS_PER_PUBDATA_BYTE * l1GasPriceConverted;
        }

        uint256 batchOverheadBaseToken = uint256(feeParams.batchOverheadL1Gas) * l1GasPriceConverted;
...
```
(https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L159-L160)

Recommendations:
(1) Consider adding a scaling multiplier for a baseToken (2)Then, scaling up the converted gas price value and then scaling down before baseToken transfer.

### Low-08 Functions intended to be called by both chain Admin and StateTransitionManager can only be called by Admin
**Instances(3)**
There are functions in Admin.sol with `onlyAdminOrStateTransitionManager` modifier, which suggests they are intended to be called by both `admin` and StateTransitionManager.

However, StateTransitionManager.sol doesn't have methods or flows to call them, making these functions only callable by chain admin. In case that StateTransitionManger needs to intervene a local chain(perhaps malicious) to change parameters through these functions. 
(1)
```solidity
//code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol
    function changeFeeParams(
        FeeParams calldata _newFeeParams
    ) external onlyAdminOrStateTransitionManager {
...
        FeeParams memory oldFeeParams = s.feeParams;
        s.feeParams = _newFeeParams;
...
```
(https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L67)
(2)
```solidity
//code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol
    function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {
...
        s.baseTokenGasPriceMultiplierNominator = _nominator;
        s.baseTokenGasPriceMultiplierDenominator = _denominator;
...
```
(https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79)

Note that StateTransitionManager.sol doesn't have methods to directly invoke calls to these functions. Neither will StateTransitionManager calls these functions through an upgrade call(`_setChainIdUpgrade()`). 

(3)
```solidity
//code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol
    function setValidator(
        address _validator,
        bool _active
    ) external onlyStateTransitionManager {
        s.validators[_validator] = _active;
...
```
(https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L45)

Note that unlike (1)&(2), `s.validators` is set only once in (`_setChainIdUpgrade()`) as part of the initialization of the new chain. But `s.validators` cannot be updated again when needed and `setValidator` cannot be called by StateTransitionManager.

Recommendations:
Consider implementing direct call methods in StateTransitionManager.sol to callow STM controls when needed.






