# QA Report

##

## [L-1] Unclaimable Failed Deposits Due to Insufficient _l1Token Balances in Specific Chains

### Impact

The issue arises in the _claimFailedDeposit function during the process of handling failed deposit claims. The function checks whether the chain has sufficient funds to cover the claim only when hyperbridging is disabled (!hyperbridgingEnabled[_chainId]). If the chain lacks enough funds (chainBalance[_chainId][_l1Token] < _amount), the transaction will revert, leaving the user unable to claim their failed deposit. This behavior could potentially lock user funds in scenarios where the chain balance is insufficient, as the function does not offer an alternative mechanism for users to recover their funds.


```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1ERC20Bridge.sol

/// @dev Withdraw funds from the initiated deposit, that failed when finalizing on L2.
    /// @param _depositSender The address of the deposit initiator
    /// @param _l1Token The address of the deposited L1 ERC20 token
    /// @param _l2TxHash The L2 transaction hash of the failed deposit finalization
    /// @param _l2BatchNumber The L2 batch number where the deposit finalization was processed
    /// @param _l2MessageIndex The position in the L2 logs Merkle tree of the l2Log that was sent with the message
    /// @param _l2TxNumberInBatch The L2 transaction number in a batch, in which the log was sent
    /// @param _merkleProof The Merkle proof of the processing L1 -> L2 transaction with deposit finalization
    function claimFailedDeposit(
        address _depositSender,
        address _l1Token,
        bytes32 _l2TxHash,
        uint256 _l2BatchNumber,
        uint256 _l2MessageIndex,
        uint16 _l2TxNumberInBatch,
        bytes32[] calldata _merkleProof
    ) external nonReentrant {
        uint256 amount = depositAmount[_depositSender][_l1Token][_l2TxHash];
        require(amount != 0, "2T"); // empty deposit
        delete depositAmount[_depositSender][_l1Token][_l2TxHash];

        sharedBridge.claimFailedDepositLegacyErc20Bridge(
            _depositSender,
            _l1Token,
            amount,
            _l2TxHash,
            _l2BatchNumber,
            _l2MessageIndex,
            _l2TxNumberInBatch,
            _merkleProof
        );
        emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L168C5-L200C6

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1SharedBridge.sol

 if (!hyperbridgingEnabled[_chainId]) {
            // check that the chain has sufficient balance
            require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
            chainBalance[_chainId][_l1Token] -= _amount;
        }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L347-L351

Mitigation Steps : 
Introduce a data structure to queue claims that cannot be immediately processed due to insufficient chain balance.

##

## [L-2] ``require(block.timestamp >= commitBatchTimestamp + delay, "5c")`` check always true when ``commitBatchTimestamp`` is 0

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition
/ValidatorTimelock.sol

unchecked {
            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
                    _newBatchesData[i].batchNumber
                );

                // Note: if the `commitBatchTimestamp` is zero, that means either:
                // * The batch was committed, but not through this contract.
                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
                // We allow executing such batches.

                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
            }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195

##

## [L-3] Mismatch Between ``tranferTokenToSharedBridge()`` and documented functionality

The function name ``tranferTokenToSharedBridge`` is missing an ``s``, making it an incorrect spelling of the intended action, which is ``transfer``.

Smart contracts where precision is crucial, every character matters. A typo can lead to misunderstandings or, in worse cases, the malfunction of contract execution if the function name is called or referenced elsewhere with the correct spelling.

```diff
FILE: https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

62: /// @dev transfer token to shared bridge as part of upgrade
- 63:    function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
+ 63:    function transferTokenToSharedBridge(address _token, uint256 _amount) external {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L63

## 

## [L-4] Mismatch between comment and the actual implementation

- ``Comment Description`` : The comment ``/// @dev transfer token to shared bridge as part of upgrade`` suggests that the function is designed to transfer a specified amount of tokens to the shared bridge, presumably as part of a smart contract upgrade process. The comment implies flexibility in the amount of tokens to be transferred.

- ``Actual Implementation``: The actual code, however, does not align with this flexibility. Instead of transferring the amount specified by the caller ``(_amount)``, the function transfers the entire balance of tokens held by the contract ``(amount = IERC20(_token).balanceOf(address(this)))``. Furthermore, the function enforces that this total balance must match the ``_amount`` specified by the caller, which effectively restricts the transfer to only the total balance rather than allowing a specific, potentially partial, amount.

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1ERC20Bridge.sol

/// @dev transfer token to shared bridge as part of upgrade
    function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
        require(msg.sender == address(sharedBridge), "Not shared bridge");
        uint256 amount = IERC20(_token).balanceOf(address(this));
        require(amount == _amount, "Incorrect amount");
        IERC20(_token).safeTransfer(address(sharedBridge), amount);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L62-L68

### Recommended Mitigation

- Align the Comment to the Actual Code (Only Full Balance Transfers)

```solidity

/// @dev Transfers the entire token balance to the shared bridge as part of an upgrade, ensuring no partial token transfers.
function transferTokenToSharedBridge(address _token, uint256 _amount) external {
    require(msg.sender == address(sharedBridge), "Not shared bridge");
    uint256 amount = IERC20(_token).balanceOf(address(this));
    require(amount == _amount, "Incorrect amount");
    IERC20(_token).safeTransfer(address(sharedBridge), amount);
}

```

## 

## [L-5] Typo Error

The comment /// @dev tranfer tokens... contains a spelling mistake: tranfer should be transfer.

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1SharedBridge.sol

- 115: /// @dev tranfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process
+ 115: /// @dev transfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L115

##

## [L-6] No same value input check

There is no check to ensure that the new pending admin (_newPendingAdmin) is different from the current pending admin (s.pendingAdmin). This means that if the function is called with the same value as the current pendingAdmin, it would still execute and emit an event, wasting gas and potentially causing confusion.

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 /// @inheritdoc IAdmin
    function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {
        // Save previous value into the stack to put it into the event later
        address oldPendingAdmin = s.pendingAdmin;
        // Change pending admin
        s.pendingAdmin = _newPendingAdmin;
        emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L23-L29

##

## [L-7] Allowance of redundant validator status assignments 

The absence of a check to see if _validator is already set to ``_active`` means the function will execute and emit an event even if there is no actual change in status. This can lead to unnecessary gas expenditure and redundant event logs, which could clutter up the event history and potentially confuse off-chain systems or services monitoring these events.

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

/// @inheritdoc IAdmin
    function setValidator(address _validator, bool _active) external onlyStateTransitionManager {
        s.validators[_validator] = _active;
        emit ValidatorStatusUpdate(_validator, _active);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L44-L48

##

## [L-8] Emit events for critical changes 

This is a critical aspect of smart contract development, especially for functions that involve significant changes to the contract's operation or state. Emitting events helps in tracking the changes and is crucial for transparency and auditability.

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition
/ValidatorTimelock.sol

/// @dev Set new validator address.
 function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {
        stateTransitionManager = _stateTransitionManager;
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L72

##

## [L-9] Misleading comment in ``setStateTransitionManager()`` function

Update the comment to accurately reflect the function's purpose. It could be like ``/// @dev Sets a new state transition manager``. The current comment suggests this function used for setting new address validator ``/// @dev Set new validator address.``

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition
/ValidatorTimelock.sol

- /// @dev Set new validator address.
+ /// @dev Sets a new state transition manager.
    function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {
        stateTransitionManager = _stateTransitionManager;
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L72





