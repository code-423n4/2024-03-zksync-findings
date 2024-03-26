## Summary

---

### Gas Optimizations
|Id|Title|Instances|Gas Saved|
|:--:|:------|:--:|---:|
|[[G-01]](#g-01-use-arrayunsafeaccess-to-avoid-repeated-array-length-checks)| Use `Array.unsafeAccess` to avoid repeated array length checks | 50 | 105,000 |
|[[G-02]](#g-02-state-variables-can-be-packed-into-fewer-storage-slots)| State variables can be packed into fewer storage slots | 2 | 40,000 |
|[[G-03]](#g-03-state-variables-can-be-modified-to-fit-in-fewer-storage-slots)| State variables can be modified to fit in fewer storage slots | 1 | 20,000 |
|[[G-04]](#g-04-structs-can-be-packed-into-fewer-storage-slots)| Structs can be packed into fewer storage slots | 3 | 60,000 |
|[[G-05]](#g-05-structs-can-be-modified-to-fit-in-fewer-storage-slots)| Structs can be modified to fit in fewer storage slots | 2 | 40,000 |
|[[G-06]](#g-06-multiple-mappings-that-share-an-id-can-be-combined-into-a-single-mapping-of-id--struct)| Multiple `mapping`s that share an ID can be combined into a single `mapping` of ID / `struct` | 3 | 60,000 |
|[[G-07]](#g-07-use-of-memory-instead-of-storage-for-structarray-state-variables)| Use of `memory` instead of `storage` for struct/array state variables | 5 | 10,500 |
|[[G-08]](#g-08-unused-non-constant-state-variables-waste-gas)| Unused non-constant state variables waste gas | 1 | - |
|[[G-09]](#g-09-state-variables-only-set-in-their-definitions-should-be-declared-constant)| State variables only set in their definitions should be declared `constant` | 3 | 66,291 |
|[[G-10]](#g-10-cache-state-variables-with-stack-variables)| Cache state variables with stack variables | 6 | 1,700 |
|[[G-11]](#g-11-low-level-call-can-be-optimized-with-assembly)| Low level `call` can be optimized with assembly | 1 | 248 |
|[[G-12]](#g-12-use-of-memory-instead-of-calldata-for-immutable-arguments)| Use of `memory` instead of `calldata` for immutable arguments | 40 | 11,528 |
|[[G-13]](#g-13-avoid-updating-storage-when-the-value-hasnt-changed)| Avoid updating storage when the value hasn't changed | 21 | 14,700 |
|[[G-14]](#g-14-use-of-emit-inside-a-loop)| Use of `emit` inside a loop | 3 | 3,078 |
|[[G-15]](#g-15-use-uint2561uint2562-instead-of-truefalse-to-save-gas-for-changes)| Use `uint256(1)/uint256(2)` instead of `true/false` to save gas for changes | 6 | 102,000 |
|[[G-16]](#g-16-shortcircuit-rules-can-be-be-used-to-optimize-some-gas-usage)| Shortcircuit rules can be be used to optimize some gas usage | 2 | 8,400 |
|[[G-17]](#g-17-cache-multiple-accesses-of-a-mappingarray)| Cache multiple accesses of a mapping/array | 8 | 546 |
|[[G-18]](#g-18-using-private-for-constants-saves-gas)| Using `private` for constants saves gas | 5 | 42,030 |
|[[G-19]](#g-19-require-or-revert-statements-that-check-input-arguments-should-be-at-the-top-of-the-function)| require() or revert() statements that check input arguments should be at the top of the function | 7 | - |
|[[G-20]](#g-20-custom-errors-cost-less-than-requireassert)| Custom `error`s cost less than `require`/`assert` | 333 | 9,657 |
|[[G-21]](#g-21-consider-activating-via-ir-for-deploying)| Consider activating `via-ir` for deploying | - | - |
|[[G-22]](#g-22-function-calls-should-be-cached-instead-of-re-calling-the-function)| Function calls should be cached instead of re-calling the function | 3 | - |
|[[G-23]](#g-23-functions-that-revert-when-called-by-normal-users-can-be-payable)| Functions that revert when called by normal users can be `payable` | 88 | 1,848 |
|[[G-24]](#g-24-cache-keccak256-with-static-arguments)| Cache `keccak256` with static arguments | 2 | 10 |
|[[G-25]](#g-25-array-length-is-not-cached)| Array `length` is not cached | 11 | 33 |
|[[G-26]](#g-26-caching-global-variables-is-more-expensive-than-using-the-actual-variable)| Caching global variables is more expensive than using the actual variable | 1 | 12 |
|[[G-27]](#g-27-add-unchecked-blocks-for-subtractions-where-the-operands-cannot-underflow)| Add `unchecked` blocks for subtractions where the operands cannot underflow | 4 | 340 |
|[[G-28]](#g-28-add-unchecked-blocks-for-divisions-where-the-operands-cannot-overflow)| Add `unchecked` blocks for divisions where the operands cannot overflow | 10 | 1,590 |
|[[G-29]](#g-29-usage-of-uintsints-smaller-than-32-bytes-256-bits-incurs-overhead)| Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead | 204 | 1,224 |
|[[G-30]](#g-30-stack-variable-cost-less-while-used-in-emitting-event)| Stack variable cost less while used in emitting event | 8 | 72 |
|[[G-31]](#g-31-using-pre-instead-of-post-incrementsdecrements)| Using pre instead of post increments/decrements | 5 | 10 |
|[[G-32]](#g-32--costs-less-gas-than)| `>=`/`<=` costs less gas than `>`/`<` | 97 | 291 |
|[[G-33]](#g-33-internal-functions-only-called-once-can-be-inlined-to-save-gas)| `internal` functions only called once can be inlined to save gas | 80 | 1,600 |
|[[G-34]](#g-34-inline-modifiers-that-are-only-used-once-to-save-gas)| Inline `modifiers` that are only used once, to save gas | 7 | - |
|[[G-35]](#g-35-private-functions-only-called-once-can-be-inlined-to-save-gas)| `private` functions only called once can be inlined to save gas | 15 | 300 |
|[[G-36]](#g-36-abiencode-is-less-efficient-than-abiencodepacked-for-non-address-arguments)| `abi.encode()` is less efficient than `abi.encodepacked()` for non-address arguments | 32 | 160 |
|[[G-37]](#g-37-boolean-comparison-with-boolean-literals-is-unnecessary)| Boolean comparison with boolean literals is unnecessary | 1 | 9 |
|[[G-38]](#g-38-unused-named-return-variables-without-optimizer-waste-gas)| Unused named return variables without optimizer waste gas | 3 | 9 |
|[[G-39]](#g-39-using-thisfn-wastes-gas)| Using `this.<fn>()` wastes gas | 4 | 400 |
|[[G-40]](#g-40-consider-pre-calculating-the-address-of-addressthis-to-save-gas)| Consider pre-calculating the address of `address(this)` to save gas | 21 | - |
|[[G-41]](#g-41-consider-using-soladys-fixedpointmathlib)| Consider using Solady's `FixedPointMathLib` | 3 | - |
|[[G-42]](#g-42-reduce-deployment-costs-by-tweaking-contracts-metadata)| Reduce deployment costs by tweaking contracts' metadata | 104 | - |
|[[G-43]](#g-43-emitting-constants-wastes-gas)| Emitting constants wastes gas | 1 | 8 |
|[[G-44]](#g-44-update-openzeppelin-dependency-to-save-gas)| Update OpenZeppelin dependency to save gas | 22 | - |
|[[G-45]](#g-45-function-names-can-be-optimized)| Function names can be optimized | 80 | 1,760 |
|[[G-46]](#g-46-using-delete-instead-of-setting-mappingstruct-to-0-saves-gas)| Using `delete` instead of setting mapping/struct to 0 saves gas | 3 | 15 |
|[[G-47]](#g-47-expression--is-cheaper-than-new-bytes0)| Expression `""` is cheaper than `new bytes(0)` | 8 | 1,904 |
|[[G-48]](#g-48-using-bool-for-storage-incurs-overhead)| Using `bool` for storage incurs overhead | 6 | 600 |
|[[G-49]](#g-49-multiplicationdivision-by-two-should-use-bit-shifting)| Multiplication/division by two should use bit shifting | 4 | 80 |
|[[G-50]](#g-50-x--y-is-more-expensive-than-x--x--y-for-state-variables)| `x += y` is more expensive than `x = x + y` for state variables | 3 | 60 |
|[[G-51]](#g-51-use-of--is-cheaper-for-mappings)| Use of `+=` is cheaper for mappings | 2 | 80 |
|[[G-52]](#g-52-mappings-are-cheaper-to-use-than-storage-arrays)| Mappings are cheaper to use than storage arrays | 1 | 2,100 |
|[[G-53]](#g-53-bytes-constants-are-more-efficient-than-string-constants)| Bytes constants are more efficient than string constants | 5 | 1,890 |
|[[G-54]](#g-54-constructors-can-be-marked-payable)| Constructors can be marked `payable` | 10 | 210 |
|[[G-55]](#g-55-long-revert-strings)| Long revert strings | 104 | 2,196 |
|[[G-56]](#g-56-splitting-require-statements-that-use--saves-gas)| Splitting `require` statements that use `&&` saves gas | 3 | 9 |
|[[G-57]](#g-57-nesting-if-statements-that-use--saves-gas)| Nesting `if` statements that use `&&` saves gas | 12 | 360 |
|[[G-58]](#g-58-counting-down-when-iterating-saves-gas)| Counting down when iterating, saves gas | 18 | 108 |
|[[G-59]](#g-59-do-while-is-cheaper-than-for-loops-when-the-initial-check-can-be-skipped)| `do-while` is cheaper than `for`-loops when the initial check can be skipped | 35 | - |
|[[G-60]](#g-60-lack-of-unchecked-in-loops)| Lack of `unchecked` in loops | 12 | 720 |
|[[G-61]](#g-61-pre-compute-hashes)| Pre-compute hashes | 2 | 10 |
|[[G-62]](#g-62-uint-comparison-with-zero-can-be-cheaper)| `uint` comparison with zero can be cheaper | 24 | 96 |
|[[G-63]](#g-63-use-assembly-to-check-for-address0)| Use assembly to check for `address(0)` | 30 | 180 |
|[[G-64]](#g-64-use-scratch-space-for-building-calldata-with-assembly)| Use scratch space for building calldata with assembly | 275 | 60,500 |
|[[G-65]](#g-65-use-assembly-to-write-hashes)| Use assembly to write hashes | 56 | 6,720 |
|[[G-66]](#g-66-use-assembly-to-validate-msgsender)| Use assembly to validate `msg.sender` | 42 | 504 |
|[[G-67]](#g-67-use-assembly-to-write-address-storage-values)| Use assembly to write `address` storage values | 16 | 1,184 |
|[[G-68]](#g-68-use-assembly-to-emit-an-event)| Use assembly to emit an `event` | 77 | 2,926 |

Total: 2056 instances over 68 issues with an estimate of **687,806 gas** saved.

## Gas Optimizations

---

### [G-01] Use `Array.unsafeAccess` to avoid repeated array length checks

When using storage arrays, solidity adds an internal lookup of the array's length (a **Gcoldsload 2100 gas**) to ensure it doesn't read past the array's end.

It's possible to avoid this lookup by using `Array.unsafeAccess` in cases where the length has already been checked.

*There are 50 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/Compressor.sol

143: 		            uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

174: 		            uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
```
[[143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L143), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L174)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

249: 		            sumOfValues += _deployments[i].value;

254: 		            this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
```
[[249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L249), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L254)]



```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

39: 		                uint256 index = _immutables[i].index;

40: 		                bytes32 value = _immutables[i].value;

41: 		                immutableDataStorage[uint256(uint160(_dest))][index] = value;
```
[[39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L39), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L40), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L41)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

31: 		                _markBytecodeAsPublished(_hashes[i], _shouldSendToL1);
```
[[31](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L31)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

211: 		            l2ToL1LogsTreeArray[i] = hashedLog;

219: 		            l2ToL1LogsTreeArray[i] = L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH;

225: 		                l2ToL1LogsTreeArray[i] = keccak256(

226: 		                    abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
```
[[211](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L211), [219](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L219), [225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L225), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L226)]



```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

52: 		            blobHashes[i] = blobHash;
```
[[52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L52)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

226: 		            (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```
[[226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

117: 		                committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);

136: 		                committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);

186: 		                uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(

187: 		                    _newBatchesData[i].batchNumber

210: 		                uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
```
[[117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L117), [136](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L136), [186](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L186), [187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L187), [210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L210)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

228: 		                L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
```
[[228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L228)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

102: 		            Action action = facetCuts[i].action;

103: 		            address facet = facetCuts[i].facet;

104: 		            bool isFacetFreezable = facetCuts[i].isFreezable;

105: 		            bytes4[] memory selectors = facetCuts[i].selectors;

139: 		            bytes4 selector = _selectors[i];

140: 		            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

159: 		            bytes4 selector = _selectors[i];

160: 		            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

179: 		            bytes4 selector = _selectors[i];

180: 		            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
```
[[102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L102), [103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L103), [104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L104), [105](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L105), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L139), [140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L140), [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L159), [160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L160), [179](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L179), [180](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L180)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

31: 		                ? _efficientHash(currentHash, _path[i])

32: 		                : _efficientHash(_path[i], currentHash);
```
[[31](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L31), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L32)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

258: 		            _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));

260: 		            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);

294: 		                _newBatchesData[i],

298: 		            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);

352: 		            _executeOneBatch(_batchesData[i], i);

353: 		            emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

408: 		                _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],

412: 		            bytes32 currentBatchCommitment = _committedBatches[i].commitment;

413: 		            proofPublicInput[i] = _getBatchProofPublicInput(

581: 		            blobAuxOutputWords[i * 2] = _blobHashes[i];

582: 		            blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];

654: 		            blobCommitments[versionedHashIndex] = keccak256(

669: 		                (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||

670: 		                    (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
```
[[258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L258), [260](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L260), [294](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L294), [298](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L298), [352](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L352), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353), [408](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L408), [412](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L412), [413](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L413), [581](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L581), [582](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L582), [654](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L654), [669](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L669), [670](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

209: 		            address facetAddr = ds.facets[i];

210: 		            Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];

212: 		            result[i] = Facet(facetAddr, facetToSelectors.selectors);
```
[[209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L209), [210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L210), [212](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L212)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

357: 		            bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);
```
[[357](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L357)]

</details>

---

### [G-02] State variables can be packed into fewer storage slots

Each slot saved can avoid an extra Gsset (**20000 gas**). Reads and writes (if two variables that occupy the same slot are written by the same function) will have a cheaper gas consumption.

*There are 2 instances of this issue.*


```solidity
File: code/system-contracts/contracts/SystemContext.sol

// @audit Can save 1 storage slot (from 17 to 16) 
// @audit Consider using the following order:
/*
  *	uint256 chainId (32)
  *	uint256 gasPrice (32)
  *	uint256 blockGasLimit (32)
  *	uint256 difficulty (32)
  *	uint256 baseFee (32)
  *	BlockInfo currentBatchInfo (32)
  *	mapping(uint256 => bytes32) batchHashes (32)
  *	BlockInfo currentL2BlockInfo (32)
  *	bytes32 currentL2BlockTxsRollingHash (32)
  *	bytes32[] l2BlockHash (32)
  *	BlockInfo currentVirtualL2BlockInfo (32)
  *	VirtualBlockUpgradeInfo virtualBlockUpgradeInfo (32)
  *	uint256 gasPerPubdataByte (32)
  *	uint256 basePubdataSpent (32)
  *	address origin (20)
  *	uint16 txNumberInBlock (2)
  *	address coinbase (20)
*/
17: 		contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract {
```
[[17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L17)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

// @audit Can save 1 storage slot (from 4 to 3) 
// @audit Consider using the following order:
/*
  *	mapping(uint256 => LibMap.Uint32Map) committedBatchTimestamp (32)
  *	mapping(uint256 => mapping(address => bool)) validators (32)
  *	IStateTransitionManager stateTransitionManager (20)
  *	uint32 executionDelay (4)
*/
22: 		contract ValidatorTimelock is IExecutor, Ownable2Step {
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L22)]


---

### [G-03] State variables can be modified to fit in fewer storage slots

Some state variables can be safely modified, and as result, the contract will use fewer storage slots. Each slot saved can avoid an extra Gsset (**20000 gas**) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings.

*There is 1 instance of this issue.*


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

// @audit Supposing an already optimal order, this can save 1 storage slot (from 3 to 2) by modifying the following variables:
// @audit uint256 minDelay -> uint32 minDelay

// @audit Consider using the following order:
/*
  *	mapping(bytes32 => uint256) timestamps (32)
  *	address securityCouncil (20)
  *	uint32 minDelay (4)
*/
20: 		contract Governance is IGovernance, Ownable2Step {
```
[[20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L20)]


---

### [G-04] Structs can be packed into fewer storage slots

Each slot saved can avoid an extra Gsset (**20000 gas**) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings.

*There are 3 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

// @audit Can save 1 storage slot (from 8 to 7) 
// @audit Consider using the following order:
/*
  *	bytes32 genesisBatchHash (32)
  *	bytes32 genesisBatchCommitment (32)
  *	uint256 protocolVersion (32)
  *	address governor (20)
  *	uint64 genesisIndexRepeatedStorageChanges (8)
  *	address validatorTimelock (20)
  *	address genesisUpgrade (20)
  *	Diamond.DiamondCutData diamondCut (20)
*/
15: 		struct StateTransitionManagerInitializeData {
16: 		    address governor;
17: 		    address validatorTimelock;
18: 		    address genesisUpgrade;
19: 		    bytes32 genesisBatchHash;
20: 		    uint64 genesisIndexRepeatedStorageChanges;
21: 		    bytes32 genesisBatchCommitment;
22: 		    Diamond.DiamondCutData diamondCut;
23: 		    uint256 protocolVersion;
24: 		}
```
[[15-24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L15-L24)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

// @audit Can save 1 storage slot (from 35 to 34) 
// @audit Consider using the following order:
/*
  *	uint256[] __DEPRECATED_diamondCutStorage (32)
  *	mapping(address => bool) validators (32)
  *	uint256 totalBatchesExecuted (32)
  *	uint256 totalBatchesVerified (32)
  *	uint256 totalBatchesCommitted (32)
  *	mapping(uint256 => bytes32) storedBatchHashes (32)
  *	mapping(uint256 => bytes32) l2LogsRootHashes (32)
  *	VerifierParams verifierParams (32)
  *	bytes32 l2BootloaderBytecodeHash (32)
  *	bytes32 l2DefaultAccountBytecodeHash (32)
  *	uint256 priorityTxMaxGasLimit (32)
  *	UpgradeStorage __DEPRECATED_upgrades (32)
  *	mapping(uint256 => mapping(uint256 => bool)) isEthWithdrawalFinalized (32)
  *	uint256 __DEPRECATED_lastWithdrawalLimitReset (32)
  *	uint256 __DEPRECATED_withdrawnAmountInWindow (32)
  *	mapping(address => uint256) __DEPRECATED_totalDepositedAmountPerUser (32)
  *	uint256 protocolVersion (32)
  *	bytes32 l2SystemContractsUpgradeTxHash (32)
  *	uint256 l2SystemContractsUpgradeBatchNumber (32)
  *	FeeParams feeParams (32)
  *	uint256 chainId (32)
  *	uint128 baseTokenGasPriceMultiplierNominator (16)
  *	uint128 baseTokenGasPriceMultiplierDenominator (16)
  *	address __DEPRECATED_governor (20)
  *	bool zkPorterIsAvailable (1)
  *	address __DEPRECATED_pendingGovernor (20)
  *	IVerifier verifier (20)
  *	PriorityQueue.Queue priorityQueue (20)
  *	address __DEPRECATED_allowList (20)
  *	address admin (20)
  *	address pendingAdmin (20)
  *	address blobVersionedHashRetriever (20)
  *	address bridgehub (20)
  *	address stateTransitionManager (20)
  *	address baseToken (20)
  *	address baseTokenBridge (20)
*/
66: 		struct ZkSyncStateTransitionStorage {
67: 		    /// @dev Storage of variables needed for deprecated diamond cut facet
68: 		    uint256[7] __DEPRECATED_diamondCutStorage;
69: 		    /// @notice Address which will exercise critical changes to the Diamond Proxy (upgrades, freezing & unfreezing). Replaced by STM
70: 		    address __DEPRECATED_governor;
71: 		    /// @notice Address that the governor proposed as one that will replace it
72: 		    address __DEPRECATED_pendingGovernor;
73: 		    /// @notice List of permitted validators
74: 		    mapping(address validatorAddress => bool isValidator) validators;
75: 		    /// @dev Verifier contract. Used to verify aggregated proof for batches
76: 		    IVerifier verifier;
77: 		    /// @notice Total number of executed batches i.e. batches[totalBatchesExecuted] points at the latest executed batch
78: 		    /// (batch 0 is genesis)
79: 		    uint256 totalBatchesExecuted;
80: 		    /// @notice Total number of proved batches i.e. batches[totalBatchesProved] points at the latest proved batch
81: 		    uint256 totalBatchesVerified;
82: 		    /// @notice Total number of committed batches i.e. batches[totalBatchesCommitted] points at the latest committed
83: 		    /// batch
84: 		    uint256 totalBatchesCommitted;
85: 		    /// @dev Stored hashed StoredBatch for batch number
86: 		    mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
87: 		    /// @dev Stored root hashes of L2 -> L1 logs
88: 		    mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;
89: 		    /// @dev Container that stores transactions requested from L1
90: 		    PriorityQueue.Queue priorityQueue;
91: 		    /// @dev The smart contract that manages the list with permission to call contract functions
92: 		    address __DEPRECATED_allowList;
93: 		    /// @notice Part of the configuration parameters of ZKP circuits. Used as an input for the verifier smart contract
94: 		    VerifierParams verifierParams;
95: 		    /// @notice Bytecode hash of bootloader program.
96: 		    /// @dev Used as an input to zkp-circuit.
97: 		    bytes32 l2BootloaderBytecodeHash;
98: 		    /// @notice Bytecode hash of default account (bytecode for EOA).
99: 		    /// @dev Used as an input to zkp-circuit.
100: 		    bytes32 l2DefaultAccountBytecodeHash;
101: 		    /// @dev Indicates that the porter may be touched on L2 transactions.
102: 		    /// @dev Used as an input to zkp-circuit.
103: 		    bool zkPorterIsAvailable;
104: 		    /// @dev The maximum number of the L2 gas that a user can request for L1 -> L2 transactions
105: 		    /// @dev This is the maximum number of L2 gas that is available for the "body" of the transaction, i.e.
106: 		    /// without overhead for proving the batch.
107: 		    uint256 priorityTxMaxGasLimit;
108: 		    /// @dev Storage of variables needed for upgrade facet
109: 		    UpgradeStorage __DEPRECATED_upgrades;
110: 		    /// @dev A mapping L2 batch number => message number => flag.
111: 		    /// @dev The L2 -> L1 log is sent for every withdrawal, so this mapping is serving as
112: 		    /// a flag to indicate that the message was already processed.
113: 		    /// @dev Used to indicate that eth withdrawal was already processed
114: 		    mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;
115: 		    /// @dev The most recent withdrawal time and amount reset
116: 		    uint256 __DEPRECATED_lastWithdrawalLimitReset;
117: 		    /// @dev The accumulated withdrawn amount during the withdrawal limit window
118: 		    uint256 __DEPRECATED_withdrawnAmountInWindow;
119: 		    /// @dev A mapping user address => the total deposited amount by the user
120: 		    mapping(address => uint256) __DEPRECATED_totalDepositedAmountPerUser;
121: 		    /// @dev Stores the protocol version. Note, that the protocol version may not only encompass changes to the
122: 		    /// smart contracts, but also to the node behavior.
123: 		    uint256 protocolVersion;
124: 		    /// @dev Hash of the system contract upgrade transaction. If 0, then no upgrade transaction needs to be done.
125: 		    bytes32 l2SystemContractsUpgradeTxHash;
126: 		    /// @dev Batch number where the upgrade transaction has happened. If 0, then no upgrade transaction has happened
127: 		    /// yet.
128: 		    uint256 l2SystemContractsUpgradeBatchNumber;
129: 		    /// @dev Address which will exercise non-critical changes to the Diamond Proxy (changing validator set & unfreezing)
130: 		    address admin;
131: 		    /// @notice Address that the admin proposed as one that will replace admin role
132: 		    address pendingAdmin;
133: 		    /// @dev Fee params used to derive gasPrice for the L1->L2 transactions. For L2 transactions,
134: 		    /// the bootloader gives enough freedom to the operator.
135: 		    FeeParams feeParams;
136: 		    /// @dev Address of the blob versioned hash getter smart contract used for EIP-4844 versioned hashes.
137: 		    address blobVersionedHashRetriever;
138: 		    /// new fields
139: 		    /// @dev The chainId of the chain
140: 		    uint256 chainId;
141: 		    /// @dev The address of the bridgehub
142: 		    address bridgehub;
143: 		    /// @dev The address of the StateTransitionManager
144: 		    address stateTransitionManager;
145: 		    /// @dev The address of the baseToken contract. Eth is address(1)
146: 		    address baseToken;
147: 		    /// @dev The address of the baseTokenbridge. Eth also uses the shared bridge
148: 		    address baseTokenBridge;
149: 		    /// @notice gasPriceMultiplier for each baseToken, so that each L1->L2 transaction pays for its transaction on the destination
150: 		    /// we multiply by the nominator, and divide by the denominator
151: 		    uint128 baseTokenGasPriceMultiplierNominator;
152: 		    uint128 baseTokenGasPriceMultiplierDenominator;
153: 		}
```
[[66-153](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L66-L153)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

// @audit Can save 1 storage slot (from 8 to 7) 
// @audit Consider using the following order:
/*
  *	bytes32 batchHash (32)
  *	uint256 numberOfLayer1Txs (32)
  *	bytes32 priorityOperationsHash (32)
  *	bytes32 l2LogsTreeRoot (32)
  *	uint256 timestamp (32)
  *	bytes32 commitment (32)
  *	uint64 batchNumber (8)
  *	uint64 indexRepeatedStorageChanges (8)
*/
83: 		    struct StoredBatchInfo {
84: 		        uint64 batchNumber;
85: 		        bytes32 batchHash;
86: 		        uint64 indexRepeatedStorageChanges;
87: 		        uint256 numberOfLayer1Txs;
88: 		        bytes32 priorityOperationsHash;
89: 		        bytes32 l2LogsTreeRoot;
90: 		        uint256 timestamp;
91: 		        bytes32 commitment;
92: 		    }
```
[[83-92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L83-L92)]

</details>

---

### [G-05] Structs can be modified to fit in fewer storage slots

Some member types can be safely modified, and as result, these `struct` will fit in fewer storage slots. Each slot saved can avoid an extra Gsset (**20000 gas**) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings.

*There are 2 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

// @audit Supposing an already optimal order, this can save 1 storage slot (from 10 to 9) by modifying the following variables:
// @audit uint256 upgradeTimestamp -> uint32 upgradeTimestamp

// @audit Consider using the following order:
/*
  *	L2CanonicalTransaction l2ProtocolUpgradeTx (32)
  *	bytes[] factoryDeps (32)
  *	bytes32 bootloaderHash (32)
  *	bytes32 defaultAccountHash (32)
  *	VerifierParams verifierParams (32)
  *	bytes l1ContractsUpgradeCalldata (32)
  *	bytes postUpgradeCalldata (32)
  *	uint256 newProtocolVersion (32)
  *	address verifier (20)
  *	uint32 upgradeTimestamp (4)
*/
28: 		struct ProposedUpgrade {
29: 		    L2CanonicalTransaction l2ProtocolUpgradeTx;
30: 		    bytes[] factoryDeps;
31: 		    bytes32 bootloaderHash;
32: 		    bytes32 defaultAccountHash;
33: 		    address verifier;
34: 		    VerifierParams verifierParams;
35: 		    bytes l1ContractsUpgradeCalldata;
36: 		    bytes postUpgradeCalldata;
37: 		    uint256 upgradeTimestamp;
38: 		    uint256 newProtocolVersion;
39: 		}
```
[[28-39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L28-L39)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

// @audit Supposing an already optimal order, this can save 1 storage slot (from 7 to 6) by modifying the following variables:
// @audit uint256 packedBatchAndL2BlockTimestamp -> uint32 packedBatchAndL2BlockTimestamp

// @audit Consider using the following order:
/*
  *	bytes32 batchHash (32)
  *	uint256 numberOfLayer1Txs (32)
  *	bytes32 priorityOperationsHash (32)
  *	bytes32 l2LogsTreeRoot (32)
  *	bytes32 commitment (32)
  *	uint64 batchNumber (8)
  *	uint64 indexRepeatedStorageChanges (8)
  *	uint32 timestamp (4)
*/
83: 		    struct StoredBatchInfo {
84: 		        uint64 batchNumber;
85: 		        bytes32 batchHash;
86: 		        uint64 indexRepeatedStorageChanges;
87: 		        uint256 numberOfLayer1Txs;
88: 		        bytes32 priorityOperationsHash;
89: 		        bytes32 l2LogsTreeRoot;
90: 		        uint256 timestamp;
91: 		        bytes32 commitment;
92: 		    }
```
[[83-92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L83-L92)]

</details>

---

### [G-06] Multiple `mapping`s that share an ID can be combined into a single `mapping` of ID / `struct`

This can avoid a Gsset (**20000 Gas**) per mapping combined. Reads and writes will also be cheaper when a function requires both values as they both can fit in the same storage slot.

Finally, if both fields are accessed in the same function, this can save **~42 gas** per access due to not having to recalculate the key's `keccak256` hash (Gkeccak256 - **30 Gas**) and that calculation's associated stack operations.

*There are 3 instances of this issue.*


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

// @audit consider merging rawNonces, nonceValues
36: 		    mapping(uint256 account => uint256 packedMinAndDeploymentNonce) internal rawNonces;

41: 		    mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;
```
[[36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L36)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

// @audit consider merging depositAmount, __DEPRECATED_totalDepositedAmountPerUser
32: 		    mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
33: 		        public depositAmount;

51: 		    mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;

// @audit consider merging __DEPRECATED_lastWithdrawalLimitReset, __DEPRECATED_withdrawnAmountInWindow
45: 		    mapping(address => uint256) private __DEPRECATED_lastWithdrawalLimitReset;

48: 		    mapping(address => uint256) private __DEPRECATED_withdrawnAmountInWindow;
```
[[32-33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L32-L33), [45](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L45)]


---

### [G-07] Use of `memory` instead of `storage` for struct/array state variables

When fetching data from `storage`, using the `memory` keyword to assign it to a variable reads all fields of the struct/array and incurs a Gcoldsload (**2100 gas**) for each field.

This can be avoided by declaring the variable with the `storage` keyword and caching the necessary fields in stack variables.

The `memory` keyword should only be used if the entire struct/array is being returned or passed to a function that requires `memory`, or if it is being read from another `memory` array/struct.

*There are 5 instances of this issue.*


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

41: 		        AccountInfo memory info = accountInfo[_address];
```
[[41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L41)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

135: 		        VirtualBlockUpgradeInfo memory currentVirtualBlockUpgradeInfo = virtualBlockUpgradeInfo;

173: 		        BlockInfo memory batchInfo = currentBatchInfo;

181: 		        BlockInfo memory blockInfo = currentL2BlockInfo;

275: 		        BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;
```
[[135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L135), [173](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L173), [181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L181), [275](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L275)]


---

### [G-08] Unused non-constant state variables waste gas

If the variable is assigned a non-zero value, saves Gsset (20000 gas). If it's assigned a zero value, saves Gsreset (2900 gas).

If the variable remains unassigned, there is no gas savings unless the variable is public, in which case the compiler-generated non-payable getter deployment cost is saved.

If the state variable is overriding an interface's public function, mark the variable as constant or immutable so that it does not use a storage slot.

*There is 1 instance of this issue.*


```solidity
File: code/system-contracts/contracts/SystemContext.sol

37: 		    uint256 public blockGasLimit = type(uint32).max;
```
[[37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L37)]


---

### [G-09] State variables only set in their definitions should be declared `constant`

Avoids a **Gsset (20000 gas)** at deployment, and replaces the first access in each transaction (**Gcoldsload - 2100 gas**) and each access thereafter (**Gwarmacces - 100 gas**) with a `PUSH32` (3 gas).

*There are 3 instances of this issue.*


```solidity
File: code/system-contracts/contracts/SystemContext.sol

37: 		    uint256 public blockGasLimit = type(uint32).max;

41: 		    address public coinbase = BOOTLOADER_FORMAL_ADDRESS;

44: 		    uint256 public difficulty = 2.5e15;
```
[[37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L37), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L41), [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L44)]


---

### [G-10] Cache state variables with stack variables

Caching of a state variable replaces each Gwarmaccess (**100 gas**) with a cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses.

*There are 6 instances of this issue.*


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

// @audit numberOfLogsToProcess on line 109
108: 		        logIdInMerkleTree = numberOfLogsToProcess;
```
[[108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L108)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

// @audit virtualBlockUpgradeInfo on lines 268, 285
303: 		            virtualBlockUpgradeInfo.virtualBlockFinishL2Block = _l2BlockNumber;
```
[[303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L303)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

// @audit pendingAdmin on line 69
66: 		        delete pendingAdmin;

// @audit sharedBridge on line 130
140: 		            address(sharedBridge),
```
[[66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L66), [140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L140)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

// @audit pendingAdmin on line 128
125: 		        delete pendingAdmin;

// @audit protocolVersion on lines 192, 216
227: 		        emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
```
[[125](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L125), [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227)]


---

### [G-11] Low level `call` can be optimized with assembly

`returnData` is copied to memory even if the variable is not utilized: the proper way to handle this is through a low level assembly call.

```solidity
// before
(bool success,) = payable(receiver).call{gas: gas, value: value}("");

//after
bool success;
assembly {
    success := call(gas, receiver, value, 0, 0, 0, 0)
}
```

*There is 1 instance of this issue.*


```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

63: 		            (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call(
64: 		                abi.encodeCall(REAL_BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo, (msg.sender, to, value))
65: 		            );
```
[[63-65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L63-L65)]


---

### [G-12] Use of `memory` instead of `calldata` for immutable arguments

Consider refactoring the function arguments from `memory` to `calldata` when they are immutable, as `calldata` is cheaper.

*There are 40 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

// @audit _newInfo
58: 		    function _storeAccountInfo(address _address, AccountInfo memory _newInfo) internal {
```
[[58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L58)]



```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

// @audit _signature
159: 		    function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {
```
[[159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L159)]



```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

// @audit _additionalData
85: 		    function withdrawWithMessage(address _l1Receiver, bytes memory _additionalData) external payable override {

// @audit _additionalData
117: 		    function _getExtendedWithdrawMessage(
118: 		        address _to,
119: 		        uint256 _amount,
120: 		        address _sender,
121: 		        bytes memory _additionalData
```
[[85](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L85), [117-121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L117-L121)]



```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

// @audit _message
90: 		    function sendMessageToL1(bytes memory _message) internal returns (bytes32) {
```
[[90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L90)]



```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

// @audit data
37: 		    function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

// @audit data
76: 		    function systemCallWithReturndata(
77: 		        uint32 gasLimit,
78: 		        address to,
79: 		        uint128 value,
80: 		        bytes memory data
```
[[37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L37), [76-80](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L76-L80)]



```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

// @audit data
76: 		    function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

// @audit data
123: 		    function systemCallWithReturndata(
124: 		        uint32 gasLimit,
125: 		        address to,
126: 		        uint128 value,
127: 		        bytes memory data

// @audit data
150: 		    function systemCallWithPropagatedRevert(
151: 		        uint32 gasLimit,
152: 		        address to,
153: 		        uint128 value,
154: 		        bytes memory data
```
[[76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L76), [123-127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L123-L127), [150-154](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L150-L154)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

// @audit _messageParams
458: 		    function _checkWithdrawal(
459: 		        uint256 _chainId,
460: 		        MessageParams memory _messageParams,
461: 		        bytes calldata _message,
462: 		        bytes32[] calldata _merkleProof

// @audit _l2ToL1message
487: 		    function _parseL2WithdrawalMessage(
488: 		        uint256 _chainId,
489: 		        bytes memory _l2ToL1message
```
[[458-462](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L458-L462), [487-489](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L487-L489)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

// @audit _data
50: 		    function bridgeInitialize(address _l1Address, bytes memory _data) external initializer {

// @audit _newName, _newSymbol
111: 		    function reinitializeToken(
112: 		        ERC20Getters calldata _availableGetters,
113: 		        string memory _newName,
114: 		        string memory _newSymbol,
115: 		        uint8 _version

// @audit _input
178: 		    function decodeString(bytes memory _input) external pure returns (string memory result) {

// @audit _input
183: 		    function decodeUint8(bytes memory _input) external pure returns (uint8 result) {
```
[[50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L50), [111-115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L111-L115), [178](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L178), [183](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L183)]



```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

// @audit _bytecode
21: 		    function hashL2Bytecode(bytes memory _bytecode) internal pure returns (bytes32 hashedBytecode) {
```
[[21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L21)]



```solidity
File: code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol

// @audit _bytes
19: 		    function readUint32(bytes memory _bytes, uint256 _start) internal pure returns (uint32 result, uint256 offset) {

// @audit _bytes
26: 		    function readAddress(bytes memory _bytes, uint256 _start) internal pure returns (address result, uint256 offset) {

// @audit _bytes
33: 		    function readUint256(bytes memory _bytes, uint256 _start) internal pure returns (uint256 result, uint256 offset) {

// @audit _bytes
40: 		    function readBytes32(bytes memory _bytes, uint256 _start) internal pure returns (bytes32 result, uint256 offset) {
```
[[19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L19), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L26), [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L33), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L40)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

// @audit _diamondCut
96: 		    function diamondCut(DiamondCutData memory _diamondCut) internal {

// @audit _selectors
126: 		    function _addFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {

// @audit _selectors
149: 		    function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {

// @audit _selectors
172: 		    function _removeFunctions(address _facet, bytes4[] memory _selectors) private {

// @audit _calldata
278: 		    function _initializeDiamondCut(address _init, bytes memory _calldata) private {
```
[[96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L96), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L126), [149](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L149), [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L172), [278](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L278)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

// @audit _operation
55: 		    function pushBack(Queue storage _queue, PriorityOperation memory _operation) internal {
```
[[55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L55)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

// @audit _transaction, _encoded
19: 		    function validateL1ToL2Transaction(
20: 		        L2CanonicalTransaction memory _transaction,
21: 		        bytes memory _encoded,
22: 		        uint256 _priorityTxMaxGasLimit,
23: 		        uint256 _priorityTxMaxPubdata

// @audit _transaction
46: 		    function validateUpgradeTransaction(L2CanonicalTransaction memory _transaction) internal pure {
```
[[19-23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L19-L23), [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L46)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

// @audit _previousBatch
32: 		    function _commitOneBatch(
33: 		        StoredBatchInfo memory _previousBatch,
34: 		        CommitBatchInfo calldata _newBatch,
35: 		        bytes32 _expectedSystemContractUpgradeTxHash

// @audit _verifierParams
453: 		    function _getBatchProofPublicInput(
454: 		        bytes32 _prevBatchCommitment,
455: 		        bytes32 _currentBatchCommitment,
456: 		        VerifierParams memory _verifierParams

// @audit _blobCommitments, _blobHashes
561: 		    function _encodeBlobAuxilaryOutput(
562: 		        bytes32[] memory _blobCommitments,
563: 		        bytes32[] memory _blobHashes

// @audit _blobHashes
625: 		    function _verifyBlobInformation(
626: 		        bytes calldata _pubdataCommitments,
627: 		        bytes32[] memory _blobHashes
```
[[32-35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L32-L35), [453-456](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L453-L456), [561-563](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L561-L563), [625-627](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L625-L627)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

// @audit _log
104: 		    function _proveL2LogInclusion(
105: 		        uint256 _batchNumber,
106: 		        uint256 _index,
107: 		        L2Log memory _log,
108: 		        bytes32[] calldata _proof

// @audit _message
130: 		    function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {

// @audit _request
228: 		    function _requestL2TransactionSender(
229: 		        BridgehubL2TransactionRequest memory _request

// @audit _calldata
258: 		    function _requestL2Transaction(
259: 		        uint256 _mintValue,
260: 		        WritePriorityOpParams memory _params,
261: 		        bytes memory _calldata,
262: 		        bytes[] memory _factoryDeps

// @audit _priorityOpParams, _calldata
289: 		    function _serializeL2Transaction(
290: 		        WritePriorityOpParams memory _priorityOpParams,
291: 		        bytes memory _calldata,
292: 		        bytes[] memory _factoryDeps

// @audit _calldata
316: 		    function _writePriorityOp(
317: 		        WritePriorityOpParams memory _priorityOpParams,
318: 		        bytes memory _calldata,
319: 		        bytes[] memory _factoryDeps

// @audit _factoryDeps
353: 		    function _hashFactoryDeps(bytes[] memory _factoryDeps) internal pure returns (uint256[] memory hashedFactoryDeps) {
```
[[104-108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L104-L108), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L130), [228-229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L228-L229), [258-262](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L258-L262), [289-292](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L289-L292), [316-319](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L316-L319), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L353)]

</details>

---

### [G-13] Avoid updating storage when the value hasn't changed

If the old value is equal to the new value, not re-storing the value will avoid a Gsreset (**2900 gas**), potentially at the expense of a Gcoldsload (**2100 gas**) or a Gwarmaccess (**100 gas**)

*There are 21 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

// @audit immutableDataStorage
34: 		    function setImmutables(address _dest, ImmutableData[] calldata _immutables) external override {
```
[[34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L34)]



```solidity
File: code/system-contracts/contracts/NonceHolder.sol

// @audit nonceValues
82: 		    function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall {
```
[[82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L82)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

// @audit chainId
84: 		    function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {

// @audit origin
99: 		    function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {

// @audit gasPrice
105: 		    function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {

// @audit basePubdataSpent, gasPerPubdataByte
112: 		    function setPubdataInfo(uint256 _gasPerPubdataByte, uint256 _basePubdataSpent) external onlyCallFromBootloader {

// @audit l2BlockHash
212: 		    function _setL2BlockHash(uint256 _block, bytes32 _hash) internal {

// @audit currentVirtualL2BlockInfo, currentVirtualL2BlockInfo
263: 		    function _setVirtualBlock(

// @audit currentL2BlockInfo, currentL2BlockTxsRollingHash
314: 		    function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal {

// @audit batchHashes, currentBatchInfo, baseFee
444: 		    function setNewBatch(
```
[[84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L84), [99](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L99), [105](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L105), [112](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L112), [212](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L212), [263](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L263), [314](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L314), [444](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L444)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

// @audit pendingAdmin
51: 		    function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

// @audit sharedBridge
108: 		    function setSharedBridge(address _sharedBridge) external onlyOwner {
```
[[51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L51), [108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

// @audit minDelay
249: 		    function updateDelay(uint256 _newDelay) external onlySelf {

// @audit securityCouncil
256: 		    function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
```
[[249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L249), [256](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L256)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

// @audit pendingAdmin
110: 		    function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

// @audit validatorTimelock
132: 		    function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {

// @audit initialCutHash
137: 		    function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {

// @audit upgradeCutHash, protocolVersion
142: 		    function setNewVersionUpgrade(

// @audit upgradeCutHash
152: 		    function setUpgradeDiamondCut(
```
[[110](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L110), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L132), [137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L137), [142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L142), [152](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L152)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

// @audit stateTransitionManager
73: 		    function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {

// @audit executionDelay
96: 		    function setExecutionDelay(uint32 _executionDelay) external onlyOwner {
```
[[73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L73), [96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96)]

</details>

---

### [G-14] Use of `emit` inside a loop

Emitting an event inside a loop performs a `LOG` op N times, where N is the loop length. Consider refactoring the code to emit the event only once at the end of loop. Gas savings should be multiplied by the average loop length.

*There are 3 instances of this issue.*


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

261: 		            emit BlockCommit(
262: 		                _lastCommittedBatchData.batchNumber,
263: 		                _lastCommittedBatchData.batchHash,
264: 		                _lastCommittedBatchData.commitment
265: 		            );

299: 		            emit BlockCommit(
300: 		                _lastCommittedBatchData.batchNumber,
301: 		                _lastCommittedBatchData.batchHash,
302: 		                _lastCommittedBatchData.commitment
303: 		            );

353: 		            emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
```
[[261-265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261-L265), [299-303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L299-L303), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353)]


---

### [G-15] Use `uint256(1)/uint256(2)` instead of `true/false` to save gas for changes

Use `uint256(1)` and `uint256(2)` for `true`/`false` to avoid a Gsset (20000 gas) when changing from `false` to `true`, after having been `true` in the past. See [source](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27).

*There are 6 instances of this issue.*


```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

27: 		    mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
28: 		        public isWithdrawalFinalized;
```
[[27-28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27-L28)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

57: 		    mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
58: 		        public isWithdrawalFinalized;

61: 		    mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;
```
[[57-58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57-L58), [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L61)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

21: 		    mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;

23: 		    mapping(address _token => bool) public tokenIsRegistered;
```
[[21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21), [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L23)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

50: 		    mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
[[50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50)]


---

### [G-16] Shortcircuit rules can be be used to optimize some gas usage

Some conditions may be reordered to save an `SLOAD` (**2100 gas**), as we avoid reading state variables when the first part of the condition fails (with `&&`), or succeeds (with `||`).

*There are 2 instances of this issue.*


```solidity
File: code/system-contracts/contracts/SystemContext.sol

// @audit switch with this condition
// virtualBlockInfo.timestamp == 0 && currentVirtualL2BlockInfo.number == 0
277: 		        if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
```
[[277](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L277)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

// @audit switch with this condition
// (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY) || msg.sender == address(bridgehub)
76: 		            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
```
[[76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L76)]


---

### [G-17] Cache multiple accesses of a mapping/array

Consider using a local `storage` or `calldata` variable when accessing a mapping/array value multiple times.

This can be useful to avoid recalculating the mapping hash and/or the array offsets.

*There are 8 instances of this issue.*


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

// @audit chainBalance on lines 122, 123, 133
133: 		            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;

// @audit depositHappened on line 237
238: 		        depositHappened[_chainId][_txHash] = _txDataHash;

// @audit depositHappened[_chainId] on line 340
343: 		                delete depositHappened[_chainId][_l2TxHash];

// @audit chainBalance on line 349
350: 		            chainBalance[_chainId][_l1Token] -= _amount;

// @audit isWithdrawalFinalized[_chainId] on line 417
418: 		        isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true;

// @audit chainBalance on line 439
440: 		            chainBalance[_chainId][l1Token] -= amount;
```
[[133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133), [238](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L238), [343](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L343), [350](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L350), [418](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L418), [440](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L440)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

// @audit validators on line 79
82: 		        validators[_chainId][_newValidator] = true;

// @audit validators on line 88
91: 		        validators[_chainId][_validator] = false;
```
[[82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L82), [91](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L91)]


---

### [G-18] Using `private` for constants saves gas

Saves deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it's used, and not adding another entry to the method ID table.

*There are 5 instances of this issue.*


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

26: 		    string public constant override getName = "ValidatorTimelock";
```
[[26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

20: 		    string public constant override getName = "AdminFacet";
```
[[20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

27: 		    string public constant override getName = "ExecutorFacet";
```
[[27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

25: 		    string public constant override getName = "GettersFacet";
```
[[25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

35: 		    string public constant override getName = "MailboxFacet";
```
[[35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35)]


---

### [G-19] require() or revert() statements that check input arguments should be at the top of the function

Checks that can be performed earlier should come before checks that involve state variables, function calls, and calculations. By doing these checks first, the function is able to revert before wasting a Gcoldsload (*2100 gas*) in a function that may ultimately revert.

*There are 7 instances of this issue.*


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

// @audit expensive op on line 83
85: 		        require(_value != 0, "Nonce value cannot be set to 0");
```
[[85](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L85)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

// @audit expensive op on line 268, 271, 275, 277, 278, 285
287: 		            require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

// @audit expensive op on line 350
355: 		            require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

// @audit expensive op on line 358, 363, 365, 370, 350
373: 		            require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");
```
[[287](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L287), [355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L355), [373](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L373)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

// @audit expensive op on line 316
327: 		        require(_amount > 0, "y1");
```
[[327](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

// @audit expensive op on line 64, 65, 66, 60, 61
68: 		            require(_l1LegecyBridge != address(0), "bf2");
```
[[68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L68)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

// @audit expensive op on line 173
175: 		        require(_facet == address(0), "a1"); // facet address must be zero
```
[[175](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175)]


---

### [G-20] Custom `error`s cost less than `require`/`assert`

Consider the use of a custom `error`, as it leads to a cheaper deploy cost and run time cost. The run time cost is only relevant when the revert condition is met.

*There are 333 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

26: 		        require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

37: 		        require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");

48: 		        require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");

57: 		        require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");
```
[[26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L26), [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L37), [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L48), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L57)]



```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

92: 		            require(vInt == 27 || vInt == 28, "Invalid v value");

191: 		            require(vInt == 27 || vInt == 28, "Invalid v value");

286: 		            require(vInt == 27 || vInt == 28, "Invalid v value");
```
[[92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L92), [191](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L191), [286](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L286)]



```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

22: 		        require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");

24: 		        require(_delegateTo.code.length > 0, "Delegatee is an EOA");
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L22), [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L24)]



```solidity
File: code/system-contracts/contracts/Compressor.sol

51: 		            require(
52: 		                encodedData.length * 4 == _bytecode.length,
53: 		                "Encoded data length should be 4 times shorter than the original bytecode"
54: 		            );

56: 		            require(
57: 		                dictionary.length / 8 <= encodedData.length / 2,
58: 		                "Dictionary should have at most the same number of entries as the encoded data"
59: 		            );

63: 		                require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

68: 		                require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");

119: 		        require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");

140: 		            require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");

156: 		        require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");

171: 		            require(enumIndex == compressedEnumIndex, "rw: enum key mismatch");

187: 		        require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");

230: 		                require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");

232: 		                require(
233: 		                    _initialValue + convertedValue == _finalValue,
234: 		                    "add: initial plus converted not equal to final"
235: 		                );

237: 		                require(
238: 		                    _initialValue - convertedValue == _finalValue,
239: 		                    "sub: initial minus converted not equal to final"
240: 		                );
```
[[51-54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L51-L54), [56-59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L56-L59), [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L63), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L68), [119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L119), [140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L140), [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L156), [171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L171), [187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L187), [230](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L230), [232-235](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L232-L235), [237-240](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L237-L240)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

29: 		        require(msg.sender == address(this), "Callable only by self");

77: 		        require(
78: 		            _nonceOrdering == AccountNonceOrdering.Arbitrary &&
79: 		                currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
80: 		            "It is only possible to change from sequential to arbitrary ordering"
81: 		        );

239: 		        require(
240: 		            msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
241: 		            "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
242: 		        );

251: 		        require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");

264: 		        require(_bytecodeHash != bytes32(0x0), "BytecodeHash cannot be zero");

265: 		        require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

268: 		        require(
269: 		            ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0,
270: 		            "Code hash is non-zero"
271: 		        );

273: 		        require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied");

303: 		        require(knownCodeMarker > 0, "The code hash is not known");

350: 		            require(value == 0, "The value must be zero if we do not call the constructor");
```
[[29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L29), [77-81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L77-L81), [239-242](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L239-L242), [251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L251), [264](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L264), [265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L265), [268-271](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L268-L271), [273](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L273), [303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L303), [350](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L350)]



```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

100: 		        require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

160: 		        require(_signature.length == 65, "Signature length is incorrect");

173: 		        require(v == 27 || v == 28, "v is neither 27 nor 28");

184: 		        require(uint256(s) <= 0x7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF5D576E7357A4501DDFE92F46681B20A0, "Invalid s");

202: 		        require(success, "Failed to pay the fee to the operator");

222: 		        assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS);
```
[[100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L100), [160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L160), [173](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L173), [184](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L184), [202](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L202), [222](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L222)]



```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

46: 		        require(_maxTotalGas >= gasleft(), "Gas limit is too low");

76: 		            require(pubdataAllowance + gasleft() >= pubdataCost + CALL_RETURN_OVERHEAD, "Not enough gas for pubdata");
```
[[46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L46), [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L76)]



```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

35: 		        require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
[[35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L35)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

20: 		        require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");

76: 		        require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");

78: 		        require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd");
```
[[20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L20), [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L76), [78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L78)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

201: 		        require(numberOfL2ToL1Logs <= L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, "Too many L2->L1 logs");

214: 		        require(
215: 		            reconstructedChainedLogsHash == chainedLogsHash,
216: 		            "reconstructedChainedLogsHash is not equal to chainedLogsHash"
217: 		        );

245: 		        require(
246: 		            reconstructedChainedMessagesHash == chainedMessagesHash,
247: 		            "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
248: 		        );

269: 		        require(
270: 		            reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
271: 		            "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
272: 		        );

279: 		        require(
280: 		            uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
281: 		                STATE_DIFF_COMPRESSION_VERSION_NUMBER,
282: 		            "state diff compression version mismatch"
283: 		        );

298: 		        require(calldataPtr <= MAX_ALLOWED_PUBDATA_PER_BATCH, "L1 Messenger pubdata is too long");

315: 		        require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");
```
[[201](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L201), [214-217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L214-L217), [245-248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L245-L248), [269-272](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L269-L272), [279-283](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L279-L283), [298](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L298), [315](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L315)]



```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

33: 		        require(
34: 		            msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
35: 		                msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
36: 		                msg.sender == BOOTLOADER_FORMAL_ADDRESS,
37: 		            "Only system contracts with special access can call this method"
38: 		        );

41: 		        require(fromBalance >= _amount, "Transfer amount exceeds balance");
```
[[33-38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L33-L38), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L41)]



```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

60: 		        require(to != address(this), "MsgValueSimulator calls itself");
```
[[60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L60)]



```solidity
File: code/system-contracts/contracts/NonceHolder.sol

66: 		        require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");

85: 		        require(_value != 0, "Nonce value cannot be set to 0");

89: 		            require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");

115: 		        require(oldMinNonce == _expectedNonce, "Incorrect nonce");

136: 		        require(
137: 		            msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
138: 		            "Only the contract deployer can increment the deployment nonce"
139: 		        );
```
[[66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L66), [85](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L85), [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L89), [115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L115), [136-139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L136-L139)]



```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

22: 		        require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L22)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

242: 		        require(_isFirstInBatch, "Upgrade transaction must be first");

245: 		        require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

249: 		            require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");

287: 		            require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

351: 		            require(
352: 		                _l2BlockTimestamp >= currentBatchTimestamp,
353: 		                "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
354: 		            );

355: 		            require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

367: 		            require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");

368: 		            require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");

369: 		            require(
370: 		                _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
371: 		                "The previous hash of the same L2 block must be same"
372: 		            );

373: 		            require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");

385: 		            require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");

386: 		            require(
387: 		                _l2BlockTimestamp > currentL2BlockTimestamp,
388: 		                "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
389: 		            );

413: 		        require(currentBatchNumber > 0, "The current batch number must be greater than 0");

429: 		        require(
430: 		            _newTimestamp > currentBlockTimestamp,
431: 		            "The timestamp of the batch must be greater than the timestamp of the previous block"
432: 		        );

451: 		        require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");

452: 		        require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
```
[[242](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L242), [245](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L245), [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L249), [287](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L287), [351-354](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L351-L354), [355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L355), [367](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L367), [368](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L368), [369-372](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L369-L372), [373](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L373), [385](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L385), [386-389](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L386-L389), [413](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L413), [429-432](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L429-L432), [451](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L451), [452](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L452)]



```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

28: 		        require(_x <= type(uint32).max, "Overflow");
```
[[28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L28)]



```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

21: 		        require(
22: 		            SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
23: 		            "This method require system call flag"
24: 		        );

31: 		        require(
32: 		            SystemContractHelper.isSystemContract(msg.sender),
33: 		            "This method require the caller to be system contract"
34: 		        );

41: 		        require(msg.sender == caller, "Inappropriate caller");

48: 		        require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");

55: 		        require(msg.sender == FORCE_DEPLOYER);
```
[[21-24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L21-L24), [31-34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L31-L34), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L41), [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L48), [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L55)]



```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

38: 		        require(returnData.length == 32, "keccak256 returned invalid data");

47: 		        require(returnData.length == 32, "sha returned invalid data");
```
[[38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L38), [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L47)]



```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

50: 		        assert(_len != 1);
```
[[50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L50)]



```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

319: 		        require(index < 10, "There are only 10 accessible registers");

350: 		        require(precompileCallSuccess, "Failed to charge gas");
```
[[319](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319), [350](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L350)]



```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

363: 		        require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");

367: 		            require(
368: 		                _transaction.paymasterInput.length >= 68,
369: 		                "The approvalBased paymaster input must be at least 68 bytes long"
370: 		            );
```
[[363](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L363), [367-370](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L367-L370)]



```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

21: 		        require(_x <= type(uint128).max, "Overflow");

27: 		        require(_x <= type(uint32).max, "Overflow");

33: 		        require(_x <= type(uint24).max, "Overflow");

84: 		        require(_bytecode.length % 32 == 0, "po");

87: 		        require(lengthInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words

88: 		        require(lengthInWords % 2 == 1, "pr"); // bytecode length in words must be odd
```
[[21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L21), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L27), [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L33), [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L84), [87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L87), [88](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L88)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

64: 		        require(msg.sender == address(sharedBridge), "Not shared bridge");

66: 		        require(amount == _amount, "Incorrect amount");

141: 		        require(_amount != 0, "0T"); // empty deposit

143: 		        require(amount == _amount, "3T"); // The token has non-standard transfer logic

186: 		        require(amount != 0, "2T"); // empty deposit

215: 		        require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw");
```
[[64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64), [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L66), [141](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141), [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L143), [186](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186), [215](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L215)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

69: 		        require(msg.sender == address(bridgehub), "ShB not BH");

75: 		        require(
76: 		            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
77: 		            "L1SharedBridge: not bridgehub or era chain"
78: 		        );

84: 		        require(msg.sender == address(legacyBridge), "ShB not legacy bridge");

108: 		        require(_owner != address(0), "ShB owner 0");

121: 		            require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");

129: 		            require(amount > 0, "ShB: 0 amount to transfer");

132: 		            require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");

138: 		        require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");

155: 		            require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");

158: 		            require(msg.value == 0, "ShB m.v > 0 b d.it");

161: 		            require(amount == _amount, "3T"); // The token has non-standard transfer logic

188: 		        require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

194: 		        require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");

195: 		        require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

200: 		            require(_depositAmount == 0, "ShB wrong withdraw amount");

202: 		            require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");

206: 		            require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic

208: 		        require(amount != 0, "6T"); // empty deposit amount

237: 		        require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");

325: 		            require(proofValid, "yn");

327: 		        require(_amount > 0, "y1");

342: 		                require(dataHash == txDataHash, "ShB: d.it not hap");

349: 		            require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");

360: 		            require(callSuccess, "ShB: claimFailedDeposit failed");

396: 		            require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");

417: 		        require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");

427: 		            require(!alreadyFinalized, "Withdrawal is already finalized 2");

439: 		            require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds

449: 		            require(callSuccess, "ShB: withdraw failed");

484: 		        require(success, "ShB withd w proof"); // withdrawal wrong proof

501: 		        require(_l2ToL1message.length >= 56, "ShB wrong msg len"); // wrong messsage length

517: 		            require(_l2ToL1message.length == 76, "ShB wrong msg len 2");

563: 		        require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

564: 		        require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
```
[[69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69), [75-78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75-L78), [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L84), [108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L108), [121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L121), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138), [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L155), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L158), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L161), [188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188), [194](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L194), [195](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195), [200](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L200), [202](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202), [206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L206), [208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L208), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L237), [325](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L325), [327](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327), [342](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L342), [349](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L349), [360](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L360), [396](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L396), [417](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L417), [427](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L427), [439](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L439), [449](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L449), [484](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L484), [501](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L501), [517](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L517), [563](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563), [564](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

46: 		        require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

62: 		        require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

83: 		        require(
84: 		            !stateTransitionManagerIsRegistered[_stateTransitionManager],
85: 		            "Bridgehub: state transition already registered"
86: 		        );

93: 		        require(
94: 		            stateTransitionManagerIsRegistered[_stateTransitionManager],
95: 		            "Bridgehub: state transition not registered yet"
96: 		        );

102: 		        require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

122: 		        require(_chainId != 0, "Bridgehub: chainId cannot be 0");

123: 		        require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");

125: 		        require(
126: 		            stateTransitionManagerIsRegistered[_stateTransitionManager],
127: 		            "Bridgehub: state transition not registered"
128: 		        );

129: 		        require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");

130: 		        require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

132: 		        require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

223: 		                require(msg.value == _request.mintValue, "Bridgehub: msg.value mismatch 1");

225: 		                require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");

269: 		                require(
270: 		                    msg.value == _request.mintValue + _request.secondBridgeValue,
271: 		                    "Bridgehub: msg.value mismatch 2"
272: 		                );

275: 		                require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3");

296: 		        require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch");

300: 		        require(
301: 		            _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
302: 		            "Bridgehub: second bridge address too low"
303: 		        ); // to avoid calls to precompiles
```
[[46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62), [83-86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83-L86), [93-96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L93-L96), [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102), [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L122), [123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123), [125-128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L125-L128), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L129), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132), [223](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L223), [225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225), [269-272](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L269-L272), [275](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L275), [296](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L296), [300-303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L300-L303)]



```solidity
File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

58: 		        require(lockSlotOldValue == 0, "1B");

75: 		        require(_status == _NOT_ENTERED, "r1");
```
[[58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L58), [75](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L75)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

42: 		        require(_admin != address(0), "Admin should be non zero address");

59: 		        require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

65: 		        require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

71: 		        require(
72: 		            msg.sender == owner() || msg.sender == securityCouncil,
73: 		            "Only the owner and security council are allowed to call this function"
74: 		        );

155: 		        require(isOperationPending(_id), "Operation must be pending");

172: 		        require(isOperationReady(id), "Operation must be ready before execution");

177: 		        require(isOperationReady(id), "Operation must be ready after execution");

191: 		        require(isOperationPending(id), "Operation must be pending before execution");

196: 		        require(isOperationPending(id), "Operation must be pending after execution");

216: 		        require(!isOperation(_id), "Operation with this proposal id already exists");

217: 		        require(_delay >= minDelay, "Proposed delay is less than minimum delay");

240: 		        require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");
```
[[42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L42), [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L59), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L65), [71-74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L71-L74), [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L155), [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L172), [177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L177), [191](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L191), [196](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L196), [216](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L216), [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L217), [240](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L240)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

64: 		        require(msg.sender == bridgehub, "StateTransition: only bridgehub");

70: 		        require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

82: 		        require(_initializeData.governor != address(0), "StateTransition: governor zero");

106: 		        assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);

121: 		        require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

256: 		        require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");
```
[[64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64), [70](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L70), [82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L82), [106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L106), [121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L121), [256](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L256)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62: 		        require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

68: 		        require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");

195: 		                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

217: 		                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
```
[[62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68), [195](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195), [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L217)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

72: 		        require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

190: 		        require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");

205: 		        require(
206: 		            _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
207: 		            "The new protocol version should be included in the L2 system upgrade tx"
208: 		        );

223: 		        require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");

224: 		        require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");

227: 		            require(
228: 		                L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
229: 		                "Wrong factory dep hash"
230: 		            );

238: 		        require(
239: 		            _newProtocolVersion > previousProtocolVersion,
240: 		            "New protocol version is not greater than the current one"
241: 		        );

242: 		        require(
243: 		            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
244: 		            "Too big protocol version difference"
245: 		        );

249: 		        require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

250: 		        require(
251: 		            s.l2SystemContractsUpgradeBatchNumber == 0,
252: 		            "The batch number of the previous upgrade has not been cleaned"
253: 		        );
```
[[72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L72), [190](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L190), [205-208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L205-L208), [223](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L223), [224](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L224), [227-230](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L227-L230), [238-241](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L238-L241), [242-245](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L242-L245), [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L249), [250-253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L250-L253)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

22: 		        require(
23: 		            // Genesis Upgrade difference: Note this is the only thing change > to >=
24: 		            _newProtocolVersion >= previousProtocolVersion,
25: 		            "New protocol version is not greater than the current one"
26: 		        );

27: 		        require(
28: 		            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
29: 		            "Too big protocol version difference"
30: 		        );

33: 		        require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

34: 		        require(
35: 		            s.l2SystemContractsUpgradeBatchNumber == 0,
36: 		            "The batch number of the previous upgrade has not been cleaned"
37: 		        );

52: 		        require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");
```
[[22-26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22-L26), [27-30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L27-L30), [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33), [34-37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L34-L37), [52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L52)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

55: 		        require(_l1Bridge != address(0), "bf");

56: 		        require(_l2TokenProxyBytecodeHash != bytes32(0), "df");

57: 		        require(_aliasedOwner != address(0), "sf");

58: 		        require(_l2TokenProxyBytecodeHash != bytes32(0), "df");

68: 		            require(_l1LegecyBridge != address(0), "bf2");

87: 		        require(
88: 		            AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
89: 		                AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
90: 		            "mq"
91: 		        );

92: 		        require(msg.value == 0, "Value should be 0 for ERC20 bridge");

98: 		            require(deployedToken == expectedL2Token, "mt");

101: 		            require(currentL1Token == _l1Token, "gg"); // Double check that the expected value equal to real one

124: 		        require(_amount > 0, "Amount cannot be zero");

129: 		        require(l1Token != address(0), "yh");

176: 		        require(success, "mk");
```
[[55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L55), [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L56), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L57), [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L58), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L68), [87-91](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L87-L91), [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92), [98](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L98), [101](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L101), [124](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L124), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L129), [176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L176)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

51: 		        require(_l1Address != address(0), "in6"); // Should be non-zero address

120: 		        require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");

130: 		        require(msg.sender == l2Bridge, "xnt"); // Only L2 bridge can call this method

137: 		        require(_version == _getInitializedVersion() + 1, "v");
```
[[51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51), [120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L130), [137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L137)]



```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

23: 		        require(_bytecode.length % 32 == 0, "pq");

26: 		        require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words

27: 		        require(bytecodeLenInWords % 2 == 1, "ps"); // bytecode length in words must be odd

41: 		        require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash

43: 		        require(bytecodeLen(_bytecodeHash) % 2 == 1, "uy"); // Code length in words must be odd
```
[[23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L26), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L27), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L41), [43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

25: 		        require(address(_initializeData.verifier) != address(0), "vt");

26: 		        require(_initializeData.admin != address(0), "vy");

27: 		        require(_initializeData.validatorTimelock != address(0), "hc");

28: 		        require(_initializeData.priorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "vu");

51: 		        assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
```
[[25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L26), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27), [28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L28), [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L51)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

14: 		        require(_chainId == block.chainid, "pr");

25: 		        require(msg.data.length >= 4 || msg.data.length == 0, "Ut");

30: 		        require(facetAddress != address(0), "F"); // Proxy has no facet for this selector

31: 		        require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen
```
[[14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L14), [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25), [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30), [31](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L31)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

107: 		            require(selectors.length > 0, "B"); // no functions for diamond cut

132: 		        require(_facet.code.length > 0, "G");

141: 		            require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists

155: 		        require(_facet.code.length > 0, "K");

161: 		            require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

175: 		        require(_facet == address(0), "a1"); // facet address must be zero

181: 		            require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet

215: 		            require(_isSelectorFreezable == ds.selectorToFacet[selector0].isFreezable, "J1");

280: 		            require(_calldata.length == 0, "H"); // Non-empty calldata for zero address

297: 		            require(data.length == 32, "lp");

298: 		            require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1");
```
[[107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132), [141](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L141), [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L155), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L161), [175](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175), [181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L181), [215](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L215), [280](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L280), [297](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L297), [298](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L298)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

24: 		        require(pathLength > 0, "xc");

25: 		        require(pathLength < 256, "bt");

26: 		        require(_index < (1 << pathLength), "px");
```
[[24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24), [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L25), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L26)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

65: 		        require(!_queue.isEmpty(), "D"); // priority queue is empty

73: 		        require(!_queue.isEmpty(), "s"); // priority queue is empty
```
[[65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L65), [73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L73)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

28: 		        require(l2GasForTxBody <= _priorityTxMaxGasLimit, "ui");

30: 		        require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");

34: 		        require(
35: 		            getMinimalPriorityTransactionGasLimit(
36: 		                _encoded.length,
37: 		                _transaction.factoryDeps.length,
38: 		                _transaction.gasPerPubdataByteLimit
39: 		            ) <= l2GasForTxBody,
40: 		            "up"
41: 		        );

48: 		        require(_transaction.from <= type(uint16).max, "ua");

49: 		        require(_transaction.to <= type(uint160).max, "ub");

50: 		        require(_transaction.paymaster == 0, "uc");

51: 		        require(_transaction.value == 0, "ud");

52: 		        require(_transaction.maxFeePerGas == 0, "uq");

53: 		        require(_transaction.maxPriorityFeePerGas == 0, "ux");

54: 		        require(_transaction.reserved[0] == 0, "ue");

55: 		        require(_transaction.reserved[1] <= type(uint160).max, "uf");

56: 		        require(_transaction.reserved[2] == 0, "ug");

57: 		        require(_transaction.reserved[3] == 0, "uo");

58: 		        require(_transaction.signature.length == 0, "uh");

59: 		        require(_transaction.paymasterInput.length == 0, "ul1");

60: 		        require(_transaction.reservedDynamic.length == 0, "um");

115: 		        require(_totalGasLimit >= overhead, "my"); // provided gas limit doesn't cover transaction overhead
```
[[28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L28), [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L30), [34-41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L34-L41), [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L48), [49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L49), [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L50), [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L51), [52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L52), [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L53), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L54), [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55), [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L56), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L57), [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L58), [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L59), [60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L60), [115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L115)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

34: 		        require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights

59: 		        require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");

70: 		        require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");

90: 		        require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed

105: 		        require(
106: 		            cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107: 		            "StateTransition: cutHash mismatch"
108: 		        );

110: 		        require(
111: 		            s.protocolVersion == _oldProtocolVersion,
112: 		            "StateTransition: protocolVersion mismatch in STC when upgrading"
113: 		        );

116: 		        require(
117: 		            s.protocolVersion > _oldProtocolVersion,
118: 		            "StateTransition: protocolVersion mismatch in STC after upgrading"
119: 		        );

136: 		        require(!diamondStorage.isFrozen, "a9"); // diamond proxy is frozen already

146: 		        require(diamondStorage.isFrozen, "a7"); // diamond proxy is not frozen
```
[[34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34), [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L59), [70](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L70), [90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90), [105-108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L105-L108), [110-113](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L110-L113), [116-119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L116-L119), [136](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L136), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L146)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

37: 		        require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f"); // only commit next batch

40: 		        require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us");

50: 		            require(logOutput.pubdataHash == 0x00, "v0h");

51: 		            require(_newBatch.pubdataCommitments.length == 1);

61: 		            require(
62: 		                logOutput.pubdataHash ==
63: 		                    keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),
64: 		                "wp"
65: 		            );

74: 		        require(_previousBatch.batchHash == logOutput.previousBatchHash, "l");

76: 		        require(logOutput.chainedPriorityTxsHash == _newBatch.priorityOperationsHash, "t");

78: 		        require(logOutput.numberOfLayer1Txs == _newBatch.numberOfLayer1Txs, "ta");

110: 		        require(batchTimestamp == _expectedBatchTimestamp, "tb");

114: 		        require(_previousBatchTimestamp < batchTimestamp, "h3");

122: 		        require(block.timestamp - COMMIT_TIMESTAMP_NOT_OLDER <= batchTimestamp, "h1"); // New batch timestamp is too small

123: 		        require(lastL2BlockTimestamp <= block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA, "h2"); // The last L2 block timestamp is too big

149: 		            require(!_checkBit(processedLogs, uint8(logKey)), "kp");

154: 		                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");

157: 		                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");

160: 		                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");

163: 		                require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");

166: 		                require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");

169: 		                require(logSender == L2_BOOTLOADER_ADDRESS, "bl");

172: 		                require(logSender == L2_BOOTLOADER_ADDRESS, "bk");

175: 		                require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");

178: 		                require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");

181: 		                require(logSender == L2_BOOTLOADER_ADDRESS, "bu");

182: 		                require(_expectedSystemContractUpgradeTxHash == logValue, "ut");

192: 		            require(processedLogs == 511, "b7");

194: 		            require(processedLogs == 1023, "b8");

226: 		        require(
227: 		            IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
228: 		            "Executor facet: wrong protocol version"
229: 		        );

231: 		        require(_newBatchesData.length == 1, "e4");

233: 		        require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data

284: 		        require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");

323: 		        require(currentBatchNumber == s.totalBatchesExecuted + _executedBatchIdx + 1, "k"); // Execute batches in order

324: 		        require(
325: 		            _hashStoredBatchInfo(_storedBatch) == s.storedBatchHashes[currentBatchNumber],
326: 		            "exe10" // executing batch should be committed
327: 		        );

330: 		        require(priorityOperationsHash == _storedBatch.priorityOperationsHash, "x"); // priority operations hash does not match to expected

358: 		        require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.

402: 		        require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");

407: 		            require(
408: 		                _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
409: 		                "o1"
410: 		            );

421: 		        require(currentTotalBatchesVerified <= s.totalBatchesCommitted, "q");

426: 		        assert(block.chainid != 1);

442: 		        require(proofPublicInput.length == 1, "t4");

449: 		        require(successVerifyProof, "p"); // Proof verification fail

482: 		        require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch

483: 		        require(_newLastBatch >= s.totalBatchesExecuted, "v2"); // Already executed batches cannot be reverted

543: 		        require(_batch.systemLogs.length <= MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES, "pu");

567: 		        require(_blobCommitments.length == MAX_NUMBER_OF_BLOBS, "b10");

568: 		        require(_blobHashes.length == MAX_NUMBER_OF_BLOBS, "b11");

616: 		        require(success, "failed to call point evaluation precompile");

618: 		        require(result == BLS_MODULUS, "precompile unexpected output");

631: 		        require(_pubdataCommitments.length > 0, "pl");

632: 		        require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");

633: 		        require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");

639: 		            require(blobVersionedHash != bytes32(0), "vh");

663: 		        require(versionedHash == bytes32(0), "lh");

668: 		            require(
669: 		                (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
670: 		                    (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
671: 		                "bh"
672: 		            );

681: 		        require(success, "vc");
```
[[37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L37), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L40), [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L50), [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L51), [61-65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L61-L65), [74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L74), [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L76), [78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L78), [110](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L110), [114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L114), [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L122), [123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L123), [149](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L149), [154](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L154), [157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L157), [160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L160), [163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L163), [166](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L166), [169](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L169), [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L172), [175](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L175), [178](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L178), [181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L181), [182](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L182), [192](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L192), [194](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L194), [226-229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L226-L229), [231](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L231), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L233), [284](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L284), [323](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L323), [324-327](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L324-L327), [330](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L330), [358](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L358), [402](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L402), [407-410](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L407-L410), [421](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L421), [426](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L426), [442](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L442), [449](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L449), [482](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L482), [483](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L483), [543](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L543), [567](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L567), [568](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L568), [616](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616), [618](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L618), [631](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631), [632](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L632), [633](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L633), [639](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L639), [663](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L663), [668-672](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L668-L672), [681](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L681)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

183: 		        require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");
```
[[183](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

39: 		        require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");

110: 		        require(_batchNumber <= s.totalBatchesExecuted, "xx");

117: 		        require(hashedLog != L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH, "tw");

158: 		        require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

185: 		        require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");

206: 		        require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");

243: 		        require(_request.l2GasPerPubdataByteLimit == REQUIRED_L2_GAS_PRICE_PER_PUBDATA, "qp");

264: 		        require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj");

272: 		        require(_mintValue >= baseCost + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost
```
[[39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39), [110](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L110), [117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L117), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L185), [206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L206), [243](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L243), [264](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L264), [272](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L272)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

16: 		        require(msg.sender == s.admin, "StateTransition Chain: not admin");

22: 		        require(s.validators[msg.sender], "StateTransition Chain: not validator");

27: 		        require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

32: 		        require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

37: 		        require(
38: 		            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
39: 		            "StateTransition Chain: Only by admin or state transition manager"
40: 		        );

45: 		        require(
46: 		            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
47: 		            "StateTransition Chain: Only by validator or state transition manager"
48: 		        );

53: 		        require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
```
[[16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16), [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32), [37-40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L37-L40), [45-48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45-L48), [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53)]

</details>

---

### [G-21] Consider activating `via-ir` for deploying

The IR-based code generator was developed to make code generation more performant by enabling optimization passes that can be applied across functions.

It is possible to activate the IR-based code generator through the command line by using the flag `--via-ir` or by including the option `{"viaIR": true}`.

Keep in mind that compiling with this option may take longer. However, you can simply test it before deploying your code. If you find that it provides better performance, you can add the `--via-ir` flag to your deploy command.



---

### [G-22] Function calls should be cached instead of re-calling the function

Consider caching the result instead of re-calling the function when possible. Note: this also includes casts, which cost between 42-46 gas, depending on the type.

*There are 3 instances of this issue.*


```solidity
File: code/system-contracts/contracts/Compressor.sol

// @audit stateDiff.readUint64(84) is duplicated on line 161
129: 		            uint64 enumIndex = stateDiff.readUint64(84);

// @audit stateDiff.readUint256(92) is duplicated on line 166
138: 		            uint256 initValue = stateDiff.readUint256(92);

// @audit stateDiff.readUint256(124) is duplicated on line 167
139: 		            uint256 finalValue = stateDiff.readUint256(124);
```
[[129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L129), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L138), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L139)]


---

### [G-23] Functions that revert when called by normal users can be `payable`

If a function modifier such as `onlyOwner` is used, the function will revert if a normal user tries to pay the function.

Marking the function as `payable` will lower the gas for legitimate callers, as the compiler will not include checks for whether a payment was provided.

The extra opcodes avoided are:

`CALLVALUE(2), DUP1(3), ISZERO(3), PUSH2(3), JUMPI(10), PUSH1(3), DUP1(3), REVERT(0), JUMPDEST(1), POP(2)`

which cost an average of about 21 gas per call to the function, in addition to the extra deployment cost.

*There are 88 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

35: 		    function storeAccountConstructingCodeHash(address _address, bytes32 _hash) external override onlyDeployer {

46: 		    function storeAccountConstructedCodeHash(address _address, bytes32 _hash) external override onlyDeployer {

54: 		    function markAccountCodeHashAsConstructed(address _address) external override onlyDeployer {
```
[[35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L35), [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L46), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L54)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

65: 		    function updateAccountVersion(AccountAbstractionVersion _version) external onlySystemCall {

74: 		    function updateNonceOrdering(AccountNonceOrdering _nonceOrdering) external onlySystemCall {
```
[[65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L65), [74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L74)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

27: 		    function markFactoryDeps(bool _shouldSendToL1, bytes32[] calldata _hashes) external onlyCallFromBootloader {

39: 		    function markBytecodeAsPublished(bytes32 _bytecodeHash) external onlyCompressor {
```
[[27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L27), [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L39)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

70: 		    function sendL2ToL1Log(
71: 		        bool _isService,
72: 		        bytes32 _key,
73: 		        bytes32 _value
74: 		    ) external onlyCallFromSystemContract returns (uint256 logIdInMerkleTree) {

161: 		    function requestBytecodeL1Publication(
162: 		        bytes32 _bytecodeHash
163: 		    ) external override onlyCallFrom(address(KNOWN_CODE_STORAGE_CONTRACT)) {

194: 		    function publishPubdataAndClearState(
195: 		        bytes calldata _totalL2ToL1PubdataAndStateDiffs
196: 		    ) external onlyCallFromBootloader {
```
[[70-74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L70-L74), [161-163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L161-L163), [194-196](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L194-L196)]



```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

64: 		    function mint(address _account, uint256 _amount) external override onlyCallFromBootloader {
```
[[64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L64)]



```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

47: 		    fallback(bytes calldata _data) external onlySystemCall returns (bytes memory) {
```
[[47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L47)]



```solidity
File: code/system-contracts/contracts/NonceHolder.sol

65: 		    function increaseMinNonce(uint256 _value) public onlySystemCall returns (uint256 oldMinNonce) {

82: 		    function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall {

110: 		    function incrementMinNonceIfEquals(uint256 _expectedNonce) external onlySystemCall {
```
[[65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L65), [82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L82), [110](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L110)]



```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

21: 		    function chunkAndPublishPubdata(bytes calldata _pubdata) external onlyCallFrom(address(L1_MESSENGER_CONTRACT)) {
```
[[21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L21)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

84: 		    function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {

99: 		    function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {

105: 		    function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {

112: 		    function setPubdataInfo(uint256 _gasPerPubdataByte, uint256 _basePubdataSpent) external onlyCallFromBootloader {

341: 		    function setL2Block(
342: 		        uint128 _l2BlockNumber,
343: 		        uint128 _l2BlockTimestamp,
344: 		        bytes32 _expectedPrevL2BlockHash,
345: 		        bool _isFirstInBatch,
346: 		        uint128 _maxVirtualBlocksToCreate
347: 		    ) external onlyCallFromBootloader {

402: 		    function appendTransactionToCurrentL2Block(bytes32 _txHash) external onlyCallFromBootloader {

408: 		    function publishTimestampDataToL1() external onlyCallFromBootloader {

444: 		    function setNewBatch(
445: 		        bytes32 _prevBatchHash,
446: 		        uint128 _newTimestamp,
447: 		        uint128 _expectedNewNumber,
448: 		        uint256 _baseFee
449: 		    ) external onlyCallFromBootloader {

471: 		    function unsafeOverrideBatch(
472: 		        uint256 _newTimestamp,
473: 		        uint256 _number,
474: 		        uint256 _baseFee
475: 		    ) external onlyCallFromBootloader {

482: 		    function incrementTxNumberInBatch() external onlyCallFromBootloader {

486: 		    function resetTxNumberInBatch() external onlyCallFromBootloader {
```
[[84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L84), [99](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L99), [105](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L105), [112](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L112), [341-347](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L341-L347), [402](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L402), [408](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L408), [444-449](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L444-L449), [471-475](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L471-L475), [482](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L482), [486](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L486)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

116: 		    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {

142: 		    function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner {

232: 		    function bridgehubConfirmL2Transaction(
233: 		        uint256 _chainId,
234: 		        bytes32 _txDataHash,
235: 		        bytes32 _txHash
236: 		    ) external override onlyBridgehub {

615: 		    function finalizeWithdrawalLegacyErc20Bridge(
616: 		        uint256 _l2BatchNumber,
617: 		        uint256 _l2MessageIndex,
618: 		        uint16 _l2TxNumberInBatch,
619: 		        bytes calldata _message,
620: 		        bytes32[] calldata _merkleProof
621: 		    ) external override onlyLegacyBridge returns (address l1Receiver, address l1Token, uint256 amount) {

644: 		    function claimFailedDepositLegacyErc20Bridge(
645: 		        address _depositSender,
646: 		        address _l1Token,
647: 		        uint256 _amount,
648: 		        bytes32 _l2TxHash,
649: 		        uint256 _l2BatchNumber,
650: 		        uint256 _l2MessageIndex,
651: 		        uint16 _l2TxNumberInBatch,
652: 		        bytes32[] calldata _merkleProof
653: 		    ) external override onlyLegacyBridge {
```
[[116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L116), [142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L142), [232-236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L232-L236), [615-621](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L615-L621), [644-653](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L644-L653)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

51: 		    function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

82: 		    function addStateTransitionManager(address _stateTransitionManager) external onlyOwner {

92: 		    function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner {

101: 		    function addToken(address _token) external onlyOwner {

108: 		    function setSharedBridge(address _sharedBridge) external onlyOwner {

114: 		    function createNewChain(
115: 		        uint256 _chainId,
116: 		        address _stateTransitionManager,
117: 		        address _baseToken,
118: 		        uint256, //_salt
119: 		        address _admin,
120: 		        bytes calldata _initData
121: 		    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
```
[[51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L51), [82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L82), [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L92), [101](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L101), [108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108), [114-121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114-L121)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

129: 		    function scheduleTransparent(Operation calldata _operation, uint256 _delay) external onlyOwner {

142: 		    function scheduleShadow(bytes32 _id, uint256 _delay) external onlyOwner {

154: 		    function cancel(bytes32 _id) external onlyOwner {

249: 		    function updateDelay(uint256 _newDelay) external onlySelf {

256: 		    function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
```
[[129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L129), [142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L142), [154](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L154), [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L249), [256](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L256)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

110: 		    function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

132: 		    function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {

137: 		    function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {

142: 		    function setNewVersionUpgrade(
143: 		        Diamond.DiamondCutData calldata _cutData,
144: 		        uint256 _oldProtocolVersion,
145: 		        uint256 _newProtocolVersion
146: 		    ) external onlyOwner {

152: 		    function setUpgradeDiamondCut(
153: 		        Diamond.DiamondCutData calldata _cutData,
154: 		        uint256 _oldProtocolVersion
155: 		    ) external onlyOwner {

160: 		    function freezeChain(uint256 _chainId) external onlyOwner {

165: 		    function unfreezeChain(uint256 _chainId) external onlyOwner {

170: 		    function revertBatches(uint256 _chainId, uint256 _newLastBatch) external onlyOwnerOrAdmin {

230: 		    function registerAlreadyDeployedStateTransition(
231: 		        uint256 _chainId,
232: 		        address _stateTransitionContract
233: 		    ) external onlyOwner {

239: 		    function createNewChain(
240: 		        uint256 _chainId,
241: 		        address _baseToken,
242: 		        address _sharedBridge,
243: 		        address _admin,
244: 		        bytes calldata _diamondCut
245: 		    ) external onlyBridgehub {
```
[[110](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L110), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L132), [137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L137), [142-146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L142-L146), [152-155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L152-L155), [160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L160), [165](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L165), [170](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L170), [230-233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L230-L233), [239-245](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L239-L245)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

73: 		    function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {

78: 		    function addValidator(uint256 _chainId, address _newValidator) external onlyChainAdmin(_chainId) {

87: 		    function removeValidator(uint256 _chainId, address _validator) external onlyChainAdmin(_chainId) {

96: 		    function setExecutionDelay(uint32 _executionDelay) external onlyOwner {

108: 		    function commitBatches(
109: 		        StoredBatchInfo calldata,
110: 		        CommitBatchInfo[] calldata _newBatchesData
111: 		    ) external onlyValidator(ERA_CHAIN_ID) {

126: 		    function commitBatchesSharedBridge(
127: 		        uint256 _chainId,
128: 		        StoredBatchInfo calldata,
129: 		        CommitBatchInfo[] calldata _newBatchesData
130: 		    ) external onlyValidator(_chainId) {

146: 		    function revertBatches(uint256) external onlyValidator(ERA_CHAIN_ID) {

153: 		    function revertBatchesSharedBridge(uint256 _chainId, uint256) external onlyValidator(_chainId) {

160: 		    function proveBatches(
161: 		        StoredBatchInfo calldata,
162: 		        StoredBatchInfo[] calldata,
163: 		        ProofInput calldata
164: 		    ) external onlyValidator(ERA_CHAIN_ID) {

171: 		    function proveBatchesSharedBridge(
172: 		        uint256 _chainId,
173: 		        StoredBatchInfo calldata,
174: 		        StoredBatchInfo[] calldata,
175: 		        ProofInput calldata
176: 		    ) external onlyValidator(_chainId) {

182: 		    function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {

203: 		    function executeBatchesSharedBridge(
204: 		        uint256 _chainId,
205: 		        StoredBatchInfo[] calldata _newBatchesData
206: 		    ) external onlyValidator(_chainId) {
```
[[73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L73), [78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L78), [87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L87), [96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96), [108-111](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L108-L111), [126-130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L126-L130), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L146), [153](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L153), [160-164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L160-L164), [171-176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L171-L176), [182](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L182), [203-206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L203-L206)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

111: 		    function reinitializeToken(
112: 		        ERC20Getters calldata _availableGetters,
113: 		        string memory _newName,
114: 		        string memory _newSymbol,
115: 		        uint8 _version
116: 		    ) external onlyNextVersion(_version) reinitializer(_version) {

145: 		    function bridgeMint(address _to, uint256 _amount) external override onlyBridge {

154: 		    function bridgeBurn(address _from, uint256 _amount) external override onlyBridge {
```
[[111-116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L111-L116), [145](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L145), [154](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L154)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

23: 		    function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {

45: 		    function setValidator(address _validator, bool _active) external onlyStateTransitionManager {

51: 		    function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {

58: 		    function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager {

67: 		    function changeFeeParams(FeeParams calldata _newFeeParams) external onlyAdminOrStateTransitionManager {

79: 		    function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {

89: 		    function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {

100: 		    function upgradeChainFromVersion(
101: 		        uint256 _oldProtocolVersion,
102: 		        Diamond.DiamondCutData calldata _diamondCut
103: 		    ) external onlyAdminOrStateTransitionManager {

123: 		    function executeUpgrade(Diamond.DiamondCutData calldata _diamondCut) external onlyStateTransitionManager {

133: 		    function freezeDiamond() external onlyAdminOrStateTransitionManager {

143: 		    function unfreezeDiamond() external onlyAdminOrStateTransitionManager {
```
[[23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L23), [45](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L45), [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L51), [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L58), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L67), [79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79), [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L89), [100-103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L100-L103), [123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L123), [133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L133), [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L143)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

199: 		    function commitBatches(
200: 		        StoredBatchInfo memory _lastCommittedBatchData,
201: 		        CommitBatchInfo[] calldata _newBatchesData
202: 		    ) external nonReentrant onlyValidator {

207: 		    function commitBatchesSharedBridge(
208: 		        uint256, // _chainId
209: 		        StoredBatchInfo memory _lastCommittedBatchData,
210: 		        CommitBatchInfo[] calldata _newBatchesData
211: 		    ) external nonReentrant onlyValidator {

337: 		    function executeBatchesSharedBridge(
338: 		        uint256,
339: 		        StoredBatchInfo[] calldata _batchesData
340: 		    ) external nonReentrant onlyValidator {

345: 		    function executeBatches(StoredBatchInfo[] calldata _batchesData) external nonReentrant onlyValidator {

368: 		    function proveBatches(
369: 		        StoredBatchInfo calldata _prevBatch,
370: 		        StoredBatchInfo[] calldata _committedBatches,
371: 		        ProofInput calldata _proof
372: 		    ) external nonReentrant onlyValidator {

377: 		    function proveBatchesSharedBridge(
378: 		        uint256, // _chainId
379: 		        StoredBatchInfo calldata _prevBatch,
380: 		        StoredBatchInfo[] calldata _committedBatches,
381: 		        ProofInput calldata _proof
382: 		    ) external nonReentrant onlyValidator {

472: 		    function revertBatches(uint256 _newLastBatch) external nonReentrant onlyValidatorOrStateTransitionManager {

477: 		    function revertBatchesSharedBridge(uint256, uint256 _newLastBatch) external nonReentrant onlyValidator {
```
[[199-202](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L199-L202), [207-211](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L207-L211), [337-340](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L337-L340), [345](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L345), [368-372](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L368-L372), [377-382](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L377-L382), [472](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L472), [477](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L477)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

38: 		    function transferEthToSharedBridge() external onlyBaseTokenBridge {
```
[[38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L38)]

</details>

---

### [G-24] Cache `keccak256` with static arguments

When the arguments are static, the `keccak256` should be calculated only once and stored in an `immutable` state variable.

*There are 2 instances of this issue.*


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

// @audit keccak256("zkSync")
139: 		            abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

// @audit keccak256("2")
139: 		            abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
```
[[139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139)]


---

### [G-25] Array `length` is not cached

Solidity compiler reads array length every iteration if not cached. Storage array requires an extra sload operation (100 gas), memory array requires an extra mload operation (3 gas).

*There are 11 instances of this issue.*


```solidity
File: code/system-contracts/contracts/Compressor.sol

61: 		            for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
```
[[61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L61)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

225: 		        for (uint256 i = 0; i < _calls.length; ++i) {
```
[[225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {

135: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {

185: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {

209: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```
[[116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185), [209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226: 		        for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
[[226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

142: 		        for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

257: 		        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

289: 		        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

636: 		        for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {
```
[[142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289), [636](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636)]


---

### [G-26] Caching global variables is more expensive than using the actual variable

It's better to not cache global variables, as their direct usage is cheaper (e.g. `msg.sender`).

*There is 1 instance of this issue.*


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

329: 		        uint256 value = msg.value;
```
[[329](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L329)]


---

### [G-27] Add `unchecked` blocks for subtractions where the operands cannot underflow

There are some checks to avoid an underflow, so it's safe to use `unchecked` to have some gas savings.

*There are 4 instances of this issue.*


```solidity
File: code/system-contracts/contracts/SystemContext.sol

// @audit check on line 144
144: 		        if (blockNumber <= _block || blockNumber - _block > 256) {
```
[[144](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L144)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

// @audit check on line 121
132: 		            require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
```
[[132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

// @audit check on line 238
243: 		            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
```
[[243](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L243)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

// @audit check on line 22
28: 		            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
```
[[28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L28)]


---

### [G-28] Add `unchecked` blocks for divisions where the operands cannot overflow

`uint` divisions can't overflow, while `int` divisions can overflow only in [one specific case](https://docs.soliditylang.org/en/latest/types.html#division).

Consider adding an `unchecked` block to have some [gas savings](https://gist.github.com/DadeKuma/3bc597338ae774b8b3bd43280d55271f).

*There are 10 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

51: 		        return KECCAK_ROUND_GAS_COST * (_length / KECCAK_ROUND_NUMBER_OF_BYTES + 1);

62: 		        return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1);
```
[[51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L51), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L62)]



```solidity
File: code/system-contracts/contracts/NonceHolder.sol

180: 		        deploymentNonce = _rawMinNonce / DEPLOY_NONCE_MULTIPLIER;
```
[[180](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L180)]



```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

86: 		        uint256 lengthInWords = _bytecode.length / 32;
```
[[86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L86)]



```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

25: 		        uint256 bytecodeLenInWords = _bytecode.length / 32;
```
[[25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

30: 		        require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");
```
[[30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L30)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

159: 		        uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
160: 		            s.baseTokenGasPriceMultiplierDenominator;

168: 		            batchOverheadBaseToken /
169: 		            uint256(feeParams.maxPubdataPerBatch);

171: 		        uint256 l2GasPrice = feeParams.minimalL2GasPrice + batchOverheadBaseToken / uint256(feeParams.maxL2GasPerBatch);

172: 		        uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata;
```
[[159-160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L159-L160), [168-169](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L168-L169), [171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L171), [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L172)]

</details>

---

### [G-29] Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead

Citing the [documentation](https://docs.soliditylang.org/en/latest/internals/layout_in_storage.html):

> When using elements that are smaller than 32 bytes, your contract’s gas usage may be higher.This is because the EVM operates on 32 bytes at a time.Therefore, if the element is smaller than that, the EVM must use more operations in order to reduce the size of the element from 32 bytes to the desired size.

For example, each operation involving a `uint8` costs an extra ** 22 - 28 gas ** (depending on whether the other operand is also a variable of type `uint8`) as compared to ones involving`uint256`, due to the compiler having to clear the higher bits of the memory word before operating on the`uint8`, as well as the associated stack operations of doing so.

Note that it might be beneficial to use reduced-size types when dealing with storage values because the compiler will pack multiple elements into one storage slot, but if not, it will have the opposite effect.

*There are 204 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

68: 		            uint64 txDataLen = uint64(_transaction.data.length);

164: 		            uint64 txDataLen = uint64(_transaction.data.length);

259: 		            uint64 txDataLen = uint64(_transaction.data.length);
```
[[68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L68), [164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L164), [259](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L259)]



```solidity
File: code/system-contracts/contracts/Compressor.sol

65: 		                uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);

66: 		                uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

129: 		            uint64 enumIndex = stateDiff.readUint64(84);

143: 		            uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

145: 		            uint8 operation = metadata & OPERATION_BITMASK;

146: 		            uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

161: 		            uint64 enumIndex = stateDiff.readUint64(84);

174: 		            uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

176: 		            uint8 operation = metadata & OPERATION_BITMASK;

177: 		            uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
```
[[65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L65), [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L66), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L129), [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L143), [145](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L145), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L146), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L161), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L174), [176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L176), [177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L177)]



```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

133: 		        uint128 value = Utils.safeCastToU128(_transaction.value);

135: 		        uint32 gas = Utils.safeCastToU32(gasleft());

161: 		        uint8 v;
```
[[133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L133), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L135), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L161)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

75: 		        uint8 version = uint8(_bytecodeHash[0]);
```
[[75](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L75)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

200: 		        uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

233: 		        uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

237: 		            uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

251: 		        uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

255: 		            uint32 currentBytecodeLength = uint32(

286: 		        uint24 compressedStateDiffSize = uint24(bytes3(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 3]));

289: 		        uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));

300: 		        uint32 numberOfStateDiffs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
```
[[200](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L200), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L233), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L237), [251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L251), [255](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L255), [286](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L286), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L289), [300](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L300)]



```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

140: 		    function decimals() external pure override returns (uint8) {
```
[[140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L140)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

89: 		    uint16 public txNumberInBlock;

133: 		        uint128 blockNumber = currentVirtualL2BlockInfo.number;

172: 		    function getBatchNumberAndTimestamp() public view returns (uint128 batchNumber, uint128 batchTimestamp) {

172: 		    function getBatchNumberAndTimestamp() public view returns (uint128 batchNumber, uint128 batchTimestamp) {

180: 		    function getL2BlockNumberAndTimestamp() public view returns (uint128 blockNumber, uint128 blockTimestamp) {

180: 		    function getL2BlockNumberAndTimestamp() public view returns (uint128 blockNumber, uint128 blockTimestamp) {

190: 		    function getBlockNumber() public view returns (uint128) {

198: 		    function getBlockTimestamp() public view returns (uint128) {

222: 		        uint128 _blockNumber,

223: 		        uint128 _blockTimestamp,

233: 		    function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {

241: 		    function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {

264: 		        uint128 _l2BlockNumber,

265: 		        uint128 _maxVirtualBlocksToCreate,

266: 		        uint128 _newTimestamp

278: 		            uint128 currentBatchNumber = currentBatchInfo.number;

314: 		    function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal {

314: 		    function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal {

342: 		        uint128 _l2BlockNumber,

343: 		        uint128 _l2BlockTimestamp,

346: 		        uint128 _maxVirtualBlocksToCreate

350: 		            uint128 currentBatchTimestamp = currentBatchInfo.timestamp;

358: 		        (uint128 currentL2BlockNumber, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();

358: 		        (uint128 currentL2BlockNumber, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();

409: 		        (uint128 currentBatchNumber, uint128 currentBatchTimestamp) = getBatchNumberAndTimestamp();

409: 		        (uint128 currentBatchNumber, uint128 currentBatchTimestamp) = getBatchNumberAndTimestamp();

410: 		        (, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();

427: 		    function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {

428: 		        uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp;

446: 		        uint128 _newTimestamp,

447: 		        uint128 _expectedNewNumber,

450: 		        (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();

450: 		        (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();

497: 		        (uint128 blockNumber, uint128 blockTimestamp) = getBatchNumberAndTimestamp();

497: 		        (uint128 blockNumber, uint128 blockTimestamp) = getBatchNumberAndTimestamp();
```
[[89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L89), [133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L133), [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L172), [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L172), [180](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L180), [180](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L180), [190](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L190), [198](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L198), [222](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L222), [223](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L223), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L233), [241](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L241), [264](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L264), [265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L265), [266](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L266), [278](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L278), [314](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L314), [314](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L314), [342](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L342), [343](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L343), [346](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L346), [350](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L350), [358](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L358), [358](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L358), [409](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L409), [409](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L409), [410](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L410), [427](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L427), [428](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L428), [446](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L446), [447](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L447), [450](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L450), [450](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L450), [497](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L497), [497](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L497)]



```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

27: 		    function safeCastToU32(uint256 _x) internal pure returns (uint32) {

37: 		    function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

40: 		        uint32 dataStart;

44: 		        uint32 dataLength = uint32(Utils.safeCastToU32(data.length));

77: 		        uint32 gasLimit,

79: 		        uint128 value,

96: 		        uint32 dataOffset,

97: 		        uint32 memoryPage,

98: 		        uint32 dataStart,

99: 		        uint32 dataLength,

100: 		        uint32 gasPassed,

101: 		        uint8 shardId,

122: 		        uint32 gasPassed,

123: 		        uint8 shardId,
```
[[27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L27), [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L37), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L40), [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L44), [77](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L77), [79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L79), [96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L96), [97](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L97), [98](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L98), [99](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L99), [100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L100), [101](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L101), [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L122), [123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L123)]



```solidity
File: code/system-contracts/contracts/interfaces/IBaseToken.sol

16: 		    function decimals() external pure returns (uint8);
```
[[16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IBaseToken.sol#L16)]



```solidity
File: code/system-contracts/contracts/interfaces/IMailbox.sol

9: 		        uint16 _l2TxNumberInBlock,
```
[[9](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IMailbox.sol#L9)]



```solidity
File: code/system-contracts/contracts/interfaces/ISystemContext.sol

13: 		        uint128 timestamp;

14: 		        uint128 number;

23: 		        uint128 virtualBlockStartBatch;

27: 		        uint128 virtualBlockFinishL2Block;

44: 		    function txNumberInBlock() external view returns (uint16);

50: 		    function getBlockNumber() external view returns (uint128);

52: 		    function getBlockTimestamp() external view returns (uint128);

54: 		    function getBatchNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);

54: 		    function getBatchNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);

56: 		    function getL2BlockNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);

56: 		    function getL2BlockNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);
```
[[13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L13), [14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L14), [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L23), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L27), [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L44), [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L50), [52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L52), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L54), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L54), [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L56), [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L56)]



```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

261: 		        uint32 shrinkTo = uint32(msg.data.length - (_data.length + dataOffset));

264: 		        uint32 gas = Utils.safeCastToU32(_gas);
```
[[261](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L261), [264](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L264)]



```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

49: 		    function encodeNonSingleBytesLen(uint64 _len) internal pure returns (bytes memory) {

56: 		    function encodeListLen(uint64 _len) internal pure returns (bytes memory) {

60: 		    function _encodeLength(uint64 _len, uint256 _offset) private pure returns (bytes memory encoded) {
```
[[49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L49), [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L56), [60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L60)]



```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

94: 		    function ptrAddIntoActive(uint32 _value) internal view {

106: 		    function ptrShrinkIntoActive(uint32 _shrink) internal view {

125: 		        uint32 _inputMemoryOffset,

126: 		        uint32 _inputMemoryLength,

127: 		        uint32 _outputMemoryOffset,

128: 		        uint32 _outputMemoryLength,

129: 		        uint64 _perPrecompileInterpreted

150: 		        uint32 _gasToBurn,

151: 		        uint32 _pubdataToSpend

168: 		    function setValueForNextFarCall(uint128 _value) internal returns (bool success) {

227: 		    function getPubdataPublishedFromMeta(uint256 meta) internal pure returns (uint32 pubdataPublished) {

237: 		    function getHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 heapSize) {

246: 		    function getAuxHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 auxHeapSize) {

254: 		    function getShardIdFromMeta(uint256 meta) internal pure returns (uint8 shardId) {

263: 		    function getCallerShardIdFromMeta(uint256 meta) internal pure returns (uint8 callerShardId) {

272: 		    function getCodeShardIdFromMeta(uint256 meta) internal pure returns (uint8 codeShardId) {

344: 		    function burnGas(uint32 _gasToPay, uint32 _pubdataToSpend) internal view {

344: 		    function burnGas(uint32 _gasToPay, uint32 _pubdataToSpend) internal view {
```
[[94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L94), [106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L106), [125](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L125), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L126), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L127), [128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L128), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L129), [150](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L150), [151](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L151), [168](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L168), [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L227), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L237), [246](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L246), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L254), [263](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L263), [272](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L272), [344](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L344), [344](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L344)]



```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

76: 		    function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

79: 		        uint32 dataStart;

83: 		        uint32 dataLength = uint32(Utils.safeCastToU32(data.length));

124: 		        uint32 gasLimit,

126: 		        uint128 value,

151: 		        uint32 gasLimit,

153: 		        uint128 value,

215: 		        uint32 dataOffset,

216: 		        uint32 memoryPage,

217: 		        uint32 dataStart,

218: 		        uint32 dataLength,

219: 		        uint32 gasPassed,

220: 		        uint8 shardId,

251: 		        uint32 gasPassed,

252: 		        uint8 shardId,
```
[[76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L76), [79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L79), [83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L83), [124](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L124), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L126), [151](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L151), [153](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L153), [215](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L215), [216](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L216), [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L217), [218](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L218), [219](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L219), [220](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L220), [251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L251), [252](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L252)]



```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

171: 		            uint64 txDataLen = uint64(_transaction.data.length);

249: 		            uint64 txDataLen = uint64(_transaction.data.length);

321: 		            uint64 txDataLen = uint64(_transaction.data.length);
```
[[171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L171), [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L249), [321](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L321)]



```solidity
File: code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol

19: 		    function readUint16(bytes calldata _bytes, uint256 _start) internal pure returns (uint16 result) {

26: 		    function readUint32(bytes calldata _bytes, uint256 _start) internal pure returns (uint32 result) {

33: 		    function readUint64(bytes calldata _bytes, uint256 _start) internal pure returns (uint64 result) {
```
[[19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L19), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L26), [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L33)]



```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

20: 		    function safeCastToU128(uint256 _x) internal pure returns (uint128) {

26: 		    function safeCastToU32(uint256 _x) internal pure returns (uint32) {

32: 		    function safeCastToU24(uint256 _x) internal pure returns (uint24) {
```
[[20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L20), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L26), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L32)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

182: 		        uint16 _l2TxNumberInBatch,

211: 		        uint16 _l2TxNumberInBatch,
```
[[182](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L182), [211](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L211)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

285: 		        uint16 _l2TxNumberInBatch,

312: 		        uint16 _l2TxNumberInBatch,

389: 		        uint16 _l2TxNumberInBatch,

404: 		        uint16 l2TxNumberInBatch;

413: 		        uint16 _l2TxNumberInBatch,

503: 		        (uint32 functionSignature, uint256 offset) = UnsafeBytes.readUint32(_l2ToL1message, 0);

618: 		        uint16 _l2TxNumberInBatch,

651: 		        uint16 _l2TxNumberInBatch,
```
[[285](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L285), [312](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L312), [389](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L389), [404](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L404), [413](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L413), [503](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L503), [618](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L618), [651](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L651)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

181: 		        uint16 _l2TxNumberInBatch,
```
[[181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L181)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol

94: 		        uint16 _l2TxNumberInBatch,
```
[[94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L94)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

53: 		    uint32 public executionDelay;

55: 		    constructor(address _initialOwner, uint32 _executionDelay) {

96: 		    function setExecutionDelay(uint32 _executionDelay) external onlyOwner {

115: 		            uint32 timestamp = uint32(block.timestamp);

134: 		            uint32 timestamp = uint32(block.timestamp);
```
[[53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L53), [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55), [96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96), [115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L115), [134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L134)]



```solidity
File: code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

22: 		    uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L22)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

31: 		    uint8 private decimals_;

93: 		        try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {

115: 		        uint8 _version

134: 		    modifier onlyNextVersion(uint8 _version) {

171: 		    function decimals() public view override returns (uint8) {

183: 		    function decodeUint8(bytes memory _input) external pure returns (uint8 result) {
```
[[31](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L31), [93](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L93), [115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L115), [134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L134), [171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L171), [183](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L183)]



```solidity
File: code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol

22: 		    uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L22)]



```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

49: 		        uint16 _l2TxNumberInBatch,

56: 		        uint16 _l2TxNumberInBatch,
```
[[49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L49), [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L56)]



```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

81: 		        uint16 _l2TxNumberInBatch,

93: 		        uint16 _l2TxNumberInBatch,

100: 		        uint16 _l2TxNumberInBatch,

109: 		        uint16 _l2TxNumberInBatch,
```
[[81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L81), [93](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L93), [100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L100), [109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L109)]



```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

40: 		        uint8 version = uint8(_bytecodeHash[0]);
```
[[40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L40)]



```solidity
File: code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol

19: 		    function readUint32(bytes memory _bytes, uint256 _start) internal pure returns (uint32 result, uint256 offset) {
```
[[19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L19)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol

40: 		    function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external;

40: 		    function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external;

84: 		        uint128 oldNominator,

85: 		        uint128 oldDenominator,

86: 		        uint128 newNominator,

87: 		        uint128 newDenominator
```
[[40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L40), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L40), [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L84), [85](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L85), [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L86), [87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L87)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

84: 		        uint64 batchNumber;

86: 		        uint64 indexRepeatedStorageChanges;

113: 		        uint64 batchNumber;

114: 		        uint64 timestamp;

115: 		        uint64 indexRepeatedStorageChanges;
```
[[84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L84), [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L86), [113](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L113), [114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L114), [115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L115)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol

112: 		    function baseTokenGasPriceMultiplierNominator() external view returns (uint128);

115: 		    function baseTokenGasPriceMultiplierDenominator() external view returns (uint128);
```
[[112](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L112), [115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L115)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

51: 		        uint16 _l2TxNumberInBatch,

65: 		        uint16 _l2TxNumberInBatch,

126: 		        uint64 expirationTimestamp,
```
[[51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L51), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L65), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L126)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

32: 		        uint16 selectorPosition;

41: 		        uint16 facetPosition;

208: 		        uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16();
```
[[32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L32), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L41), [208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L208)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

18: 		    function get(Uint32Map storage _map, uint256 _index) internal view returns (uint32 result) {

38: 		    function set(Uint32Map storage _map, uint256 _index, uint32 _value) internal {

54: 		            uint32 oldValue = uint32(mapValue >> bitOffset);
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L18), [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L38), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L54)]



```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol

12: 		        uint16 _l2TxNumberInBatch,
```
[[12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L12)]



```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol

13: 		        uint16 _l2TxNumberInBatch,
```
[[13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L13)]



```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol

6: 		    event BridgeInitialize(address indexed l1Token, string name, string symbol, uint8 decimals);
```
[[6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L6)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

79: 		    function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {

79: 		    function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {

80: 		        uint128 oldNominator = s.baseTokenGasPriceMultiplierNominator;

81: 		        uint128 oldDenominator = s.baseTokenGasPriceMultiplierDenominator;
```
[[79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79), [79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79), [80](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L80), [81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L81)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

39: 		        uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));

592: 		    function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

597: 		    function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {
```
[[39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L39), [592](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L592), [597](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

67: 		    function baseTokenGasPriceMultiplierNominator() external view returns (uint128) {

72: 		    function baseTokenGasPriceMultiplierDenominator() external view returns (uint128) {
```
[[67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L67), [72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L72)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

78: 		        uint16 _l2TxNumberInBatch,

181: 		        uint16 _l2TxNumberInBatch,
```
[[78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L78), [181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L181)]

</details>

---

### [G-30] Stack variable cost less while used in emitting event

Using a stack variable instead of a state variable is cheaper when emitting an event.

*There are 8 instances of this issue.*


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

// @audit pendingAdmin
69: 		        emit NewAdmin(previousAdmin, pendingAdmin);
```
[[69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

// @audit minDelay
250: 		        emit ChangeMinDelay(minDelay, _newDelay);

// @audit securityCouncil
257: 		        emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```
[[250](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L250), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L257)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

// @audit pendingAdmin
128: 		        emit NewAdmin(previousAdmin, pendingAdmin);

// @audit protocolVersion
227: 		        emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
```
[[128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L128), [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

// @audit decimals_
101: 		        emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);

// @audit l1Address
126: 		        emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);

// @audit decimals_
126: 		        emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);
```
[[101](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L101), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126)]


---

### [G-31] Using pre instead of post increments/decrements

Pre increments/decrements (`++i/--i`) are cheaper than post increments/decrements (`i++/i--`): it saves 6 gas per expression.

*There are 5 instances of this issue.*


```solidity
File: code/system-contracts/contracts/Compressor.sol

135: 		            numInitialWritesProcessed++;

144: 		            stateDiffPtr++;
```
[[135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L135), [144](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L144)]



```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

36: 		        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[[36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

580: 		        for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

667: 		        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[[580](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580), [667](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)]


---

### [G-32] `>=`/`<=` costs less gas than `>`/`<`

The compiler uses opcodes `GT` and `ISZERO` for code that uses `>`, but only requires `LT` for `>=`. A similar behaviour applies for `>`, which uses opcodes `LT` and `ISZERO`, but only requires `GT` for `<=`.

*There are 97 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

102: 		        if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {

132: 		            uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS &&
```
[[102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L102), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L132)]



```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

24: 		        require(_delegateTo.code.length > 0, "Delegatee is an EOA");
```
[[24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L24)]



```solidity
File: code/system-contracts/contracts/Compressor.sol

61: 		            for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {

63: 		                require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

127: 		        for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

159: 		        for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
```
[[61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L63), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L127), [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L159)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

48: 		            _address > address(MAX_SYSTEM_CONTRACT_ADDRESS) &&

248: 		        for (uint256 i = 0; i < deploymentsLength; ++i) {

253: 		        for (uint256 i = 0; i < deploymentsLength; ++i) {

265: 		        require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

303: 		        require(knownCodeMarker > 0, "The code hash is not known");

332: 		            if (value > 0) {

339: 		            if (value > 0) {
```
[[48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L48), [248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L248), [253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L253), [265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L265), [303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L303), [332](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L332), [339](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L339)]



```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

49: 		        uint256 pubdataAllowance = _maxTotalGas > expectedForCompute ? _maxTotalGas - expectedForCompute : 0;

63: 		        uint256 pubdataSpent = pubdataPublishedAfter > pubdataPublishedBefore
```
[[49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L49), [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L63)]



```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

38: 		            for (uint256 i = 0; i < immutablesLength; ++i) {
```
[[38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L38)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

30: 		            for (uint256 i = 0; i < hashesLen; ++i) {
```
[[30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L30)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

206: 		        for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

218: 		        for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

222: 		        while (nodesOnCurrentLevel > 1) {

224: 		            for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

236: 		        for (uint256 i = 0; i < numberOfMessages; ++i) {

254: 		        for (uint256 i = 0; i < numberOfBytecodes; ++i) {
```
[[206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L206), [218](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L218), [222](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L222), [224](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L224), [236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L236), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L254)]



```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

53: 		        uint256 userGas = gasInContext > MSG_VALUE_SIMULATOR_STIPEND_GAS
```
[[53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L53)]



```solidity
File: code/system-contracts/contracts/NonceHolder.sol

156: 		        return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);

156: 		        return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);
```
[[156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L156), [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L156)]



```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

36: 		        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[[36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

119: 		        return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;

144: 		        if (blockNumber <= _block || blockNumber - _block > 256) {

146: 		        } else if (_block < currentVirtualBlockUpgradeInfo.virtualBlockStartBatch) {

152: 		            currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0

245: 		        require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

287: 		            require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

355: 		            require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

387: 		                _l2BlockTimestamp > currentL2BlockTimestamp,

413: 		        require(currentBatchNumber > 0, "The current batch number must be greater than 0");

430: 		            _newTimestamp > currentBlockTimestamp,

451: 		        require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");
```
[[119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L119), [144](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L144), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L146), [152](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L152), [245](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L245), [287](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L287), [355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L355), [387](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L387), [413](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L413), [430](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L430), [451](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L451)]



```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

26: 		            if (_val < 128) {

62: 		            if (_len < 56) {

86: 		            if (_number > type(uint128).max) {

90: 		            if (_number > type(uint64).max) {

94: 		            if (_number > type(uint32).max) {

98: 		            if (_number > type(uint16).max) {

102: 		            if (_number > type(uint8).max) {
```
[[26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L26), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L62), [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L86), [90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L90), [94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L94), [98](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L98), [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L102)]



```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

319: 		        require(index < 10, "There are only 10 accessible registers");
```
[[319](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319)]



```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

378: 		            if (currentAllowance < minAllowance) {
```
[[378](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L378)]



```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

87: 		        require(lengthInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words
```
[[87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L87)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

121: 		            require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");

129: 		            require(amount > 0, "ShB: 0 amount to transfer");

327: 		        require(_amount > 0, "y1");

375: 		        return (_chainId == ERA_CHAIN_ID) && (_l2BatchNumber < eraFirstPostUpgradeBatch);
```
[[121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L121), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129), [327](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327), [375](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L375)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

301: 		            _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,

329: 		        } else if (_refundRecipient.code.length > 0) {
```
[[301](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L301), [329](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L329)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

111: 		        } else if (timestamp > block.timestamp) {

225: 		        for (uint256 i = 0; i < _calls.length; ++i) {
```
[[111](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L111), [225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {

135: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {

185: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {

209: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```
[[116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185), [209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226: 		        for (uint256 i = 0; i < _factoryDeps.length; ++i) {

239: 		            _newProtocolVersion > previousProtocolVersion,
```
[[226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226), [239](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L239)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

124: 		        require(_amount > 0, "Amount cannot be zero");
```
[[124](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L124)]



```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

26: 		        require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words
```
[[26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L26)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

101: 		        for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {

107: 		            require(selectors.length > 0, "B"); // no functions for diamond cut

132: 		        require(_facet.code.length > 0, "G");

138: 		        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

155: 		        require(_facet.code.length > 0, "K");

158: 		        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

178: 		        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
```
[[101](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101), [107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L138), [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L155), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158), [178](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L178)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

24: 		        require(pathLength > 0, "xc");

25: 		        require(pathLength < 256, "bt");

26: 		        require(_index < (1 << pathLength), "px");

29: 		        for (uint256 i; i < pathLength; i = i.uncheckedInc()) {
```
[[24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24), [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L25), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L26), [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L29)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

117: 		            s.protocolVersion > _oldProtocolVersion,
```
[[117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L117)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

114: 		        require(_previousBatchTimestamp < batchTimestamp, "h3");

142: 		        for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

257: 		        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

289: 		        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

311: 		        for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {

351: 		        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {

405: 		        for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {

429: 		        if (_proof.serializedProof.length > 0) {

482: 		        require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch

485: 		        if (_newLastBatch < s.totalBatchesVerified) {

492: 		        if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) {

580: 		        for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

593: 		        return (_bitMap & (1 << _index)) > 0;

631: 		        require(_pubdataCommitments.length > 0, "pl");

636: 		        for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {

667: 		        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[[114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L114), [142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289), [311](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L311), [351](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351), [405](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L405), [429](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L429), [482](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L482), [485](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L485), [492](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L492), [580](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580), [593](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L593), [631](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631), [636](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636), [667](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

208: 		        for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {
```
[[208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

158: 		        require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

277: 		        if (refundRecipient.code.length > 0) {

356: 		        for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {
```
[[158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158), [277](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L277), [356](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356)]

</details>

---

### [G-33] `internal` functions only called once can be inlined to save gas

Consider removing the following internal functions, and put the logic directly where they are called, as they are called only once.

*There are 80 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

44: 		    function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {

139: 		    function encodeEIP2930TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {

229: 		    function encodeEIP1559TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {
```
[[44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L44), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L139), [229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L229)]



```solidity
File: code/system-contracts/contracts/Compressor.sol

197: 		    function _decodeRawBytecode(
```
[[197](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L197)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

283: 		    function _performDeployOnAddress(

309: 		    function _storeConstructingByteCodeHashOnAddress(address _newAddress, bytes32 _bytecodeHash) internal {
```
[[283](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L283), [309](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L309)]



```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

78: 		    function _validateTransaction(

131: 		    function _execute(Transaction calldata _transaction) internal {

159: 		    function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {
```
[[78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L78), [131](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L131), [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L159)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

74: 		    function _validateBytecode(bytes32 _bytecodeHash) internal pure {
```
[[74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L74)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

61: 		    function sha256GasCost(uint256 _length) internal pure returns (uint256) {
```
[[61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L61)]



```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

112: 		    function _getL1WithdrawMessage(address _to, uint256 _amount) internal pure returns (bytes memory) {

117: 		    function _getExtendedWithdrawMessage(
```
[[112](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L112), [117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L117)]



```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

25: 		    function _getAbiParams() internal view returns (uint256 value, bool isSystemCall, address to) {
```
[[25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L25)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

221: 		    function _calculateL2BlockHash(

233: 		    function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {

241: 		    function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {

263: 		    function _setVirtualBlock(

427: 		    function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {
```
[[221](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L221), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L233), [241](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L241), [263](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L263), [427](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L427)]



```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

37: 		    function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

95: 		    function getFarCallABI(

121: 		    function getFarCallABIWithEmptyFatPointer(
```
[[37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L37), [95](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L95), [121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L121)]



```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

124: 		    function rawCall(

159: 		    function rawStaticCall(uint256 _gas, address _address, bytes calldata _data) internal view returns (bool success) {

173: 		    function rawDelegateCall(uint256 _gas, address _address, bytes calldata _data) internal returns (bool success) {

191: 		    function rawMimicCall(

232: 		    function propagateRevert() internal pure {
```
[[124](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L124), [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L159), [173](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L173), [191](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L191), [232](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L232)]



```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

148: 		    function unsafePrecompileCall(

203: 		    function getZkSyncMetaBytes() internal view returns (uint256 meta) {

227: 		    function getPubdataPublishedFromMeta(uint256 meta) internal pure returns (uint32 pubdataPublished) {

237: 		    function getHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 heapSize) {

246: 		    function getAuxHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 auxHeapSize) {

254: 		    function getShardIdFromMeta(uint256 meta) internal pure returns (uint8 shardId) {

263: 		    function getCallerShardIdFromMeta(uint256 meta) internal pure returns (uint8 callerShardId) {

272: 		    function getCodeShardIdFromMeta(uint256 meta) internal pure returns (uint8 codeShardId) {

296: 		    function getCallFlags() internal view returns (uint256 callFlags) {
```
[[148](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L148), [203](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L203), [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L227), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L237), [246](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L246), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L254), [263](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L263), [272](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L272), [296](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L296)]



```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

76: 		    function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

123: 		    function systemCallWithReturndata(

250: 		    function getFarCallABIWithEmptyFatPointer(
```
[[76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L76), [123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L123), [250](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L250)]



```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

44: 		    function bytecodeLenInWords(bytes32 _bytecodeHash) internal pure returns (uint256 codeLengthInWords) {

71: 		    function constructedBytecodeHash(bytes32 _bytecodeHash) internal pure returns (bytes32) {
```
[[44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L44), [71](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L71)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

160: 		    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```
[[160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

254: 		    function _getERC20Getters(address _token) internal view returns (bytes memory) {

458: 		    function _checkWithdrawal(

487: 		    function _parseL2WithdrawalMessage(
```
[[254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L254), [458](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L458), [487](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L487)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

177: 		    function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
```
[[177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

163: 		    function _upgradeVerifier(address _newVerifier, VerifierParams calldata _verifierParams) internal {

171: 		    function _setBaseSystemContracts(bytes32 _bootloaderHash, bytes32 _defaultAccountHash) internal {

180: 		    function _setL2SystemContractUpgrade(

236: 		    function _setNewProtocolVersion(uint256 _newProtocolVersion) internal virtual {

263: 		    function _upgradeL1Contract(bytes calldata _customCallDataForUpgrade) internal virtual {}

269: 		    function _postUpgrade(bytes calldata _customCallDataForUpgrade) internal virtual {}
```
[[163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L163), [171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L171), [180](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L180), [236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L236), [263](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L263), [269](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L269)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

109: 		    function _deployL2Token(address _l1Token, bytes calldata _data) internal returns (address) {

138: 		    function _getL1WithdrawMessage(

164: 		    function _deployBeaconProxy(bytes32 salt) internal returns (BeaconProxy proxy) {
```
[[109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L109), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L138), [164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L164)]



```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

49: 		    function bytecodeLen(bytes32 _bytecodeHash) internal pure returns (uint256 codeLengthInWords) {
```
[[49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L49)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

69: 		    function getMinimalPriorityTransactionGasLimit(

109: 		    function getTransactionBodyGasLimit(

128: 		    function getOverheadForTransaction(
```
[[69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L69), [109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L109), [128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L128)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

103: 		    function _verifyBatchTimestamp(

130: 		    function _processL2Logs(

253: 		    function _commitBatchesWithoutSystemContractsUpgrade(

273: 		    function _commitBatchesWithSystemContractsUpgrade(

308: 		    function _collectOperationsFromPriorityQueue(uint256 _nPriorityOps) internal returns (bytes32 concatHash) {

321: 		    function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {

453: 		    function _getBatchProofPublicInput(

500: 		    function _createBatchCommitment(

515: 		    function _batchPassThroughData(CommitBatchInfo calldata _batch) internal pure returns (bytes memory) {

525: 		    function _batchMetaParameters() internal view returns (bytes memory) {

537: 		    function _batchAuxiliaryOutput(

561: 		    function _encodeBlobAuxilaryOutput(

592: 		    function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

597: 		    function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {

605: 		    function _pointEvaluationPrecompile(

625: 		    function _verifyBlobInformation(
```
[[103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L103), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L130), [253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L253), [273](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L273), [308](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L308), [321](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L321), [453](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L453), [500](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L500), [515](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515), [525](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525), [537](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537), [561](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L561), [592](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L592), [597](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597), [605](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L605), [625](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L625)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

130: 		    function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {

258: 		    function _requestL2Transaction(

289: 		    function _serializeL2Transaction(

316: 		    function _writePriorityOp(

353: 		    function _hashFactoryDeps(bytes[] memory _factoryDeps) internal pure returns (uint256[] memory hashedFactoryDeps) {
```
[[130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L130), [258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L258), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L289), [316](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L316), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L353)]

</details>

---

### [G-34] Inline `modifiers` that are only used once, to save gas

Consider removing the following modifiers, and put the logic directly in the function where they are used, as they are used only once.

*There are 7 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

28: 		    modifier onlySelf() {
29: 		        require(msg.sender == address(this), "Callable only by self");
30: 		        _;
31: 		    }
```
[[28-31](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L28-L31)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

19: 		    modifier onlyCompressor() {
20: 		        require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");
21: 		        _;
22: 		    }
```
[[19-22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L19-L22)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

74: 		    modifier onlyBridgehubOrEra(uint256 _chainId) {
75: 		        require(
76: 		            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
77: 		            "L1SharedBridge: not bridgehub or era chain"
78: 		        );
79: 		        _;
80: 		    }
```
[[74-80](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L74-L80)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

64: 		    modifier onlySecurityCouncil() {
65: 		        require(msg.sender == securityCouncil, "Only security council is allowed to call this function");
66: 		        _;
67: 		    }

70: 		    modifier onlyOwnerOrSecurityCouncil() {
71: 		        require(
72: 		            msg.sender == owner() || msg.sender == securityCouncil,
73: 		            "Only the owner and security council are allowed to call this function"
74: 		        );
75: 		        _;
76: 		    }
```
[[64-67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L64-L67), [70-76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L70-L76)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

63: 		    modifier onlyBridgehub() {
64: 		        require(msg.sender == bridgehub, "StateTransition: only bridgehub");
65: 		        _;
66: 		    }
```
[[63-66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L63-L66)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

134: 		    modifier onlyNextVersion(uint8 _version) {
135: 		        // The version should be incremented by 1. Otherwise, the governor risks disabling
136: 		        // future reinitialization of the token by providing too large a version.
137: 		        require(_version == _getInitializedVersion() + 1, "v");
138: 		        _;
139: 		    }
```
[[134-139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L134-L139)]

</details>

---

### [G-35] `private` functions only called once can be inlined to save gas

Consider removing the following private functions, and put the logic directly where they are called, as they are called only once.

*There are 15 instances of this issue.*


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

118: 		    function _encodeHashEIP712Transaction(Transaction calldata _transaction) private view returns (bytes32) {

147: 		    function _encodeHashLegacyTransaction(Transaction calldata _transaction) private view returns (bytes32) {

219: 		    function _encodeHashEIP2930Transaction(Transaction calldata _transaction) private view returns (bytes32) {

289: 		    function _encodeHashEIP1559Transaction(Transaction calldata _transaction) private view returns (bytes32) {
```
[[118](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L118), [147](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L147), [219](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L219), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L289)]



```solidity
File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

46: 		    function _initializeReentrancyGuard() private {
```
[[46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L46)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

92: 		    function _setL2DefaultAccountBytecodeHash(bytes32 _l2DefaultAccountBytecodeHash) private {

109: 		    function _setL2BootloaderBytecodeHash(bytes32 _l2BootloaderBytecodeHash) private {

126: 		    function _setVerifier(IVerifier _newVerifier) private {

142: 		    function _setVerifierParams(VerifierParams calldata _newVerifierParams) private {

222: 		    function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure {
```
[[92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L92), [109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L109), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L126), [142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L142), [222](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L222)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

126: 		    function _addFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {

149: 		    function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {

172: 		    function _removeFunctions(address _facet, bytes4[] memory _selectors) private {

257: 		    function _removeFacet(address _facet) private {

278: 		    function _initializeDiamondCut(address _init, bytes memory _calldata) private {
```
[[126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L126), [149](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L149), [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L172), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L257), [278](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L278)]


---

### [G-36] `abi.encode()` is less efficient than `abi.encodepacked()` for non-address arguments

Consider refactoring the code by using `abi.encodepacked` instead of `abi.encode`, as the former is cheaper when used with non-address arguments.

*There are 32 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

106: 		        chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

122: 		        chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

164: 		        chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

212: 		            reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));

226: 		                    abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])

243: 		            reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));

260: 		                abi.encode(
261: 		                    reconstructedChainedL1BytecodesRevealDataHash,
262: 		                    Utils.hashL2Bytecode(
263: 		                        _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
264: 		                    )
265: 		                )
```
[[106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L106), [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L122), [164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L164), [212](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L212), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L226), [243](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L243), [260-265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L260-L265)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

159: 		            hash = keccak256(abi.encode(_block));

227: 		        return keccak256(abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash));

403: 		        currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));
```
[[159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L159), [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L227), [403](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L403)]



```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

120: 		            abi.encode(
121: 		                EIP712_TRANSACTION_TYPE_HASH,
122: 		                _transaction.txType,
123: 		                _transaction.from,
124: 		                _transaction.to,
125: 		                _transaction.gasLimit,
126: 		                _transaction.gasPerPubdataByteLimit,
127: 		                _transaction.maxFeePerGas,
128: 		                _transaction.maxPriorityFeePerGas,
129: 		                _transaction.paymaster,
130: 		                _transaction.nonce,
131: 		                _transaction.value,
132: 		                EfficientCall.keccak(_transaction.data),
133: 		                keccak256(abi.encodePacked(_transaction.factoryDeps)),
134: 		                EfficientCall.keccak(_transaction.paymasterInput)
135: 		            )

139: 		            abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
```
[[120-135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L120-L135), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

76: 		        bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
```
[[76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

210: 		        bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));

258: 		            bytes memory decimals = abi.encode(uint8(18));

259: 		            return abi.encode(name, symbol, decimals); // when depositing eth to a non-eth based chain it is an ERC20

265: 		        return abi.encode(data1, data2, data3);

341: 		                bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));

598: 		        bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
```
[[210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L210), [258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L258), [259](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L259), [265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L265), [341](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L341), [598](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L598)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

205: 		        return keccak256(abi.encode(_operation));
```
[[205](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L205)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

100: 		        storedBatchZero = keccak256(abi.encode(batchZero));

102: 		        initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

138: 		        initialCutHash = keccak256(abi.encode(_diamondCut));

147: 		        upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

156: 		        upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
```
[[100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100), [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138), [147](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L147), [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L156)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

192: 		        bytes memory encodedTransaction = abi.encode(_l2ProtocolUpgradeTx);
```
[[192](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L192)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

104: 		        bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
```
[[104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

313: 		            concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));

512: 		        return keccak256(abi.encode(passThroughDataHash, metadataHash, auxiliaryOutputHash));

588: 		        return keccak256(abi.encode(_storedBatchInfo));

680: 		        (bool success, bytes memory data) = s.blobVersionedHashRetriever.staticcall(abi.encode(_index));
```
[[313](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313), [512](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L512), [588](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L588), [680](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L680)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

323: 		        bytes memory transactionEncoding = abi.encode(transaction);
```
[[323](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L323)]

</details>

---

### [G-37] Boolean comparison with boolean literals is unnecessary

These comparisons should be avoided, as they are implicit. Considering refactoring by using following approach instead:

`if (x == true) -> if (x), if (x == false) => if (!x)`

*There is 1 instance of this issue.*


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

68: 		        require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
```
[[68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68)]


---

### [G-38] Unused named return variables without optimizer waste gas

Consider changing the variable to be an unnamed one, since the variable is never assigned, nor is it returned by name. If the optimizer is not turned on, leaving the code as it is will also waste gas for the stack variable.

*There are 3 instances of this issue.*


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

// @audit bytes32 txHash
44: 		    function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {
```
[[44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L44)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

// @audit AccountInfo memory info
34: 		    function getAccountInfo(address _address) external view returns (AccountInfo memory info) {
```
[[34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L34)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

// @audit uint256 chainId
121: 		    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
```
[[121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L121)]


---

### [G-39] Using `this.<fn>()` wastes gas

Calling an external function internally, through the use of `this` wastes the gas overhead of calling an external function (**100 gas**). Instead, change the function from `external` to `public`, and remove the `this`

*There are 4 instances of this issue.*


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

254: 		            this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
```
[[254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L254)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

75: 		        try this.decodeString(nameBytes) returns (string memory nameString) {

81: 		        try this.decodeString(symbolBytes) returns (string memory symbolString) {

93: 		        try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {
```
[[75](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L75), [81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L81), [93](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L93)]


---

### [G-40] Consider pre-calculating the address of `address(this)` to save gas

Use Foundry's [`script.sol`](https://book.getfoundry.sh/reference/forge-std/compute-create-address) or Solady's [`LibRlp.sol`](https://github.com/Vectorized/solady/blob/main/src/utils/LibRLP.sol) to save the value in a constant, which will avoid having to spend gas to push the value on the stack every time it's used.

*There are 21 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

29: 		        require(msg.sender == address(this), "Callable only by self");

333: 		                BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo(address(this), _newAddress, value);
```
[[29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L29), [333](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L333)]



```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

47: 		        if (codeAddress != address(this)) {

100: 		        require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

188: 		        return recoveredAddress == address(this) && recoveredAddress != address(0);
```
[[47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L47), [100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L100), [188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L188)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

129: 		            sender: address(this),
```
[[129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L129)]



```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

106: 		            balance[address(this)] -= amount;
```
[[106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L106)]



```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

60: 		        require(to != address(this), "MsgValueSimulator calls itself");
```
[[60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L60)]



```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

377: 		            uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);
```
[[377](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

65: 		        uint256 amount = IERC20(_token).balanceOf(address(this));
```
[[65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

118: 		            uint256 balanceBefore = address(this).balance;

120: 		            uint256 balanceAfter = address(this).balance;

127: 		            uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

131: 		            uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

174: 		        uint256 balanceBefore = _token.balanceOf(address(this));

175: 		        _token.safeTransferFrom(_from, address(this), _amount);

176: 		        uint256 balanceAfter = _token.balanceOf(address(this));
```
[[118](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118), [120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127), [131](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L174), [175](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175), [176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

59: 		        require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
```
[[59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L59)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

265: 		            bytes32(uint256(uint160(address(this)))),
```
[[265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L265)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

153: 		            L2ContractHelper.computeCreate2Address(address(this), salt, l2TokenProxyBytecodeHash, constructorInputHash);
```
[[153](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L153)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

41: 		        uint256 amount = address(this).balance;
```
[[41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41)]

</details>

---

### [G-41] Consider using Solady's `FixedPointMathLib`

Saves gas, and works to avoid unnecessary [overflows](https://github.com/Vectorized/solady/blob/6cce088e69d6e46671f2f622318102bd5db77a65/src/utils/FixedPointMathLib.sol#L267).

*There are 3 instances of this issue.*


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

51: 		        return KECCAK_ROUND_GAS_COST * (_length / KECCAK_ROUND_NUMBER_OF_BYTES + 1);

62: 		        return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1);
```
[[51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L51), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L62)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

159: 		        uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
160: 		            s.baseTokenGasPriceMultiplierDenominator;
```
[[159-160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L159-L160)]


---

### [G-42] Reduce deployment costs by tweaking contracts' metadata

When solidity generates the bytecode for the smart contract to be deployed, it appends metadata about the compilation at the end of the bytecode.

By default, the solidity compiler appends metadata at the end of the “actual” initcode, which gets stored to the blockchain when the constructor finishes executing.

Consider tweaking the metadata to avoid this unnecessary allocation. A full guide can be found [here](https://www.rareskills.io/post/solidity-metadata).

*There are 104 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

22: 		contract AccountCodeStorage is IAccountCodeStorage {
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L22)]



```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

16: 		contract BootloaderUtilities is IBootloaderUtilities {
```
[[16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L16)]



```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

14: 		contract ComplexUpgrader is IComplexUpgrader {
```
[[14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L14)]



```solidity
File: code/system-contracts/contracts/Compressor.sol

22: 		contract Compressor is ICompressor, ISystemContract {
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L22)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

23: 		contract ContractDeployer is IContractDeployer, ISystemContract {
```
[[23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L23)]



```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

19: 		contract DefaultAccount is IAccount {
```
[[19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L19)]



```solidity
File: code/system-contracts/contracts/EmptyContract.sol

10: 		contract EmptyContract {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/EmptyContract.sol#L10)]



```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

15: 		contract GasBoundCaller {
```
[[15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L15)]



```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

18: 		contract ImmutableSimulator is IImmutableSimulator {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L18)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

18: 		contract KnownCodesStorage is IKnownCodesStorage, ISystemContract {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L18)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

25: 		contract L1Messenger is IL1Messenger, ISystemContract {
```
[[25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L25)]



```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

18: 		contract L2BaseToken is IBaseToken, ISystemContract {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L18)]



```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

19: 		contract MsgValueSimulator is ISystemContract {
```
[[19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L19)]



```solidity
File: code/system-contracts/contracts/NonceHolder.sol

27: 		contract NonceHolder is INonceHolder, ISystemContract {
```
[[27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L27)]



```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

16: 		contract PubdataChunkPublisher is IPubdataChunkPublisher, ISystemContract {
```
[[16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L16)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

17: 		contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract {
```
[[17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L17)]



```solidity
File: code/contracts/zksync/contracts/ForceDeployUpgrader.sol

10: 		contract ForceDeployUpgrader {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L10)]



```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

18: 		interface IL2Messenger {

30: 		interface IContractDeployer {

61: 		interface IBaseToken {

83: 		library L2ContractHelper {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L18), [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L30), [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L61), [83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L83)]



```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

26: 		library Utils {

36: 		library SystemContractsCaller {
```
[[26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L26), [36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L36)]



```solidity
File: code/system-contracts/contracts/interfaces/IAccount.sol

9: 		interface IAccount {
```
[[9](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IAccount.sol#L9)]



```solidity
File: code/system-contracts/contracts/interfaces/IAccountCodeStorage.sol

5: 		interface IAccountCodeStorage {
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IAccountCodeStorage.sol#L5)]



```solidity
File: code/system-contracts/contracts/interfaces/IBaseToken.sol

5: 		interface IBaseToken {
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IBaseToken.sol#L5)]



```solidity
File: code/system-contracts/contracts/interfaces/IBootloaderUtilities.sol

7: 		interface IBootloaderUtilities {
```
[[7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IBootloaderUtilities.sol#L7)]



```solidity
File: code/system-contracts/contracts/interfaces/IComplexUpgrader.sol

10: 		interface IComplexUpgrader {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IComplexUpgrader.sol#L10)]



```solidity
File: code/system-contracts/contracts/interfaces/ICompressor.sol

18: 		interface ICompressor {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ICompressor.sol#L18)]



```solidity
File: code/system-contracts/contracts/interfaces/IContractDeployer.sol

5: 		interface IContractDeployer {
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IContractDeployer.sol#L5)]



```solidity
File: code/system-contracts/contracts/interfaces/IImmutableSimulator.sol

10: 		interface IImmutableSimulator {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IImmutableSimulator.sol#L10)]



```solidity
File: code/system-contracts/contracts/interfaces/IKnownCodesStorage.sol

11: 		interface IKnownCodesStorage {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IKnownCodesStorage.sol#L11)]



```solidity
File: code/system-contracts/contracts/interfaces/IL1Messenger.sol

40: 		interface IL1Messenger {
```
[[40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IL1Messenger.sol#L40)]



```solidity
File: code/system-contracts/contracts/interfaces/IL2StandardToken.sol

5: 		interface IL2StandardToken {
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IL2StandardToken.sol#L5)]



```solidity
File: code/system-contracts/contracts/interfaces/IMailbox.sol

5: 		interface IMailbox {
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IMailbox.sol#L5)]



```solidity
File: code/system-contracts/contracts/interfaces/INonceHolder.sol

13: 		interface INonceHolder {
```
[[13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/INonceHolder.sol#L13)]



```solidity
File: code/system-contracts/contracts/interfaces/IPaymaster.sol

14: 		interface IPaymaster {
```
[[14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPaymaster.sol#L14)]



```solidity
File: code/system-contracts/contracts/interfaces/IPaymasterFlow.sol

12: 		interface IPaymasterFlow {
```
[[12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPaymasterFlow.sol#L12)]



```solidity
File: code/system-contracts/contracts/interfaces/IPubdataChunkPublisher.sol

9: 		interface IPubdataChunkPublisher {
```
[[9](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPubdataChunkPublisher.sol#L9)]



```solidity
File: code/system-contracts/contracts/interfaces/ISystemContext.sol

11: 		interface ISystemContext {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L11)]



```solidity
File: code/system-contracts/contracts/interfaces/ISystemContextDeprecated.sol

10: 		interface ISystemContextDeprecated {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContextDeprecated.sol#L10)]



```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

17: 		abstract contract ISystemContract {
```
[[17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L17)]



```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

32: 		library EfficientCall {
```
[[32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L32)]



```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

10: 		library RLPEncoder {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L10)]



```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

41: 		library SystemContractHelper {
```
[[41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L41)]



```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

68: 		library SystemContractsCaller {
```
[[68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L68)]



```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

78: 		library TransactionHelper {
```
[[78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L78)]



```solidity
File: code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol

18: 		library UnsafeBytesCalldata {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L18)]



```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

11: 		library Utils {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L11)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

19: 		contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {
```
[[19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L19)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

30: 		contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {
```
[[30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L30)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

16: 		contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
```
[[16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L16)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol

42: 		interface IBridgehub {
```
[[42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L42)]



```solidity
File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

25: 		abstract contract ReentrancyGuard {
```
[[25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L25)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

20: 		contract Governance is IGovernance, Ownable2Step {
```
[[20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L20)]



```solidity
File: code/contracts/ethereum/contracts/governance/IGovernance.sol

8: 		interface IGovernance {
```
[[8](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/IGovernance.sol#L8)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

26: 		interface IStateTransitionManager {
```
[[26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L26)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

25: 		contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {
```
[[25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L25)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

22: 		contract ValidatorTimelock is IExecutor, Ownable2Step {
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L22)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

44: 		abstract contract BaseZkSyncUpgrade is ZkSyncStateTransitionBase {
```
[[44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L44)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

17: 		abstract contract BaseZkSyncUpgradeGenesis is BaseZkSyncUpgrade {
```
[[17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L17)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

10: 		contract DefaultUpgrade is BaseZkSyncUpgrade {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L10)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

11: 		contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L11)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol

7: 		interface IDefaultUpgrade {
```
[[7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L7)]



```solidity
File: code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

21: 		library AddressAliasHelper {
```
[[21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L21)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

23: 		contract L2SharedBridge is IL2SharedBridge, Initializable {
```
[[23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L23)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

15: 		contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {
```
[[15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L15)]



```solidity
File: code/contracts/zksync/contracts/interfaces/IPaymaster.sol

14: 		interface IPaymaster {
```
[[14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L14)]



```solidity
File: code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol

13: 		interface IPaymasterFlow {
```
[[13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L13)]



```solidity
File: code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol

21: 		library AddressAliasHelper {
```
[[21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L21)]



```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

11: 		interface IL1ERC20Bridge {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11)]



```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

12: 		interface IL1SharedBridge {
```
[[12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L12)]



```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol

6: 		interface IL2Bridge {
```
[[6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L6)]



```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol

4: 		interface IWETH9 {
```
[[4](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L4)]



```solidity
File: code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol

9: 		interface IL2ContractDeployer {
```
[[9](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L9)]



```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

10: 		library L2ContractHelper {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L10)]



```solidity
File: code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol

10: 		library UncheckedMath {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L10)]



```solidity
File: code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol

18: 		library UnsafeBytes {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L18)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

17: 		contract DiamondInit is ZkSyncStateTransitionBase, IDiamondInit {
```
[[17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L17)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

10: 		contract DiamondProxy {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L10)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol

13: 		interface IAdmin is IZkSyncStateTransitionBase {
```
[[13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L13)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol

61: 		interface IDiamondInit {
```
[[61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L61)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

73: 		interface IExecutor is IZkSyncStateTransitionBase {
```
[[73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L73)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol

13: 		interface IGetters is IZkSyncStateTransitionBase {
```
[[13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L13)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol

11: 		interface ILegacyGetters is IZkSyncStateTransitionBase {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L11)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

11: 		interface IMailbox is IZkSyncStateTransitionBase {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L11)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol

15: 		interface IVerifier {
```
[[15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L15)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol

15: 		interface IZkSyncStateTransition is IAdmin, IExecutor, IGetters, IMailbox {
```
[[15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L15)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol

7: 		interface IZkSyncStateTransitionBase {
```
[[7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L7)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol

4: 		interface ISystemContext {
```
[[4](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L4)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

11: 		library Diamond {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L11)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

8: 		library LibMap {
```
[[8](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L8)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

9: 		library Merkle {
```
[[9](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L9)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

20: 		library PriorityQueue {
```
[[20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L20)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

13: 		library TransactionValidator {
```
[[13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L13)]



```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol

8: 		interface IL1ERC20Bridge {
```
[[8](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L8)]



```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol

8: 		interface IL1SharedBridge {
```
[[8](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L8)]



```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol

6: 		interface IL2SharedBridge {
```
[[6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L6)]



```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol

5: 		interface IL2StandardToken {
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L5)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

18: 		contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L18)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

22: 		contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L22)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

20: 		contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {
```
[[20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L20)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

30: 		contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {
```
[[30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L30)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

11: 		contract ZkSyncStateTransitionBase is ReentrancyGuard {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L11)]

</details>

---

### [G-43] Emitting constants wastes gas

Every event parameter costs `Glogdata` (**8 gas**) per byte. You can avoid this extra cost, in cases where you're emitting a constant, by creating a second version of the event, which doesn't have the parameter (and have users look to the contract's variables for its value instead), and using the new event in the cases shown below.

*There is 1 instance of this issue.*


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

// @audit 0
50: 		        emit ChangeMinDelay(0, _minDelay);
```
[[50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L50)]


---

### [G-44] Update OpenZeppelin dependency to save gas

Every release contains new gas optimizations, use the latest version to take advantage of this.

*There are 22 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

5: 		import "../openzeppelin/token/ERC20/IERC20.sol";

6: 		import "../openzeppelin/token/ERC20/utils/SafeERC20.sol";
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L5), [6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L6)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

5: 		import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";

6: 		import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L5), [6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L6)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

5: 		import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";

6: 		import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";

8: 		import {IERC20Metadata} from "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";

9: 		import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";

10: 		import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L5), [6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L6), [8](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L8), [9](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L9), [10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L10)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

5: 		import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L5)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

5: 		import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L5)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

16: 		import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```
[[16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L16)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

5: 		import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L5)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

5: 		import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";

6: 		import {BeaconProxy} from "@openzeppelin/contracts/proxy/beacon/BeaconProxy.sol";

7: 		import {UpgradeableBeacon} from "@openzeppelin/contracts/proxy/beacon/UpgradeableBeacon.sol";
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L5), [6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L6), [7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L7)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

5: 		import {ERC20PermitUpgradeable} from "@openzeppelin/contracts-upgradeable/token/ERC20/extensions/draft-ERC20PermitUpgradeable.sol";

6: 		import {UpgradeableBeacon} from "@openzeppelin/contracts/proxy/beacon/UpgradeableBeacon.sol";

7: 		import {ERC1967Upgrade} from "@openzeppelin/contracts/proxy/ERC1967/ERC1967Upgrade.sol";
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L5), [6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L6), [7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L7)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

5: 		import {SafeCast} from "@openzeppelin/contracts/utils/math/SafeCast.sol";
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L5)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

5: 		import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L5)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

5: 		import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L5)]

</details>

---

### [G-45] Function names can be optimized

Function that are `public`/`external` and `public` state variable names can be optimized to save gas.

Method IDs that have two leading zero bytes can save **128 gas** each during deployment, and renaming functions to have lower method IDs will save **22 gas** per call, per sorted position shifted. [Reference](https://blog.emn178.cc/en/post/solidity-gas-optimization-function-name/)

*There are 80 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

22: 		contract AccountCodeStorage is IAccountCodeStorage {
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L22)]



```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

16: 		contract BootloaderUtilities is IBootloaderUtilities {
```
[[16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L16)]



```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

14: 		contract ComplexUpgrader is IComplexUpgrader {
```
[[14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L14)]



```solidity
File: code/system-contracts/contracts/Compressor.sol

22: 		contract Compressor is ICompressor, ISystemContract {
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L22)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

23: 		contract ContractDeployer is IContractDeployer, ISystemContract {
```
[[23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L23)]



```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

19: 		contract DefaultAccount is IAccount {
```
[[19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L19)]



```solidity
File: code/system-contracts/contracts/EmptyContract.sol

10: 		contract EmptyContract {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/EmptyContract.sol#L10)]



```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

15: 		contract GasBoundCaller {
```
[[15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L15)]



```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

18: 		contract ImmutableSimulator is IImmutableSimulator {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L18)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

18: 		contract KnownCodesStorage is IKnownCodesStorage, ISystemContract {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L18)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

25: 		contract L1Messenger is IL1Messenger, ISystemContract {
```
[[25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L25)]



```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

18: 		contract L2BaseToken is IBaseToken, ISystemContract {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L18)]



```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

19: 		contract MsgValueSimulator is ISystemContract {
```
[[19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L19)]



```solidity
File: code/system-contracts/contracts/NonceHolder.sol

27: 		contract NonceHolder is INonceHolder, ISystemContract {
```
[[27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L27)]



```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

16: 		contract PubdataChunkPublisher is IPubdataChunkPublisher, ISystemContract {
```
[[16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L16)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

17: 		contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract {
```
[[17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L17)]



```solidity
File: code/contracts/zksync/contracts/ForceDeployUpgrader.sol

10: 		contract ForceDeployUpgrader {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L10)]



```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

18: 		interface IL2Messenger {

30: 		interface IContractDeployer {

61: 		interface IBaseToken {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L18), [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L30), [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L61)]



```solidity
File: code/system-contracts/contracts/interfaces/IAccount.sol

9: 		interface IAccount {
```
[[9](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IAccount.sol#L9)]



```solidity
File: code/system-contracts/contracts/interfaces/IAccountCodeStorage.sol

5: 		interface IAccountCodeStorage {
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IAccountCodeStorage.sol#L5)]



```solidity
File: code/system-contracts/contracts/interfaces/IBaseToken.sol

5: 		interface IBaseToken {
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IBaseToken.sol#L5)]



```solidity
File: code/system-contracts/contracts/interfaces/IBootloaderUtilities.sol

7: 		interface IBootloaderUtilities {
```
[[7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IBootloaderUtilities.sol#L7)]



```solidity
File: code/system-contracts/contracts/interfaces/IComplexUpgrader.sol

10: 		interface IComplexUpgrader {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IComplexUpgrader.sol#L10)]



```solidity
File: code/system-contracts/contracts/interfaces/ICompressor.sol

18: 		interface ICompressor {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ICompressor.sol#L18)]



```solidity
File: code/system-contracts/contracts/interfaces/IContractDeployer.sol

5: 		interface IContractDeployer {
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IContractDeployer.sol#L5)]



```solidity
File: code/system-contracts/contracts/interfaces/IImmutableSimulator.sol

10: 		interface IImmutableSimulator {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IImmutableSimulator.sol#L10)]



```solidity
File: code/system-contracts/contracts/interfaces/IKnownCodesStorage.sol

11: 		interface IKnownCodesStorage {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IKnownCodesStorage.sol#L11)]



```solidity
File: code/system-contracts/contracts/interfaces/IL1Messenger.sol

40: 		interface IL1Messenger {
```
[[40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IL1Messenger.sol#L40)]



```solidity
File: code/system-contracts/contracts/interfaces/IL2StandardToken.sol

5: 		interface IL2StandardToken {
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IL2StandardToken.sol#L5)]



```solidity
File: code/system-contracts/contracts/interfaces/IMailbox.sol

5: 		interface IMailbox {
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IMailbox.sol#L5)]



```solidity
File: code/system-contracts/contracts/interfaces/INonceHolder.sol

13: 		interface INonceHolder {
```
[[13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/INonceHolder.sol#L13)]



```solidity
File: code/system-contracts/contracts/interfaces/IPaymaster.sol

14: 		interface IPaymaster {
```
[[14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPaymaster.sol#L14)]



```solidity
File: code/system-contracts/contracts/interfaces/IPaymasterFlow.sol

12: 		interface IPaymasterFlow {
```
[[12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPaymasterFlow.sol#L12)]



```solidity
File: code/system-contracts/contracts/interfaces/IPubdataChunkPublisher.sol

9: 		interface IPubdataChunkPublisher {
```
[[9](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPubdataChunkPublisher.sol#L9)]



```solidity
File: code/system-contracts/contracts/interfaces/ISystemContext.sol

11: 		interface ISystemContext {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L11)]



```solidity
File: code/system-contracts/contracts/interfaces/ISystemContextDeprecated.sol

10: 		interface ISystemContextDeprecated {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContextDeprecated.sol#L10)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

19: 		contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {
```
[[19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L19)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

30: 		contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {
```
[[30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L30)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

16: 		contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
```
[[16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L16)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol

42: 		interface IBridgehub {
```
[[42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L42)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

20: 		contract Governance is IGovernance, Ownable2Step {
```
[[20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L20)]



```solidity
File: code/contracts/ethereum/contracts/governance/IGovernance.sol

8: 		interface IGovernance {
```
[[8](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/IGovernance.sol#L8)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

26: 		interface IStateTransitionManager {
```
[[26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L26)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

25: 		contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {
```
[[25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L25)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

22: 		contract ValidatorTimelock is IExecutor, Ownable2Step {
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L22)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

44: 		abstract contract BaseZkSyncUpgrade is ZkSyncStateTransitionBase {
```
[[44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L44)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

17: 		abstract contract BaseZkSyncUpgradeGenesis is BaseZkSyncUpgrade {
```
[[17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L17)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

10: 		contract DefaultUpgrade is BaseZkSyncUpgrade {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L10)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

11: 		contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L11)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol

7: 		interface IDefaultUpgrade {
```
[[7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L7)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

23: 		contract L2SharedBridge is IL2SharedBridge, Initializable {
```
[[23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L23)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

15: 		contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {
```
[[15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L15)]



```solidity
File: code/contracts/zksync/contracts/interfaces/IPaymaster.sol

14: 		interface IPaymaster {
```
[[14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L14)]



```solidity
File: code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol

13: 		interface IPaymasterFlow {
```
[[13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L13)]



```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

11: 		interface IL1ERC20Bridge {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11)]



```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

12: 		interface IL1SharedBridge {
```
[[12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L12)]



```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol

6: 		interface IL2Bridge {
```
[[6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L6)]



```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol

4: 		interface IWETH9 {
```
[[4](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L4)]



```solidity
File: code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol

9: 		interface IL2ContractDeployer {
```
[[9](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L9)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

17: 		contract DiamondInit is ZkSyncStateTransitionBase, IDiamondInit {
```
[[17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L17)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

10: 		contract DiamondProxy {
```
[[10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L10)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol

13: 		interface IAdmin is IZkSyncStateTransitionBase {
```
[[13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L13)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol

61: 		interface IDiamondInit {
```
[[61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L61)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

73: 		interface IExecutor is IZkSyncStateTransitionBase {
```
[[73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L73)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol

13: 		interface IGetters is IZkSyncStateTransitionBase {
```
[[13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L13)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol

11: 		interface ILegacyGetters is IZkSyncStateTransitionBase {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L11)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

11: 		interface IMailbox is IZkSyncStateTransitionBase {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L11)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol

15: 		interface IVerifier {
```
[[15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L15)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol

7: 		interface IZkSyncStateTransitionBase {
```
[[7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L7)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol

4: 		interface ISystemContext {
```
[[4](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L4)]



```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol

8: 		interface IL1ERC20Bridge {
```
[[8](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L8)]



```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol

8: 		interface IL1SharedBridge {
```
[[8](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L8)]



```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol

6: 		interface IL2SharedBridge {
```
[[6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L6)]



```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol

5: 		interface IL2StandardToken {
```
[[5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L5)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

18: 		contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {
```
[[18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L18)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

22: 		contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L22)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

20: 		contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {
```
[[20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L20)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

30: 		contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {
```
[[30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L30)]

</details>

---

### [G-46] Using `delete` instead of setting mapping/struct to 0 saves gas

Avoid an assignment by deleting the value instead of setting it to zero, as it's [cheaper](https://gist.github.com/DadeKuma/ea874815202fc77e9d81f81a047c1e5e).

*There are 3 instances of this issue.*


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

330: 		        numberOfLogsToProcess = 0;
```
[[330](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L330)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

487: 		        txNumberInBlock = 0;
```
[[487](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L487)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

276: 		                baseTokenMsgValue = 0;
```
[[276](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L276)]


---

### [G-47] Expression `""` is cheaper than `new bytes(0)`

Saves 238 gas per instance

*There are 8 instances of this issue.*


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

196: 		            signature: new bytes(0),

198: 		            paymasterInput: new bytes(0),

199: 		            reservedDynamic: new bytes(0)

213: 		            l1ContractsUpgradeCalldata: new bytes(0),

214: 		            postUpgradeCalldata: new bytes(0),
```
[[196](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L196), [198](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L198), [199](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L199), [213](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L213), [214](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L214)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

308: 		            signature: new bytes(0),

310: 		            paymasterInput: new bytes(0),

311: 		            reservedDynamic: new bytes(0)
```
[[308](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L308), [310](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L310), [311](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L311)]


---

### [G-48] Using `bool` for storage incurs overhead

Booleans are more expensive than `uint256` or any type that takes up a full word because each write operation emits an extra SLOAD to first read the slot's contents, replace the bits taken up by the boolean, and then write back.

This is the compiler's defense against contract upgrades and pointer aliasing, and it cannot be disabled. Use `uint256(0) and uint256(1)` for `true/false` to avoid a Gwarmaccess (**100 gas**) for the extra `SLOAD`.

*There are 6 instances of this issue.*


```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

27: 		    mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
28: 		        public isWithdrawalFinalized;
```
[[27-28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27-L28)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

57: 		    mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
58: 		        public isWithdrawalFinalized;

61: 		    mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;
```
[[57-58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57-L58), [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L61)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

21: 		    mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;

23: 		    mapping(address _token => bool) public tokenIsRegistered;
```
[[21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21), [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L23)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

50: 		    mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
[[50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50)]


---

### [G-49] Multiplication/division by two should use bit shifting

`X * 2` is equivalent to `X << 1` and `X / 2` is the same as `X >> 1`.

The `MUL` and `DIV` opcodes cost 5 gas, whereas `SHL` and `SHR` only cost 3 gas.

*There are 4 instances of this issue.*


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

97: 		                vInt += 8 + block.chainid * 2;
```
[[97](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L97)]



```solidity
File: code/system-contracts/contracts/Compressor.sol

57: 		                dictionary.length / 8 <= encodedData.length / 2,
```
[[57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L57)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

581: 		            blobAuxOutputWords[i * 2] = _blobHashes[i];

582: 		            blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
```
[[581](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L581), [582](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L582)]


---

### [G-50] `x += y` is more expensive than `x = x + y` for state variables

Not inlining costs 20 to 40 gas because of two extra JUMP instructions and additional stack operations needed for function calls.

*There are 3 instances of this issue.*


```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

65: 		        totalSupply += _amount;

107: 		            totalSupply -= amount;
```
[[65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L65), [107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L107)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

483: 		        txNumberInBlock += 1;
```
[[483](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L483)]


---

### [G-51] Use of `+=` is cheaper for mappings

Using `+=` for mappings saves 40 gas due to not having to recalculate the mapping's value's hash.

*There are 2 instances of this issue.*


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

122: 		            chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
123: 		                chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
124: 		                balanceAfter -
125: 		                balanceBefore;

133: 		            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
```
[[122-125](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L122-L125), [133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133)]


---

### [G-52] Mappings are cheaper to use than storage arrays

When using storage arrays, solidity adds an internal lookup of the array's length (a **Gcoldsload 2100 gas**) to ensure you don't read past the array's end.

You can avoid this lookup by using a mapping and storing the number of entries in a separate storage variable. In cases where you have sentinel values (e.g. 'zero' means invalid), you can avoid length checks.

*There is 1 instance of this issue.*


```solidity
File: code/system-contracts/contracts/SystemContext.sol

70: 		    bytes32[MINIBLOCK_HASHES_TO_STORE] internal l2BlockHash;
```
[[70](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L70)]


---

### [G-53] Bytes constants are more efficient than string constants

If a string can fit in 32 bytes is it better to use `bytes32` instead of `string`, as it is cheaper.

```solidity
// @audit avoid this
string constant stringVariable = "LessThan32Bytes";

// @audit as this is cheaper
bytes32 constant stringVariable = "LessThan32Bytes";
```

*There are 5 instances of this issue.*


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

26: 		    string public constant override getName = "ValidatorTimelock";
```
[[26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

20: 		    string public constant override getName = "AdminFacet";
```
[[20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

27: 		    string public constant override getName = "ExecutorFacet";
```
[[27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

25: 		    string public constant override getName = "GettersFacet";
```
[[25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

35: 		    string public constant override getName = "MailboxFacet";
```
[[35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35)]


---

### [G-54] Constructors can be marked `payable`

`payable` functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided.

A `constructor` can safely be marked as `payable`, since only the deployer would be able to pass funds, and the project itself would not pass any funds.

*There are 10 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

55: 		    constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
```
[[55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

90: 		    constructor(
```
[[90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

38: 		    constructor() reentrancyGuardInitializer {}
```
[[38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

41: 		    constructor(address _admin, address _securityCouncil, uint256 _minDelay) {
```
[[41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L41)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

58: 		    constructor(address _bridgehub) reentrancyGuardInitializer {
```
[[58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

55: 		    constructor(address _initialOwner, uint32 _executionDelay) {
```
[[55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

41: 		    constructor() {
```
[[41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L41)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

40: 		    constructor() {
```
[[40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L40)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

19: 		    constructor() reentrancyGuardInitializer {}
```
[[19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

11: 		    constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
```
[[11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11)]

</details>

---

### [G-55] Long revert strings

Considering refactoring the revert message to fit in 32 bytes to avoid using more than one memory slot.

*There are 104 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

26: 		        require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

37: 		        require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");

48: 		        require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");

57: 		        require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");
```
[[26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L26), [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L37), [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L48), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L57)]



```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

22: 		        require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L22)]



```solidity
File: code/system-contracts/contracts/Compressor.sol

51: 		            require(
52: 		                encodedData.length * 4 == _bytecode.length,
53: 		                "Encoded data length should be 4 times shorter than the original bytecode"
54: 		            );

56: 		            require(
57: 		                dictionary.length / 8 <= encodedData.length / 2,
58: 		                "Dictionary should have at most the same number of entries as the encoded data"
59: 		            );

63: 		                require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

68: 		                require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");

119: 		        require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");

156: 		        require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");

187: 		        require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");

230: 		                require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");

232: 		                require(
233: 		                    _initialValue + convertedValue == _finalValue,
234: 		                    "add: initial plus converted not equal to final"
235: 		                );

237: 		                require(
238: 		                    _initialValue - convertedValue == _finalValue,
239: 		                    "sub: initial minus converted not equal to final"
240: 		                );
```
[[51-54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L51-L54), [56-59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L56-L59), [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L63), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L68), [119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L119), [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L156), [187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L187), [230](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L230), [232-235](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L232-L235), [237-240](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L237-L240)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

77: 		        require(
78: 		            _nonceOrdering == AccountNonceOrdering.Arbitrary &&
79: 		                currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
80: 		            "It is only possible to change from sequential to arbitrary ordering"
81: 		        );

239: 		        require(
240: 		            msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
241: 		            "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
242: 		        );

251: 		        require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");

265: 		        require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

350: 		            require(value == 0, "The value must be zero if we do not call the constructor");
```
[[77-81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L77-L81), [239-242](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L239-L242), [251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L251), [265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L265), [350](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L350)]



```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

100: 		        require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

202: 		        require(success, "Failed to pay the fee to the operator");
```
[[100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L100), [202](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L202)]



```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

35: 		        require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
[[35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L35)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

76: 		        require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
```
[[76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L76)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

214: 		        require(
215: 		            reconstructedChainedLogsHash == chainedLogsHash,
216: 		            "reconstructedChainedLogsHash is not equal to chainedLogsHash"
217: 		        );

245: 		        require(
246: 		            reconstructedChainedMessagesHash == chainedMessagesHash,
247: 		            "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
248: 		        );

269: 		        require(
270: 		            reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
271: 		            "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
272: 		        );

279: 		        require(
280: 		            uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
281: 		                STATE_DIFF_COMPRESSION_VERSION_NUMBER,
282: 		            "state diff compression version mismatch"
283: 		        );

315: 		        require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");
```
[[214-217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L214-L217), [245-248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L245-L248), [269-272](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L269-L272), [279-283](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L279-L283), [315](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L315)]



```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

33: 		        require(
34: 		            msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
35: 		                msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
36: 		                msg.sender == BOOTLOADER_FORMAL_ADDRESS,
37: 		            "Only system contracts with special access can call this method"
38: 		        );
```
[[33-38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L33-L38)]



```solidity
File: code/system-contracts/contracts/NonceHolder.sol

66: 		        require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");

136: 		        require(
137: 		            msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
138: 		            "Only the contract deployer can increment the deployment nonce"
139: 		        );
```
[[66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L66), [136-139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L136-L139)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

242: 		        require(_isFirstInBatch, "Upgrade transaction must be first");

245: 		        require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

249: 		            require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");

287: 		            require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

351: 		            require(
352: 		                _l2BlockTimestamp >= currentBatchTimestamp,
353: 		                "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
354: 		            );

355: 		            require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

367: 		            require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");

368: 		            require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");

369: 		            require(
370: 		                _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
371: 		                "The previous hash of the same L2 block must be same"
372: 		            );

373: 		            require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");

385: 		            require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");

386: 		            require(
387: 		                _l2BlockTimestamp > currentL2BlockTimestamp,
388: 		                "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
389: 		            );

413: 		        require(currentBatchNumber > 0, "The current batch number must be greater than 0");

429: 		        require(
430: 		            _newTimestamp > currentBlockTimestamp,
431: 		            "The timestamp of the batch must be greater than the timestamp of the previous block"
432: 		        );

452: 		        require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
```
[[242](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L242), [245](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L245), [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L249), [287](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L287), [351-354](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L351-L354), [355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L355), [367](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L367), [368](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L368), [369-372](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L369-L372), [373](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L373), [385](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L385), [386-389](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L386-L389), [413](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L413), [429-432](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L429-L432), [452](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L452)]



```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

21: 		        require(
22: 		            SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
23: 		            "This method require system call flag"
24: 		        );

31: 		        require(
32: 		            SystemContractHelper.isSystemContract(msg.sender),
33: 		            "This method require the caller to be system contract"
34: 		        );
```
[[21-24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L21-L24), [31-34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L31-L34)]



```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

319: 		        require(index < 10, "There are only 10 accessible registers");
```
[[319](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319)]



```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

363: 		        require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");

367: 		            require(
368: 		                _transaction.paymasterInput.length >= 68,
369: 		                "The approvalBased paymaster input must be at least 68 bytes long"
370: 		            );
```
[[363](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L363), [367-370](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L367-L370)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

75: 		        require(
76: 		            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
77: 		            "L1SharedBridge: not bridgehub or era chain"
78: 		        );

155: 		            require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");

195: 		        require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

427: 		            require(!alreadyFinalized, "Withdrawal is already finalized 2");

564: 		        require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
```
[[75-78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75-L78), [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L155), [195](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195), [427](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L427), [564](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

83: 		        require(
84: 		            !stateTransitionManagerIsRegistered[_stateTransitionManager],
85: 		            "Bridgehub: state transition already registered"
86: 		        );

93: 		        require(
94: 		            stateTransitionManagerIsRegistered[_stateTransitionManager],
95: 		            "Bridgehub: state transition not registered yet"
96: 		        );

102: 		        require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

125: 		        require(
126: 		            stateTransitionManagerIsRegistered[_stateTransitionManager],
127: 		            "Bridgehub: state transition not registered"
128: 		        );

132: 		        require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

225: 		                require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");

300: 		        require(
301: 		            _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
302: 		            "Bridgehub: second bridge address too low"
303: 		        ); // to avoid calls to precompiles
```
[[83-86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83-L86), [93-96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L93-L96), [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102), [125-128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L125-L128), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132), [225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225), [300-303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L300-L303)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

59: 		        require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

65: 		        require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

71: 		        require(
72: 		            msg.sender == owner() || msg.sender == securityCouncil,
73: 		            "Only the owner and security council are allowed to call this function"
74: 		        );

172: 		        require(isOperationReady(id), "Operation must be ready before execution");

177: 		        require(isOperationReady(id), "Operation must be ready after execution");

191: 		        require(isOperationPending(id), "Operation must be pending before execution");

196: 		        require(isOperationPending(id), "Operation must be pending after execution");

216: 		        require(!isOperation(_id), "Operation with this proposal id already exists");

217: 		        require(_delay >= minDelay, "Proposed delay is less than minimum delay");

240: 		        require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");
```
[[59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L59), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L65), [71-74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L71-L74), [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L172), [177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L177), [191](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L191), [196](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L196), [216](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L216), [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L217), [240](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L240)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

256: 		        require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");
```
[[256](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L256)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62: 		        require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

68: 		        require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
```
[[62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

190: 		        require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");

205: 		        require(
206: 		            _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
207: 		            "The new protocol version should be included in the L2 system upgrade tx"
208: 		        );

238: 		        require(
239: 		            _newProtocolVersion > previousProtocolVersion,
240: 		            "New protocol version is not greater than the current one"
241: 		        );

242: 		        require(
243: 		            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
244: 		            "Too big protocol version difference"
245: 		        );

249: 		        require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

250: 		        require(
251: 		            s.l2SystemContractsUpgradeBatchNumber == 0,
252: 		            "The batch number of the previous upgrade has not been cleaned"
253: 		        );
```
[[190](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L190), [205-208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L205-L208), [238-241](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L238-L241), [242-245](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L242-L245), [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L249), [250-253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L250-L253)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

22: 		        require(
23: 		            // Genesis Upgrade difference: Note this is the only thing change > to >=
24: 		            _newProtocolVersion >= previousProtocolVersion,
25: 		            "New protocol version is not greater than the current one"
26: 		        );

27: 		        require(
28: 		            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
29: 		            "Too big protocol version difference"
30: 		        );

33: 		        require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

34: 		        require(
35: 		            s.l2SystemContractsUpgradeBatchNumber == 0,
36: 		            "The batch number of the previous upgrade has not been cleaned"
37: 		        );
```
[[22-26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22-L26), [27-30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L27-L30), [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33), [34-37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L34-L37)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

92: 		        require(msg.value == 0, "Value should be 0 for ERC20 bridge");
```
[[92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

90: 		        require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed

105: 		        require(
106: 		            cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107: 		            "StateTransition: cutHash mismatch"
108: 		        );

110: 		        require(
111: 		            s.protocolVersion == _oldProtocolVersion,
112: 		            "StateTransition: protocolVersion mismatch in STC when upgrading"
113: 		        );

116: 		        require(
117: 		            s.protocolVersion > _oldProtocolVersion,
118: 		            "StateTransition: protocolVersion mismatch in STC after upgrading"
119: 		        );
```
[[90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90), [105-108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L105-L108), [110-113](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L110-L113), [116-119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L116-L119)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

226: 		        require(
227: 		            IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
228: 		            "Executor facet: wrong protocol version"
229: 		        );

616: 		        require(success, "failed to call point evaluation precompile");
```
[[226-229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L226-L229), [616](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

39: 		        require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");

158: 		        require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

185: 		        require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");

206: 		        require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");
```
[[39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L185), [206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L206)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

22: 		        require(s.validators[msg.sender], "StateTransition Chain: not validator");

27: 		        require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

32: 		        require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

37: 		        require(
38: 		            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
39: 		            "StateTransition Chain: Only by admin or state transition manager"
40: 		        );

45: 		        require(
46: 		            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
47: 		            "StateTransition Chain: Only by validator or state transition manager"
48: 		        );

53: 		        require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32), [37-40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L37-L40), [45-48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45-L48), [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53)]

</details>

---

### [G-56] Splitting `require` statements that use `&&` saves gas

Using operator && on a single require costs more gas than using two require.

```solidity
//expensive
require(version == 1 && index == 2);

//cheaper
require(version == 1);
require(index == 2 == bytes1(0));
```

*There are 3 instances of this issue.*


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

77: 		        require(
78: 		            _nonceOrdering == AccountNonceOrdering.Arbitrary &&
79: 		                currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
80: 		            "It is only possible to change from sequential to arbitrary ordering"
81: 		        );
```
[[77-81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L77-L81)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

76: 		        require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
```
[[76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L76)]



```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

41: 		        require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash
```
[[41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L41)]


---

### [G-57] Nesting `if` statements that use `&&` saves gas

Using the `&&` operator on a single `if` [costs more gas](https://gist.github.com/DadeKuma/931ce6794a050201ec6544dbcc31316c) than using two nested `if`.

*There are 12 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

102: 		        if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {

132: 		            uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS &&
133: 		            codeHash != 0x00 &&
134: 		            !Utils.isContractConstructing(codeHash)
```
[[102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L102), [132-134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L132-L134)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

48: 		            _address > address(MAX_SYSTEM_CONTRACT_ADDRESS) &&
49: 		            ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getRawCodeHash(_address) == 0
```
[[48-49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L48-L49)]



```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

139: 		        if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) {
```
[[139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L139)]



```solidity
File: code/system-contracts/contracts/NonceHolder.sol

88: 		        if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {

169: 		        if (isUsed && !_shouldBeUsed) {

171: 		        } else if (!isUsed && _shouldBeUsed) {
```
[[88](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L88), [169](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L169), [171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L171)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

151: 		            _block >= currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block &&
152: 		            currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0

277: 		        if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {

360: 		        if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {
```
[[151-152](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L151-L152), [277](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L277), [360](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L360)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

148: 		            _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) &&
149: 		            _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) &&
150: 		            _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)
```
[[148-150](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L148-L150)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

361: 		        if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {
```
[[361](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L361)]

</details>

---

### [G-58] Counting down when iterating, saves gas

Counting down saves **6 gas** per loop, since checks for zero are more efficient than checks against any other value.

*There are 18 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

248: 		        for (uint256 i = 0; i < deploymentsLength; ++i) {

253: 		        for (uint256 i = 0; i < deploymentsLength; ++i) {
```
[[248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L248), [253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L253)]



```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

38: 		            for (uint256 i = 0; i < immutablesLength; ++i) {
```
[[38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L38)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

30: 		            for (uint256 i = 0; i < hashesLen; ++i) {
```
[[30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L30)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

206: 		        for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

218: 		        for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

224: 		            for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

236: 		        for (uint256 i = 0; i < numberOfMessages; ++i) {

254: 		        for (uint256 i = 0; i < numberOfBytecodes; ++i) {
```
[[206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L206), [218](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L218), [224](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L224), [236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L236), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L254)]



```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

36: 		        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[[36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

225: 		        for (uint256 i = 0; i < _calls.length; ++i) {
```
[[225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {

135: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {

185: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {

209: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```
[[116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185), [209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226: 		        for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
[[226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

580: 		        for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

667: 		        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[[580](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580), [667](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)]

</details>

---

### [G-59] `do-while` is cheaper than `for`-loops when the initial check can be skipped

Example:

```solidity
for (uint256 i; i < len; ++i){ ... } -> do { ...; ++i } while (i < len);
```

*There are 35 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/Compressor.sol

61: 		            for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {

127: 		        for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

159: 		        for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
```
[[61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L61), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L127), [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L159)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

248: 		        for (uint256 i = 0; i < deploymentsLength; ++i) {

253: 		        for (uint256 i = 0; i < deploymentsLength; ++i) {
```
[[248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L248), [253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L253)]



```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

38: 		            for (uint256 i = 0; i < immutablesLength; ++i) {
```
[[38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L38)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

30: 		            for (uint256 i = 0; i < hashesLen; ++i) {
```
[[30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L30)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

206: 		        for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

218: 		        for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

224: 		            for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

236: 		        for (uint256 i = 0; i < numberOfMessages; ++i) {

254: 		        for (uint256 i = 0; i < numberOfBytecodes; ++i) {
```
[[206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L206), [218](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L218), [224](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L224), [236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L236), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L254)]



```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

36: 		        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[[36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

225: 		        for (uint256 i = 0; i < _calls.length; ++i) {
```
[[225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {

135: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {

185: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {

209: 		            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```
[[116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185), [209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226: 		        for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
[[226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

101: 		        for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {

138: 		        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

158: 		        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

178: 		        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
```
[[101](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L138), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158), [178](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L178)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

29: 		        for (uint256 i; i < pathLength; i = i.uncheckedInc()) {
```
[[29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L29)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

142: 		        for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

257: 		        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

289: 		        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

311: 		        for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {

351: 		        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {

405: 		        for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {

580: 		        for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

636: 		        for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {

667: 		        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[[142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289), [311](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L311), [351](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351), [405](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L405), [580](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580), [636](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636), [667](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

208: 		        for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {
```
[[208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

356: 		        for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {
```
[[356](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356)]

</details>

---

### [G-60] Lack of `unchecked` in loops

Use `unchecked` to increment the loop variable as it can save gas:

```solidity
for(uint256 i; i < length;) {
	unchecked{
		++i;
	}
}
```

*There are 12 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

248: 		        for (uint256 i = 0; i < deploymentsLength; ++i) {

253: 		        for (uint256 i = 0; i < deploymentsLength; ++i) {
```
[[248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L248), [253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L253)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

206: 		        for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

218: 		        for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

224: 		            for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

236: 		        for (uint256 i = 0; i < numberOfMessages; ++i) {

254: 		        for (uint256 i = 0; i < numberOfBytecodes; ++i) {
```
[[206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L206), [218](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L218), [224](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L224), [236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L236), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L254)]



```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

36: 		        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[[36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

225: 		        for (uint256 i = 0; i < _calls.length; ++i) {
```
[[225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226: 		        for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
[[226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

580: 		        for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

667: 		        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[[580](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580), [667](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)]

</details>

---

### [G-61] Pre-compute hashes

Consider pre-compute hashes (e.g. `keccak256("transfer(address,uint256)")` -> `0xa9059cbb`) instead of calculating them inside the contract.

*There are 2 instances of this issue.*


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

// @audit keccak256("zkSync")
139: 		            abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

// @audit keccak256("2")
139: 		            abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
```
[[139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139)]


---

### [G-62] `uint` comparison with zero can be cheaper

Checking for `!= 0` is cheaper than `> 0` for unsigned integers.

*There are 24 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

102: 		        if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {
```
[[102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L102)]



```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

24: 		        require(_delegateTo.code.length > 0, "Delegatee is an EOA");
```
[[24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L24)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

303: 		        require(knownCodeMarker > 0, "The code hash is not known");

332: 		            if (value > 0) {

339: 		            if (value > 0) {
```
[[303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L303), [332](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L332), [339](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L339)]



```solidity
File: code/system-contracts/contracts/NonceHolder.sol

156: 		        return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);
```
[[156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L156)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

152: 		            currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0

245: 		        require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

287: 		            require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

355: 		            require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

413: 		        require(currentBatchNumber > 0, "The current batch number must be greater than 0");
```
[[152](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L152), [245](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L245), [287](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L287), [355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L355), [413](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L413)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

129: 		            require(amount > 0, "ShB: 0 amount to transfer");

327: 		        require(_amount > 0, "y1");
```
[[129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129), [327](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

329: 		        } else if (_refundRecipient.code.length > 0) {
```
[[329](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L329)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

124: 		        require(_amount > 0, "Amount cannot be zero");
```
[[124](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L124)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

107: 		            require(selectors.length > 0, "B"); // no functions for diamond cut

132: 		        require(_facet.code.length > 0, "G");

155: 		        require(_facet.code.length > 0, "K");
```
[[107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132), [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L155)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

24: 		        require(pathLength > 0, "xc");
```
[[24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

429: 		        if (_proof.serializedProof.length > 0) {

593: 		        return (_bitMap & (1 << _index)) > 0;

631: 		        require(_pubdataCommitments.length > 0, "pl");
```
[[429](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L429), [593](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L593), [631](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

158: 		        require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

277: 		        if (refundRecipient.code.length > 0) {
```
[[158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158), [277](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L277)]

</details>

---

### [G-63] Use assembly to check for `address(0)`

[A simple zero address check](https://medium.com/@kalexotsu/solidity-assembly-checking-if-an-address-is-0-efficiently-d2bfe071331) can be written in assembly to save some gas.

*There are 30 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

188: 		        return recoveredAddress == address(this) && recoveredAddress != address(0);

188: 		        return recoveredAddress == address(this) && recoveredAddress != address(0);
```
[[188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L188), [188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L188)]



```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

406: 		        if (address(uint160(_transaction.paymaster)) != address(0)) {
```
[[406](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L406)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

108: 		        require(_owner != address(0), "ShB owner 0");

188: 		        require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

563: 		        require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

578: 		            if (_refundRecipient == address(0)) {
```
[[108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L108), [188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188), [563](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563), [578](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L578)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

130: 		        require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

132: 		        require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

326: 		        if (_refundRecipient == address(0)) {
```
[[130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132), [326](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L326)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

42: 		        require(_admin != address(0), "Admin should be non zero address");
```
[[42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L42)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

82: 		        require(_initializeData.governor != address(0), "StateTransition: governor zero");

246: 		        if (stateTransition[_chainId] != address(0)) {
```
[[82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L82), [246](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L246)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

55: 		        require(_l1Bridge != address(0), "bf");

57: 		        require(_aliasedOwner != address(0), "sf");

68: 		            require(_l1LegecyBridge != address(0), "bf2");

96: 		        if (currentL1Token == address(0)) {

129: 		        require(l1Token != address(0), "yh");
```
[[55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L57), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L68), [96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L96), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L129)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

51: 		        require(_l1Address != address(0), "in6"); // Should be non-zero address
```
[[51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

25: 		        require(address(_initializeData.verifier) != address(0), "vt");

26: 		        require(_initializeData.admin != address(0), "vy");

27: 		        require(_initializeData.validatorTimelock != address(0), "hc");
```
[[25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L26), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

30: 		        require(facetAddress != address(0), "F"); // Proxy has no facet for this selector
```
[[30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

141: 		            require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists

161: 		            require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

175: 		        require(_facet == address(0), "a1"); // facet address must be zero

181: 		            require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet

279: 		        if (_init == address(0)) {
```
[[141](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L141), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L161), [175](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175), [181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L181), [279](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L279)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

183: 		        require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");
```
[[183](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

275: 		        address refundRecipient = _params.refundRecipient == address(0) ? _params.sender : _params.refundRecipient;
```
[[275](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L275)]

</details>

---

### [G-64] Use scratch space for building calldata with assembly

If an external call's calldata can fit into two or fewer words, use the scratch space to build the calldata, rather than allowing Solidity to do a memory expansion.

*There are 275 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

37: 		        require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");

48: 		        require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");

57: 		        require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");

60: 		        bytes32 constructedBytecodeHash = Utils.constructedBytecodeHash(codeHash);

102: 		        if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {

107: 		        else if (Utils.isContractConstructing(codeHash)) {

134: 		            !Utils.isContractConstructing(codeHash)

136: 		            codeSize = Utils.bytecodeLenInBytes(codeHash);
```
[[37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L37), [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L48), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L57), [60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L60), [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L102), [107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L107), [134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L134), [136](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L136)]



```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

27: 		        signedTxHash = _transaction.encodeHash();

29: 		            txHash = keccak256(bytes.concat(signedTxHash, EfficientCall.keccak(_transaction.signature)));

29: 		            txHash = keccak256(bytes.concat(signedTxHash, EfficientCall.keccak(_transaction.signature)));

52: 		        bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);

56: 		            bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);

57: 		            bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

58: 		            encodedGasParam = bytes.concat(encodedGasPrice, encodedGasLimit);

61: 		        bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

62: 		        bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);

71: 		                encodedDataLength = RLPEncoder.encodeNonSingleBytesLen(txDataLen);

82: 		            rEncoded = RLPEncoder.encodeUint256(rInt);

87: 		            sEncoded = RLPEncoder.encodeUint256(sInt);

100: 		            vEncoded = RLPEncoder.encodeUint256(vInt);

116: 		            encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));

143: 		            bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);

144: 		            bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);

145: 		            bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);

146: 		            bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

147: 		            bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

148: 		            bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);

167: 		                encodedDataLength = RLPEncoder.encodeNonSingleBytesLen(txDataLen);

176: 		        bytes memory encodedAccessListLength = RLPEncoder.encodeListLen(0);

181: 		            rEncoded = RLPEncoder.encodeUint256(rInt);

186: 		            sEncoded = RLPEncoder.encodeUint256(sInt);

193: 		            vEncoded = RLPEncoder.encodeUint256(vInt - 27);

207: 		            encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));

236: 		            bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);

237: 		            bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);

238: 		            bytes memory encodedMaxPriorityFeePerGas = RLPEncoder.encodeUint256(_transaction.maxPriorityFeePerGas);

239: 		            bytes memory encodedMaxFeePerGas = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);

240: 		            bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

241: 		            bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

242: 		            bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);

262: 		                encodedDataLength = RLPEncoder.encodeNonSingleBytesLen(txDataLen);

271: 		        bytes memory encodedAccessListLength = RLPEncoder.encodeListLen(0);

276: 		            rEncoded = RLPEncoder.encodeUint256(rInt);

281: 		            sEncoded = RLPEncoder.encodeUint256(sInt);

288: 		            vEncoded = RLPEncoder.encodeUint256(vInt - 27);

302: 		            encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));
```
[[27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L27), [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L29), [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L29), [52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L52), [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L56), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L57), [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L58), [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L61), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L62), [71](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L71), [82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L82), [87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L87), [100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L100), [116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L116), [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L143), [144](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L144), [145](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L145), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L146), [147](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L147), [148](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L148), [167](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L167), [176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L176), [181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L181), [186](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L186), [193](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L193), [207](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L207), [236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L236), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L237), [238](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L238), [239](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L239), [240](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L240), [241](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L241), [242](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L242), [262](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L262), [271](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L271), [276](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L276), [281](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L281), [288](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L288), [302](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L302)]



```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

25: 		        (bool success, bytes memory returnData) = _delegateTo.delegatecall(_calldata);
```
[[25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L25)]



```solidity
File: code/system-contracts/contracts/Compressor.sol

62: 		                uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;

65: 		                uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);

66: 		                uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

72: 		        bytecodeHash = Utils.hashL2Bytecode(_bytecode);

73: 		        L1_MESSENGER_CONTRACT.sendToL1(_rawCompressedData);

74: 		        KNOWN_CODE_STORAGE_CONTRACT.markBytecodeAsPublished(bytecodeHash);

121: 		        uint256 numberOfInitialWrites = uint256(_compressedStateDiffs.readUint16(0));

129: 		            uint64 enumIndex = stateDiff.readUint64(84);

137: 		            bytes32 derivedKey = stateDiff.readBytes32(52);

138: 		            uint256 initValue = stateDiff.readUint256(92);

139: 		            uint256 finalValue = stateDiff.readUint256(124);

140: 		            require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");

161: 		            uint64 enumIndex = stateDiff.readUint64(84);

166: 		            uint256 initValue = stateDiff.readUint256(92);

167: 		            uint256 finalValue = stateDiff.readUint256(124);

189: 		        stateDiffHash = EfficientCall.keccak(_stateDiffs);

202: 		            uint256 dictionaryLen = uint256(_rawCompressedData.readUint16(0));
```
[[62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L62), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L65), [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L66), [72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L72), [73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L73), [74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L74), [121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L121), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L129), [137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L137), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L138), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L139), [140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L140), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L161), [166](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L166), [167](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L167), [189](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L189), [202](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L202)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

49: 		            ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getRawCodeHash(_address) == 0

103: 		        bytes32 constructorInputHash = EfficientCall.keccak(_input);

168: 		        NONCE_HOLDER_SYSTEM_CONTRACT.incrementDeploymentNonce(msg.sender);

188: 		        uint256 senderNonce = NONCE_HOLDER_SYSTEM_CONTRACT.incrementDeploymentNonce(msg.sender);

269: 		            ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0,

273: 		        require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied");

302: 		        uint256 knownCodeMarker = KNOWN_CODE_STORAGE_CONTRACT.getMarker(_bytecodeHash);

311: 		        bytes32 constructingBytecodeHash = Utils.constructingBytecodeHash(_bytecodeHash);

312: 		        ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.storeAccountConstructingCodeHash(_newAddress, constructingBytecodeHash);

341: 		                SystemContractHelper.setValueForNextFarCall(uint128(value));

345: 		            ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.markAccountCodeHashAsConstructed(_newAddress);

348: 		            IMMUTABLE_SIMULATOR_SYSTEM_CONTRACT.setImmutables(_newAddress, immutables);

352: 		            ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.storeAccountConstructedCodeHash(_newAddress, _bytecodeHash);
```
[[49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L49), [103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L103), [168](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L168), [188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L188), [269](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L269), [273](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L273), [302](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L302), [311](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L311), [312](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L312), [341](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L341), [345](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L345), [348](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L348), [352](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L352)]



```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

94: 		        bytes32 txHash = _suggestedSignedHash != bytes32(0) ? _suggestedSignedHash : _transaction.encodeHash();

99: 		        uint256 totalRequiredBalance = _transaction.totalRequiredBalance();

133: 		        uint128 value = Utils.safeCastToU128(_transaction.value);

135: 		        uint32 gas = Utils.safeCastToU32(gasleft());

151: 		            EfficientCall.propagateRevert();

201: 		        bool success = _transaction.payToTheBootloader();

217: 		        _transaction.processPaymasterInput();

46: 		        address codeAddress = SystemContractHelper.getCodeAddress();
```
[[94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L94), [99](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L99), [133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L133), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L135), [151](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L151), [201](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L201), [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L217), [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L46)]



```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

51: 		        uint256 pubdataPublishedBefore = REAL_SYSTEM_CONTEXT_CONTRACT.getCurrentPubdataSpent();

59: 		        uint256 pubdataPublishedAfter = REAL_SYSTEM_CONTEXT_CONTRACT.getCurrentPubdataSpent();

67: 		        uint256 pubdataPrice = REAL_SYSTEM_CONTEXT_CONTRACT.gasPerPubdataByte();
```
[[51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L51), [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L59), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L67)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

51: 		                L1_MESSENGER_CONTRACT.requestBytecodeL1Publication(_bytecodeHash);

78: 		        require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd");
```
[[51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L51), [78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L78)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

78: 		            txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),

90: 		        SystemContractHelper.burnGas(Utils.safeCastToU32(gasToPay), 0);

90: 		        SystemContractHelper.burnGas(Utils.safeCastToU32(gasToPay), 0);

118: 		        hash = EfficientCall.keccak(_message);

128: 		            txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),

154: 		        SystemContractHelper.burnGas(Utils.safeCastToU32(gasToPay), uint32(pubdataLen));

154: 		        SystemContractHelper.burnGas(Utils.safeCastToU32(gasToPay), uint32(pubdataLen));

166: 		        uint256 bytecodeLen = Utils.bytecodeLenInBytes(_bytecodeHash);

179: 		        SystemContractHelper.burnGas(Utils.safeCastToU32(gasToPay), uint32(pubdataLen));

179: 		        SystemContractHelper.burnGas(Utils.safeCastToU32(gasToPay), uint32(pubdataLen));

207: 		            bytes32 hashedLog = EfficientCall.keccak(
208: 		                _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + L2_TO_L1_LOG_SERIALIZE_SIZE]
209: 		            );

239: 		            bytes32 hashedMessage = EfficientCall.keccak(
240: 		                _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentMessageLength]
241: 		            );

262: 		                    Utils.hashL2Bytecode(
263: 		                        _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
264: 		                    )

317: 		        PUBDATA_CHUNK_PUBLISHER.chunkAndPublishPubdata(totalL2ToL1Pubdata);

324: 		            EfficientCall.keccak(totalL2ToL1Pubdata)
```
[[78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L78), [90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L90), [90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L90), [118](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L118), [128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L128), [154](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L154), [154](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L154), [166](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L166), [179](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L179), [179](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L179), [207-209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L207-L209), [239-241](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L239-L241), [262-264](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L262-L264), [317](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L317), [324](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L324)]



```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

77: 		        L1_MESSENGER_CONTRACT.sendToL1(message);

90: 		        L1_MESSENGER_CONTRACT.sendToL1(message);
```
[[77](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L77), [90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L90)]



```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

26: 		        value = SystemContractHelper.getExtraAbiData(0);

27: 		        uint256 addressAsUint = SystemContractHelper.getExtraAbiData(1);

28: 		        uint256 mask = SystemContractHelper.getExtraAbiData(2);

63: 		            (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call(
64: 		                abi.encodeCall(REAL_BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo, (msg.sender, to, value))
65: 		            );

79: 		        SystemContractHelper.setValueForNextFarCall(Utils.safeCastToU128(value));

79: 		        SystemContractHelper.setValueForNextFarCall(Utils.safeCastToU128(value));
```
[[26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L26), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L27), [28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L28), [63-65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L63-L65), [79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L79), [79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L79)]



```solidity
File: code/system-contracts/contracts/NonceHolder.sol

83: 		        IContractDeployer.AccountInfo memory accountInfo = DEPLOYER_SYSTEM_CONTRACT.getAccountInfo(msg.sender);
```
[[83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L83)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

118: 		        uint256 pubdataPublished = SystemContractHelper.getZkSyncMeta().pubdataPublished;
```
[[118](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L118)]



```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

91: 		        return L2_MESSENGER.sendToL1(_message);
```
[[91](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L91)]



```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

44: 		        uint32 dataLength = uint32(Utils.safeCastToU32(data.length));
```
[[44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L44)]



```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

22: 		            SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),

22: 		            SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),

32: 		            SystemContractHelper.isSystemContract(msg.sender),
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L22), [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L22), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L32)]



```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

251: 		        SystemContractHelper.loadCalldataIntoActivePtr();

259: 		        SystemContractHelper.ptrAddIntoActive(uint32(dataOffset));

262: 		        SystemContractHelper.ptrShrinkIntoActive(shrinkTo);

264: 		        uint32 gas = Utils.safeCastToU32(_gas);

273: 		        SystemContractHelper.ptrPackIntoActivePtr(farCallAbi);
```
[[251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L251), [259](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L259), [262](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L262), [264](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L264), [273](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L273)]



```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

83: 		        uint32 dataLength = uint32(Utils.safeCastToU32(data.length));
```
[[83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L83)]



```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

132: 		                EfficientCall.keccak(_transaction.data),

134: 		                EfficientCall.keccak(_transaction.paymasterInput)

155: 		        bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);

159: 		            bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);

160: 		            bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

161: 		            encodedGasParam = bytes.concat(encodedGasPrice, encodedGasLimit);

164: 		        bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

165: 		        bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);

174: 		                encodedDataLength = RLPEncoder.encodeNonSingleBytesLen(txDataLen);

185: 		            encodedChainId = bytes.concat(RLPEncoder.encodeUint256(block.chainid), hex"80_80");

185: 		            encodedChainId = bytes.concat(RLPEncoder.encodeUint256(block.chainid), hex"80_80");

199: 		            encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));

228: 		            bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);

229: 		            bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);

230: 		            bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);

231: 		            bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

232: 		            bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

233: 		            bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);

252: 		                encodedDataLength = RLPEncoder.encodeNonSingleBytesLen(txDataLen);

261: 		        bytes memory encodedAccessListLength = RLPEncoder.encodeListLen(0);

271: 		            encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));

298: 		            bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);

299: 		            bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);

300: 		            bytes memory encodedMaxPriorityFeePerGas = RLPEncoder.encodeUint256(_transaction.maxPriorityFeePerGas);

301: 		            bytes memory encodedMaxFeePerGas = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);

302: 		            bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

303: 		            bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

304: 		            bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);

324: 		                encodedDataLength = RLPEncoder.encodeNonSingleBytesLen(txDataLen);

333: 		        bytes memory encodedAccessListLength = RLPEncoder.encodeListLen(0);

343: 		            encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));

377: 		            uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);

382: 		                IERC20(token).safeApprove(paymaster, 0);

383: 		                IERC20(token).safeApprove(paymaster, minAllowance);
```
[[132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L132), [134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L134), [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L155), [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L159), [160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L160), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L161), [164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L164), [165](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L165), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L174), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L185), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L185), [199](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L199), [228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L228), [229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L229), [230](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L230), [231](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L231), [232](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L232), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L233), [252](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L252), [261](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L261), [271](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L271), [298](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L298), [299](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L299), [300](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L300), [301](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L301), [302](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L302), [303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L303), [304](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L304), [324](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L324), [333](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L333), [343](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L343), [377](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377), [382](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L382), [383](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L383)]



```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

90: 		            EfficientCall.sha(_bytecode) &
```
[[90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L90)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

65: 		        uint256 amount = IERC20(_token).balanceOf(address(this));

67: 		        IERC20(_token).safeTransfer(address(sharedBridge), amount);

161: 		        uint256 balanceBefore = _token.balanceOf(address(sharedBridge));

163: 		        uint256 balanceAfter = _token.balanceOf(address(sharedBridge));
```
[[65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L161), [163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L163)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

119: 		            IMailbox(_target).transferEthToSharedBridge();

127: 		            uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

128: 		            uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));

130: 		            IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);

131: 		            uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

138: 		        require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");

174: 		        uint256 balanceBefore = _token.balanceOf(address(this));

176: 		        uint256 balanceAfter = _token.balanceOf(address(this));

195: 		        require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

262: 		        (, bytes memory data1) = _token.staticcall(abi.encodeCall(IERC20Metadata.name, ()));

263: 		        (, bytes memory data2) = _token.staticcall(abi.encodeCall(IERC20Metadata.symbol, ()));

264: 		        (, bytes memory data3) = _token.staticcall(abi.encodeCall(IERC20Metadata.decimals, ()));

362: 		            IERC20(_l1Token).safeTransfer(_depositSender, _amount);

396: 		            require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");

423: 		            bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
424: 		                _l2BatchNumber,
425: 		                _l2MessageIndex
426: 		            );

452: 		            IERC20(l1Token).safeTransfer(l1Receiver, amount);

467: 		            bool baseTokenWithdrawal = (l1Token == bridgehub.baseToken(_chainId));

503: 		        (uint32 functionSignature, uint256 offset) = UnsafeBytes.readUint32(_l2ToL1message, 0);

506: 		            (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);

507: 		            (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);

508: 		            l1Token = bridgehub.baseToken(_chainId);

518: 		            (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);

519: 		            (l1Token, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);

520: 		            (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);

580: 		                    ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
```
[[119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L119), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127), [128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L128), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L130), [131](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L174), [176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176), [195](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195), [262](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L262), [263](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L263), [264](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L264), [362](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L362), [396](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L396), [423-426](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L423-L426), [452](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L452), [467](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L467), [503](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L503), [506](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L506), [507](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L507), [508](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L508), [518](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L518), [519](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L519), [520](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L520), [580](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L580)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

76: 		        return IStateTransitionManager(stateTransitionManager[_chainId]).stateTransition(_chainId);

238: 		        canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction(
239: 		            BridgehubL2TransactionRequest({
240: 		                sender: msg.sender,
241: 		                contractL2: _request.l2Contract,
242: 		                mintValue: _request.mintValue,
243: 		                l2Value: _request.l2Value,
244: 		                l2Calldata: _request.l2Calldata,
245: 		                l2GasLimit: _request.l2GasLimit,
246: 		                l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
247: 		                factoryDeps: _request.factoryDeps,
248: 		                refundRecipient: refundRecipient
249: 		            })
250: 		        );

304: 		        canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction(
305: 		            BridgehubL2TransactionRequest({
306: 		                sender: _request.secondBridgeAddress,
307: 		                contractL2: outputRequest.l2Contract,
308: 		                mintValue: _request.mintValue,
309: 		                l2Value: _request.l2Value,
310: 		                l2Calldata: outputRequest.l2Calldata,
311: 		                l2GasLimit: _request.l2GasLimit,
312: 		                l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
313: 		                factoryDeps: outputRequest.factoryDeps,
314: 		                refundRecipient: refundRecipient
315: 		            })
316: 		        );

328: 		            _recipient = msg.sender == tx.origin ? msg.sender : AddressAliasHelper.applyL1ToL2Alias(msg.sender);

331: 		            _recipient = AddressAliasHelper.applyL1ToL2Alias(_refundRecipient);
```
[[76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L76), [238-250](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L238-L250), [304-316](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L304-L316), [328](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L328), [331](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L331)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

75: 		        return IZkSyncStateTransition(stateTransition[_chainId]).getAdmin();

161: 		        IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();

166: 		        IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();

171: 		        IZkSyncStateTransition(stateTransition[_chainId]).revertBatches(_newLastBatch);

226: 		        IAdmin(_chainContract).executeUpgrade(cutData);
```
[[75](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L75), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L161), [166](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L166), [171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L171), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L226)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

103: 		        return committedBatchTimestamp[_chainId].get(_l2BatchNumber);

117: 		                committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);

136: 		                committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);

186: 		                uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
187: 		                    _newBatchesData[i].batchNumber
188: 		                );

210: 		                uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);

226: 		        address contractAddress = stateTransitionManager.stateTransition(_chainId);

62: 		        require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");
```
[[103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L103), [117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L117), [136](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L136), [186-188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L186-L188), [210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L210), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L226), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

97: 		        L2ContractHelper.validateBytecodeHash(_l2DefaultAccountBytecodeHash);

114: 		        L2ContractHelper.validateBytecodeHash(_l2BootloaderBytecodeHash);

201: 		        TransactionValidator.validateUpgradeTransaction(_l2ProtocolUpgradeTx);

228: 		                L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
```
[[97](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L97), [114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L114), [201](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L201), [228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L228)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

66: 		            l2TokenBeacon.transferOwnership(_aliasedOwner);

88: 		            AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||

89: 		                AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,

104: 		        IL2StandardToken(expectedL2Token).bridgeMint(_l2Receiver, _amount);

113: 		        L2StandardERC20(address(l2Token)).bridgeInitialize(_l1Token, _data);

126: 		        IL2StandardToken(_l2Token).bridgeBurn(msg.sender, _amount);

132: 		        L2ContractHelper.sendMessageToL1(message);
```
[[66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L66), [88](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L88), [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L89), [104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L104), [113](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L113), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L126), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L132)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

120: 		        require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");
```
[[120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

15: 		        Diamond.diamondCut(_diamondCut);

21: 		        Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
```
[[15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L15), [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L21)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

101: 		        for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {

138: 		        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

158: 		        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

178: 		        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

195: 		            ds.facetToSelectors[_facet].facetPosition = ds.facets.length.toUint16();

208: 		        uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16();

240: 		            ds.selectorToFacet[lastSelector].selectorPosition = selectorPosition.toUint16();

269: 		            ds.facetToSelectors[lastFacet].facetPosition = facetPosition.toUint16();

283: 		            (bool success, bytes memory data) = _init.delegatecall(_calldata);
```
[[101](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L138), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158), [178](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L178), [195](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L195), [208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L208), [240](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L240), [269](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L269), [283](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L283)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

29: 		        for (uint256 i; i < pathLength; i = i.uncheckedInc()) {
```
[[29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L29)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

65: 		        require(!_queue.isEmpty(), "D"); // priority queue is empty

73: 		        require(!_queue.isEmpty(), "s"); // priority queue is empty
```
[[65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L65), [73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L73)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

83: 		            costForComputation += Math.ceilDiv(_encodingLength * L1_TX_DELTA_544_ENCODING_BYTES, 544);

89: 		            costForComputation = Math.max(costForComputation, L1_TX_MIN_L2_GAS_BASE);

136: 		        batchOverheadForTransaction = Math.max(batchOverheadForTransaction, overheadForLength);
```
[[83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L83), [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L89), [136](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L136)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

106: 		            cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),

114: 		        Diamond.diamondCut(_diamondCut);

124: 		        Diamond.diamondCut(_diamondCut);

134: 		        Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();

144: 		        Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
```
[[106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L106), [114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L114), [124](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L124), [134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L134), [144](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L144)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

142: 		        for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

144: 		            (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);

145: 		            (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);

146: 		            (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);

227: 		            IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,

257: 		        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

289: 		        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

311: 		        for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {

312: 		            PriorityOperation memory priorityOp = s.priorityQueue.popFront();

351: 		        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {

405: 		        for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {

406: 		            currentTotalBatchesVerified = currentTotalBatchesVerified.uncheckedInc();

612: 		        (bool success, bytes memory data) = POINT_EVALUATION_PRECOMPILE_ADDR.staticcall(precompileInput);

680: 		        (bool success, bytes memory data) = s.blobVersionedHashRetriever.staticcall(abi.encode(_index));
```
[[142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142), [144](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L144), [145](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L145), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L146), [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L227), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289), [311](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L311), [312](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L312), [351](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351), [405](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L405), [406](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L406), [612](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L612), [680](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L680)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

93: 		        return s.priorityQueue.getTotalPriorityTxs();

98: 		        return s.priorityQueue.getFirstUnprocessedPriorityTx();

103: 		        return s.priorityQueue.getSize();

108: 		        return s.priorityQueue.front();

158: 		        Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();

164: 		        Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();

182: 		        Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();

203: 		        Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();

208: 		        for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {

218: 		        Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();

224: 		        Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();

230: 		        Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();
```
[[93](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L93), [98](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L98), [103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L103), [108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L108), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L158), [164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L164), [182](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L182), [203](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L203), [208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208), [218](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L218), [224](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L224), [230](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L230)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

174: 		        return Math.max(l2GasPrice, minL2GasPriceBaseToken);

235: 		            l2Sender = AddressAliasHelper.applyL1ToL2Alias(_request.sender);

265: 		        _params.txId = s.priorityQueue.getTotalPriorityTxs();

278: 		            refundRecipient = AddressAliasHelper.applyL1ToL2Alias(refundRecipient);

334: 		        s.priorityQueue.pushBack(
335: 		            PriorityOperation({
336: 		                canonicalTxHash: canonicalTxHash,
337: 		                expirationTimestamp: _priorityOpParams.expirationTimestamp,
338: 		                layer2Tip: uint192(0) // TODO: Restore after fee modeling will be stable. (SMA-1230)
339: 		            })
340: 		        );

356: 		        for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {

357: 		            bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);
```
[[174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L174), [235](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L235), [265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L265), [278](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L278), [334-340](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L334-L340), [356](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356), [357](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L357)]

</details>

---

### [G-65] Use assembly to write hashes

Considering using [assembly](https://medium.com/@kalexotsu/understanding-solidity-assembly-hashing-a-string-from-calldata-fbd2ece82263) to write hashes, as it's possible to save a considerable amount of gas.

*There are 56 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

29: 		            txHash = keccak256(bytes.concat(signedTxHash, EfficientCall.keccak(_transaction.signature)));

120: 		            keccak256(
121: 		                bytes.concat(
122: 		                    encodedListLength,
123: 		                    encodedNonce,
124: 		                    encodedGasParam,
125: 		                    encodedTo,
126: 		                    encodedValue,
127: 		                    encodedDataLength,
128: 		                    _transaction.data,
129: 		                    vEncoded,
130: 		                    rEncoded,
131: 		                    sEncoded
132: 		                )
133: 		            );

211: 		            keccak256(
212: 		                bytes.concat(
213: 		                    "\x01",
214: 		                    encodedListLength,
215: 		                    encodedFixedLengthParams,
216: 		                    encodedDataLength,
217: 		                    _transaction.data,
218: 		                    encodedAccessListLength,
219: 		                    vEncoded,
220: 		                    rEncoded,
221: 		                    sEncoded
222: 		                )
223: 		            );

306: 		            keccak256(
307: 		                bytes.concat(
308: 		                    "\x02",
309: 		                    encodedListLength,
310: 		                    encodedFixedLengthParams,
311: 		                    encodedDataLength,
312: 		                    _transaction.data,
313: 		                    encodedAccessListLength,
314: 		                    vEncoded,
315: 		                    rEncoded,
316: 		                    sEncoded
317: 		                )
318: 		            );
```
[[29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L29), [120-133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L120-L133), [211-223](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L211-L223), [306-318](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L306-L318)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

105: 		        bytes32 hash = keccak256(
106: 		            bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, constructorInputHash)
107: 		        );

121: 		        bytes32 hash = keccak256(
122: 		            bytes.concat(CREATE_PREFIX, bytes32(uint256(uint160(_sender))), bytes32(_senderNonce))
123: 		        );
```
[[105-107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L105-L107), [121-123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L121-L123)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

95: 		        bytes32 hashedLog = keccak256(
96: 		            abi.encodePacked(
97: 		                _l2ToL1Log.l2ShardId,
98: 		                _l2ToL1Log.isService,
99: 		                _l2ToL1Log.txNumberInBlock,
100: 		                _l2ToL1Log.sender,
101: 		                _l2ToL1Log.key,
102: 		                _l2ToL1Log.value
103: 		            )
104: 		        );

106: 		        chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

122: 		        chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

164: 		        chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

212: 		            reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));

225: 		                l2ToL1LogsTreeArray[i] = keccak256(
226: 		                    abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
227: 		                );

243: 		            reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));

259: 		            reconstructedChainedL1BytecodesRevealDataHash = keccak256(
260: 		                abi.encode(
261: 		                    reconstructedChainedL1BytecodesRevealDataHash,
262: 		                    Utils.hashL2Bytecode(
263: 		                        _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
264: 		                    )
265: 		                )
266: 		            );
```
[[95-104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L95-L104), [106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L106), [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L122), [164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L164), [212](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L212), [225-227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L225-L227), [243](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L243), [259-266](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L259-L266)]



```solidity
File: code/system-contracts/contracts/SystemContext.sol

159: 		            hash = keccak256(abi.encode(_block));

227: 		        return keccak256(abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash));

234: 		        return keccak256(abi.encodePacked(uint32(_blockNumber)));

403: 		        currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));
```
[[159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L159), [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L227), [234](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L234), [403](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L403)]



```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

108: 		        bytes32 data = keccak256(
109: 		            bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
110: 		        );
```
[[108-110](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L108-L110)]



```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

119: 		        bytes32 structHash = keccak256(
120: 		            abi.encode(
121: 		                EIP712_TRANSACTION_TYPE_HASH,
122: 		                _transaction.txType,
123: 		                _transaction.from,
124: 		                _transaction.to,
125: 		                _transaction.gasLimit,
126: 		                _transaction.gasPerPubdataByteLimit,
127: 		                _transaction.maxFeePerGas,
128: 		                _transaction.maxPriorityFeePerGas,
129: 		                _transaction.paymaster,
130: 		                _transaction.nonce,
131: 		                _transaction.value,
132: 		                EfficientCall.keccak(_transaction.data),
133: 		                keccak256(abi.encodePacked(_transaction.factoryDeps)),
134: 		                EfficientCall.keccak(_transaction.paymasterInput)
135: 		            )
136: 		        );

133: 		                keccak256(abi.encodePacked(_transaction.factoryDeps)),

138: 		        bytes32 domainSeparator = keccak256(
139: 		            abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
140: 		        );

139: 		            abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

139: 		            abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

142: 		        return keccak256(abi.encodePacked("\x19\x01", domainSeparator, structHash));

203: 		            keccak256(
204: 		                bytes.concat(
205: 		                    encodedListLength,
206: 		                    encodedNonce,
207: 		                    encodedGasParam,
208: 		                    encodedTo,
209: 		                    encodedValue,
210: 		                    encodedDataLength,
211: 		                    _transaction.data,
212: 		                    encodedChainId
213: 		                )
214: 		            );

275: 		            keccak256(
276: 		                bytes.concat(
277: 		                    "\x01",
278: 		                    encodedListLength,
279: 		                    encodedFixedLengthParams,
280: 		                    encodedDataLength,
281: 		                    _transaction.data,
282: 		                    encodedAccessListLength
283: 		                )
284: 		            );

347: 		            keccak256(
348: 		                bytes.concat(
349: 		                    "\x02",
350: 		                    encodedListLength,
351: 		                    encodedFixedLengthParams,
352: 		                    encodedDataLength,
353: 		                    _transaction.data,
354: 		                    encodedAccessListLength
355: 		                )
356: 		            );
```
[[119-136](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L119-L136), [133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L133), [138-140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L138-L140), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139), [142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L142), [203-214](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L203-L214), [275-284](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L275-L284), [347-356](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L347-L356)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

76: 		        bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
```
[[76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

210: 		        bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));

341: 		                bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));

598: 		        bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
```
[[210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L210), [341](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L341), [598](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L598)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

205: 		        return keccak256(abi.encode(_operation));
```
[[205](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L205)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

100: 		        storedBatchZero = keccak256(abi.encode(batchZero));

102: 		        initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

138: 		        initialCutHash = keccak256(abi.encode(_diamondCut));

147: 		        upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

156: 		        upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

255: 		        bytes32 cutHashInput = keccak256(_diamondCut);
```
[[100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100), [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138), [147](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L147), [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L156), [255](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L255)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

212: 		        bytes32 l2ProtocolUpgradeTxHash = keccak256(encodedTransaction);
```
[[212](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L212)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

150: 		        bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""));
```
[[150](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150)]



```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

67: 		        bytes32 data = keccak256(
68: 		            bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
69: 		        );
```
[[67-69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L67-L69)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

104: 		        bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
```
[[104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

63: 		                    keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),

313: 		            concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));

460: 		                keccak256(
461: 		                    abi.encodePacked(
462: 		                        _prevBatchCommitment,
463: 		                        _currentBatchCommitment,
464: 		                        _verifierParams.recursionNodeLevelVkHash,
465: 		                        _verifierParams.recursionLeafLevelVkHash
466: 		                    )
467: 		                )

506: 		        bytes32 passThroughDataHash = keccak256(_batchPassThroughData(_newBatchData));

507: 		        bytes32 metadataHash = keccak256(_batchMetaParameters());

508: 		        bytes32 auxiliaryOutputHash = keccak256(
509: 		            _batchAuxiliaryOutput(_newBatchData, _stateDiffHash, _blobCommitments, _blobHashes)
510: 		        );

512: 		        return keccak256(abi.encode(passThroughDataHash, metadataHash, auxiliaryOutputHash));

545: 		        bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs);

588: 		        return keccak256(abi.encode(_storedBatchInfo));

654: 		            blobCommitments[versionedHashIndex] = keccak256(
655: 		                abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
656: 		            );
```
[[63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L63), [313](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313), [460-467](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L460-L467), [506](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L506), [507](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L507), [508-510](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L508-L510), [512](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L512), [545](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L545), [588](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L588), [654-656](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L654-L656)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

112: 		        bytes32 hashedLog = keccak256(
113: 		            abi.encodePacked(_log.l2ShardId, _log.isService, _log.txNumberInBatch, _log.sender, _log.key, _log.value)
114: 		        );

138: 		                value: keccak256(_message.data)

332: 		        canonicalTxHash = keccak256(transactionEncoding);
```
[[112-114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L112-L114), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L138), [332](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L332)]

</details>

---

### [G-66] Use assembly to validate `msg.sender`

It is possible to use assembly to efficiently validate `msg.sender` with the least amount of opcodes. For more details check the [following report](https://code4rena.com/reports/2023-05-juicebox#g-06-use-assembly-to-validate-msgsender).

*There are 42 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

26: 		        require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
[[26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L26)]



```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

22: 		        require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");
```
[[22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L22)]



```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

29: 		        require(msg.sender == address(this), "Callable only by self");

239: 		        require(
240: 		            msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
241: 		            "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
242: 		        );
```
[[29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L29), [239-242](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L239-L242)]



```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

29: 		        if (msg.sender != BOOTLOADER_FORMAL_ADDRESS) {

222: 		        assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS);
```
[[29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L29), [222](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L222)]



```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

35: 		        require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
[[35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L35)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

20: 		        require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");
```
[[20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L20)]



```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

33: 		        require(
34: 		            msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
35: 		                msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
36: 		                msg.sender == BOOTLOADER_FORMAL_ADDRESS,
37: 		            "Only system contracts with special access can call this method"
38: 		        );
```
[[33-38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L33-L38)]



```solidity
File: code/system-contracts/contracts/NonceHolder.sol

89: 		            require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");

136: 		        require(
137: 		            msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
138: 		            "Only the contract deployer can increment the deployment nonce"
139: 		        );
```
[[89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L89), [136-139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L136-L139)]



```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

21: 		        require(
22: 		            SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
23: 		            "This method require system call flag"
24: 		        );

31: 		        require(
32: 		            SystemContractHelper.isSystemContract(msg.sender),
33: 		            "This method require the caller to be system contract"
34: 		        );

41: 		        require(msg.sender == caller, "Inappropriate caller");

48: 		        require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");

55: 		        require(msg.sender == FORCE_DEPLOYER);
```
[[21-24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L21-L24), [31-34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L31-L34), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L41), [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L48), [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L55)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

64: 		        require(msg.sender == address(sharedBridge), "Not shared bridge");
```
[[64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

69: 		        require(msg.sender == address(bridgehub), "ShB not BH");

75: 		        require(
76: 		            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
77: 		            "L1SharedBridge: not bridgehub or era chain"
78: 		        );

84: 		        require(msg.sender == address(legacyBridge), "ShB not legacy bridge");

138: 		        require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");
```
[[69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69), [75-78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75-L78), [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L84), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

46: 		        require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

62: 		        require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights
```
[[46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

59: 		        require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

65: 		        require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

71: 		        require(
72: 		            msg.sender == owner() || msg.sender == securityCouncil,
73: 		            "Only the owner and security council are allowed to call this function"
74: 		        );
```
[[59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L59), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L65), [71-74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L71-L74)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

64: 		        require(msg.sender == bridgehub, "StateTransition: only bridgehub");

70: 		        require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

121: 		        require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights
```
[[64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64), [70](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L70), [121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L121)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62: 		        require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

68: 		        require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
```
[[62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

87: 		        require(
88: 		            AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
89: 		                AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
90: 		            "mq"
91: 		        );
```
[[87-91](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L87-L91)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

120: 		        require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");

130: 		        require(msg.sender == l2Bridge, "xnt"); // Only L2 bridge can call this method
```
[[120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L130)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

34: 		        require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights
```
[[34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

16: 		        require(msg.sender == s.admin, "StateTransition Chain: not admin");

22: 		        require(s.validators[msg.sender], "StateTransition Chain: not validator");

27: 		        require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

32: 		        require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

37: 		        require(
38: 		            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
39: 		            "StateTransition Chain: Only by admin or state transition manager"
40: 		        );

45: 		        require(
46: 		            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
47: 		            "StateTransition Chain: Only by validator or state transition manager"
48: 		        );

53: 		        require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
```
[[16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16), [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32), [37-40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L37-L40), [45-48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45-L48), [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53)]

</details>

---

### [G-67] Use assembly to write `address` storage values

Using assembly `{ sstore(state.slot, addr)` instead of `state = addr` can save gas.

*There are 16 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/SystemContext.sol

100: 		        origin = _newOrigin;
```
[[100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L100)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

96: 		        l1WethAddress = _l1WethAddress;
```
[[96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L96)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

55: 		        pendingAdmin = _newPendingAdmin;

65: 		        admin = currentPendingAdmin;

109: 		        sharedBridge = IL1SharedBridge(_sharedBridge);
```
[[55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L65), [109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L109)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

46: 		        securityCouncil = _securityCouncil;

258: 		        securityCouncil = _newSecurityCouncil;
```
[[46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L46), [258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L258)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

59: 		        bridgehub = _bridgehub;

85: 		        genesisUpgrade = _initializeData.genesisUpgrade;

87: 		        validatorTimelock = _initializeData.validatorTimelock;

114: 		        pendingAdmin = _newPendingAdmin;

124: 		        admin = currentPendingAdmin;

133: 		        validatorTimelock = _validatorTimelock;
```
[[59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L59), [85](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L85), [87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L87), [114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L114), [124](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L124), [133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L133)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

60: 		        l1Bridge = _l1Bridge;
```
[[60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L60)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

52: 		        l1Address = _l1Address;

54: 		        l2Bridge = msg.sender;
```
[[52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L52), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L54)]

</details>

---

### [G-68] Use assembly to emit an `event`

To efficiently emit events, it's possible to utilize assembly by making use of scratch space and the free memory pointer. This approach has the advantage of potentially avoiding the costs associated with memory expansion.

However, it's important to note that in order to safely optimize this process, it is preferable to cache and restore the free memory pointer.

A good example of such practice can be seen in [Solady's](https://github.com/Vectorized/solady/blob/main/src/tokens/ERC1155.sol#L167) codebase.

*There are 77 instances of this issue.*

<details>
<summary>Expand findings</summary>


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

68: 		        emit AccountVersionUpdated(msg.sender, _version);

86: 		        emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);

355: 		        emit ContractDeployed(_sender, _bytecodeHash, _newAddress);
```
[[68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L68), [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L86), [355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L355)]



```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

59: 		            emit MarkedAsKnown(_bytecodeHash, _shouldSendToL1);
```
[[59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L59)]



```solidity
File: code/system-contracts/contracts/L1Messenger.sol

111: 		        emit L2ToL1LogSent(_l2ToL1Log);

156: 		        emit L1MessageSent(msg.sender, hash, _message);

181: 		        emit BytecodeL1PublicationRequested(_bytecodeHash);
```
[[111](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L111), [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L156), [181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L181)]



```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

49: 		        emit Transfer(_from, _to, _amount);

67: 		        emit Mint(_account, _amount);

79: 		        emit Withdrawal(msg.sender, _l1Receiver, amount);

92: 		        emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData);
```
[[49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L49), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L67), [79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L79), [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L92)]



```solidity
File: code/system-contracts/contracts/NonceHolder.sol

96: 		        emit ValueSetUnderNonce(msg.sender, _key, _value);
```
[[96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L96)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

155: 		        emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);

199: 		        emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);

225: 		        emit WithdrawalFinalized(l1Receiver, l1Token, amount);
```
[[155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L155), [199](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L199), [225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L225)]



```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

168: 		        emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);

227: 		        emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);

239: 		        emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);

367: 		        emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);

454: 		        emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);

602: 		        emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
```
[[168](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L168), [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L227), [239](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L239), [367](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L367), [454](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L454), [602](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L602)]



```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

56: 		        emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

68: 		        emit NewPendingAdmin(currentPendingAdmin, address(0));

69: 		        emit NewAdmin(previousAdmin, pendingAdmin);

145: 		        emit NewChain(_chainId, _stateTransitionManager, _admin);
```
[[56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L56), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68), [69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69), [145](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L145)]



```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

47: 		        emit ChangeSecurityCouncil(address(0), _securityCouncil);

50: 		        emit ChangeMinDelay(0, _minDelay);

132: 		        emit TransparentOperationScheduled(id, _delay, _operation);

144: 		        emit ShadowOperationScheduled(_id, _delay);

157: 		        emit OperationCancelled(_id);

180: 		        emit OperationExecuted(id);

199: 		        emit OperationExecuted(id);

250: 		        emit ChangeMinDelay(minDelay, _newDelay);

257: 		        emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```
[[47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L47), [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L50), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L132), [144](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L144), [157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L157), [180](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L180), [199](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L199), [250](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L250), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L257)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

115: 		        emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

127: 		        emit NewPendingAdmin(currentPendingAdmin, address(0));

128: 		        emit NewAdmin(previousAdmin, pendingAdmin);

227: 		        emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);

235: 		        emit StateTransitionNewChain(_chainId, _stateTransitionContract);

287: 		        emit StateTransitionNewChain(_chainId, stateTransitionAddress);
```
[[115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L115), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L127), [128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L128), [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227), [235](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L235), [287](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L287)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

83: 		        emit ValidatorAdded(_chainId, _newValidator);

92: 		        emit ValidatorRemoved(_chainId, _validator);

98: 		        emit NewExecutionDelay(_executionDelay);
```
[[83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L83), [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L92), [98](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

87: 		        emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);

104: 		        emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);

121: 		        emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);

137: 		        emit NewVerifier(address(oldVerifier), address(_newVerifier));

157: 		        emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

256: 		        emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
```
[[87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L87), [104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L104), [121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L121), [137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L137), [157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L157), [256](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L256)]



```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

40: 		        emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);

67: 		        emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);
```
[[40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L40), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L67)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

105: 		        emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);

134: 		        emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount);
```
[[105](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L105), [134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L134)]



```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

101: 		        emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);

126: 		        emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);

147: 		        emit BridgeMint(_to, _amount);

156: 		        emit BridgeBurn(_from, _amount);
```
[[101](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L101), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126), [147](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L147), [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L156)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

121: 		        emit DiamondCut(facetCuts, initAddress, initCalldata);
```
[[121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L121)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

28: 		        emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

40: 		        emit NewPendingAdmin(pendingAdmin, address(0));

41: 		        emit NewAdmin(previousAdmin, pendingAdmin);

47: 		        emit ValidatorStatusUpdate(_validator, _active);

54: 		        emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);

63: 		        emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);

75: 		        emit NewFeeParams(oldFeeParams, _newFeeParams);

86: 		        emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator);

92: 		        emit ValidiumModeStatusUpdate(_validiumMode);

115: 		        emit ExecuteUpgrade(_diamondCut);

125: 		        emit ExecuteUpgrade(_diamondCut);

139: 		        emit Freeze();

149: 		        emit Unfreeze();
```
[[28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L28), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L41), [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L47), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L54), [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L63), [75](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L75), [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L86), [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92), [115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L115), [125](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L125), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L139), [149](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L149)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

261: 		            emit BlockCommit(
262: 		                _lastCommittedBatchData.batchNumber,
263: 		                _lastCommittedBatchData.batchHash,
264: 		                _lastCommittedBatchData.commitment
265: 		            );

299: 		            emit BlockCommit(
300: 		                _lastCommittedBatchData.batchNumber,
301: 		                _lastCommittedBatchData.batchHash,
302: 		                _lastCommittedBatchData.commitment
303: 		            );

353: 		            emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

436: 		        emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

496: 		        emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
```
[[261-265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261-L265), [299-303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L299-L303), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353), [436](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436), [496](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496)]



```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

343: 		        emit NewPriorityRequest(
344: 		            _priorityOpParams.txId,
345: 		            canonicalTxHash,
346: 		            _priorityOpParams.expirationTimestamp,
347: 		            transaction,
348: 		            _factoryDeps
349: 		        );
```
[[343-349](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L343-L349)]

</details>