### Low Risk Issues

## [L-1] Owner can renounce Ownership
Each of the following contracts implements or inherits the `renounceOwnership()` function. This can represent a certain risk if the ownership is renounced for any other reason than by design. Renouncing ownership will leave the contract without an owner, thereby removing any functionality that is only available to the owner.

**Total Instances:** 5

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 30: contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L30

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 16: contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L16

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 20: contract Governance is IGovernance, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L20

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 25: contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L25

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 22: contract ValidatorTimelock is IExecutor, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L22


## [L-2] Addition/multiplication in `unchecked` block is unsafe
The additions/multiplications may silently overflow because they’re in `unchecked` blocks with no preceding value checks, which may lead to unexpected results.

**Total Instances:** 25

```solidity
File: contracts/ethereum/contracts/common/libraries/UncheckedMath.sol

 13:             return _number + 1;

 19:             return _lhs + _rhs;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L13

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 195:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

 217:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

 27:             uint256 bitOffset = (_index & 7) * 32;

 48:             uint256 bitOffset = (_index & 7) * 32;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L27

```solidity
File: contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

 30:             l2Address = address(uint160(l1Address) + offset);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L30

```solidity
File: contracts/zksync/contracts/vendor/AddressAliasHelper.sol

 30:             l2Address = address(uint160(l1Address) + offset);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L30

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol

 105:             uint256 listLength = encodedNonce.length +

 198:             uint256 listLength = encodedFixedLengthParams.length +

 293:             uint256 listLength = encodedFixedLengthParams.length +

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L105

```solidity
File: system-contracts/contracts/Compressor.sol

 52:                 encodedData.length * 4 == _bytecode.length,
                    "Encoded data length should be 4 times shorter than the original bytecode"
                );
    
                require(
                    dictionary.length / 8 <= encodedData.length / 2,
                    "Dictionary should have at most the same number of entries as the encoded data"
                );
    
                for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
                    uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
                    require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");
    
                    uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);
                    uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

 203:             dictionary = _rawCompressedData[2:2 + dictionaryLen * 8];
                 encodedData = _rawCompressedData[2 + dictionaryLen * 8:];

 233:                     _initialValue + convertedValue == _finalValue,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L52

```solidity
File: system-contracts/contracts/L1Messenger.sol

 140:             pubdataLen = 4 + _message.length + L2_TO_L1_LOG_SERIALIZE_SIZE;

 171:             pubdataLen = 4 + bytecodeLen;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L140

```solidity
File: system-contracts/contracts/NonceHolder.sol

 72:             rawNonces[addressAsKey] = (oldRawNonce + _value);

 118:             rawNonces[addressAsKey] = oldRawNonce + 1;

 144:             rawNonces[addressAsKey] = (oldRawNonce + DEPLOY_NONCE_MULTIPLIER);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L72

```solidity
File: system-contracts/contracts/libraries/RLPEncoder.sol

 33:                 encoded = new bytes(hbs + 2);
                    encoded[0] = bytes1(uint8(hbs + 0x81));

 68:                 encoded = new bytes(hbs + 2);
                    encoded[0] = bytes1(uint8(_offset + hbs + 56));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L33

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 190:             uint256 listLength = encodedNonce.length +

 265:             uint256 listLength = encodedFixedLengthParams.length +

 337:             uint256 listLength = encodedFixedLengthParams.length +

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L190

```solidity
File: system-contracts/contracts/libraries/Utils.sol

 46:             codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L46


## [L-3] Array is `push()ed` but not `pop()ed`
Array entries are added but are never removed. Consider whether this should be the case, or whether there should be a maximum, or whether old entries should be removed. Cases where there are specific potential problems will be flagged separately under a different issue.

**Total Instances:** 2

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 196:             ds.facets.push(_facet);

 223:         ds.facetToSelectors[_facet].selectors.push(_selector);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L223


