## LOW Risk

| Number | Issue | Instances |
|--------|-------|-----------|
|[L-01]| Consider bounding input array length  | 1 |
|[L-02]| constructor/initialize function lacks parameter validation  | 5 |
|[L-03]| require() should be used instead of assert() | 5 |
|[L-04]| Unused/empty receive()/fallback() function | 4 |
|[L-05]| Low level calls to custom addresse   | 1 |
|[L-06]| Missing zero address check in functions with address parameters  | 14 |
|[L-07]| Some tokens may revert when zero value transfers are made   | 3 |
|[L-08]| Use of abi.encodePacked with dynamic types inside keccak256   | 5 |
|[L-09]| Using zero as a parameter   | 13 |
|[L-10]| Truncating block.timestamp can reduce the lifespan of a contract   | 2 |



## [L-01] Consider bounding input array length

The functions below take in an unbounded array, and make function calls for entries in the array. While the function will revert if it eventually runs out of gas, it may be a nicer user experience to require() that the length of the array is below some reasonable maximum, so that the user doesn't have to use up a full transaction's gas only to see that the transaction reverts.


```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

224  function _execute(Call[] calldata _calls) internal {
        for (uint256 i = 0; i < _calls.length; ++i) {
            (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
            if (!success) {
                // Propagate an error if the call fails.
                assembly {
                    revert(add(returnData, 0x20), mload(returnData))
                }
            }
        }
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L224-L234


## [L-02] constructor/initialize function lacks parameter validation

Constructors and initialization functions play a critical role in contracts by setting important initial states when the contract is first deployed before the system starts. The parameters passed to the constructor and initialization functions directly affect the behavior of the contract / protocol. If incorrect parameters are provided, the system may fail to run, behave abnormally, be unstable, or lack security. Therefore, it's crucial to carefully check each parameter in the constructor and initialization functions. If an exception is found, the transaction should be rolled back.

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

91  address _l1WethAddress,

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L91


### the _securityCouncil address consturctor parameter is not checked for address zero 

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

41   constructor(address _admin, address _securityCouncil, uint256 _minDelay) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L41


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

58  constructor(address _bridgehub) reentrancyGuardInitializer {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

55  constructor(address _initialOwner, uint32 _executionDelay) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55


```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

