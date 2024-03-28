### Low Risk Issues

| |Issue|Instances|
|-|:-|:-:|
| [[L001](#l001---abiencodepacked-should-not-be-used-with-dynamic-types-when-passing-the-result-to-a-hash-function-such-as-keccak256)] | `abi.encodePacked()` should not be used with dynamic types when passing the result to a hash function such as `keccak256()` | 5 |
| [[L002](#l002---safeapprove-is-deprecated)] | `safeApprove` is Deprecated | 4 |
| [[L003](#l003---_setuprole-is-deprecated)] | `_setupRole` is Deprecated | 4 |
| [[L004](#l004--- External calls in modifiers should be avoided:)]  | 1 |
| [[L005](#l005---array-lengths-not-checked)] | Array lengths not checked | 2 |
| [[L006](#l006---missing-checks-for-address0x0-when-assigning-values-to-address-state-variables)] | Missing checks for `address(0x0)` when assigning values to address state variables | 6 |
| [[L007](#l007---upgradeable-contract-is-missing-a-__gap50-storage-variable-to-allow-for-new-storage-variables-in-later-versions)] | Upgradeable contract is missing a __gap[50] storage variable to allow for new storage variables in later versions | 4 |
| [[L008](#l008---unsafe-downcast)] | Unsafe downcast | 30 |
| [[L009](#l009---array-does-not-have-a-pop-function)] | Array does not have a `pop` function | 2 |
| [[L010](#l010---setters-should-have-initial-value-check)] | Setters should have initial value check | 28 |
| [[L011](#l011---empty-receivepayable-fallback-function-does-not-authorize-requests)] | Empty `receive()`/`payable fallback()` function does not authorize requests | 4 |
| [[L012](#l012---contracts-are-designed-to-receive-eth-but-do-not-implement-function-for-withdrawal)] | Contracts are designed to receive ETH but do not implement function for withdrawal | 3 |
| [[L013](#l013---draft-imports-may-break-in-new-minor-versions)] | Draft imports may break in new minor versions | 1 |
| [[L014](#l014---int-casting-blocktimestamp-can-reduce-the-lifespan-of-a-contract)] | Int casting `block.timestamp` can reduce the lifespan of a contract | 2 |
| [[L015](#l015---no-limits-when-setting-state-variable-amounts)] | No limits when setting state variable amounts | 28 |
| [[L016](#l016---double-type-casts-create-complexity-within-the-code)] | Double type casts create complexity within the code | 91 |
| [[L017](#l017---constructor-contains-no-validation)] | Constructor contains no validation | 4 |
| [[L018](#l018---for-loops-in-public-or-external-functions-should-be-avoided-due-to-high-gas-costs-and-possible-dos)] | For loops in `public` or `external` functions should be avoided due to high gas costs and possible DOS | 11 |
| [[L019](#l019---function-calls-within-for-loops)] | Function calls within for loops | 14 |
| [[L020](#l020---external-calls-in-an-unbounded-for-loop-may-result-in-a-dos)] | External calls in an unbounded for-loop may result in a DoS | 11 |
| [[L021](#l021---contracts-are-not-using-their-oz-upgradeable-counterparts)] | Contracts are not using their OZ Upgradeable counterparts | 20 |
| [[L022](#l022---multiplication-on-the-result-of-a-division)] | Multiplication on the result of a division | 2 |
| [[L023](#l023---decimals-is-not-a-part-of-the-erc-20-standard)] | `decimals()` is not a part of the ERC-20 standard | 1 |
| [[L024](#l024---symbol-is-not-a-part-of-the-erc-20-standard)] | `symbol()` is not a part of the ERC-20 standard | 1 |
| [[L025](#l025---name-is-not-a-part-of-the-erc-20-standard)] | `name()` is not a part of the ERC-20 standard | 1 |
| [[L026](#l026---missing-checks-for-address0x0-in-the-constructor)] | Missing checks for address(0x0) in the constructor | 3 |
| [[L027](#l027---missing-checks-for-address0x0-in-the-initializer)] | Missing checks for address(0x0) in the initializer | 1 |
| [[L028](#l028---governance-functions-should-be-controlled-by-time-locks)] | Governance functions should be controlled by time locks | 19 |
| [[L029](#l029---code-does-not-follow-the-best-practice-of-check-effects-interaction)] | Code does not follow the best practice of check-effects-interaction | 7 |
| [[L030](#l030---addresses-upcast-and-compared-to-values-larger-than-a-uint160-may-result-in-collisions)] | addresses upcast and compared to values larger than a uint160, may result in collisions | 1 |
| [[L031](#l031---missing-checks-for-address0x0-when-updating-address-state-variables)] | Missing checks for address(0x0) when updating address state variables | 17 |
| [[L032](#l032---the-additionsmultiplications-may-silently-overflow-because-theyre-in-unchecked-blocks-with-no-preceding-value-checks-which-may-lead-to-unexpected-results)] | The additions/multiplications may silently overflow because they're in unchecked blocks with no preceding value checks, which may lead to unexpected results. | 45 |



## L001 - `abi.encodePacked()` should not be used with dynamic types when passing the result to a hash function such as `keccak256()`:

Use `abi.encode()` instead which will pad items to 32 bytes, which will [prevent hash collisions](https://docs.soliditylang.org/en/v0.8.13/abi-spec.html#non-standard-packed-mode) (e.g. `abi.encodePacked(0x123,0x456)` => `0x123456` => `abi.encodePacked(0x1,0x23456)`, but `abi.encode(0x123,0x456)` => `0x0...1230...456`). Unless there is a compelling reason, `abi.encode` should be preferred. If there is only one argument to `abi.encodePacked()` it can often be cast to `bytes()` or `bytes32()` [instead](https://ethereum.stackexchange.com/questions/30912/how-to-compare-strings-in-solidity#answer-82739). If all arguments are strings and or bytes, `bytes.concat()` should be used instead.


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: system-contracts/contracts/SystemContext.sol


// that's why the legacy L2 blocks' hashes are keccak256(abi.encodePacked(uint32(_block))), while these are equivalent to

// keccak256(abi.encodePacked(_block))

return keccak256(abi.encodePacked(uint32(_blockNumber)));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L234:234

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol


keccak256(abi.encodePacked(_transaction.factoryDeps)),

return keccak256(abi.encodePacked("\x19\x01", domainSeparator, structHash));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L142:142

</details>

## L002 - `safeApprove` is Deprecated:

`safeApprove` is deprecated in favor of `safeIncreaseAllowance` and `safeDecreaseAllowance`.


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol


IERC20(token).safeApprove(paymaster, 0);

IERC20(token).safeApprove(paymaster, minAllowance);

IERC20(token).safeApprove(paymaster, 0);

IERC20(token).safeApprove(paymaster, minAllowance);

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L383:383

</details>

## L003 - `_setupRole` is Deprecated:

`_setupRole` is deprecated in favor of `grantRole` and `renounceRole`.


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol


IERC20(token).safeApprove(paymaster, 0);

IERC20(token).safeApprove(paymaster, minAllowance);

IERC20(token).safeApprove(paymaster, 0);

IERC20(token).safeApprove(paymaster, minAllowance);

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L383:383

</details>


## L004 - External calls in modifiers should be avoided:

Using external calls within modifiers can introduce reentrancy risks and make a contract's logic less transparent. Modifiers are meant for pre-execution checks, and external calls can lead to unpredictable flow and potential reentrancy issues. Avoiding external calls in modifiers and placing them directly in the function body enhances code clarity, aids in auditing, and minimizes unexpected behaviors. This practice ensures a more explicit execution order and clearer understanding of the code's effects.


```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


62              require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62:62



## L005 - Array lengths not checked:

If the length of the arrays are not required to be of the same length, user operations may not be fully executed due to a mismatch in the number of items iterated over, versus the number of items provided in the second array.


```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


500         function _createBatchCommitment(
501             CommitBatchInfo calldata _newBatchData,
502             bytes32 _stateDiffHash,
503             bytes32[] memory _blobCommitments,
504             bytes32[] memory _blobHashes
505         ) internal view returns (bytes32) {
506             bytes32 passThroughDataHash = keccak256(_batchPassThroughData(_newBatchData));
507             bytes32 metadataHash = keccak256(_batchMetaParameters());
508             bytes32 auxiliaryOutputHash = keccak256(
509                 _batchAuxiliaryOutput(_newBatchData, _stateDiffHash, _blobCommitments, _blobHashes)
510             );
511     
512             return keccak256(abi.encode(passThroughDataHash, metadataHash, auxiliaryOutputHash));
513         }


537         function _batchAuxiliaryOutput(
538             CommitBatchInfo calldata _batch,
539             bytes32 _stateDiffHash,
540             bytes32[] memory _blobCommitments,
541             bytes32[] memory _blobHashes
542         ) internal pure returns (bytes memory) {
543             require(_batch.systemLogs.length <= MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES, "pu");
544     
545             bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs);
546     
547             return
548                 abi.encodePacked(
549                     l2ToL1LogsHash,
550                     _stateDiffHash,
551                     _batch.bootloaderHeapInitialContentsHash,
552                     _batch.eventsQueueStateHash,
553                     _encodeBlobAuxilaryOutput(_blobCommitments, _blobHashes)
554                 );
555         }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537:555



## L006 - Missing checks for `address(0x0)` when assigning values to address state variables:

This issue arises when an address state variable is assigned a value without a preceding check to ensure it isn't address(0x0). This can lead to unexpected behavior as address(0x0) often represents an uninitialized address.


<details>
<summary>Click to show 6 findings</summary>

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


55              pendingAdmin = _newPendingAdmin;


109             sharedBridge = IL1SharedBridge(_sharedBridge);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L109:109

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol


258             securityCouncil = _newSecurityCouncil;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L258:258

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


114             pendingAdmin = _newPendingAdmin;


133             validatorTimelock = _validatorTimelock;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L133:133

```solidity
File: system-contracts/contracts/SystemContext.sol


100             origin = _newOrigin;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L100:100

</details>

## L007 - Upgradeable contract is missing a __gap[50] storage variable to allow for new storage variables in later versions:

This issue arises when an upgradeable contract doesn't include a __gap[50] storage variable. This variable is crucial for facilitating future upgrades and preserving storage layout.


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


30      contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L30:30

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


23      contract L2SharedBridge is IL2SharedBridge, Initializable {


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L23:23

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol


15      contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L15:15

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol


41      library SystemContractHelper {


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L41:41

</details>

## L008 - Unsafe downcast:

When a type is downcast to a smaller type, the higher order bits are truncated, effectively applying a modulo to the original value. Without any other checks, this wrapping will lead to unexpected behavior and bugs.


<details>
<summary>Click to show 30 findings</summary>

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


71              return address(uint160(uint256(data)));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L71:71

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


134                 uint32 timestamp = uint32(block.timestamp);


115                 uint32 timestamp = uint32(block.timestamp);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L115:115

```solidity
File: contracts/zksync/contracts/L2ContractHelper.sol


112             return address(uint160(uint256(data)));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L112:112

```solidity
File: contracts/zksync/contracts/SystemContractsCaller.sol


30              return uint32(_x);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L30:30

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol


92              address account = address(uint160(_input));


120             address account = address(uint160(_input));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L120:120

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol


259                 uint64 txDataLen = uint64(_transaction.data.length);


164                 uint64 txDataLen = uint64(_transaction.data.length);


68                  uint64 txDataLen = uint64(_transaction.data.length);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L68:68

```solidity
File: system-contracts/contracts/ContractDeployer.sol


125             newAddress = address(uint160(uint256(hash)));


109             newAddress = address(uint160(uint256(hash)));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L109:109

```solidity
File: system-contracts/contracts/L2BaseToken.sol


57              return balance[address(uint160(_account))];


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L57:57

```solidity
File: system-contracts/contracts/SystemContext.sol


234             return keccak256(abi.encodePacked(uint32(_blockNumber)));


476             BlockInfo memory newBlockInfo = BlockInfo({number: uint128(_number), timestamp: uint128(_newTimestamp)});


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L476:476

```solidity
File: system-contracts/contracts/libraries/RLPEncoder.sol


69                      encoded[0] = bytes1(uint8(_offset + hbs + 56));


64                      encoded[0] = bytes1(uint8(_len + _offset));


29                      encoded[0] = (_val == 0) ? bytes1(uint8(128)) : bytes1(uint8(_val));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L29:29

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol


247             auxHeapSize = uint32(extractNumberFromMeta(meta, META_AUX_HEAP_SIZE_OFFSET, 32));


238             heapSize = uint32(extractNumberFromMeta(meta, META_HEAP_SIZE_OFFSET, 32));


228             pubdataPublished = uint32(extractNumberFromMeta(meta, META_GAS_PER_PUBDATA_BYTE_OFFSET, 32));


264             callerShardId = uint8(extractNumberFromMeta(meta, META_CALLER_SHARD_ID_OFFSET, 8));


273             codeShardId = uint8(extractNumberFromMeta(meta, META_CODE_SHARD_ID_OFFSET, 8));


255             shardId = uint8(extractNumberFromMeta(meta, META_SHARD_ID_OFFSET, 8));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L255:255

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol


321                 uint64 txDataLen = uint64(_transaction.data.length);


171                 uint64 txDataLen = uint64(_transaction.data.length);


249                 uint64 txDataLen = uint64(_transaction.data.length);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L249:249

```solidity
File: system-contracts/contracts/libraries/Utils.sol


23              return uint128(_x);


29              return uint32(_x);


35              return uint24(_x);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L35:35

</details>


## L009 - Array does not have a `pop` function:

Arrays without the pop operation in Solidity can lead to inefficient memory management and increase the likelihood of out-of-gas errors.


```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


196                 ds.facets.push(_facet);


223             ds.facetToSelectors[_facet].selectors.push(_selector);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L223:223

## L010 - Setters should have initial value check:

Setters should have initial value check to prevent assigning wrong value to the variable. Assginment of wrong value can lead to unexpected behavior of the contract.


<details>
<summary>Click to show 28 findings</summary>

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


51          function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
52              // Save previous value into the stack to put it into the event later
53              address oldPendingAdmin = pendingAdmin;
54              // Change pending admin
55              pendingAdmin = _newPendingAdmin;
56              emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
57          }


108         function setSharedBridge(address _sharedBridge) external onlyOwner {
109             sharedBridge = IL1SharedBridge(_sharedBridge);
110         }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108:110

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


110         function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
111             // Save previous value into the stack to put it into the event later
112             address oldPendingAdmin = pendingAdmin;
113             // Change pending admin
114             pendingAdmin = _newPendingAdmin;
115             emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
116         }


132         function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {
133             validatorTimelock = _validatorTimelock;
134         }


137         function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {
138             initialCutHash = keccak256(abi.encode(_diamondCut));
139         }


142         function setNewVersionUpgrade(
143             Diamond.DiamondCutData calldata _cutData,
144             uint256 _oldProtocolVersion,
145             uint256 _newProtocolVersion
146         ) external onlyOwner {
147             upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
148             protocolVersion = _newProtocolVersion;
149         }


152         function setUpgradeDiamondCut(
153             Diamond.DiamondCutData calldata _cutData,
154             uint256 _oldProtocolVersion
155         ) external onlyOwner {
156             upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
157         }


177         function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
178             bytes memory systemContextCalldata = abi.encodeCall(ISystemContext.setChainId, (_chainId));
179             uint256[] memory uintEmptyArray;
180             bytes[] memory bytesEmptyArray;
181     
182             L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
183                 txType: SYSTEM_UPGRADE_L2_TX_TYPE,
184                 from: uint256(uint160(L2_FORCE_DEPLOYER_ADDR)),
185                 to: uint256(uint160(L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR)),
186                 gasLimit: $(PRIORITY_TX_MAX_GAS_LIMIT),
187                 gasPerPubdataByteLimit: REQUIRED_L2_GAS_PRICE_PER_PUBDATA,
188                 maxFeePerGas: uint256(0),
189                 maxPriorityFeePerGas: uint256(0),
190                 paymaster: uint256(0),
191                 // Note, that the priority operation id is used as "nonce" for L1->L2 transactions
192                 nonce: protocolVersion,
193                 value: 0,
194                 reserved: [uint256(0), 0, 0, 0],
195                 data: systemContextCalldata,
196                 signature: new bytes(0),
197                 factoryDeps: uintEmptyArray,
198                 paymasterInput: new bytes(0),
199                 reservedDynamic: new bytes(0)
200             });
201     
202             ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
203                 l2ProtocolUpgradeTx: l2ProtocolUpgradeTx,
204                 factoryDeps: bytesEmptyArray,
205                 bootloaderHash: bytes32(0),
206                 defaultAccountHash: bytes32(0),
207                 verifier: address(0),
208                 verifierParams: VerifierParams({
209                     recursionNodeLevelVkHash: bytes32(0),
210                     recursionLeafLevelVkHash: bytes32(0),
211                     recursionCircuitsSetVksHash: bytes32(0)
212                 }),
213                 l1ContractsUpgradeCalldata: new bytes(0),
214                 postUpgradeCalldata: new bytes(0),
215                 upgradeTimestamp: 0,
216                 newProtocolVersion: protocolVersion
217             });
218     
219             Diamond.FacetCut[] memory emptyArray;
220             Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({
221                 facetCuts: emptyArray,
222                 initAddress: genesisUpgrade,
223                 initCalldata: abi.encodeCall(IDefaultUpgrade.upgrade, (proposedUpgrade))
224             });
225     
226             IAdmin(_chainContract).executeUpgrade(cutData);
227             emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
228         }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177:228

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


73          function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {
74              stateTransitionManager = _stateTransitionManager;
75          }


96          function setExecutionDelay(uint32 _executionDelay) external onlyOwner {
97              executionDelay = _executionDelay;
98              emit NewExecutionDelay(_executionDelay);
99          }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96:99

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


23          function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {
24              // Save previous value into the stack to put it into the event later
25              address oldPendingAdmin = s.pendingAdmin;
26              // Change pending admin
27              s.pendingAdmin = _newPendingAdmin;
28              emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
29          }


45          function setValidator(address _validator, bool _active) external onlyStateTransitionManager {
46              s.validators[_validator] = _active;
47              emit ValidatorStatusUpdate(_validator, _active);
48          }


51          function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {
52              // Change the porter availability
53              s.zkPorterIsAvailable = _zkPorterIsAvailable;
54              emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);
55          }


58          function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager {
59              require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");
60      
61              uint256 oldPriorityTxMaxGasLimit = s.priorityTxMaxGasLimit;
62              s.priorityTxMaxGasLimit = _newPriorityTxMaxGasLimit;
63              emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);
64          }


79          function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {
80              uint128 oldNominator = s.baseTokenGasPriceMultiplierNominator;
81              uint128 oldDenominator = s.baseTokenGasPriceMultiplierDenominator;
82      
83              s.baseTokenGasPriceMultiplierNominator = _nominator;
84              s.baseTokenGasPriceMultiplierDenominator = _denominator;
85      
86              emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator);
87          }


89          function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {
90              require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed
91              s.feeParams.pubdataPricingMode = _validiumMode;
92              emit ValidiumModeStatusUpdate(_validiumMode);
93          }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L89:93

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


597         function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {
598             return _bitMap | (1 << _index);
599         }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597:599

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol


34          function setImmutables(address _dest, ImmutableData[] calldata _immutables) external override {
35              require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
36              unchecked {
37                  uint256 immutablesLength = _immutables.length;
38                  for (uint256 i = 0; i < immutablesLength; ++i) {
39                      uint256 index = _immutables[i].index;
40                      bytes32 value = _immutables[i].value;
41                      immutableDataStorage[uint256(uint160(_dest))][index] = value;
42                  }
43              }
44          }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L34:44

```solidity
File: system-contracts/contracts/NonceHolder.sol


82          function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall {
83              IContractDeployer.AccountInfo memory accountInfo = DEPLOYER_SYSTEM_CONTRACT.getAccountInfo(msg.sender);
84      
85              require(_value != 0, "Nonce value cannot be set to 0");
86              // If an account has sequential nonce ordering, we enforce that the previous
87              // nonce has already been used.
88              if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {
89                  require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");
90              }
91      
92              uint256 addressAsKey = uint256(uint160(msg.sender));
93      
94              nonceValues[addressAsKey][_key] = _value;
95      
96              emit ValueSetUnderNonce(msg.sender, _key, _value);
97          }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L82:97

```solidity
File: system-contracts/contracts/SystemContext.sol


84          function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {
85              chainId = _newChainId;
86          }


99          function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {
100             origin = _newOrigin;
101         }


105         function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {
106             gasPrice = _gasPrice;
107         }


112         function setPubdataInfo(uint256 _gasPerPubdataByte, uint256 _basePubdataSpent) external onlyCallFromBootloader {
113             basePubdataSpent = _basePubdataSpent;
114             gasPerPubdataByte = _gasPerPubdataByte;
115         }


212         function _setL2BlockHash(uint256 _block, bytes32 _hash) internal {
213             l2BlockHash[_block % MINIBLOCK_HASHES_TO_STORE] = _hash;
214         }


263         function _setVirtualBlock(
264             uint128 _l2BlockNumber,
265             uint128 _maxVirtualBlocksToCreate,
266             uint128 _newTimestamp
267         ) internal {
268             if (virtualBlockUpgradeInfo.virtualBlockFinishL2Block != 0) {
269                 // No need to to do anything about virtual blocks anymore
270                 // All the info is the same as for L2 blocks.
271                 currentVirtualL2BlockInfo = currentL2BlockInfo;
272                 return;
273             }
274     
275             BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;
276     
277             if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
278                 uint128 currentBatchNumber = currentBatchInfo.number;
279     
280                 // The virtual block is set for the first time. We can count it as 1 creation of a virtual block.
281                 // Note, that when setting the virtual block number we use the batch number to make a smoother upgrade from batch number to
282                 // the L2 block number.
283                 virtualBlockInfo.number = currentBatchNumber;
284                 // Remembering the batch number on which the upgrade to the virtual blocks has been done.
285                 virtualBlockUpgradeInfo.virtualBlockStartBatch = currentBatchNumber;
286     
287                 require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");
288                 _maxVirtualBlocksToCreate -= 1;
289             } else if (_maxVirtualBlocksToCreate == 0) {
290                 // The virtual blocks have been already initialized, but the operator didn't ask to create
291                 // any new virtual blocks. So we can just return.
292                 return;
293             }
294     
295             virtualBlockInfo.number += _maxVirtualBlocksToCreate;
296             virtualBlockInfo.timestamp = _newTimestamp;
297     
298             // The virtual block number must never exceed the L2 block number.
299             // We do not use a `require` here, since the virtual blocks are a temporary solution to let the Solidity's `block.number`
300             // catch up with the L2 block number and so the situation where virtualBlockInfo.number starts getting larger
301             // than _l2BlockNumber is expected once virtual blocks have caught up the L2 blocks.
302             if (virtualBlockInfo.number >= _l2BlockNumber) {
303                 virtualBlockUpgradeInfo.virtualBlockFinishL2Block = _l2BlockNumber;
304                 virtualBlockInfo.number = _l2BlockNumber;
305             }
306     
307             currentVirtualL2BlockInfo = virtualBlockInfo;
308         }


314         function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal {
315             // In the unsafe version we do not check that the block data is correct
316             currentL2BlockInfo = BlockInfo({number: _l2BlockNumber, timestamp: _l2BlockTimestamp});
317     
318             // It is always assumed in production that _l2BlockNumber > 0
319             _setL2BlockHash(_l2BlockNumber - 1, _prevL2BlockHash);
320     
321             // Reseting the rolling hash
322             currentL2BlockTxsRollingHash = bytes32(0);
323         }


341         function setL2Block(
342             uint128 _l2BlockNumber,
343             uint128 _l2BlockTimestamp,
344             bytes32 _expectedPrevL2BlockHash,
345             bool _isFirstInBatch,
346             uint128 _maxVirtualBlocksToCreate
347         ) external onlyCallFromBootloader {
348             // We check that the timestamp of the L2 block is consistent with the timestamp of the batch.
349             if (_isFirstInBatch) {
350                 uint128 currentBatchTimestamp = currentBatchInfo.timestamp;
351                 require(
352                     _l2BlockTimestamp >= currentBatchTimestamp,
353                     "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
354                 );
355                 require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");
356             }
357     
358             (uint128 currentL2BlockNumber, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();
359     
360             if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {
361                 // Since currentL2BlockNumber and currentL2BlockTimestamp are zero it means that it is
362                 // the first ever batch with L2 blocks, so we need to initialize those.
363                 _upgradeL2Blocks(_l2BlockNumber, _expectedPrevL2BlockHash, _isFirstInBatch);
364     
365                 _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);
366             } else if (currentL2BlockNumber == _l2BlockNumber) {
367                 require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");
368                 require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");
369                 require(
370                     _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
371                     "The previous hash of the same L2 block must be same"
372                 );
373                 require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");
374             } else if (currentL2BlockNumber + 1 == _l2BlockNumber) {
375                 // From the checks in _upgradeL2Blocks it is known that currentL2BlockNumber can not be 0
376                 bytes32 prevL2BlockHash = _getLatest257L2blockHash(currentL2BlockNumber - 1);
377     
378                 bytes32 pendingL2BlockHash = _calculateL2BlockHash(
379                     currentL2BlockNumber,
380                     currentL2BlockTimestamp,
381                     prevL2BlockHash,
382                     currentL2BlockTxsRollingHash
383                 );
384     
385                 require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");
386                 require(
387                     _l2BlockTimestamp > currentL2BlockTimestamp,
388                     "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
389                 );
390     
391                 // Since the new block is created, we'll clear out the rolling hash
392                 _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);
393             } else {
394                 revert("Invalid new L2 block number");
395             }
396     
397             _setVirtualBlock(_l2BlockNumber, _maxVirtualBlocksToCreate, _l2BlockTimestamp);
398         }


444         function setNewBatch(
445             bytes32 _prevBatchHash,
446             uint128 _newTimestamp,
447             uint128 _expectedNewNumber,
448             uint256 _baseFee
449         ) external onlyCallFromBootloader {
450             (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();
451             require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");
452             require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
453     
454             _ensureBatchConsistentWithL2Block(_newTimestamp);
455     
456             batchHashes[previousBatchNumber] = _prevBatchHash;
457     
458             // Setting new block number and timestamp
459             BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp});
460     
461             currentBatchInfo = newBlockInfo;
462     
463             baseFee = _baseFee;
464     
465             // The correctness of this block hash:
466             SystemContractHelper.toL1(false, bytes32(uint256(SystemLogKey.PREV_BATCH_HASH_KEY)), _prevBatchHash);
467         }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L444:467

</details>

## L011 - Empty `receive()`/`payable fallback()` function does not authorize requests:

If the intention is for the Ether to be used, the function should call another function, otherwise it should revert (e.g. `require(msg.sender == address(weth))`). Having no access control on the function means that someone may send Ether to the contract, and have no way to get anything back out, which is a loss of funds. If the concern is having to spend a small amount of gas to check the sender against an immutable address, the code should at least have a function to rescue unused Ether.


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol


262         receive() external payable {}


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L262:262

```solidity
File: system-contracts/contracts/DefaultAccount.sol


227         receive() external payable {
228             // If the contract is called directly, behave like an EOA
229         }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L227:229

```solidity
File: system-contracts/contracts/EmptyContract.sol


11          fallback() external payable {}


13          receive() external payable {}


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/EmptyContract.sol#L13:13

</details>

## L012 - Contracts are designed to receive ETH but do not implement function for withdrawal:

The following contracts can receive ETH but can not withdraw, ETH is occasionally sent by users will be stuck in those contracts. This functionality also applies to baseTokens resulting in locked tokens and loss of funds.


```solidity
File: contracts/ethereum/contracts/governance/Governance.sol


262         receive() external payable {}


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L262:262

```solidity
File: system-contracts/contracts/DefaultAccount.sol


227         receive() external payable {
228             // If the contract is called directly, behave like an EOA
229         }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L227:229

```solidity
File: system-contracts/contracts/EmptyContract.sol


11          fallback() external payable {}


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/EmptyContract.sol#L11:11


## L013 - Draft imports may break in new minor versions:

While OpenZeppelin draft contracts are safe to use and have been audited, their 'draft' status means that the EIPs they're based on are not finalized, and thus there may be breaking changes in even minor releases. If a bug is found in this version of OpenZeppelin, and the version that you're forced to upgrade to has breaking changes in the new version, you'll encounter unnecessary delays in porting and testing replacement contracts. Ensure that you have extensive test coverage of this area so that differences can be automatically detected, and have a plan in place for how you would fully test a new version of these contracts if they do indeed change unexpectedly. Consider creating a forked version of the file rather than importing it from the package, and manually patch your fork as changes are made.


```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol


5       import {ERC20PermitUpgradeable} from "@openzeppelin/contracts-upgradeable/token/ERC20/extensions/draft-ERC20PermitUpgradeable.sol";


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L5:5

## L014 - Int casting `block.timestamp` can reduce the lifespan of a contract:

Consider removing casting to ensure future functionality.


```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


115                 uint32 timestamp = uint32(block.timestamp);


134                 uint32 timestamp = uint32(block.timestamp);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L134:134

## L015 - No limits when setting state variable amounts:

It is important to ensure state variables numbers are set to a reasonable value.


<details>
<summary>Click to show 28 findings</summary>

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


111             eraFirstPostUpgradeBatch = _eraFirstPostUpgradeBatch;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L111:111

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol


49              minDelay = _minDelay;


251             minDelay = _newDelay;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L251:251

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


148             protocolVersion = _newProtocolVersion;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L148:148

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


57              executionDelay = _executionDelay;


97              executionDelay = _executionDelay;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L97:97

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


83              s.baseTokenGasPriceMultiplierNominator = _nominator;


84              s.baseTokenGasPriceMultiplierDenominator = _denominator;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L84:84

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


164                     logOutput.packedBatchAndL2BlockTimestamp = uint256(logValue);


173                     logOutput.numberOfLayer1Txs = uint256(logValue);


357             s.totalBatchesExecuted = newTotalBatchesExecuted;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L357:357

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


30                  result = uint32(mapValue >> bitOffset);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L30:30

```solidity
File: system-contracts/contracts/Compressor.sol


252             number = uint256(bytes32(_calldataSlice));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L252:252

```solidity
File: system-contracts/contracts/L1Messenger.sol


108             logIdInMerkleTree = numberOfLogsToProcess;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L108:108

```solidity
File: system-contracts/contracts/SystemContext.sol


85              chainId = _newChainId;


106             gasPrice = _gasPrice;


113             basePubdataSpent = _basePubdataSpent;


114             gasPerPubdataByte = _gasPerPubdataByte;


285                 virtualBlockUpgradeInfo.virtualBlockStartBatch = currentBatchNumber;


463             baseFee = _baseFee;


479             baseFee = _baseFee;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L479:479

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol


131             rawParams = _inputMemoryOffset;


228             pubdataPublished = uint32(extractNumberFromMeta(meta, META_GAS_PER_PUBDATA_BYTE_OFFSET, 32));


238             heapSize = uint32(extractNumberFromMeta(meta, META_HEAP_SIZE_OFFSET, 32));


247             auxHeapSize = uint32(extractNumberFromMeta(meta, META_AUX_HEAP_SIZE_OFFSET, 32));


255             shardId = uint8(extractNumberFromMeta(meta, META_SHARD_ID_OFFSET, 8));


264             callerShardId = uint8(extractNumberFromMeta(meta, META_CALLER_SHARD_ID_OFFSET, 8));


273             codeShardId = uint8(extractNumberFromMeta(meta, META_CODE_SHARD_ID_OFFSET, 8));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L273:273

</details>

## L016 - Double type casts create complexity within the code:

Double type casting should be avoided in Solidity contracts to prevent unintended consequences and ensure accurate data representation. Performing multiple type casts in succession can lead to unexpected truncation, rounding errors, or loss of precision, potentially compromising the contract's functionality and reliability. Furthermore, double type casting can make the code less readable and harder to maintain, increasing the likelihood of errors and misunderstandings during development and debugging. To ensure precise and consistent data handling, developers should use appropriate data types and avoid unnecessary or excessive type casting, promoting a more robust and dependable contract execution.


<details>
<summary>Click to show 91 findings</summary>

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


bytes32 salt = bytes32(uint256(uint160(_l1Token)));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L77:77

```solidity
File: contracts/ethereum/contracts/common/Config.sol


bytes32 constant TWO_BRIDGES_MAGIC_VALUE = bytes32(uint256(keccak256("TWO_BRIDGES_MAGIC_VALUE")) - 1);

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L112:112

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


hashedBytecode = (hashedBytecode | bytes32(uint256(1 << 248)));

codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));

bytes32 senderBytes = bytes32(uint256(uint160(_sender)));

return address(uint160(uint256(data)));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L71:71

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


from: uint256(uint160(L2_FORCE_DEPLOYER_ADDR)),

to: uint256(uint160(L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR)),

bytes32(uint256(uint160(bridgehub))),

bytes32(uint256(uint160(address(this)))),

bytes32(uint256(protocolVersion)),

bytes32(uint256(uint160(_admin))),

bytes32(uint256(uint160(validatorTimelock))),

bytes32(uint256(uint160(_baseToken))),

bytes32(uint256(uint160(_sharedBridge))),

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L270:270

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));

uint256(uint128(bytes16(_pubdataCommitments[i:i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET])))

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L644:644

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


value: bytes32(uint256(_status))

key: bytes32(uint256(uint160(_message.sender))),

from: uint256(uint160(_priorityOpParams.sender)),

to: uint256(uint160(_priorityOpParams.contractAddressL2)),

reserved: [_priorityOpParams.valueToMint, uint256(uint160(_priorityOpParams.refundRecipient)), 0, 0],

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L306:306

```solidity
File: contracts/zksync/contracts/L2ContractHelper.sol


bytes32 senderBytes = bytes32(uint256(uint160(_sender)));

return address(uint160(uint256(data)));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L112:112

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


salt = bytes32(uint256(uint160(_l1Token)));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L158:158

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol


uint256 addressAsKey = uint256(uint160(_address));

uint256 addressAsKey = uint256(uint160(_address));

address account = address(uint160(_input));

address account = address(uint160(_input));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L120:120

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol


bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

uint256 rInt = uint256(bytes32(_transaction.signature[0:32]));

uint256 sInt = uint256(bytes32(_transaction.signature[32:64]));

uint256 vInt = uint256(uint8(_transaction.signature[64]));

bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

uint256 rInt = uint256(bytes32(_transaction.signature[0:32]));

uint256 sInt = uint256(bytes32(_transaction.signature[32:64]));

uint256 vInt = uint256(uint8(_transaction.signature[64]));

bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

uint256 rInt = uint256(bytes32(_transaction.signature[0:32]));

uint256 sInt = uint256(bytes32(_transaction.signature[32:64]));

uint256 vInt = uint256(uint8(_transaction.signature[64]));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L285:285

```solidity
File: system-contracts/contracts/Compressor.sol


uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

number = uint256(bytes32(_calldataSlice));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L252:252

```solidity
File: system-contracts/contracts/ContractDeployer.sol


bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, constructorInputHash)

newAddress = address(uint160(uint256(hash)));

bytes.concat(CREATE_PREFIX, bytes32(uint256(uint160(_sender))), bytes32(_senderNonce))

newAddress = address(uint160(uint256(hash)));

ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0,

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L269:269

```solidity
File: system-contracts/contracts/DefaultAccount.sol


address to = address(uint160(_transaction.to));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L132:132

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol


return immutableDataStorage[uint256(uint160(_dest))][_index];

immutableDataStorage[uint256(uint160(_dest))][index] = value;

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L41:41

```solidity
File: system-contracts/contracts/L1Messenger.sol


key: bytes32(uint256(uint160(msg.sender))),

uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==

uint24 compressedStateDiffSize = uint24(bytes3(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 3]));

uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));

uint32 numberOfStateDiffs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)), l2ToL1LogsTreeRoot);

bytes32(uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)),

SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.STATE_DIFF_HASH_KEY)), stateDiffHash);

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L326:326

```solidity
File: system-contracts/contracts/L2BaseToken.sol


return balance[address(uint160(_account))];

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L57:57

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol


to = address(uint160(addressAsUint));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L32:32

```solidity
File: system-contracts/contracts/NonceHolder.sol


uint256 addressAsKey = uint256(uint160(_address));

uint256 addressAsKey = uint256(uint160(_address));

uint256 addressAsKey = uint256(uint160(msg.sender));

uint256 addressAsKey = uint256(uint160(msg.sender));

uint256 addressAsKey = uint256(uint160(msg.sender));

uint256 addressAsKey = uint256(uint160(msg.sender));

uint256 addressAsKey = uint256(uint160(_address));

uint256 addressAsKey = uint256(uint160(_address));

uint256 addressAsKey = uint256(uint160(_address));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L155:155

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol


SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.BLOB_ONE_HASH_KEY)), blobHashes[0]);

SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.BLOB_TWO_HASH_KEY)), blobHashes[1]);

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L56:56

```solidity
File: system-contracts/contracts/SystemContext.sol


bytes32(uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)),

SystemContractHelper.toL1(false, bytes32(uint256(SystemLogKey.PREV_BATCH_HASH_KEY)), _prevBatchHash);

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L466:466

```solidity
File: system-contracts/contracts/libraries/RLPEncoder.sol


encoded[0] = (_val == 0) ? bytes1(uint8(128)) : bytes1(uint8(_val));

encoded[0] = bytes1(uint8(hbs + 0x81));

encoded[0] = bytes1(uint8(_len + _offset));

encoded[0] = bytes1(uint8(_offset + hbs + 56));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L69:69

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol


return _addr == uint256(uint160(address(BASE_TOKEN_SYSTEM_CONTRACT))) || _addr == 0;

bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

address paymaster = address(uint160(_transaction.paymaster));

if (address(uint160(_transaction.paymaster)) != address(0)) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L406:406

```solidity
File: system-contracts/contracts/libraries/Utils.sol


codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));

hashedBytecode = (hashedBytecode | bytes32(uint256(1 << 248)));

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L93:93

</details>

## L017 - Constructor contains no validation:

In Solidity, when values are being assigned in constructors to unsigned or integer variables, it's crucial to ensure the provided values adhere to the protocol's specific operational boundaries as laid out in the project specifications and documentation. If the constructors lack appropriate validation checks, there's a risk of setting state variables with values that could cause unexpected and potentially detrimental behavior within the contract's operations, violating the intended logic of the protocol. This can compromise the contract's security and impact the maintainability and reliability of the system. In order to avoid such issues, it is recommended to incorporate rigorous validation checks in constructors. These checks should align with the project's defined rules and constraints, making use of Solidity's built-in require function to enforce these conditions. If the validation checks fail, the require function will cause the transaction to revert, ensuring the integrity and adherence to the protocol's expected behavior.


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


55          constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
56              sharedBridge = _sharedBridge;
57          }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55:57

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


90          constructor(
91              address _l1WethAddress,
92              IBridgehub _bridgehub,
93              IL1ERC20Bridge _legacyBridge
94          ) reentrancyGuardInitializer {
95              _disableInitializers();
96              l1WethAddress = _l1WethAddress;
97              bridgehub = _bridgehub;
98              legacyBridge = _legacyBridge;
99          }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90:99

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


58          constructor(address _bridgehub) reentrancyGuardInitializer {
59              bridgehub = _bridgehub;
60          }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58:60

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


55          constructor(address _initialOwner, uint32 _executionDelay) {
56              _transferOwnership(_initialOwner);
57              executionDelay = _executionDelay;
58          }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55:58

</details>

## L018 - For loops in `public` or `external` functions should be avoided due to high gas costs and possible DOS:

In Solidity, for loops can potentially cause Denial of Service (DoS) attacks if not handled carefully. DoS attacks can occur when an attacker intentionally exploits the gas cost of a function, causing it to run out of gas or making it too expensive for other users to call. Below are some scenarios where for loops can lead to DoS attacks: Nested for loops can become exceptionally gas expensive and should be used sparingly.


<details>
<summary>Click to show 11 findings</summary>

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


108         function commitBatches(
109             StoredBatchInfo calldata,
110             CommitBatchInfo[] calldata _newBatchesData
111         ) external onlyValidator(ERA_CHAIN_ID) {
112             unchecked {
113                 // This contract is only a temporary solution, that hopefully will be disabled until 2106 year, so...
114                 // It is safe to cast.
115                 uint32 timestamp = uint32(block.timestamp);
116                 for (uint256 i = 0; i < _newBatchesData.length; ++i) {
117                     committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);
118                 }
119             }
120     
121             _propagateToZkSyncStateTransition(ERA_CHAIN_ID);
122         }


126         function commitBatchesSharedBridge(
127             uint256 _chainId,
128             StoredBatchInfo calldata,
129             CommitBatchInfo[] calldata _newBatchesData
130         ) external onlyValidator(_chainId) {
131             unchecked {
132                 // This contract is only a temporary solution, that hopefully will be disabled until 2106 year, so...
133                 // It is safe to cast.
134                 uint32 timestamp = uint32(block.timestamp);
135                 for (uint256 i = 0; i < _newBatchesData.length; ++i) {
136                     committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);
137                 }
138             }
139     
140             _propagateToZkSyncStateTransition(_chainId);
141         }


182         function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {
183             uint256 delay = executionDelay; // uint32
184             unchecked {
185                 for (uint256 i = 0; i < _newBatchesData.length; ++i) {
186                     uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
187                         _newBatchesData[i].batchNumber
188                     );
189     
190                     // Note: if the `commitBatchTimestamp` is zero, that means either:
191                     // * The batch was committed, but not through this contract.
192                     // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
193                     // We allow executing such batches.
194     
195                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
196                 }
197             }
198             _propagateToZkSyncStateTransition(ERA_CHAIN_ID);
199         }


203         function executeBatchesSharedBridge(
204             uint256 _chainId,
205             StoredBatchInfo[] calldata _newBatchesData
206         ) external onlyValidator(_chainId) {
207             uint256 delay = executionDelay; // uint32
208             unchecked {
209                 for (uint256 i = 0; i < _newBatchesData.length; ++i) {
210                     uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
211     
212                     // Note: if the `commitBatchTimestamp` is zero, that means either:
213                     // * The batch was committed, but not through this contract.
214                     // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
215                     // We allow executing such batches.
216     
217                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
218                 }
219             }
220             _propagateToZkSyncStateTransition(_chainId);
221         }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L203:221

```solidity
File: system-contracts/contracts/Compressor.sol


44          function publishCompressedBytecode(
45              bytes calldata _bytecode,
46              bytes calldata _rawCompressedData
47          ) external payable onlyCallFromBootloader returns (bytes32 bytecodeHash) {
48              unchecked {
49                  (bytes calldata dictionary, bytes calldata encodedData) = _decodeRawBytecode(_rawCompressedData);
50      
51                  require(
52                      encodedData.length * 4 == _bytecode.length,
53                      "Encoded data length should be 4 times shorter than the original bytecode"
54                  );
55      
56                  require(
57                      dictionary.length / 8 <= encodedData.length / 2,
58                      "Dictionary should have at most the same number of entries as the encoded data"
59                  );
60      
61                  for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
62                      uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
63                      require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");
64      
65                      uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);
66                      uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);
67      
68                      require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");
69                  }
70              }
71      
72              bytecodeHash = Utils.hashL2Bytecode(_bytecode);
73              L1_MESSENGER_CONTRACT.sendToL1(_rawCompressedData);
74              KNOWN_CODE_STORAGE_CONTRACT.markBytecodeAsPublished(bytecodeHash);
75          }


110         function verifyCompressedStateDiffs(
111             uint256 _numberOfStateDiffs,
112             uint256 _enumerationIndexSize,
113             bytes calldata _stateDiffs,
114             bytes calldata _compressedStateDiffs
115         ) external payable onlyCallFrom(address(L1_MESSENGER_CONTRACT)) returns (bytes32 stateDiffHash) {
116             // We do not enforce the operator to use the optimal, i.e. the minimally possible _enumerationIndexSize.
117             // We do enforce however, that the _enumerationIndexSize is not larger than 8 bytes long, which is the
118             // maximal ever possible size for enumeration index.
119             require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");
120     
121             uint256 numberOfInitialWrites = uint256(_compressedStateDiffs.readUint16(0));
122     
123             uint256 stateDiffPtr = 2;
124             uint256 numInitialWritesProcessed = 0;
125     
126             // Process initial writes
127             for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
128                 bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
129                 uint64 enumIndex = stateDiff.readUint64(84);
130                 if (enumIndex != 0) {
131                     // It is a repeated write, so we skip it.
132                     continue;
133                 }
134     
135                 numInitialWritesProcessed++;
136     
137                 bytes32 derivedKey = stateDiff.readBytes32(52);
138                 uint256 initValue = stateDiff.readUint256(92);
139                 uint256 finalValue = stateDiff.readUint256(124);
140                 require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");
141                 stateDiffPtr += 32;
142     
143                 uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
144                 stateDiffPtr++;
145                 uint8 operation = metadata & OPERATION_BITMASK;
146                 uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
147                 _verifyValueCompression(
148                     initValue,
149                     finalValue,
150                     operation,
151                     _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
152                 );
153                 stateDiffPtr += len;
154             }
155     
156             require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");
157     
158             // Process repeated writes
159             for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
160                 bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
161                 uint64 enumIndex = stateDiff.readUint64(84);
162                 if (enumIndex == 0) {
163                     continue;
164                 }
165     
166                 uint256 initValue = stateDiff.readUint256(92);
167                 uint256 finalValue = stateDiff.readUint256(124);
168                 uint256 compressedEnumIndex = _sliceToUint256(
169                     _compressedStateDiffs[stateDiffPtr:stateDiffPtr + _enumerationIndexSize]
170                 );
171                 require(enumIndex == compressedEnumIndex, "rw: enum key mismatch");
172                 stateDiffPtr += _enumerationIndexSize;
173     
174                 uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
175                 stateDiffPtr += 1;
176                 uint8 operation = metadata & OPERATION_BITMASK;
177                 uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
178                 _verifyValueCompression(
179                     initValue,
180                     finalValue,
181                     operation,
182                     _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
183                 );
184                 stateDiffPtr += len;
185             }
186     
187             require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");
188     
189             stateDiffHash = EfficientCall.keccak(_stateDiffs);
190         }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L110:190

```solidity
File: system-contracts/contracts/ContractDeployer.sol


238         function forceDeployOnAddresses(ForceDeployment[] calldata _deployments) external payable {
239             require(
240                 msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
241                 "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
242             );
243     
244             uint256 deploymentsLength = _deployments.length;
245             // We need to ensure that the `value` provided by the call is enough to provide `value`
246             // for all of the deployments
247             uint256 sumOfValues = 0;
248             for (uint256 i = 0; i < deploymentsLength; ++i) {
249                 sumOfValues += _deployments[i].value;
250             }
251             require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");
252     
253             for (uint256 i = 0; i < deploymentsLength; ++i) {
254                 this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
255             }
256         }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L238:256

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol


34          function setImmutables(address _dest, ImmutableData[] calldata _immutables) external override {
35              require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
36              unchecked {
37                  uint256 immutablesLength = _immutables.length;
38                  for (uint256 i = 0; i < immutablesLength; ++i) {
39                      uint256 index = _immutables[i].index;
40                      bytes32 value = _immutables[i].value;
41                      immutableDataStorage[uint256(uint160(_dest))][index] = value;
42                  }
43              }
44          }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L34:44

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol


27          function markFactoryDeps(bool _shouldSendToL1, bytes32[] calldata _hashes) external onlyCallFromBootloader {
28              unchecked {
29                  uint256 hashesLen = _hashes.length;
30                  for (uint256 i = 0; i < hashesLen; ++i) {
31                      _markBytecodeAsPublished(_hashes[i], _shouldSendToL1);
32                  }
33              }
34          }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L27:34

```solidity
File: system-contracts/contracts/L1Messenger.sol


194         function publishPubdataAndClearState(
195             bytes calldata _totalL2ToL1PubdataAndStateDiffs
196         ) external onlyCallFromBootloader {
197             uint256 calldataPtr = 0;
198     
199             /// Check logs
200             uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
201             require(numberOfL2ToL1Logs <= L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, "Too many L2->L1 logs");
202             calldataPtr += 4;
203     
204             bytes32[] memory l2ToL1LogsTreeArray = new bytes32[](L2_TO_L1_LOGS_MERKLE_TREE_LEAVES);
205             bytes32 reconstructedChainedLogsHash;
206             for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {
207                 bytes32 hashedLog = EfficientCall.keccak(
208                     _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + L2_TO_L1_LOG_SERIALIZE_SIZE]
209                 );
210                 calldataPtr += L2_TO_L1_LOG_SERIALIZE_SIZE;
211                 l2ToL1LogsTreeArray[i] = hashedLog;
212                 reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));
213             }
214             require(
215                 reconstructedChainedLogsHash == chainedLogsHash,
216                 "reconstructedChainedLogsHash is not equal to chainedLogsHash"
217             );
218             for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {
219                 l2ToL1LogsTreeArray[i] = L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH;
220             }
221             uint256 nodesOnCurrentLevel = L2_TO_L1_LOGS_MERKLE_TREE_LEAVES;
222             while (nodesOnCurrentLevel > 1) {
223                 nodesOnCurrentLevel /= 2;
224                 for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {
225                     l2ToL1LogsTreeArray[i] = keccak256(
226                         abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
227                     );
228                 }
229             }
230             bytes32 l2ToL1LogsTreeRoot = l2ToL1LogsTreeArray[0];
231     
232             /// Check messages
233             uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
234             calldataPtr += 4;
235             bytes32 reconstructedChainedMessagesHash;
236             for (uint256 i = 0; i < numberOfMessages; ++i) {
237                 uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
238                 calldataPtr += 4;
239                 bytes32 hashedMessage = EfficientCall.keccak(
240                     _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentMessageLength]
241                 );
242                 calldataPtr += currentMessageLength;
243                 reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));
244             }
245             require(
246                 reconstructedChainedMessagesHash == chainedMessagesHash,
247                 "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
248             );
249     
250             /// Check bytecodes
251             uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
252             calldataPtr += 4;
253             bytes32 reconstructedChainedL1BytecodesRevealDataHash;
254             for (uint256 i = 0; i < numberOfBytecodes; ++i) {
255                 uint32 currentBytecodeLength = uint32(
256                     bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])
257                 );
258                 calldataPtr += 4;
259                 reconstructedChainedL1BytecodesRevealDataHash = keccak256(
260                     abi.encode(
261                         reconstructedChainedL1BytecodesRevealDataHash,
262                         Utils.hashL2Bytecode(
263                             _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
264                         )
265                     )
266                 );
267                 calldataPtr += currentBytecodeLength;
268             }
269             require(
270                 reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
271                 "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
272             );
273     
274             /// Check State Diffs
275             /// encoding is as follows:
276             /// header (1 byte version, 3 bytes total len of compressed, 1 byte enumeration index size)
277             /// body (`compressedStateDiffSize` bytes, 4 bytes number of state diffs, `numberOfStateDiffs` * `STATE_DIFF_ENTRY_SIZE` bytes for the uncompressed state diffs)
278             /// encoded state diffs: [20bytes address][32bytes key][32bytes derived key][8bytes enum index][32bytes initial value][32bytes final value]
279             require(
280                 uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
281                     STATE_DIFF_COMPRESSION_VERSION_NUMBER,
282                 "state diff compression version mismatch"
283             );
284             calldataPtr++;
285     
286             uint24 compressedStateDiffSize = uint24(bytes3(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 3]));
287             calldataPtr += 3;
288     
289             uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));
290             calldataPtr++;
291     
292             bytes calldata compressedStateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr +
293                 compressedStateDiffSize];
294             calldataPtr += compressedStateDiffSize;
295     
296             bytes calldata totalL2ToL1Pubdata = _totalL2ToL1PubdataAndStateDiffs[:calldataPtr];
297     
298             require(calldataPtr <= MAX_ALLOWED_PUBDATA_PER_BATCH, "L1 Messenger pubdata is too long");
299     
300             uint32 numberOfStateDiffs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
301             calldataPtr += 4;
302     
303             bytes calldata stateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr +
304                 (numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE)];
305             calldataPtr += numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE;
306     
307             bytes32 stateDiffHash = COMPRESSOR_CONTRACT.verifyCompressedStateDiffs(
308                 numberOfStateDiffs,
309                 enumerationIndexSize,
310                 stateDiffs,
311                 compressedStateDiffs
312             );
313     
314             /// Check for calldata strict format
315             require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");
316     
317             PUBDATA_CHUNK_PUBLISHER.chunkAndPublishPubdata(totalL2ToL1Pubdata);
318     
319             /// Native (VM) L2 to L1 log
320             SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)), l2ToL1LogsTreeRoot);
321             SystemContractHelper.toL1(
322                 true,
323                 bytes32(uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)),
324                 EfficientCall.keccak(totalL2ToL1Pubdata)
325             );
326             SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.STATE_DIFF_HASH_KEY)), stateDiffHash);
327     
328             /// Clear logs state
329             chainedLogsHash = bytes32(0);
330             numberOfLogsToProcess = 0;
331             chainedMessagesHash = bytes32(0);
332             chainedL1BytecodesRevealDataHash = bytes32(0);
333         }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L194:333

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol


21          function chunkAndPublishPubdata(bytes calldata _pubdata) external onlyCallFrom(address(L1_MESSENGER_CONTRACT)) {
22              require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");
23      
24              bytes32[] memory blobHashes = new bytes32[](MAX_NUMBER_OF_BLOBS);
25      
26              // We allocate to the full size of MAX_NUMBER_OF_BLOBS * BLOB_SIZE_BYTES because we need to pad
27              // the data on the right with 0s if it doesn't take up the full blob
28              bytes memory totalBlobs = new bytes(BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS);
29      
30              assembly {
31                  // The pointer to the allocated memory above. We skip 32 bytes to avoid overwriting the length.
32                  let ptr := add(totalBlobs, 0x20)
33                  calldatacopy(ptr, _pubdata.offset, _pubdata.length)
34              }
35      
36              for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
37                  uint256 start = BLOB_SIZE_BYTES * i;
38      
39                  // We break if the pubdata isn't enough to cover 2 blobs. On L1 it is expected that the hash
40                  // will be bytes32(0) if a blob isn't going to be used.
41                  if (start >= _pubdata.length) {
42                      break;
43                  }
44      
45                  bytes32 blobHash;
46                  assembly {
47                      // The pointer to the allocated memory above skipping the length.
48                      let ptr := add(totalBlobs, 0x20)
49                      blobHash := keccak256(add(ptr, start), BLOB_SIZE_BYTES)
50                  }
51      
52                  blobHashes[i] = blobHash;
53              }
54      
55              SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.BLOB_ONE_HASH_KEY)), blobHashes[0]);
56              SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.BLOB_TWO_HASH_KEY)), blobHashes[1]);
57          }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L21:57

</details>

## L019 - Function calls within for loops:

Making function calls within loops in Solidity can lead to inefficient gas usage, potential bottlenecks, and increased vulnerability to attacks. Each function call or external call consumes gas, and when executed within a loop, the gas cost multiplies, potentially causing the transaction to run out of gas or exceed block gas limits. This can result in transaction failure or unpredictable behavior.


<details>
<summary>Click to show 14 findings</summary>

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


289             for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
290                 // The upgrade transaction must only be included in the first batch.
291                 bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
292                 _lastCommittedBatchData = _commitOneBatch(
293                     _lastCommittedBatchData,
294                     _newBatchesData[i],
295                     expectedUpgradeTxHash
296                 );
297     
298                 s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
299                 emit BlockCommit(
300                     _lastCommittedBatchData.batchNumber,
301                     _lastCommittedBatchData.batchHash,
302                     _lastCommittedBatchData.commitment
303                 );
304             }


351             for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
352                 _executeOneBatch(_batchesData[i], i);
353                 emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
354             }


142             for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
143                 // Extract the values to be compared to/used such as the log sender, key, and value
144                 (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
145                 (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
146                 (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);
147     
148                 // Ensure that the log hasn't been processed already
149                 require(!_checkBit(processedLogs, uint8(logKey)), "kp");
150                 processedLogs = _setBit(processedLogs, uint8(logKey));
151     
152                 // Need to check that each log was sent by the correct address.
153                 if (logKey == uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)) {
154                     require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");
155                     logOutput.l2LogsTreeRoot = logValue;
156                 } else if (logKey == uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)) {
157                     require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");
158                     logOutput.pubdataHash = logValue;
159                 } else if (logKey == uint256(SystemLogKey.STATE_DIFF_HASH_KEY)) {
160                     require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");
161                     logOutput.stateDiffHash = logValue;
162                 } else if (logKey == uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)) {
163                     require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");
164                     logOutput.packedBatchAndL2BlockTimestamp = uint256(logValue);
165                 } else if (logKey == uint256(SystemLogKey.PREV_BATCH_HASH_KEY)) {
166                     require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");
167                     logOutput.previousBatchHash = logValue;
168                 } else if (logKey == uint256(SystemLogKey.CHAINED_PRIORITY_TXN_HASH_KEY)) {
169                     require(logSender == L2_BOOTLOADER_ADDRESS, "bl");
170                     logOutput.chainedPriorityTxsHash = logValue;
171                 } else if (logKey == uint256(SystemLogKey.NUMBER_OF_LAYER_1_TXS_KEY)) {
172                     require(logSender == L2_BOOTLOADER_ADDRESS, "bk");
173                     logOutput.numberOfLayer1Txs = uint256(logValue);
174                 } else if (logKey == uint256(SystemLogKey.BLOB_ONE_HASH_KEY)) {
175                     require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");
176                     logOutput.blob1Hash = logValue;
177                 } else if (logKey == uint256(SystemLogKey.BLOB_TWO_HASH_KEY)) {
178                     require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");
179                     logOutput.blob2Hash = logValue;
180                 } else if (logKey == uint256(SystemLogKey.EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY)) {
181                     require(logSender == L2_BOOTLOADER_ADDRESS, "bu");
182                     require(_expectedSystemContractUpgradeTxHash == logValue, "ut");
183                 } else {
184                     revert("ul");
185                 }
186             }


405             for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {
406                 currentTotalBatchesVerified = currentTotalBatchesVerified.uncheckedInc();
407                 require(
408                     _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
409                     "o1"
410                 );
411     
412                 bytes32 currentBatchCommitment = _committedBatches[i].commitment;
413                 proofPublicInput[i] = _getBatchProofPublicInput(
414                     prevBatchCommitment,
415                     currentBatchCommitment,
416                     verifierParams
417                 );
418     
419                 prevBatchCommitment = currentBatchCommitment;
420             }


257             for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
258                 _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));
259     
260                 s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
261                 emit BlockCommit(
262                     _lastCommittedBatchData.batchNumber,
263                     _lastCommittedBatchData.batchHash,
264                     _lastCommittedBatchData.commitment
265                 );
266             }


636             for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {
637                 bytes32 blobVersionedHash = _getBlobVersionedHash(versionedHashIndex);
638     
639                 require(blobVersionedHash != bytes32(0), "vh");
640     
641                 // First 16 bytes is the opening point. While we get the point as 16 bytes, the point evaluation precompile
642                 // requires it to be 32 bytes. The blob commitment must use the opening point as 16 bytes though.
643                 bytes32 openingPoint = bytes32(
644                     uint256(uint128(bytes16(_pubdataCommitments[i:i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET])))
645                 );
646     
647                 _pointEvaluationPrecompile(
648                     blobVersionedHash,
649                     openingPoint,
650                     _pubdataCommitments[i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET:i + PUBDATA_COMMITMENT_SIZE]
651                 );
652     
653                 // Take the hash of the versioned hash || opening point || claimed value
654                 blobCommitments[versionedHashIndex] = keccak256(
655                     abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
656                 );
657                 versionedHashIndex += 1;
658             }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636:658

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


178             for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
179                 bytes4 selector = _selectors[i];
180                 SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
181                 require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet
182     
183                 _removeOneFunction(oldFacet.facetAddress, selector);
184             }


138             for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
139                 bytes4 selector = _selectors[i];
140                 SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
141                 require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists
142     
143                 _addOneFunction(_facet, selector, _isFacetFreezable);
144             }


158             for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
159                 bytes4 selector = _selectors[i];
160                 SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
161                 require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address
162     
163                 _removeOneFunction(oldFacet.facetAddress, selector);
164                 // Add facet to the list of facets if the facet address is a new one
165                 _saveFacetIfNew(_facet);
166                 _addOneFunction(_facet, selector, _isFacetFreezable);
167             }


101             for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {
102                 Action action = facetCuts[i].action;
103                 address facet = facetCuts[i].facet;
104                 bool isFacetFreezable = facetCuts[i].isFreezable;
105                 bytes4[] memory selectors = facetCuts[i].selectors;
106     
107                 require(selectors.length > 0, "B"); // no functions for diamond cut
108     
109                 if (action == Action.Add) {
110                     _addFunctions(facet, selectors, isFacetFreezable);
111                 } else if (action == Action.Replace) {
112                     _replaceFunctions(facet, selectors, isFacetFreezable);
113                 } else if (action == Action.Remove) {
114                     _removeFunctions(facet, selectors);
115                 } else {
116                     revert("C"); // undefined diamond cut action
117                 }
118             }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101:118

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


29              for (uint256 i; i < pathLength; i = i.uncheckedInc()) {
30                  currentHash = (_index % 2 == 0)
31                      ? _efficientHash(currentHash, _path[i])
32                      : _efficientHash(_path[i], currentHash);
33                  _index /= 2;
34              }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L29:34

```solidity
File: system-contracts/contracts/Compressor.sol


159             for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
160                 bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
161                 uint64 enumIndex = stateDiff.readUint64(84);
162                 if (enumIndex == 0) {
163                     continue;
164                 }
165     
166                 uint256 initValue = stateDiff.readUint256(92);
167                 uint256 finalValue = stateDiff.readUint256(124);
168                 uint256 compressedEnumIndex = _sliceToUint256(
169                     _compressedStateDiffs[stateDiffPtr:stateDiffPtr + _enumerationIndexSize]
170                 );
171                 require(enumIndex == compressedEnumIndex, "rw: enum key mismatch");
172                 stateDiffPtr += _enumerationIndexSize;
173     
174                 uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
175                 stateDiffPtr += 1;
176                 uint8 operation = metadata & OPERATION_BITMASK;
177                 uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
178                 _verifyValueCompression(
179                     initValue,
180                     finalValue,
181                     operation,
182                     _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
183                 );
184                 stateDiffPtr += len;
185             }


127             for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
128                 bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
129                 uint64 enumIndex = stateDiff.readUint64(84);
130                 if (enumIndex != 0) {
131                     // It is a repeated write, so we skip it.
132                     continue;
133                 }
134     
135                 numInitialWritesProcessed++;
136     
137                 bytes32 derivedKey = stateDiff.readBytes32(52);
138                 uint256 initValue = stateDiff.readUint256(92);
139                 uint256 finalValue = stateDiff.readUint256(124);
140                 require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");
141                 stateDiffPtr += 32;
142     
143                 uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
144                 stateDiffPtr++;
145                 uint8 operation = metadata & OPERATION_BITMASK;
146                 uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
147                 _verifyValueCompression(
148                     initValue,
149                     finalValue,
150                     operation,
151                     _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
152                 );
153                 stateDiffPtr += len;
154             }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L127:154

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol


30                  for (uint256 i = 0; i < hashesLen; ++i) {
31                      _markBytecodeAsPublished(_hashes[i], _shouldSendToL1);
32                  }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L30:32

</details>

## L020 - External calls in an unbounded for-loop may result in a DoS:

Consider limiting the number of iterations in for-loops that make external calls.


<details>
<summary>Click to show 11 findings</summary>

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


185                 for (uint256 i = 0; i < _newBatchesData.length; ++i) {


209                 for (uint256 i = 0; i < _newBatchesData.length; ++i) {


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209:209

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


142             for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {


257             for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {


289             for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {


636             for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {


667             for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667:667

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


226             for (uint256 i = 0; i < _factoryDeps.length; ++i) {


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226:226

```solidity
File: system-contracts/contracts/Compressor.sol


61                  for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {


127             for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {


159             for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L159:159

</details>

## L021 - Contracts are not using their OZ Upgradeable counterparts:

The non-upgradeable standard version of OpenZeppelinâ€™s library is inherited/used by the contracts. It would be safer to use the upgradeable versions of the library contracts to avoid unexpected behavior.

Use the contracts from `@openzeppelin/contracts-upgradeable` instead of `@openzeppelin/contracts` where applicable. See https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/tree/master/contracts for a list of available upgradeable contracts


<details>
<summary>Click to show 20 findings</summary>

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


6       import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";


5       import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L5:5

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


8       import {IERC20Metadata} from "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";


5       import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";


9       import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";


10      import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";


6       import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L6:6

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


5       import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L5:5

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol


5       import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L5:5

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


16      import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L16:16

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


5       import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L5:5

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


5       import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L5:5

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


5       import {SafeCast} from "@openzeppelin/contracts/utils/math/SafeCast.sol";


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L5:5

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


5       import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L5:5

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


6       import {BeaconProxy} from "@openzeppelin/contracts/proxy/beacon/BeaconProxy.sol";


5       import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";


7       import {UpgradeableBeacon} from "@openzeppelin/contracts/proxy/beacon/UpgradeableBeacon.sol";


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L7:7

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol


6       import {UpgradeableBeacon} from "@openzeppelin/contracts/proxy/beacon/UpgradeableBeacon.sol";


5       import {ERC20PermitUpgradeable} from "@openzeppelin/contracts-upgradeable/token/ERC20/extensions/draft-ERC20PermitUpgradeable.sol";


7       import {ERC1967Upgrade} from "@openzeppelin/contracts/proxy/ERC1967/ERC1967Upgrade.sol";


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L7:7

</details>

## L022 - Multiplication on the result of a division:

Dividing an integer by another integer will often result in loss of precision. When the result is multiplied by another number, the loss of precision is magnified, often to material magnitudes. (X / Z) * Y should be re-written as (X * Y) / Z.


```solidity
File: system-contracts/contracts/L1Messenger.sol


51              return KECCAK_ROUND_GAS_COST * (_length / KECCAK_ROUND_NUMBER_OF_BYTES + 1);


62              return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L62:62


## L023 - `decimals()` is not a part of the ERC-20 standard:

The `decimals()` function is not a part of the [ERC-20 standard](https://eips.ethereum.org/EIPS/eip-20), and was added later as an [optional extension](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/IERC20Metadata.sol). As such, some valid ERC20 tokens do not support this interface, so it is unsafe to blindly cast all tokens to this interface, and then call this function.


```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


264             (, bytes memory data3) = _token.staticcall(abi.encodeCall(IERC20Metadata.decimals, ()));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L264:264

## L024 - `symbol()` is not a part of the ERC-20 standard:

The `symbol()` function is not a part of the [ERC-20 standard](https://eips.ethereum.org/EIPS/eip-20), and was added later as an [optional extension](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/IERC20Metadata.sol). As such, some valid ERC20 tokens do not support this interface, so it is unsafe to blindly cast all tokens to this interface, and then call this function.


```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


263             (, bytes memory data2) = _token.staticcall(abi.encodeCall(IERC20Metadata.symbol, ()));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L263:263

## L025 - `name()` is not a part of the ERC-20 standard:

The `name()` function is not a part of the [ERC-20 standard](https://eips.ethereum.org/EIPS/eip-20), and was added later as an [optional extension](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/IERC20Metadata.sol). As such, some valid ERC20 tokens do not support this interface, so it is unsafe to blindly cast all tokens to this interface, and then call this function.


```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


262             (, bytes memory data1) = _token.staticcall(abi.encodeCall(IERC20Metadata.name, ()));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L262:262

## L026 - Missing checks for address(0x0) in the constructor:




```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


96              l1WethAddress = _l1WethAddress;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L96:96

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol


46              securityCouncil = _securityCouncil;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L46:46

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


59              bridgehub = _bridgehub;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L59:59

## L027 - Missing checks for address(0x0) in the initializer:




```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


41          function initialize(address _owner) external reentrancyGuardInitializer {
42              _transferOwnership(_owner);
43          }


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L41:43

## L028 - Governance functions should be controlled by time locks:

Governance functions (such as upgrading contracts, setting critical parameters) should be controlled using time locks to introduce a delay between a proposal and its execution. This gives users time to exit before a potentially dangerous or malicious operation is applied.


<details>
<summary>Click to show 19 findings</summary>

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


116         function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {

142         function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L142:144

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


108         function setSharedBridge(address _sharedBridge) external onlyOwner {

92          function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner {

82          function addStateTransitionManager(address _stateTransitionManager) external onlyOwner {

101         function addToken(address _token) external onlyOwner {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L101:104

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol


129         function scheduleTransparent(Operation calldata _operation, uint256 _delay) external onlyOwner {

154         function cancel(bytes32 _id) external onlyOwner {

142         function scheduleShadow(bytes32 _id, uint256 _delay) external onlyOwner {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L142:145

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


160         function freezeChain(uint256 _chainId) external onlyOwner {

230         function registerAlreadyDeployedStateTransition(
231             uint256 _chainId,
232             address _stateTransitionContract
233         ) external onlyOwner {

165         function unfreezeChain(uint256 _chainId) external onlyOwner {

152         function setUpgradeDiamondCut(
153             Diamond.DiamondCutData calldata _cutData,
154             uint256 _oldProtocolVersion
155         ) external onlyOwner {

142         function setNewVersionUpgrade(
143             Diamond.DiamondCutData calldata _cutData,
144             uint256 _oldProtocolVersion,
145             uint256 _newProtocolVersion
146         ) external onlyOwner {

137         function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L137:139

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


73          function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {

96          function setExecutionDelay(uint32 _executionDelay) external onlyOwner {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96:99

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


23          function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {

89          function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L89:93

</details>

## L029 - Code does not follow the best practice of check-effects-interaction:

Code should follow the best-practice of [check-effects-interaction](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs.


<details>
<summary>Click to show 7 findings</summary>

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


/// @audit IMailbox.transferEthToSharedBridge() called prior to this assignment
133                 chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;


/// @audit _depositFunds() called prior to this assignment
/// @audit contains nested function call _token.balanceOf() 
/// @audit located in file zksync/contracts/ethereum/contracts/bridge/L1SharedBridge.sol  
165                 chainBalance[_chainId][_l1Token] += _amount;


/// @audit _depositFunds() called prior to this assignment
/// @audit contains nested function call _token.balanceOf() 
/// @audit located in file zksync/contracts/ethereum/contracts/bridge/L1SharedBridge.sol  
212                 chainBalance[_chainId][_l1Token] += amount;


/// @audit _finalizeWithdrawal() called prior to this assignment
/// @audit contains nested function call IGetters.isEthWithdrawalFinalized() 
/// @audit located in file zksync/contracts/ethereum/contracts/bridge/L1SharedBridge.sol  
440                 chainBalance[_chainId][l1Token] -= amount;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L440:440

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


/// @audit bytes.concat() called prior to this assignment
282             stateTransition[_chainId] = stateTransitionAddress;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L282:282

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


/// @audit IStateTransitionManager.protocolVersion() called prior to this assignment
260                 s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L260:260

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


/// @audit l2TokenAddress() called prior to this assignment
/// @audit contains nested function call bytes.concat() 
/// @audit located in file zksync/contracts/zksync/contracts/bridge/L2SharedBridge.sol  
99                  l1TokenAddress[expectedL2Token] = _l1Token;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L99:99

</details>

## L030 - addresses upcast and compared to values larger than a uint160, may result in collisions:

If the value is being compared to an input value in order to reject it, rather than allowing it to be converted to an address, the check will pass if the value is larger than type(uint160).max, even if, when cast, it matches the gating address.


```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol


95              return _addr == uint256(uint160(address(BASE_TOKEN_SYSTEM_CONTRACT))) || _addr == 0;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L95:95

## L031 - Missing checks for address(0x0) when updating address state variables:

issing checks for address(0x0) when updating address state variables


<details>
<summary>Click to show 17 findings</summary>

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


96              l1WethAddress = _l1WethAddress;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L96:96

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


55              pendingAdmin = _newPendingAdmin;


65              admin = currentPendingAdmin;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L65:65

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol


46              securityCouncil = _securityCouncil;


258             securityCouncil = _newSecurityCouncil;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L258:258

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


59              bridgehub = _bridgehub;


114             pendingAdmin = _newPendingAdmin;


124             admin = currentPendingAdmin;


133             validatorTimelock = _validatorTimelock;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L133:133

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


27              s.pendingAdmin = _newPendingAdmin;


37              s.admin = pendingAdmin;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L37:37

```solidity
File: contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


30                  l2Address = address(uint160(l1Address) + offset);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L30:30

```solidity
File: contracts/zksync/contracts/vendor/AddressAliasHelper.sol


30                  l2Address = address(uint160(l1Address) + offset);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L30:30

```solidity
File: system-contracts/contracts/ContractDeployer.sol


109             newAddress = address(uint160(uint256(hash)));


125             newAddress = address(uint160(uint256(hash)));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L125:125

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol


32              to = address(uint160(addressAsUint));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L32:32

```solidity
File: system-contracts/contracts/SystemContext.sol


100             origin = _newOrigin;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L100:100

</details>

## L032 - The additions/multiplications may silently overflow because they're in unchecked blocks with no preceding value checks, which may lead to unexpected results.:

The additions/multiplications may silently overflow because they're in unchecked blocks with no preceding value checks, which may lead to unexpected results.


<details>
<summary>Click to show 45 findings</summary>

```solidity
File: contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


13                  return _number + 1;


19                  return _lhs + _rhs;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L19:19

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


195                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed


217                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L217:217

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


23                  uint256 mapValue = _map.map[_index / 8];


27                  uint256 bitOffset = (_index & 7) * 32;


43                  uint256 mapIndex = _index / 8;


48                  uint256 bitOffset = (_index & 7) * 32;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L48:48

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


118                 txBodyGasLimit = _totalGasLimit - overhead;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L118:118

```solidity
File: contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


30                  l2Address = address(uint160(l1Address) + offset);


40                  l1Address = address(uint160(l2Address) - offset);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L40:40

```solidity
File: contracts/zksync/contracts/vendor/AddressAliasHelper.sol


30                  l2Address = address(uint160(l1Address) + offset);


40                  l1Address = address(uint160(l2Address) - offset);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L40:40

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol


105                 uint256 listLength = encodedNonce.length +
106                     encodedGasParam.length +
107                     encodedTo.length +
108                     encodedValue.length +
109                     encodedDataLength.length +
110                     _transaction.data.length +
111                     rEncoded.length +
112                     sEncoded.length +
113                     vEncoded.length;


198                 uint256 listLength = encodedFixedLengthParams.length +
199                     encodedDataLength.length +
200                     _transaction.data.length +
201                     encodedAccessListLength.length +
202                     rEncoded.length +
203                     sEncoded.length +
204                     vEncoded.length;


293                 uint256 listLength = encodedFixedLengthParams.length +
294                     encodedDataLength.length +
295                     _transaction.data.length +
296                     encodedAccessListLength.length +
297                     rEncoded.length +
298                     sEncoded.length +
299                     vEncoded.length;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L293:299

```solidity
File: system-contracts/contracts/Compressor.sol


52                      encodedData.length * 4 == _bytecode.length,


57                      dictionary.length / 8 <= encodedData.length / 2,


62                      uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;


66                      uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);


203                 dictionary = _rawCompressedData[2:2 + dictionaryLen * 8];


204                 encodedData = _rawCompressedData[2 + dictionaryLen * 8:];


233                         _initialValue + convertedValue == _finalValue,


238                         _initialValue - convertedValue == _finalValue,


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L238:238

```solidity
File: system-contracts/contracts/L1Messenger.sol


140                 pubdataLen = 4 + _message.length + L2_TO_L1_LOG_SERIALIZE_SIZE;


171                 pubdataLen = 4 + bytecodeLen;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L171:171

```solidity
File: system-contracts/contracts/L2BaseToken.sol


43                  balance[_from] = fromBalance - _amount;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L43:43

```solidity
File: system-contracts/contracts/NonceHolder.sol


72                  rawNonces[addressAsKey] = (oldRawNonce + _value);


118                 rawNonces[addressAsKey] = oldRawNonce + 1;


144                 rawNonces[addressAsKey] = (oldRawNonce + DEPLOY_NONCE_MULTIPLIER);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L144:144

```solidity
File: system-contracts/contracts/SystemContext.sol


248                 bytes32 correctPrevBlockHash = _calculateLegacyL2BlockHash(_l2BlockNumber - 1);


255                 _setL2BlockHash(_l2BlockNumber - 1, correctPrevBlockHash);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L255:255

```solidity
File: system-contracts/contracts/libraries/RLPEncoder.sol


33                      encoded = new bytes(hbs + 2);


34                      encoded[0] = bytes1(uint8(hbs + 0x81));


36                      uint256 lbs = 31 - hbs;


37                      uint256 shiftedVal = _val << (lbs * 8);


64                      encoded[0] = bytes1(uint8(_len + _offset));


68                      encoded = new bytes(hbs + 2);


69                      encoded[0] = bytes1(uint8(_offset + hbs + 56));


71                      uint256 lbs = 31 - hbs;


72                      uint256 shiftedVal = uint256(_len) << (lbs * 8);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L72:72

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol


190                 uint256 listLength = encodedNonce.length +
191                     encodedGasParam.length +
192                     encodedTo.length +
193                     encodedValue.length +
194                     encodedDataLength.length +
195                     _transaction.data.length +
196                     encodedChainId.length;


265                 uint256 listLength = encodedFixedLengthParams.length +
266                     encodedDataLength.length +
267                     _transaction.data.length +
268                     encodedAccessListLength.length;


337                 uint256 listLength = encodedFixedLengthParams.length +
338                     encodedDataLength.length +
339                     _transaction.data.length +
340                     encodedAccessListLength.length;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L337:340

```solidity
File: system-contracts/contracts/libraries/Utils.sol


46                  codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L46:46

</details>