## [L-4] Code does not follow the best practice of check-effects-interaction
Code should follow the best-practice of [check-effects-interaction](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs.

**Total Instances:** 6

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 /// @audit  transferEthToSharedBridge() prior to this assignment
 122:             chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =

 /// @audit  balanceOf() prior to this assignment
 133:             chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;

 /// @audit  balanceOf() prior to this assignment
 133:             chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L122

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 /// @audit  StoredBatchInfo() prior to this assignment
 100:         storedBatchZero = keccak256(abi.encode(batchZero));

 /// @audit  StoredBatchInfo() prior to this assignment
 102:         initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 /// @audit  owner() prior to this assignment
 124:         availableGetters = _availableGetters;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L124


## [L-5] Consider implementing two-step procedure for updating protocol addresses
A copy-paste error or a typo may end up bricking protocol functionality, or sending tokens to an address with no known private key. Consider implementing a two-step procedure for updating protocol addresses, where the recipient is set as pending, and must "accept" the assignment by making an affirmative call. A straight forward way of doing this would be to have the target contracts implement [EIP-165](https://eips.ethereum.org/EIPS/eip-165), and to have the "set" functions ensure that the recipient is of the right interface type.

**Total Instances:** 17

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 51:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

 108:     function setSharedBridge(address _sharedBridge) external onlyOwner {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L51

```solidity
File: contracts/ethereum/contracts/bridgehub/IBridgehub.sol

 53:     function setPendingAdmin(address _newPendingAdmin) external;

 131:     function setSharedBridge(address _sharedBridge) external;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L53

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 256:     function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L256

```solidity
File: contracts/ethereum/contracts/governance/IGovernance.sol

 65:     function updateSecurityCouncil(address _newSecurityCouncil) external;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/IGovernance.sol#L65

```solidity
File: contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

 48:     function setPendingAdmin(address _newPendingAdmin) external;

 69:     function setValidatorTimelock(address _validatorTimelock) external;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L48

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 110:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

 132:     function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L110

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 23:     function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {

 45:     function setValidator(address _validator, bool _active) external onlyStateTransitionManager {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L23

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol

 17:     function setPendingAdmin(address _newPendingAdmin) external;

 25:     function setValidator(address _validator, bool _active) external;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L17

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

 34:     function setImmutables(address _dest, ImmutableData[] calldata _immutables) external override {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L34

```solidity
File: system-contracts/contracts/SystemContext.sol

 99:     function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L99

```solidity
File: system-contracts/contracts/interfaces/IImmutableSimulator.sol

 13:     function setImmutables(address _dest, ImmutableData[] calldata _immutables) external;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IImmutableSimulator.sol#L13


## [L-6] Empty `receive()`/`fallback()` function
If the intention is for Ether sent by a caller to be used for an actual purpose (i.e. the function is not just a WETH `withdraw()` handler), the function should call another function (e.g. call `weth.deposit()` and use the token on the caller’s behalf) or at least emit an event to track that funds were sent directly to it.

**Total Instances:** 4

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 262:     receive() external payable {}

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L262

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 227:     receive() external payable {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L227

```solidity
File: system-contracts/contracts/EmptyContract.sol

 11:     fallback() external payable {}

 13:     receive() external payable {}

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/EmptyContract.sol#L13


## [L-7] Gas griefing/theft is possible on an unsafe external call
'A low-level call will copy any amount of bytes to local memory. When bytes are copied from returndata to memory, the memory expansion cost is paid. This means that when using a standard solidity call, the callee can 'returnbomb' the caller, imposing an arbitrary gas cost. Because this gas is paid by the caller and in the caller's context, it can cause the caller to run out of gas and halt execution.Consider replacing all unsafe `call` with `excessivelySafeCall` from this [repository](https://github.com/nomad-xyz/ExcessivelySafeCall).'

**Total Instances:** 1

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 /// @audit  _execute()
 226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226


## [L-8] External function calls within loops
Calling external functions within loops can easily result in insufficient gas. This greatly increases the likelihood of transaction failures, DOS attacks, and other unexpected actions. It is recommended to limit the number of loops within loops that call external functions, and to limit the gas line for each external call.

**Total Instances:** 1

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226


## [L-9] File allows a version of solidity that is susceptible to .selector-related optimizer bug
'In solidity versions prior to 0.8.21, there is a legacy code generation [bug](https://soliditylang.org/blog/2023/07/19/missing-side-effects-on-selector-access-bug/) where if `foo().selector` is called, `foo()` doesn't actually get evaluated. It is listed as low-severity, because projects usually use the contract name rather than a function call to look up the selector.'

**Total Instances:** 15

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 504:         if (bytes4(functionSignature) == IMailbox.finalizeEthWithdrawal.selector) {

 509:         } else if (bytes4(functionSignature) == IL1ERC20Bridge.finalizeWithdrawal.selector) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L504

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 262:             IDiamondInit.initialize.selector,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L262

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 145:         return abi.encodePacked(IL1ERC20Bridge.finalizeWithdrawal.selector, _to, _l1Token, _amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L145

```solidity
File: contracts/zksync/contracts/interfaces/IPaymaster.sol

 12: bytes4 constant PAYMASTER_VALIDATION_SUCCESS_MAGIC = IPaymaster.validateAndPayForPaymasterTransaction.selector;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L12

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 144:                 selector == DEPLOYER_SYSTEM_CONTRACT.create.selector ||

 145:                 selector == DEPLOYER_SYSTEM_CONTRACT.create2.selector ||

 146:                 selector == DEPLOYER_SYSTEM_CONTRACT.createAccount.selector ||

 147:                 selector == DEPLOYER_SYSTEM_CONTRACT.create2Account.selector;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L144

```solidity
File: system-contracts/contracts/L2BaseToken.sol

 113:         return abi.encodePacked(IMailbox.finalizeEthWithdrawal.selector, _to, _amount);

 123:         return abi.encodePacked(IMailbox.finalizeEthWithdrawal.selector, _to, _amount, _sender, _additionalData);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L113

```solidity
File: system-contracts/contracts/interfaces/IAccount.sol

 7: bytes4 constant ACCOUNT_VALIDATION_SUCCESS_MAGIC = IAccount.validateTransaction.selector;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IAccount.sol#L7

```solidity
File: system-contracts/contracts/interfaces/IPaymaster.sol

 12: bytes4 constant PAYMASTER_VALIDATION_SUCCESS_MAGIC = IPaymaster.validateAndPayForPaymasterTransaction.selector;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPaymaster.sol#L12

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 366:         if (paymasterInputSelector == IPaymasterFlow.approvalBased.selector) {

 385:         } else if (paymasterInputSelector == IPaymasterFlow.general.selector) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L385


## [L-10] Function can return unassigned variable
Make sure that functions with a return value always return a valid and assigned value. Even if the default value is as expected, it should be assigned with the default value for code clarity and to reduce confusion.

**Total Instances:** 4

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 /// @audit  _chainId is unassigned!
 146:         return _chainId;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L146

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 /// @audit  decimals_ is unassigned!
 174:         return decimals_;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L174

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol

 /// @audit  EMPTY_STRING_KECCAK is unassigned!
 94:             return EMPTY_STRING_KECCAK;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L94

```solidity
File: system-contracts/contracts/NonceHolder.sol

 /// @audit  deploymentNonce is unassigned!
 129:         return deploymentNonce;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L129


## [L-11] Functions calling contracts/addresses with transfer hooks should be protected by reentrancy guard
Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks opens the users of this protocol up to [read-only reentrancy vulnerability](https://chainsecurity.com/curve-lp-oracle-manipulation-post-mortem/) with no way to protect them except by block-listing the entire protocol.

**Total Instances:** 1

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 67:         IERC20(_token).safeTransfer(address(sharedBridge), amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67


## [L-12] Governance functions should be controlled by time locks
Governance functions (such as upgrading contracts, setting critical parameters) should be controlled using time locks to introduce a delay between a proposal and its execution. This gives users time to exit before a potentially dangerous or malicious operation is applied.

**Total Instances:** 15

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 51:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

 108:     function setSharedBridge(address _sharedBridge) external onlyOwner {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L51

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 249:     function updateDelay(uint256 _newDelay) external onlySelf {

 256:     function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L249

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 110:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

 132:     function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {

 137:     function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {

 142:     function setNewVersionUpgrade(
             Diamond.DiamondCutData calldata _cutData,
             uint256 _oldProtocolVersion,
             uint256 _newProtocolVersion
         ) external onlyOwner {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L110

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 73:     function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {

 96:     function setExecutionDelay(uint32 _executionDelay) external onlyOwner {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L73

```solidity
File: system-contracts/contracts/SystemContext.sol

 84:     function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {

 99:     function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {

 105:     function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {

 112:     function setPubdataInfo(uint256 _gasPerPubdataByte, uint256 _basePubdataSpent) external onlyCallFromBootloader {

 444:     function setNewBatch(
             bytes32 _prevBatchHash,
             uint128 _newTimestamp,
             uint128 _expectedNewNumber,
             uint256 _baseFee
         ) external onlyCallFromBootloader {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L444



## [L-13] Missing checks for `address(0x0)` in the constructor
'Constructors often take address parameters to initialize important components of a contract, such as owner or linked contracts. However, without a checking, there's a risk that an address parameter could be mistakenly set to the zero address (0x0). This could be due to an error or oversight during contract deployment. A zero address in a crucial role can cause serious issues, as it cannot perform actions like a normal address, and any funds sent to it will be irretrievable. It's therefore crucial to include a zero address check in constructors to prevent such potential problems. If a zero address is detected, the constructor should revert the transaction.'

**Total Instances:** 4

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 /// @audit  _l1WethAddress not checked!
 90:     constructor(
            address _l1WethAddress,
            IBridgehub _bridgehub,
            IL1ERC20Bridge _legacyBridge
        ) reentrancyGuardInitializer {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 /// @audit  _securityCouncil not checked!
 41:     constructor(address _admin, address _securityCouncil, uint256 _minDelay) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L41

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 /// @audit  _bridgehub not checked!
 58:     constructor(address _bridgehub) reentrancyGuardInitializer {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 /// @audit  _initialOwner not checked!
 55:     constructor(address _initialOwner, uint32 _executionDelay) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55


## [L-14] Missing checks for `address(0x0)` in the initializer
Consider adding a zero address check for address type variables in the initializer

**Total Instances:** 1

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 /// @audit  _owner not checked!
 41:     function initialize(address _owner) external reentrancyGuardInitializer {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L41


## [L-15] Missing checks for address(0x0) when updating address state variables
Consider adding a zero address check when updating address state variables.

**Total Instances:** 14

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 143:         l2BridgeAddress[_chainId] = _l2BridgeAddress;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L143

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 55:         pendingAdmin = _newPendingAdmin;

 109:         sharedBridge = IL1SharedBridge(_sharedBridge);

 134:         stateTransitionManager[_chainId] = _stateTransitionManager;

 135:         baseToken[_chainId] = _baseToken;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 258:         securityCouncil = _newSecurityCouncil;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L258

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 114:         pendingAdmin = _newPendingAdmin;

 133:         validatorTimelock = _validatorTimelock;

 234:         stateTransition[_chainId] = _stateTransitionContract;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L114

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 27:         s.pendingAdmin = _newPendingAdmin;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L27

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 60:         l1Bridge = _l1Bridge;

 99:             l1TokenAddress[expectedL2Token] = _l1Token;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L60

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 52:         l1Address = _l1Address;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L52

```solidity
File: system-contracts/contracts/SystemContext.sol

 100:         origin = _newOrigin;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L100


## [L-16] Missing contract-existence checks before low-level calls
Low-level calls return success if there is no code present at the specified address. In addition to the zero-address checks, add a check to verify that `<address>.code.length > 0`

**Total Instances:** 5

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 612:         (bool success, bytes memory data) = POINT_EVALUATION_PRECOMPILE_ADDR.staticcall(precompileInput);

 680:         (bool success, bytes memory data) = s.blobVersionedHashRetriever.staticcall(abi.encode(_index));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L612

```solidity
File: system-contracts/contracts/GasBoundCaller.sol

 57:         bytes memory returnData = EfficientCall.call(gasleft(), _to, msg.value, _data, false);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L57

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol

 63:             (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call(

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L63


## [L-17] Missing contract-existence checks before yul `call()`
Low-level calls return success if there is no code present at the specified address. In addition to the zero-address checks, add a check to verify that `extcodesize()` is non-zero.

**Total Instances:** 15

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 358:                 callSuccess := call(gas(), _depositSender, _amount, 0, 0, 0, 0)

 447:                 callSuccess := call(gas(), l1Receiver, amount, 0, 0, 0, 0)

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L358

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 231:             let result := call(gas(), contractAddress, 0, 0, calldatasize(), 0, 0)

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L231

```solidity
File: contracts/zksync/contracts/SystemContractsCaller.sol

 62:                 success := call(to, callAddr, 0, 0, farCallAbi, 0, 0)

 71:                 success := call(msgValueSimulator, callAddr, value, to, farCallAbi, forwardMask, 0)

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L62

```solidity
File: system-contracts/contracts/libraries/EfficientCall.sol

 136:                 success := call(_address, callAddr, 0, 0, 0xFFFF, 0, 0)

 149:                 success := call(msgValueSimulator, callAddr, _value, _address, 0xFFFF, forwardMask, 0)

 208:             success := call(_address, callAddr, 0, 0, _whoToMimic, 0, 0)

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L136

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol

 55:             let success := call(_isService, callAddr, _key, _value, 0xFFFF, 0, 0)

 174:             success := call(0, callAddr, _value, 0, 0xFFFF, 0, 0)

 184:             pop(call(initializer, callAddr, value1, 0, 0xFFFF, 0, 0))

 194:             pop(call(value1, callAddr, value2, 0, 0xFFFF, 0, 0))

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L55

```solidity
File: system-contracts/contracts/libraries/SystemContractsCaller.sol

 101:                 success := call(to, callAddr, 0, 0, farCallAbi, 0, 0)

 110:                 success := call(msgValueSimulator, callAddr, value, to, farCallAbi, forwardMask, 0)

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L101

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 400:             success := call(gas(), bootloaderAddr, amount, 0, 0, 0, 0)

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L400


## [L-18] `onlyOwner` functions not accessible if `owner` renounces ownership
 'The owner is able to perform certain privileged activities, but it's possible to set the owner to address(0). This can represent a certain risk if the ownership is renounced for any other reason than by design. Renouncing ownership will leave the contract without an owner, therefore limiting any functionality that needs authority.'

**Total Instances:** 17

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 116:     function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {

 142:     function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L116

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 82:     function addStateTransitionManager(address _stateTransitionManager) external onlyOwner {

 92:     function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner {

 101:     function addToken(address _token) external onlyOwner {

 108:     function setSharedBridge(address _sharedBridge) external onlyOwner {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L82

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 129:     function scheduleTransparent(Operation calldata _operation, uint256 _delay) external onlyOwner {

 142:     function scheduleShadow(bytes32 _id, uint256 _delay) external onlyOwner {

 154:     function cancel(bytes32 _id) external onlyOwner {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L129

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 137:     function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {

 142:     function setNewVersionUpgrade(
             Diamond.DiamondCutData calldata _cutData,
             uint256 _oldProtocolVersion,
             uint256 _newProtocolVersion
         ) external onlyOwner {

 152:     function setUpgradeDiamondCut(
             Diamond.DiamondCutData calldata _cutData,
             uint256 _oldProtocolVersion
         ) external onlyOwner {

 160:     function freezeChain(uint256 _chainId) external onlyOwner {

 165:     function unfreezeChain(uint256 _chainId) external onlyOwner {

 230:     function registerAlreadyDeployedStateTransition(
             uint256 _chainId,
             address _stateTransitionContract
         ) external onlyOwner {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L137

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 73:     function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {

 96:     function setExecutionDelay(uint32 _executionDelay) external onlyOwner {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96


## [L-19] `receive()`/`payable fallback()` function does not authorize requests
Having no access control on the function (e.g. `require(msg.sender == address(weth))`) means that someone may send Ether to the contract, and have no way to get anything back out, which is a loss of funds. If the concern is having to spend a small amount of gas to check the sender against an immutable address, the code should at least have a function to rescue mistakenly-sent Ether.

**Total Instances:** 5

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 262:     receive() external payable {}

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L262

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

 20:     fallback() external payable {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L20

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 227:     receive() external payable {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L227

```solidity
File: system-contracts/contracts/EmptyContract.sol

 11:     fallback() external payable {}

 13:     receive() external payable {}

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/EmptyContract.sol#L13


## [L-20] `require()` should be used instead of `assert()`
Prior to solidity version 0.8.0, hitting an assert consumes the remainder of the transaction’s available gas rather than returning it, as `require()`/`revert()` do. `assert()` should be avoided even past solidity version 0.8.0 as its [documentation](https://docs.soliditylang.org/en/v0.8.14/control-structures.html#panic-via-assert-and-error-via-require) states that “The assert function creates an error of type Panic(uint256). … Properly functioning code should never create a Panic, not even on invalid external input. If this happens, then there is a bug in your contract which you should fix”.

**Total Instances:** 5

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 106:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L106

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

 51:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L51

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 426:         assert(block.chainid != 1);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L426

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 222:         assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L222

```solidity
File: system-contracts/contracts/libraries/RLPEncoder.sol

 50:         assert(_len != 1);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L50


## [L-21] Revert on transfer to the zero address
It’s good practice to revert a token transfer transaction if the recipient’s address is the zero address. This can prevent unintentional transfers to the zero address due to accidental operations or programming errors. Many token contracts implement such a safeguard, such as `OpenZeppelin - ERC20`, `OpenZeppelin - ERC721`.

**Total Instances:** 3

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 67:         IERC20(_token).safeTransfer(address(sharedBridge), amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 362:             IERC20(_l1Token).safeTransfer(_depositSender, _amount);

 452:             IERC20(l1Token).safeTransfer(l1Receiver, amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L452


## [L-22] Some tokens may revert when large transfers are made
Tokens such as COMP or UNI will revert when an address’ balance reaches `type(uint96).max`. Ensure that the calls below can be broken up into smaller batches if necessary.

**Total Instances:** 3

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 /// @audit  tranferTokenToSharedBridge()
 67:         IERC20(_token).safeTransfer(address(sharedBridge), amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 /// @audit  _claimFailedDeposit()
 362:             IERC20(_l1Token).safeTransfer(_depositSender, _amount);

 /// @audit  _finalizeWithdrawal()
 452:             IERC20(l1Token).safeTransfer(l1Receiver, amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L452


## [L-23] Some tokens may revert when zero value transfers are made
Despite the fact that [EIP-20 states](https://github.com/ethereum/EIPs/blob/7500ac4fc1bbdfaf684e7ef851f798f6b667b2fe/EIPS/eip-20.md?plain=1#L116) that zero-value transfers must be accepted, some tokens, such as LEND, will revert if this is attempted, which may cause transactions that involve other tokens (such as batch operations) to fully revert. Consider skipping the transfer if the amount is zero, which will also save gas.

**Total Instances:** 3

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 /// @audit  tranferTokenToSharedBridge()
 67:         IERC20(_token).safeTransfer(address(sharedBridge), amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 /// @audit  _claimFailedDeposit()
 362:             IERC20(_l1Token).safeTransfer(_depositSender, _amount);

 /// @audit  _finalizeWithdrawal()
 452:             IERC20(l1Token).safeTransfer(l1Receiver, amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L452


## [L-24] Upgradeable contract is missing a `__gap[50]` storage variable to allow for new storage variables in later versions
See [this](https://docs.openzeppelin.com/contracts/4.x/upgradeable#storage_gaps) link for a description of this storage variable. While some contracts may not currently be sub-classed, adding the variable now protects against forgetting to add it in the future.

**Total Instances:** 1

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 15: contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L15


## [L-25] Use `increaseAllowance()`/`decreaseAllowance()` instead of `approve()`/`safeApprove()`
Changing an allowance with `approve()` brings the risk that someone may use both the old and the new allowance by unfortunate transaction ordering. Refer to [ERC20 API: An Attack Vector on the Approve/TransferFrom Methods](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM/edit#heading=h.m9fhqynw2xvt). It is recommended to use the `increaseAllowance()`/`decreaseAllowance()` to avoid ths problem.

**Total Instances:** 2

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 382:                 IERC20(token).safeApprove(paymaster, 0);

 383:                 IERC20(token).safeApprove(paymaster, minAllowance);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L383


## [L-26] Use of abi.encodePacked with dynamic types inside keccak256
Using abi.encodePacked with dynamic types for hashing functions like keccak256 can be risky due to the potential for hash collisions. This function concatenates arguments tightly, without padding, which might lead to different inputs producing the same hash. This is especially problematic with dynamic types, where the boundaries between inputs can blur. To mitigate this, use abi.encode instead. abi.encode pads its arguments to 32 bytes, creating clear distinctions between different inputs and significantly reducing the chance of hash collisions. This approach ensures more reliable and collision-resistant hashing, crucial for maintaining data integrity and security in smart contracts.

**Total Instances:** 3

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 460:                 keccak256(
                         abi.encodePacked(
                             _prevBatchCommitment,
                             _currentBatchCommitment,

 654:             blobCommitments[versionedHashIndex] = keccak256(
                     abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L460

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 142:         return keccak256(abi.encodePacked("\x19\x01", domainSeparator, structHash));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L142


## [L-27] Use of a single-step ownership transfer
The existing `transferOwnership` function immediately transfers ownership to the new address. Consider implementing a two-step variant, where the ‘acceptor’ of the ownership must call a separate function in order for the transfer to take effect. This can help to prevent mistakes where the wrong address is used, and ownership is irrecoverably lost.

**Total Instances:** 5

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 109:         _transferOwnership(_owner);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L109

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 42:         _transferOwnership(_owner);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L42

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 44:         _transferOwnership(_admin);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L44

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 83:         _transferOwnership(_initializeData.governor);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L83

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 56:         _transferOwnership(_initialOwner);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L56



## [L-28] Using zero as a parameter
Taking `0` as a valid argument in Solidity without checks can lead to severe security issues. A historical example is the infamous `0x0` address bug where numerous tokens were lost. This happens because `0` can be interpreted as an uninitialized `address`, leading to transfers to the `0x0` `address`, effectively burning tokens. Moreover, `0` as a denominator in division operations would cause a runtime exception. It’s also often indicative of a logical error in the caller’s code. It’s important to always validate input and handle edge cases like `0` appropriately. Use `require()` statements to enforce conditions and provide clear error messages to facilitate debugging and safer code.

**Total Instances:** 7

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 584:             L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
                     chainId: ERA_CHAIN_ID,
                     l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
                     mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
                     l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L584

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 182:         L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
                 txType: SYSTEM_UPGRADE_L2_TX_TYPE,
                 from: uint256(uint160(L2_FORCE_DEPLOYER_ADDR)),
                 to: uint256(uint160(L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR)),
                 gasLimit: $(PRIORITY_TX_MAX_GAS_LIMIT),
                 gasPerPubdataByteLimit: REQUIRED_L2_GAS_PRICE_PER_PUBDATA,
                 maxFeePerGas: uint256(0),
                 maxPriorityFeePerGas: uint256(0),
                 paymaster: uint256(0),
                 // Note, that the priority operation id is used as "nonce" for L1->L2 transactions
                 nonce: protocolVersion,
                 value: 0,

 202:         ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
                 l2ProtocolUpgradeTx: l2ProtocolUpgradeTx,
                 factoryDeps: bytesEmptyArray,
                 bootloaderHash: bytes32(0),
                 defaultAccountHash: bytes32(0),
                 verifier: address(0),
                 verifierParams: VerifierParams({
                     recursionNodeLevelVkHash: bytes32(0),
                     recursionLeafLevelVkHash: bytes32(0),
                     recursionCircuitsSetVksHash: bytes32(0)
                 }),
                 l1ContractsUpgradeCalldata: new bytes(0),
                 postUpgradeCalldata: new bytes(0),
                 upgradeTimestamp: 0,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L182

```solidity
File: contracts/zksync/contracts/SystemContractsCaller.sol

 46:         uint256 farCallAbi = getFarCallABI(
                0,
                0,
                dataStart,
                dataLength,
                gasLimit,
                // Only rollup is supported for now
                0,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L46

```solidity
File: system-contracts/contracts/L1Messenger.sol

 75:         L2ToL1Log memory l2ToL1Log = L2ToL1Log({
                l2ShardId: 0,

 125:         L2ToL1Log memory l2ToL1Log = L2ToL1Log({
                 l2ShardId: 0,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L75

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol

 345:         bool precompileCallSuccess = unsafePrecompileCall(
                 0, // The precompile parameters are formal ones. We only need the precompile call to burn gas.

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L345