41  function initialize(address _owner) external reentrancyGuardInitializer {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L41


## [L-03] require() should be used instead of assert()

Prior to solidity version 0.8.0, hitting an assert consumes the remainder of the transaction's available gas rather than returning it, as require()/revert() do. assert() should be avoided even past solidity version 0.8.0 as its documentation https://docs.soliditylang.org/en/v0.8.14/control-structures.html#panic-via-assert-and-error-via-require states that "The assert function creates an error of type Panic(uint256). ... Properly functioning code should never create a Panic, not even on invalid external input. If this happens, then there is a bug in your contract which you should fix".


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

106  assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L106

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

426  assert(block.chainid != 1);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L426


```solidity
file: blob/main/code/system-contracts/contracts/DefaultAccount.sol

222 assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L222

```solidity
file: blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol

50   assert(_len != 1);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L50

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

51  assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L51

## [L-04] Unused/empty receive()/fallback() function

If the intention is for the Ether to be used, the function should call another function or emit an event, otherwise it should revert

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

262  receive() external payable {}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L262

```solidity
file: blob/main/code/system-contracts/contracts/DefaultAccount.sol

227  receive() external payable {
        // If the contract is called directly, behave like an EOA
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L227-L229


```solidity
file: blob/main/code/system-contracts/contracts/EmptyContract.sol

11  fallback() external payable {}

13  receive() external payable {}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/EmptyContract.sol#L11

## [L-05] Low level calls to custom addresses

Low-level calls (such as .call(), .delegatecall(), or .callcode()) in Solidity provide a way to interact with other contracts or addresses. However, when these calls are made to addresses that are provided as parameters or are not well-validated, they pose a significant security risk. Untrusted addresses might contain malicious code leading to unexpected behavior, loss of funds, or vulnerabilities.

Resolution: Prefer using high-level Solidity function calls or interface-based interactions with known contracts to ensure security. If low-level calls are necessary, rigorously validate the addresses and test all possible interactions. Implementing additional checks and fail-safes can help mitigate potential risks associated with low-level calls.



```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

278  function _initializeDiamondCut(address _init, bytes memory _calldata) private {
        if (_init == address(0)) {
            require(_calldata.length == 0, "H"); // Non-empty calldata for zero address
        } else {
            // Do not check whether `_init` is a contract since later we check that it returns data.
            (bool success, bytes memory data) = _init.delegatecall(_calldata);
            if (!success) {
                // If the returndata is too small, we still want to produce some meaningful error
                if (data.length <= 4) {
                    revert("I"); // delegatecall failed
                }

                assembly {
                    revert(add(data, 0x20), mload(data))
                }
            }

            // Check that called contract returns magic value to make sure that contract logic
            // supposed to be used as diamond cut initializer.
            require(data.length == 32, "lp");
            require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1");
        }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L278-L299

## [L-06] Missing zero address check in functions with address parameters

Adding a zero address check for each address type parameter can prevent errors.

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

177  function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {

239  function createNewChain(
        uint256 _chainId,
        address _baseToken,
        address _sharedBridge,
        address _admin,
        bytes calldata _diamondCut
    ) external onlyBridgehub {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

75  function l2TokenAddress(address _l1Token) external view returns (address) {

98  function deposit(
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte
    ) external payable returns (bytes32 l2TxHash) {

160 function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L75

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

148  function bridgehubDepositBaseToken(
        uint256 _chainId,
        address _prevMsgSender,
        address _l1Token,
        uint256 _amount
    ) external payable virtual onlyBridgehubOrEra(_chainId) {

173  function _depositFunds(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {

182 function bridgehubDeposit(
        uint256 _chainId,
        address _prevMsgSender,
        uint256, // l2Value, needed for Weth deposits in the future
        bytes calldata _data
    ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
     
243 function _getDepositL2Calldata(
        address _l1Sender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount
    ) internal view returns (bytes memory) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L148-L153


```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

114  function createNewChain(
        uint256 _chainId,
        address _stateTransitionManager,
        address _baseToken,
        uint256, //_salt
        address _admin,
        bytes calldata _initData
    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114-L122


```solidity
file: blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

28  function applyL1ToL2Alias(address l1Address) internal pure returns (address l2Address) {

38  function undoL1ToL2Alias(address l2Address) internal pure returns (address l1Address) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L28


```solidity
file: blob/main/code/system-contracts/contracts/ContractDeployer.sol

309   function _storeConstructingByteCodeHashOnAddress(address _newAddress, bytes32 _bytecodeHash) internal {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L309

```solidity
file: blob/main/code/system-contracts/contracts/SystemContext.sol

99  function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#99


## [L-07] Some tokens may revert when zero value transfers are made

In spite of the fact that EIP-20 states https://github.com/ethereum/EIPs/blob/46b9b698815abbfa628cd1097311deee77dd45c5/EIPS/eip-20.md?plain=1#L116 that zero-valued transfers must be accepted, some tokens, such as LEND will revert if this is attempted, which may cause transactions that involve other tokens (such as batch operations) to fully revert. Consider skipping the transfer if the amount is zero, which will also save gas.



```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

67  IERC20(_token).safeTransfer(address(sharedBridge), amount);

162 _token.safeTransferFrom(_from, address(sharedBridge), _amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67


```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

175  _token.safeTransferFrom(_from, address(this), _amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175



## [L-08] Use of abi.encodePacked with dynamic types inside keccak256

abi.encodePacked should not be used with dynamic types when passing the result to a hash function such as keccak256. Use abi.encode instead, which will pad items to 32 bytes, to prevent any hash collisions.

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

460  keccak256(
                    abi.encodePacked(
                        _prevBatchCommitment,
                        _currentBatchCommitment,
                        _verifierParams.recursionNodeLevelVkHash,
                        _verifierParams.recursionLeafLevelVkHash
                    )
                )

654  blobCommitments[versionedHashIndex] = keccak256(
                abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
            );

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L460-L467

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

112   bytes32 hashedLog = keccak256(
            abi.encodePacked(_log.l2ShardId, _log.isService, _log.txNumberInBatch, _log.sender, _log.key, _log.value)
        );

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L112-L115


```solidity
file:

95   bytes32 hashedLog = keccak256(
            abi.encodePacked(
                _l2ToL1Log.l2ShardId,
                _l2ToL1Log.isService,
                _l2ToL1Log.txNumberInBlock,
                _l2ToL1Log.sender,
                _l2ToL1Log.key,
                _l2ToL1Log.value
            )
        );

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#Ls95-L104

```solidity
file: blob/main/code/system-contracts/contracts/SystemContext.sol

234  return keccak256(abi.encodePacked(uint32(_blockNumber)));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L134

## [L‑09] Using zero as a parameter

Taking 0 as a valid argument in Solidity without checks can lead to severe security issues. A historical example is the infamous 0x0 address bug where numerous tokens were lost. This happens because '0' can be interpreted as an uninitialized address, leading to transfers to the '0x0' address, effectively burning tokens. Moreover, 0 as a denominator in division operations would cause a runtime exception. It's also often indicative of a logical error in the caller's code. It's important to always validate input and handle edge cases like 0 appropriately. Use require() statements to enforce conditions and provide clear error messages to facilitate debugging and safer code.


```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

358  callSuccess := call(gas(), _depositSender, _amount, 0, 0, 0, 0)

447  callSuccess := call(gas(), l1Receiver, amount, 0, 0, 0, 0)

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L358

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

90  IExecutor.StoredBatchInfo memory batchZero = IExecutor.StoredBatchInfo(
            0,
            _initializeData.genesisBatchHash,
            _initializeData.genesisIndexRepeatedStorageChanges,
            0,
            EMPTY_STRING_KECCAK,
            DEFAULT_L2_LOGS_TREE_ROOT_HASH,
            0,
            _initializeData.genesisBatchCommitment
        );
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L90-L98


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

229  calldatacopy(0, 0, calldatasize())

231  let result := call(gas(), contractAddress, 0, 0, calldatasize(), 0, 0)

235   returndatacopy(0, 0, size)

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L229


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

43  returndatacopy(ptr, 0, size)

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L43

```solidity
file: blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol

208  success := call(_address, callAddr, 0, 0, _whoToMimic, 0, 0)

224  returndatacopy(add(returnData, 0x20), 0, size)

235  returndatacopy(0, 0, size)

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L208


```solidity
file: blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol

66  addr := staticcall(0, callAddr, 0, 0xFFFF, 0, 0)

77  pop(staticcall(0, callAddr, 0, 0xFFFF, 0, 0))

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L66

## [L-10] Truncating block.timestamp can reduce the lifespan of a contract

Consider removing the casting to extend the lifespan of these contracts.

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

115   uint32 timestamp = uint32(block.timestamp);

134   uint32 timestamp = uint32(block.timestamp);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L115