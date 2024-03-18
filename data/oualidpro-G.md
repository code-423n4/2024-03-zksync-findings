## Summary

### Gas Optimizations

| |Issue|Instances|Total Gas Saved|
|-|:-|:-:|:-:|
| [[GAS&#x2011;1](#gas1-multiple-accesses-of-a-mapping-array-should-use-a-local-variable-cache)] | Multiple accesses of a mapping/array should use a local variable cache | 42 | 1764 | 
| [[GAS&#x2011;2](#gas2-use-assembly-to-calculate-hashes-to-save-gas)] | Use assembly to calculate hashes to save gas | 61 | 4880 | 
| [[GAS&#x2011;3](#gas3-use-assembly-to-check-for-address-0)] | Use assembly to check for `address(0)` | 50 | 300 | 
| [[GAS&#x2011;4](#gas4-use-assembly-in-place-of-abi-decode-to-extract-calldata-values-more-efficiently)] | Use assembly in place of `abi.decode` to extract `calldata` values more efficiently | 1 | - | 
| [[GAS&#x2011;5](#gas5-optimize-address-storage-value-management-with-assembly)] | Optimize Address Storage Value Management with `assembly` | 14 | - | 
| [[GAS&#x2011;6](#gas6-use-assembly-to-emit-events)] | Use assembly to emit events | 77 | 2926 | 
| [[GAS&#x2011;7](#gas7-using-bools-for-storage-incurs-overhead)] | Using bools for storage incurs overhead | 19 | 1900 | 
| [[GAS&#x2011;8](#gas8-cache-array-length-outside-of-loop)] | Cache array length outside of loop | 11 | 1067 | 
| [[GAS&#x2011;9](#gas9-state-variables-should-be-cached-in-stack-variables-rather-than-re-reading-them-from-storage)] | State variables should be cached in stack variables rather than re-reading them from storage | 4 | 388 | 
| [[GAS&#x2011;10](#gas10-with-assembly-call-bool-success-transfer-can-be-done-gas-optimized)] | With assembly, `.call (bool success)` transfer can be done gas-optimized | 5 | - | 
| [[GAS&#x2011;11](#gas11-add-unchecked-for-subtractions-where-the-operands-cannot-underflow-because-of-a-previous-require-or-if-statement)] | Add `unchecked {}` for subtractions where the operands cannot underflow because of a previous `require()` or `if`-statement | 6 | 510 | 
| [[GAS&#x2011;12](#gas12-x-y-costs-more-gas-than-x-x-y-for-state-variables)] | `x += y` costs more gas than `x = x + y` for state variables | 3 | 339 | 
| [[GAS&#x2011;13](#gas13-don-t-compare-boolean-expressions-to-boolean-literals)] | Don't compare boolean expressions to boolean literals | 1 | 9 | 
| [[GAS&#x2011;14](#gas14-use-custom-errors-rather-than-revert-require-strings-to-save-gas)] | Use custom errors rather than `revert()`/`require()` strings to save gas | 340 | - | 
| [[GAS&#x2011;15](#gas15-divisions-which-do-not-divide-by-x-cannot-overflow-or-overflow-so-such-operations-can-be-unchecked-to-save-gas)] | Divisions which do not divide by -X cannot overflow or overflow so such operations can be unchecked to save gas | 14 | - | 
| [[GAS&#x2011;16](#gas16-do-not-calculate-constants)] | Do not calculate constants | 12 | 4800 | 
| [[GAS&#x2011;17](#gas17-stack-variable-cost-less-while-used-in-emiting-event)] | Stack variable cost less while used in emiting event | 14 | 1400 | 
| [[GAS&#x2011;18](#gas18-events-should-be-emitted-outside-of-loops)] | Events should be emitted outside of loops | 3 | 1125 | 
| [[GAS&#x2011;19](#gas19-empty-blocks-should-be-removed-or-emit-something)] | Empty blocks should be removed or emit something | 1 | - | 
| [[GAS&#x2011;20](#gas20-the-result-of-function-calls-should-be-cached-rather-than-re-calling-the-function)] | The result of function calls should be cached rather than re-calling the function | 1 | - | 
| [[GAS&#x2011;21](#gas21-don-t-initialize-uint-variables-with-default-value)] | Don't initialize `uint` variables with default value | 38 | - | 
| [[GAS&#x2011;22](#gas22-require-or-revert-statements-that-check-input-arguments-should-be-at-the-top-of-the-function)] | `require()` or `revert()` statements that check input arguments should be at the top of the function | 12 | - | 
| [[GAS&#x2011;23](#gas23-internal-functions-only-called-once-can-be-inlined-to-save-gas)] | `internal` functions only called once can be inlined to save gas | 55 | 1100 | 
| [[GAS&#x2011;24](#gas24-require-revert-strings-longer-than-32-bytes-cost-extra-gas)] | `require()`/`revert()` strings longer than 32 bytes cost extra gas | 105 | 1890 | 
| [[GAS&#x2011;25](#gas25-consider-merging-sequential-for-loops)] | Consider merging sequential for loops | 2 | - | 
| [[GAS&#x2011;26](#gas26-multiple-address-id-mappings-can-be-combined-into-a-single-mapping-of-an-address-id-to-a-struct-where-appropriate)] | Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct`, where appropriate | 6 | - | 
| [[GAS&#x2011;27](#gas27-optimize-names-to-save-gas)] | Optimize names to save gas | 49 | 1078 | 
| [[GAS&#x2011;28](#gas28-not-using-the-named-return-variables-anywhere-in-the-function-wast-gas)] | Not using the named return variables anywhere in the function wast gas | 4 | 12 | 
| [[GAS&#x2011;29](#gas29-enable-solidity-s-optimizer)] | Enable Solidity's optimizer | 1 | - | 
| [[GAS&#x2011;30](#gas30-structs-can-be-packed-into-fewer-storage-slots)] | Structs can be packed into fewer storage slots | 2 | 4000 | 
| [[GAS&#x2011;31](#gas31-constructors-can-be-marked-payable)] | Constructors can be marked `payable` | 10 | 210 | 
| [[GAS&#x2011;32](#gas32-using-private-rather-than-public-for-constants-saves-gas)] | Using `private` rather than `public` for constants, saves gas | 5 | - | 
| [[GAS&#x2011;33](#gas33-private-functions-only-called-once-can-be-inlined-to-save-gas)] | `private` functions only called once can be inlined to save gas | 6 | - | 
| [[GAS&#x2011;34](#gas34-remove-or-replace-unused-state-variables)] | Remove or replace unused state variables | 3 | - | 
| [[GAS&#x2011;35](#gas35-redundant-else-statement)] | Redundant else statement | 1 | - | 
| [[GAS&#x2011;36](#gas36-functions-guaranteed-to-revert-when-called-by-normal-users-can-be-marked-payable)] | Functions guaranteed to revert when called by normal users can be marked `payable` | 96 | 2016 | 
| [[GAS&#x2011;37](#gas37-avoid-updating-storage-when-the-value-hasn-t-changed-to-save-gas)] | Avoid updating storage when the value hasn't changed to save gas | 28 | 22400 | 
| [[GAS&#x2011;38](#gas38-use-shift-right-instead-of-division-if-possible-to-save-gas)] | Use shift Right instead of division if possible to save gas | 4 | 80 | 
| [[GAS&#x2011;39](#gas39-use-shift-left-instead-of-multiplication-if-possible-to-save-gas)] | Use shift Left instead of multiplication if possible to save gas | 19 | - | 
| [[GAS&#x2011;40](#gas40-usage-of-uints-ints-smaller-than-32-bytes-256-bits-incurs-overhead)] | Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead | 178 | - | 
| [[GAS&#x2011;41](#gas41-the-use-of-a-logical-and-in-place-of-double-if-is-slightly-less-gas-efficient-in-instances-where-there-isn-t-a-corresponding-else-statement-for-the-given-if-statement)] | The use of a logical AND in place of double if is slightly less gas efficient in instances where there isn't a corresponding else statement for the given if statement | 7 | 105 | 
| [[GAS&#x2011;42](#gas42-splitting-require-statements-that-use-saves-gas)] | Splitting `require()` statements that use `&&` saves gas | 3 | 9 | 
| [[GAS&#x2011;43](#gas43-stack-variable-used-as-a-cheaper-cache-for-a-state-variable-is-only-used-once)] | Stack variable used as a cheaper cache for a state variable is only used once | 312 | 936 | 
| [[GAS&#x2011;44](#gas44-using-storage-instead-of-memory-for-structs-arrays-saves-gas)] | Using `storage` instead of `memory` for structs/arrays saves gas | 11 | 46200 | 
| [[GAS&#x2011;45](#gas45-costs-less-gas-than)] | `>=`/`<=` costs less gas than `>`/`<` | 60 | 180 | 
| [[GAS&#x2011;46](#gas46-using-this-fn-wastes-gas)] | Using `this.<fn>()` wastes gas | 3 | 300 | 
| [[GAS&#x2011;47](#gas47-use-assembly-to-validate-msg-sender)] | Use assembly to validate `msg.sender` | 36 | 432 | 
| [[GAS&#x2011;48](#gas48-can-make-the-variable-outside-the-loop-to-save-gas)] | Can make the variable outside the loop to save gas | 53 | - | 
| [[GAS&#x2011;49](#gas49-consider-activating-via-ir-for-deploying)] | Consider activating via-ir for deploying | 3 | 750 | 
| [[GAS&#x2011;50](#gas50-i-costs-less-gas-than-i-especially-when-it-s-used-in-for-loops-i-i-too)] | `++i` costs less gas than `i++`, especially when it's used in `for`-loops (`--i`/`i--` too) | 8 | - | 
| [[GAS&#x2011;51](#gas51-unnecessary-casting-as-variable-is-already-of-the-same-type)] | Unnecessary casting as variable is already of the same type | 3 | 66 | 
| [[GAS&#x2011;52](#gas52-structs-can-be-packed-into-fewer-storage-slots-by-truncating-timestamp-bytes)] | Structs can be packed into fewer storage slots by truncating timestamp bytes | 2 | - | 
| [[GAS&#x2011;53](#gas53-stat-variables-can-be-packed-into-fewer-storage-slots-by-truncating-timestamp-bytes)] | Stat variables can be packed into fewer storage slots by truncating timestamp bytes | 1 | - | 
| [[GAS&#x2011;54](#gas54-state-variables-can-be-packed-into-fewer-storage-slots)] | State variables can be packed into fewer storage slots | 1 | 2000 | 
| [[GAS&#x2011;55](#gas55-use-do-while-loops-instead-of-for-loops)] | Use `do while` loops instead of `for` loops | 35 | 4235 | 
| [[GAS&#x2011;56](#gas56-use-for-mapping-s)] | Use `+=` for `mapping`s | 1 | - | 
| [[GAS&#x2011;57](#gas57-avoid-transferring-amounts-of-zero-in-order-to-save-gas)] | Avoid transferring amounts of zero in order to save gas | 2 | - | 
| [[GAS&#x2011;58](#gas58-when-no-addresses-are-used-abi-encodepacked-outperforms-abi-encode-in-efficiency)] | When no `addresses` are used `abi.encodepacked()` Outperforms `abi.encode()` in Efficiency | 28 | 1708 | 
| [[GAS&#x2011;59](#gas59-a-modifier-used-only-once-and-not-being-inherited-should-be-inlined-to-save-gas)] | A `modifier` used only once and not being inherited should be inlined to save gas | 7 | - | 
| [[GAS&#x2011;60](#gas60-simple-checks-for-zero-uint-can-be-done-using-assembly-to-save-gas)] | Simple checks for zero `uint` can be done using assembly to save gas | 48 | 288 | 
| [[GAS&#x2011;61](#gas61-i-i-should-be-unchecked-i-unchecked-i-when-it-is-not-possible-for-them-to-overflow-as-is-the-case-when-used-in-for-and-while-loops)] | `++i`/`i++` should be `unchecked{++i}`/`unchecked{i++}` when it is not possible for them to overflow, as is the case when used in `for`- and `while`-loops | 12 | - | 
| [[GAS&#x2011;62](#gas62-do-not-cache-constants-to-save-gas)] | Do not cache constants to save gas | 1 | - | 
| [[GAS&#x2011;63](#gas63-using-private-for-constants-saves-gas)] | Using `private` for constants saves gas | 10 | - | 
| [[GAS&#x2011;64](#gas64-initializer-can-be-marked-payable)] | Initializer can be marked `payable` | 9 | 189 | 
| [[GAS&#x2011;65](#gas65-avoid-caching-global-special-variables)] | Avoid caching global special variables | 1 | 12 | 
| [[GAS&#x2011;66](#gas66-use-s-x-s-x-y-instead-of-s-x-y-for-memory-structs)] | Use `s.x = s.x + y` instead of `s.x += y` for memory structs | 1 | 100 | 
| [[GAS&#x2011;67](#gas67-using-constant-s-instead-of-enum-can-save-gas)] | Using `constant`s instead of `enum` can save gas | 15 | - | 
| [[GAS&#x2011;68](#gas68-gas-savings-can-be-achieved-by-changing-the-model-for-assigning-value-to-the-structure-123-gas)] | Gas savings can be achieved by changing the model for assigning value to the structure ***123 gas*** | 17 | 2091 | 
| [[GAS&#x2011;69](#gas69-refactor-modifiers-to-call-a-local-function)] | Refactor modifiers to call a local function | 14 | 14000 | 
| [[GAS&#x2011;70](#gas70-use-solady-library-where-possible-to-save-gas)] | Use `solady` library where possible to save gas | 1 | - | 
| [[GAS&#x2011;71](#gas71-consider-using-oz-enumerateset-in-place-of-nested-mappings)] | Consider using OZ EnumerateSet in place of nested mappings | 9 | 9000 | 
| [[GAS&#x2011;72](#gas72-consider-using-solady-s-fixedpointmathlib)] | Consider using solady's 'FixedPointMathLib' | 69 | - | 
| [[GAS&#x2011;73](#gas73-counting-down-in-for-statements-is-more-gas-efficient)] | Counting down in for statements is more gas efficient | 18 | - | 
| [[GAS&#x2011;74](#gas74-trade-offs-between-modifiers-and-internal-functions)] | Trade-offs Between Modifiers and Internal Functions | 196 | 6076 | 
| [[GAS&#x2011;75](#gas75-optimize-deployment-size-by-fine-tuning-ipfs-hash)] | Optimize Deployment Size by Fine-tuning IPFS Hash | 103 | 1091800 | 
| [[GAS&#x2011;76](#gas76-use-assembly-scratch-space-to-build-calldata-for-external-calls)] | Use assembly scratch space to build calldata for external calls | 57 | 12540 | 
| [[GAS&#x2011;77](#gas77-use-more-recent-openzeppelin-version-for-gas-boost)] | Use more recent OpenZeppelin version for gas boost | 21 | - | 
| [[GAS&#x2011;78](#gas78-use-array-unsafeaccess-to-avoid-repeated-array-length-checks)] | Use Array.unsafeAccess() to avoid repeated array length checks | 40 | 84000 | 
| [[GAS&#x2011;79](#gas79-state-variables-only-set-in-their-definitions-should-be-declared-constant)] | State variables only set in their definitions should be declared constant | 3 | 6291 | 
| [[GAS&#x2011;80](#gas80-combine-mapping-s-referenced-in-the-same-function-by-the-same-key)] | Combine `mapping`s referenced in the same function by the same key | 17 | 714 | 
| [[GAS&#x2011;81](#gas81-consider-pre-calculating-the-address-of-address-this-to-save-gas)] | Consider pre-calculating the address of `address(this)` to save gas | 21 | - | 
| [[GAS&#x2011;82](#gas82-avoid-emitting-event-on-every-iteration)] | Avoid emitting event on every iteration | 3 | 1125 | 
| [[GAS&#x2011;83](#gas83-memory-safe-annotation-missing)] | Memory-safe annotation missing | 71 | - | 
| [[GAS&#x2011;84](#gas84-reduce-deployment-costs-by-tweaking-contracts-metadata)] | Reduce deployment costs by tweaking contracts' metadata | 103 | - | 
| [[GAS&#x2011;85](#gas85-use-the-inputs-results-of-assignments-rather-than-re-reading-state-variables)] | Use the inputs/results of assignments rather than re-reading state variables | 3 | 291 | 

Total: 2742 instances over 85 issues with **1339632 gas** saved




## Gas Optimizations

### [GAS&#x2011;1] Multiple accesses of a mapping/array should use a local variable cache 
The instances below point to the second+ access of a value inside a mapping/array, within a function. Caching a mapping's value in a local `storage` or `calldata` variable when the value is accessed [multiple times](https://gist.github.com/IllIllI000/ec23a57daa30a8f8ca8b9681c8ccefb0), saves **~42 gas per access** due to not having to recalculate the key's keccak256 hash (Gkeccak256 - **30 gas**) and that calculation's associated stack operations. Caching an array's struct avoids recalculating the array offsets into memory/calldata


*There are 42 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/Compressor.sol

174:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L174-L174) 


```solidity

File: contracts/ContractDeployer.sol

249:             sumOfValues += _deployments[i].value;

254:             this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L249-L249) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L254-L254)


```solidity

File: contracts/ImmutableSimulator.sol

40:                 bytes32 value = _immutables[i].value;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L40-L40) 


```solidity

File: contracts/L1Messenger.sol

219:             l2ToL1LogsTreeArray[i] = L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH;

225:                 l2ToL1LogsTreeArray[i] = keccak256(

280:             uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L219-L219) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L225-L225), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L280-L280)


```solidity

File: contracts/L2BaseToken.sol

43:             balance[_from] = fromBalance - _amount;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L43-L43) 


```solidity

File: contracts/NonceHolder.sol

72:             rawNonces[addressAsKey] = (oldRawNonce + _value);

118:             rawNonces[addressAsKey] = oldRawNonce + 1;

144:             rawNonces[addressAsKey] = (oldRawNonce + DEPLOY_NONCE_MULTIPLIER);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L72-L72) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L118-L118), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L144-L144)


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

187:         delete depositAmount[_depositSender][_l1Token][_l2TxHash];


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L187-L187) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

122:             chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =

123:                 chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +

133:             chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;

221:                 l2Contract: l2BridgeAddress[_chainId],

237:         require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");

343:                 delete depositHappened[_chainId][_l2TxHash];

349:             require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");

417:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");

439:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds

586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L122-L122) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L123-L123), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L133-L133), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L221-L221), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L237-L237), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L343-L343), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L349-L349), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L417-L417), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L439-L439), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L586-L586)


```solidity

File: contracts/bridgehub/Bridgehub.sol

84:             !stateTransitionManagerIsRegistered[_stateTransitionManager],

97:         stateTransitionManagerIsRegistered[_stateTransitionManager] = false;

102:         require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L84-L84) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L97-L97), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L102-L102), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L132-L132)


```solidity

File: contracts/governance/Governance.sol

226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L226-L226) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L226-L226)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

282:         stateTransition[_chainId] = stateTransitionAddress;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L282-L282) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

82:         validators[_chainId][_newValidator] = true;

91:         validators[_chainId][_validator] = false;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L82-L82) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L91-L91)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

408:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],

670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),

670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L353-L353) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L353-L353), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L353-L353), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L408-L408), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L670-L670), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L670-L670)


```solidity

File: contracts/state-transition/libraries/Diamond.sol

103:             address facet = facetCuts[i].facet;

104:             bool isFacetFreezable = facetCuts[i].isFreezable;

105:             bytes4[] memory selectors = facetCuts[i].selectors;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L103-L103) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L104-L104), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L105-L105)


```solidity

File: contracts/state-transition/libraries/Merkle.sol

31:                 ? _efficientHash(currentHash, _path[i])


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L31-L31) 


```solidity

File: contracts/bridge/L2SharedBridge.sol

99:             l1TokenAddress[expectedL2Token] = _l1Token;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L99-L99) 


</details>


### [GAS&#x2011;2] Use assembly to calculate hashes to save gas 
Using assembly to calculate hashes can save *** 80 gas *** per instance


*There are 61 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/BootloaderUtilities.sol

29:             txHash = keccak256(bytes.concat(signedTxHash, EfficientCall.keccak(_transaction.signature)));

120:             keccak256(

211:             keccak256(

306:             keccak256(


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L29-L29) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L120-L120), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L211-L211), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L306-L306)


```solidity

File: contracts/ContractDeployer.sol

105:         bytes32 hash = keccak256(

121:         bytes32 hash = keccak256(


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L105-L105) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L121-L121)


```solidity

File: contracts/L1Messenger.sol

95:         bytes32 hashedLog = keccak256(

106:         chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

122:         chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

164:         chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

212:             reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));

225:                 l2ToL1LogsTreeArray[i] = keccak256(

243:             reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));

259:             reconstructedChainedL1BytecodesRevealDataHash = keccak256(


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L95-L95) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L106-L106), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L122-L122), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L164-L164), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L212-L212), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L225-L225), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L243-L243), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L259-L259)


```solidity

File: contracts/SystemContext.sol

159:             hash = keccak256(abi.encode(_block));

227:         return keccak256(abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash));

234:         return keccak256(abi.encodePacked(uint32(_blockNumber)));

403:         currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L159-L159) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L227-L227), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L234-L234), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L403-L403)


```solidity

File: contracts/libraries/TransactionHelper.sol

82:     bytes32 constant EIP712_DOMAIN_TYPEHASH = keccak256("EIP712Domain(string name,string version,uint256 chainId)");

85:         keccak256(

119:         bytes32 structHash = keccak256(

133:                 keccak256(abi.encodePacked(_transaction.factoryDeps)),

138:         bytes32 domainSeparator = keccak256(

139:             abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

139:             abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

142:         return keccak256(abi.encodePacked("\x19\x01", domainSeparator, structHash));

203:             keccak256(

275:             keccak256(

347:             keccak256(


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L82-L82) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L85-L85), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L119-L119), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L133-L133), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L138-L138), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L139-L139), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L139-L139), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L142-L142), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L203-L203), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L275-L275), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L347-L347)


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

76:         bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L76-L76) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

210:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));

341:                 bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));

598:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L210-L210) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L341-L341), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L598-L598)


```solidity

File: contracts/common/Config.sol

112: bytes32 constant TWO_BRIDGES_MAGIC_VALUE = bytes32(uint256(keccak256("TWO_BRIDGES_MAGIC_VALUE")) - 1);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/Config.sol#L112-L112) 


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

12:     bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");

67:         bytes32 data = keccak256(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L12-L12) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L67-L67)


```solidity

File: contracts/governance/Governance.sol

205:         return keccak256(abi.encode(_operation));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L205-L205) 


```solidity

File: contracts/state-transition/StateTransitionManager.sol

100:         storedBatchZero = keccak256(abi.encode(batchZero));

102:         initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

138:         initialCutHash = keccak256(abi.encode(_diamondCut));

147:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

156:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

255:         bytes32 cutHashInput = keccak256(_diamondCut);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L100-L100) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L102-L102), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L138-L138), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L147-L147), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L156-L156), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L255-L255)


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

104:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L104-L104) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

63:                     keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),

313:             concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));

460:                 keccak256(

506:         bytes32 passThroughDataHash = keccak256(_batchPassThroughData(_newBatchData));

507:         bytes32 metadataHash = keccak256(_batchMetaParameters());

508:         bytes32 auxiliaryOutputHash = keccak256(

512:         return keccak256(abi.encode(passThroughDataHash, metadataHash, auxiliaryOutputHash));

545:         bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs);

588:         return keccak256(abi.encode(_storedBatchInfo));

654:             blobCommitments[versionedHashIndex] = keccak256(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L63-L63) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L313-L313), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L460-L460), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L506-L506), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L507-L507), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L508-L508), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L512-L512), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L545-L545), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L588-L588), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L654-L654)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

112:         bytes32 hashedLog = keccak256(

138:                 value: keccak256(_message.data)

332:         canonicalTxHash = keccak256(transactionEncoding);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L112-L112) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L138-L138), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L332-L332)


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

212:         bytes32 l2ProtocolUpgradeTxHash = keccak256(encodedTransaction);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L212-L212) 


```solidity

File: contracts/L2ContractHelper.sol

85:     bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");

108:         bytes32 data = keccak256(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L85-L85) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L108-L108)


```solidity

File: contracts/bridge/L2SharedBridge.sol

150:         bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L150-L150) 


</details>


### [GAS&#x2011;3] Use assembly to check for `address(0)` 
*Saves 6 gas per instance*


*There are 50 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/DefaultAccount.sol

94:         bytes32 txHash = _suggestedSignedHash != bytes32(0) ? _suggestedSignedHash : _transaction.encodeHash();

188:         return recoveredAddress == address(this) && recoveredAddress != address(0);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L94-L94) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L188-L188)


```solidity

File: contracts/KnownCodesStorage.sol

76:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L76-L76) 


```solidity

File: contracts/libraries/TransactionHelper.sol

406:         if (address(uint160(_transaction.paymaster)) != address(0)) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L406-L406) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

108:         require(_owner != address(0), "ShB owner 0");

188:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

578:             if (_refundRecipient == address(0)) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L108-L108) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L188-L188), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L563-L563), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L578-L578)


```solidity

File: contracts/bridgehub/Bridgehub.sol

130:         require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

326:         if (_refundRecipient == address(0)) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L130-L130) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L132-L132), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L326-L326)


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

41:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L41-L41) 


```solidity

File: contracts/governance/Governance.sol

42:         require(_admin != address(0), "Admin should be non zero address");

240:         require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L42-L42) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L240-L240)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

82:         require(_initializeData.governor != address(0), "StateTransition: governor zero");

246:         if (stateTransition[_chainId] != address(0)) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L82-L82) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L246-L246)


```solidity

File: contracts/state-transition/chain-deps/DiamondInit.sol

25:         require(address(_initializeData.verifier) != address(0), "vt");

26:         require(_initializeData.admin != address(0), "vy");

27:         require(_initializeData.validatorTimelock != address(0), "hc");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondInit.sol#L25-L25) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondInit.sol#L26-L26), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondInit.sol#L27-L27)


```solidity

File: contracts/state-transition/chain-deps/DiamondProxy.sol

30:         require(facetAddress != address(0), "F"); // Proxy has no facet for this selector


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondProxy.sol#L30-L30) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

191:         if (_expectedSystemContractUpgradeTxHash == bytes32(0)) {

237:         if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {

639:             require(blobVersionedHash != bytes32(0), "vh");

663:         require(versionedHash == bytes32(0), "lh");

669:                 (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||

669:                 (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||

670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),

670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L191-L191) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L237-L237), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L639-L639), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L663-L663), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L669-L669), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L669-L669), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L670-L670), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L670-L670)


```solidity

File: contracts/state-transition/chain-deps/facets/Getters.sol

183:         require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L183-L183) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

275:         address refundRecipient = _params.refundRecipient == address(0) ? _params.sender : _params.refundRecipient;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L275-L275) 


```solidity

File: contracts/state-transition/libraries/Diamond.sol

141:             require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists

161:             require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

175:         require(_facet == address(0), "a1"); // facet address must be zero

181:             require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet

279:         if (_init == address(0)) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L141-L141) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L161-L161), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L175-L175), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L181-L181), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L279-L279)


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

93:         if (_l2DefaultAccountBytecodeHash == bytes32(0)) {

110:         if (_l2BootloaderBytecodeHash == bytes32(0)) {

148:             _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) &&

149:             _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) &&

150:             _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)

249:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L93-L93) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L110-L110), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L148-L148), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L149-L149), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L150-L150), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L249-L249)


```solidity

File: contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

33:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33-L33) 


```solidity

File: contracts/bridge/L2SharedBridge.sol

55:         require(_l1Bridge != address(0), "bf");

56:         require(_l2TokenProxyBytecodeHash != bytes32(0), "df");

57:         require(_aliasedOwner != address(0), "sf");

58:         require(_l2TokenProxyBytecodeHash != bytes32(0), "df");

68:             require(_l1LegecyBridge != address(0), "bf2");

96:         if (currentL1Token == address(0)) {

129:         require(l1Token != address(0), "yh");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L55-L55) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L56-L56), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L57-L57), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L58-L58), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L68-L68), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L96-L96), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L129-L129)


```solidity

File: contracts/bridge/L2StandardERC20.sol

51:         require(_l1Address != address(0), "in6"); // Should be non-zero address


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L51-L51) 


</details>


### [GAS&#x2011;4] Use assembly in place of `abi.decode` to extract `calldata` values more efficiently 
Instead of using abi.decode, we can use assembly to decode our desired calldata values directly. This will allow us to avoid decoding calldata values that we will not use.
For more details on how to implement this, check the following [report](https://code4rena.com/reports/2023-05-juicebox#g-04-use-assembly-in-place-of-abidecode-to-extract-calldata-values-more-efficiently)


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/state-transition/chain-deps/facets/Executor.sol

617:         (, uint256 result) = abi.decode(data, (uint256, uint256));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L617-L617) 


</details>


### [GAS&#x2011;5] Optimize Address Storage Value Management with `assembly` 



*There are 14 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/bridge/L1SharedBridge.sol

96:         l1WethAddress = _l1WethAddress;

112:         l2BridgeAddress[ERA_CHAIN_ID] = ERA_ERC20_BRIDGE_ADDRESS;

143:         l2BridgeAddress[_chainId] = _l2BridgeAddress;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L96-L96) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L112-L112), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L143-L143)


```solidity

File: contracts/bridgehub/Bridgehub.sol

55:         pendingAdmin = _newPendingAdmin;

65:         admin = currentPendingAdmin;

134:         stateTransitionManager[_chainId] = _stateTransitionManager;

135:         baseToken[_chainId] = _baseToken;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L55-L55) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L65-L65), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L134-L134), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L135-L135)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

114:         pendingAdmin = _newPendingAdmin;

124:         admin = currentPendingAdmin;

234:         stateTransition[_chainId] = _stateTransitionContract;

282:         stateTransition[_chainId] = stateTransitionAddress;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L114-L114) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L124-L124), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L234-L234), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L282-L282)


```solidity

File: contracts/bridge/L2SharedBridge.sol

60:         l1Bridge = _l1Bridge;

99:             l1TokenAddress[expectedL2Token] = _l1Token;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L60-L60) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L99-L99)


```solidity

File: contracts/bridge/L2StandardERC20.sol

54:         l2Bridge = msg.sender;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L54-L54) 


</details>


### [GAS&#x2011;6] Use assembly to emit events 
We can use assembly to emit events efficiently by utilizing `scratch space` and the `free memory pointer`. This will allow us to potentially avoid memory expansion costs. Note: In order to do this optimization safely, we will need to cache and restore the free memory pointer.


*There are 77 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ContractDeployer.sol

68:         emit AccountVersionUpdated(msg.sender, _version);

86:         emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);

355:         emit ContractDeployed(_sender, _bytecodeHash, _newAddress);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L68-L68) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L86-L86), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L355-L355)


```solidity

File: contracts/KnownCodesStorage.sol

59:             emit MarkedAsKnown(_bytecodeHash, _shouldSendToL1);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L59-L59) 


```solidity

File: contracts/L1Messenger.sol

111:         emit L2ToL1LogSent(_l2ToL1Log);

156:         emit L1MessageSent(msg.sender, hash, _message);

181:         emit BytecodeL1PublicationRequested(_bytecodeHash);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L111-L111) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L156-L156), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L181-L181)


```solidity

File: contracts/L2BaseToken.sol

49:         emit Transfer(_from, _to, _amount);

67:         emit Mint(_account, _amount);

79:         emit Withdrawal(msg.sender, _l1Receiver, amount);

92:         emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L49-L49) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L67-L67), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L79-L79), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L92-L92)


```solidity

File: contracts/NonceHolder.sol

96:         emit ValueSetUnderNonce(msg.sender, _key, _value);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L96-L96) 


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

155:         emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);

199:         emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);

225:         emit WithdrawalFinalized(l1Receiver, l1Token, amount);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L155-L155) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L199-L199), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L225-L225)


```solidity

File: contracts/bridge/L1SharedBridge.sol

168:         emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);

227:         emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);

239:         emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);

367:         emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);

454:         emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);

602:         emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L168-L168) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L227-L227), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L239-L239), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L367-L367), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L454-L454), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L602-L602)


```solidity

File: contracts/bridgehub/Bridgehub.sol

56:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

68:         emit NewPendingAdmin(currentPendingAdmin, address(0));

69:         emit NewAdmin(previousAdmin, pendingAdmin);

145:         emit NewChain(_chainId, _stateTransitionManager, _admin);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L56-L56) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L68-L68), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L69-L69), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L145-L145)


```solidity

File: contracts/governance/Governance.sol

47:         emit ChangeSecurityCouncil(address(0), _securityCouncil);

50:         emit ChangeMinDelay(0, _minDelay);

132:         emit TransparentOperationScheduled(id, _delay, _operation);

144:         emit ShadowOperationScheduled(_id, _delay);

157:         emit OperationCancelled(_id);

180:         emit OperationExecuted(id);

199:         emit OperationExecuted(id);

250:         emit ChangeMinDelay(minDelay, _newDelay);

257:         emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L47-L47) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L50-L50), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L132-L132), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L144-L144), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L157-L157), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L180-L180), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L199-L199), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L250-L250), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L257-L257)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

115:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

127:         emit NewPendingAdmin(currentPendingAdmin, address(0));

128:         emit NewAdmin(previousAdmin, pendingAdmin);

227:         emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);

235:         emit StateTransitionNewChain(_chainId, _stateTransitionContract);

287:         emit StateTransitionNewChain(_chainId, stateTransitionAddress);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L115-L115) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L127-L127), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L128-L128), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L227-L227), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L235-L235), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L287-L287)


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

83:         emit ValidatorAdded(_chainId, _newValidator);

92:         emit ValidatorRemoved(_chainId, _validator);

98:         emit NewExecutionDelay(_executionDelay);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L83-L83) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L92-L92), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L98-L98)


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

28:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

40:         emit NewPendingAdmin(pendingAdmin, address(0));

41:         emit NewAdmin(previousAdmin, pendingAdmin);

47:         emit ValidatorStatusUpdate(_validator, _active);

54:         emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);

63:         emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);

75:         emit NewFeeParams(oldFeeParams, _newFeeParams);

86:         emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator);

92:         emit ValidiumModeStatusUpdate(_validiumMode);

115:         emit ExecuteUpgrade(_diamondCut);

125:         emit ExecuteUpgrade(_diamondCut);

139:         emit Freeze();

149:         emit Unfreeze();


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L28-L28) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L40-L40), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L41-L41), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L47-L47), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L54-L54), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L63-L63), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L75-L75), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L86-L86), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L92-L92), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L115-L115), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L125-L125), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L139-L139), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L149-L149)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

261:             emit BlockCommit(

299:             emit BlockCommit(

353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

436:         emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

496:         emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L261-L261) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L299-L299), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L353-L353), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L436-L436), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L496-L496)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

343:         emit NewPriorityRequest(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L343-L343) 


```solidity

File: contracts/state-transition/libraries/Diamond.sol

121:         emit DiamondCut(facetCuts, initAddress, initCalldata);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L121-L121) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

87:         emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);

104:         emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);

121:         emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);

137:         emit NewVerifier(address(oldVerifier), address(_newVerifier));

157:         emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

256:         emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L87-L87) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L104-L104), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L121-L121), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L137-L137), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L157-L157), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L256-L256)


```solidity

File: contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

40:         emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);

67:         emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L40-L40) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L67-L67)


```solidity

File: contracts/bridge/L2SharedBridge.sol

105:         emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);

134:         emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L105-L105) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L134-L134)


```solidity

File: contracts/bridge/L2StandardERC20.sol

101:         emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);

126:         emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);

147:         emit BridgeMint(_to, _amount);

156:         emit BridgeBurn(_from, _amount);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L101-L101) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L126-L126), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L147-L147), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L156-L156)


</details>


### [GAS&#x2011;7] Using bools for storage incurs overhead 
Use uint256(1) and uint256(2) for true/false to avoid a Gwarmaccess (100 gas), and to avoid Gsset (20000 gas) when changing from 'false' to 'true', after having been 'true' in the past. See [source](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27).


*There are 19 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ContractDeployer.sol

//@audit change `callConstructor` to `uint256`
197:     struct ForceDeployment {
198:         // The bytecode hash to put on an address
199:         bytes32 bytecodeHash;
200:         // The address on which to deploy the bytecodehash to
201:         address newAddress;
202:         // Whether to run the constructor on the force deployment
203:         bool callConstructor;
204:         // The value with which to initialize a contract
205:         uint256 value;
206:         // The constructor calldata
207:         bytes input;
208:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L197-L208) 


```solidity

File: contracts/interfaces/IL1Messenger.sol

//@audit change `isService` to `uint256`
14: struct L2ToL1Log {
15:     uint8 l2ShardId;
16:     bool isService;
17:     uint16 txNumberInBlock;
18:     address sender;
19:     bytes32 key;
20:     bytes32 value;
21: }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IL1Messenger.sol#L14-L21) 


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

//@audit avoid using `bool` type for mapping values
27:     mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L27-L27) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

//@audit avoid using `bool` type for mapping values
57:     mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))

//@audit avoid using `bool` type for mapping values
61:     mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L57-L57) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L61-L61)


```solidity

File: contracts/bridgehub/Bridgehub.sol

//@audit avoid using `bool` type for mapping values
21:     mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;

//@audit avoid using `bool` type for mapping values
23:     mapping(address _token => bool) public tokenIsRegistered;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L21-L21) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L23-L23)


```solidity

File: contracts/common/Messaging.sol

//@audit change `isService` to `uint256`
23: struct L2Log {
24:     uint8 l2ShardId;
25:     bool isService;
26:     uint16 txNumberInBatch;
27:     address sender;
28:     bytes32 key;
29:     bytes32 value;
30: }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/Messaging.sol#L23-L30) 


```solidity

File: contracts/common/interfaces/IL2ContractDeployer.sol

//@audit change `callConstructor` to `uint256`
16:     struct ForceDeployment {
17:         bytes32 bytecodeHash;
18:         address newAddress;
19:         bool callConstructor;
20:         uint256 value;
21:         bytes input;
22:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/interfaces/IL2ContractDeployer.sol#L16-L22) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

//@audit avoid using `bool` type for mapping values
50:     mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L50-L50) 


```solidity

File: contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

//@audit change `approvedBySecurityCouncil` to `uint256`
27: struct UpgradeStorage {
28:     bytes32 proposedUpgradeHash;
29:     UpgradeState state;
30:     address securityCouncil;
31:     bool approvedBySecurityCouncil;
32:     uint40 proposedUpgradeTimestamp;
33:     uint40 currentProposalId;
34: }

//@audit change `zkPorterIsAvailable` to `uint256`
066: struct ZkSyncStateTransitionStorage {
067:     /// @dev Storage of variables needed for deprecated diamond cut facet
068:     uint256[7] __DEPRECATED_diamondCutStorage;
069:     /// @notice Address which will exercise critical changes to the Diamond Proxy (upgrades, freezing & unfreezing). Replaced by STM
070:     address __DEPRECATED_governor;
071:     /// @notice Address that the governor proposed as one that will replace it
072:     address __DEPRECATED_pendingGovernor;
073:     /// @notice List of permitted validators
074:     mapping(address validatorAddress => bool isValidator) validators;
075:     /// @dev Verifier contract. Used to verify aggregated proof for batches
076:     IVerifier verifier;
077:     /// @notice Total number of executed batches i.e. batches[totalBatchesExecuted] points at the latest executed batch
078:     /// (batch 0 is genesis)
079:     uint256 totalBatchesExecuted;
080:     /// @notice Total number of proved batches i.e. batches[totalBatchesProved] points at the latest proved batch
081:     uint256 totalBatchesVerified;
082:     /// @notice Total number of committed batches i.e. batches[totalBatchesCommitted] points at the latest committed
083:     /// batch
084:     uint256 totalBatchesCommitted;
085:     /// @dev Stored hashed StoredBatch for batch number
086:     mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
087:     /// @dev Stored root hashes of L2 -> L1 logs
088:     mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;
089:     /// @dev Container that stores transactions requested from L1
090:     PriorityQueue.Queue priorityQueue;
091:     /// @dev The smart contract that manages the list with permission to call contract functions
092:     address __DEPRECATED_allowList;
093:     /// @notice Part of the configuration parameters of ZKP circuits. Used as an input for the verifier smart contract
094:     VerifierParams verifierParams;
095:     /// @notice Bytecode hash of bootloader program.
096:     /// @dev Used as an input to zkp-circuit.
097:     bytes32 l2BootloaderBytecodeHash;
098:     /// @notice Bytecode hash of default account (bytecode for EOA).
099:     /// @dev Used as an input to zkp-circuit.
100:     bytes32 l2DefaultAccountBytecodeHash;
101:     /// @dev Indicates that the porter may be touched on L2 transactions.
102:     /// @dev Used as an input to zkp-circuit.
103:     bool zkPorterIsAvailable;
104:     /// @dev The maximum number of the L2 gas that a user can request for L1 -> L2 transactions
105:     /// @dev This is the maximum number of L2 gas that is available for the "body" of the transaction, i.e.
106:     /// without overhead for proving the batch.
107:     uint256 priorityTxMaxGasLimit;
108:     /// @dev Storage of variables needed for upgrade facet
109:     UpgradeStorage __DEPRECATED_upgrades;
110:     /// @dev A mapping L2 batch number => message number => flag.
111:     /// @dev The L2 -> L1 log is sent for every withdrawal, so this mapping is serving as
112:     /// a flag to indicate that the message was already processed.
113:     /// @dev Used to indicate that eth withdrawal was already processed
114:     mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;
115:     /// @dev The most recent withdrawal time and amount reset
116:     uint256 __DEPRECATED_lastWithdrawalLimitReset;
117:     /// @dev The accumulated withdrawn amount during the withdrawal limit window
118:     uint256 __DEPRECATED_withdrawnAmountInWindow;
119:     /// @dev A mapping user address => the total deposited amount by the user
120:     mapping(address => uint256) __DEPRECATED_totalDepositedAmountPerUser;
121:     /// @dev Stores the protocol version. Note, that the protocol version may not only encompass changes to the
122:     /// smart contracts, but also to the node behavior.
123:     uint256 protocolVersion;
124:     /// @dev Hash of the system contract upgrade transaction. If 0, then no upgrade transaction needs to be done.
125:     bytes32 l2SystemContractsUpgradeTxHash;
126:     /// @dev Batch number where the upgrade transaction has happened. If 0, then no upgrade transaction has happened
127:     /// yet.
128:     uint256 l2SystemContractsUpgradeBatchNumber;
129:     /// @dev Address which will exercise non-critical changes to the Diamond Proxy (changing validator set & unfreezing)
130:     address admin;
131:     /// @notice Address that the admin proposed as one that will replace admin role
132:     address pendingAdmin;
133:     /// @dev Fee params used to derive gasPrice for the L1->L2 transactions. For L2 transactions,
134:     /// the bootloader gives enough freedom to the operator.
135:     FeeParams feeParams;
136:     /// @dev Address of the blob versioned hash getter smart contract used for EIP-4844 versioned hashes.
137:     address blobVersionedHashRetriever;
138:     /// new fields
139:     /// @dev The chainId of the chain
140:     uint256 chainId;
141:     /// @dev The address of the bridgehub
142:     address bridgehub;
143:     /// @dev The address of the StateTransitionManager
144:     address stateTransitionManager;
145:     /// @dev The address of the baseToken contract. Eth is address(1)
146:     address baseToken;
147:     /// @dev The address of the baseTokenbridge. Eth also uses the shared bridge
148:     address baseTokenBridge;
149:     /// @notice gasPriceMultiplier for each baseToken, so that each L1->L2 transaction pays for its transaction on the destination
150:     /// we multiply by the nominator, and divide by the denominator
151:     uint128 baseTokenGasPriceMultiplierNominator;
152:     uint128 baseTokenGasPriceMultiplierDenominator;
153: }

//@audit avoid using `bool` type for mapping values
74:     mapping(address validatorAddress => bool isValidator) validators;

//@audit avoid using `bool` type for mapping values
114:     mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L27-L34) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L66-L153), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L74-L74), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L114-L114)


```solidity

File: contracts/state-transition/libraries/Diamond.sol

//@audit change `isFreezable` to `uint256`
30:     struct SelectorToFacet {
31:         address facetAddress;
32:         uint16 selectorPosition;
33:         bool isFreezable;
34:     }

//@audit change `isFrozen` to `uint256`
50:     struct DiamondStorage {
51:         mapping(bytes4 selector => SelectorToFacet selectorInfo) selectorToFacet;
52:         mapping(address facetAddress => FacetToSelectors facetInfo) facetToSelectors;
53:         address[] facets;
54:         bool isFrozen;
55:     }

//@audit change `isFreezable` to `uint256`
62:     struct FacetCut {
63:         address facet;
64:         Action action;
65:         bool isFreezable;
66:         bytes4[] selectors;
67:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L30-L34) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L50-L55), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L62-L67)


```solidity

File: contracts/L2ContractHelper.sol

//@audit change `callConstructor` to `uint256`
37:     struct ForceDeployment {
38:         bytes32 bytecodeHash;
39:         address newAddress;
40:         bool callConstructor;
41:         uint256 value;
42:         bytes input;
43:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L37-L43) 


```solidity

File: contracts/bridge/L2StandardERC20.sol

//@audit change `ignoreName` to `uint256`
//@audit change `ignoreSymbol` to `uint256`
//@audit change `ignoreDecimals` to `uint256`
20:     struct ERC20Getters {
21:         bool ignoreName;
22:         bool ignoreSymbol;
23:         bool ignoreDecimals;
24:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L20-L24) 


</details>


### [GAS&#x2011;8] Cache array length outside of loop 
If not cached, the solidity compiler will always read the length of the array during each iteration. That is, if it is a storage array, this is an extra sload operation (100 additional extra gas for each iteration except for the first) and if it is a memory array, this is an extra mload operation (3 additional gas for each iteration except for the first).


*There are 11 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/Compressor.sol

61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L61-L61) 


```solidity

File: contracts/governance/Governance.sol

225:         for (uint256 i = 0; i < _calls.length; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L225-L225) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

116:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

135:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

185:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

209:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L116-L116) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L135-L135), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L185-L185), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L209-L209)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

142:         for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

257:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

289:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

636:         for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L142-L142) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L257-L257), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L289-L289), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L636-L636)


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L226-L226) 


</details>


### [GAS&#x2011;9] State variables should be cached in stack variables rather than re-reading them from storage 
The instances below point to the second+ access of a state variable within a function. Caching of a state variable replaces each Gwarmaccess (100 gas) with a much cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses.

*Saves 100 gas per instance*


*There are 4 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/bridgehub/Bridgehub.sol

69:         emit NewAdmin(previousAdmin, pendingAdmin);

140:             address(sharedBridge),


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L69-L69) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L140-L140)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

128:         emit NewAdmin(previousAdmin, pendingAdmin);

216:             newProtocolVersion: protocolVersion


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L128-L128) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L216-L216)


</details>


### [GAS&#x2011;10] With assembly, `.call (bool success)` transfer can be done gas-optimized 
`return` data `(bool success,)` has to be stored due to EVM architecture, but in a usage like below, `out` and `outsize` values are given (0,0), this storage disappears and gas optimization is provided.


*There are 5 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ComplexUpgrader.sol

25:         (bool success, bytes memory returnData) = _delegateTo.delegatecall(_calldata);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ComplexUpgrader.sol#L25-L25) 


```solidity

File: contracts/libraries/EfficientCall.sol

178:             success := delegatecall(_address, callAddr, 0, 0xFFFF, 0, 0)


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L178-L178) 


```solidity

File: contracts/governance/Governance.sol

226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L226-L226) 


```solidity

File: contracts/state-transition/chain-deps/DiamondProxy.sol

39:             let result := delegatecall(gas(), facetAddress, ptr, calldatasize(), 0, 0)


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondProxy.sol#L39-L39) 


```solidity

File: contracts/state-transition/libraries/Diamond.sol

283:             (bool success, bytes memory data) = _init.delegatecall(_calldata);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L283-L283) 


</details>


### [GAS&#x2011;11] Add `unchecked {}` for subtractions where the operands cannot underflow because of a previous `require()` or `if`-statement 
`require(a <= b); x = b - a` => `require(a <= b); unchecked { x = b - a }`


*There are 6 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/MsgValueSimulator.sol

54:             ? gasInContext - MSG_VALUE_SIMULATOR_STIPEND_GAS


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/MsgValueSimulator.sol#L54-L54) 


```solidity

File: contracts/SystemContext.sol

119:         return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;

144:         if (blockNumber <= _block || blockNumber - _block > 256) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L119-L119) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L144-L144)


```solidity

File: contracts/bridge/L1SharedBridge.sol

132:             require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L132-L132) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

243:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L243-L243) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

28:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L28-L28) 


</details>


### [GAS&#x2011;12] `x += y` costs more gas than `x = x + y` for state variables 
Not inlining costs 20 to 40 gas because of two extra JUMP instructions and additional stack operations needed for function calls.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/L2BaseToken.sol

65:         totalSupply += _amount;

107:             totalSupply -= amount;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L65-L65) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L107-L107)


```solidity

File: contracts/SystemContext.sol

483:         txNumberInBlock += 1;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L483-L483) 


</details>


### [GAS&#x2011;13] Don't compare boolean expressions to boolean literals 
`if (<x> == true)` => `if (<x>)`, `if (<x> == false)` => `if (!<x>)`


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/state-transition/ValidatorTimelock.sol

The left expression is already a boolean expression
68:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L68-L68) 


</details>


### [GAS&#x2011;14] Use custom errors rather than `revert()`/`require()` strings to save gas 
Custom errors are available from solidity version 0.8.4. Custom errors save [**~50 gas**](https://gist.github.com/IllIllI000/ad1bd0d29a0101b25e57c293b4b0c746) each time they're hit by [avoiding having to allocate and store the revert string](https://blog.soliditylang.org/2021/04/21/custom-errors/#errors-in-depth). Not defining the strings also save deployment gas


*There are 340 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/AccountCodeStorage.sol

26:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

37:         require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");

48:         require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");

57:         require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L26-L26) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L37-L37), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L48-L48), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L57-L57)


```solidity

File: contracts/BootloaderUtilities.sol

37:             revert("Unsupported tx type");

92:             require(vInt == 27 || vInt == 28, "Invalid v value");

191:             require(vInt == 27 || vInt == 28, "Invalid v value");

286:             require(vInt == 27 || vInt == 28, "Invalid v value");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L37-L37) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L92-L92), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L191-L191), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L286-L286)


```solidity

File: contracts/ComplexUpgrader.sol

22:         require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");

24:         require(_delegateTo.code.length > 0, "Delegatee is an EOA");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ComplexUpgrader.sol#L22-L22) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ComplexUpgrader.sol#L24-L24)


```solidity

File: contracts/Compressor.sol

51:             require(
52:                 encodedData.length * 4 == _bytecode.length,
53:                 "Encoded data length should be 4 times shorter than the original bytecode"
54:             );

56:             require(
57:                 dictionary.length / 8 <= encodedData.length / 2,
58:                 "Dictionary should have at most the same number of entries as the encoded data"
59:             );

63:                 require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

68:                 require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");

119:         require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");

140:             require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");

156:         require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");

171:             require(enumIndex == compressedEnumIndex, "rw: enum key mismatch");

187:         require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");

230:                 require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");

232:                 require(
233:                     _initialValue + convertedValue == _finalValue,
234:                     "add: initial plus converted not equal to final"
235:                 );

237:                 require(
238:                     _initialValue - convertedValue == _finalValue,
239:                     "sub: initial minus converted not equal to final"
240:                 );

242:                 revert("unsupported operation");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L51-L54) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L56-L59), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L63-L63), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L68-L68), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L119-L119), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L140-L140), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L156-L156), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L171-L171), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L187-L187), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L230-L230), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L232-L235), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L237-L240), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L242-L242)


```solidity

File: contracts/ContractDeployer.sol

29:         require(msg.sender == address(this), "Callable only by self");

77:         require(
78:             _nonceOrdering == AccountNonceOrdering.Arbitrary &&
79:                 currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
80:             "It is only possible to change from sequential to arbitrary ordering"
81:         );

239:         require(
240:             msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
241:             "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
242:         );

251:         require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");

264:         require(_bytecodeHash != bytes32(0x0), "BytecodeHash cannot be zero");

265:         require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

268:         require(
269:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0,
270:             "Code hash is non-zero"
271:         );

273:         require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied");

303:         require(knownCodeMarker > 0, "The code hash is not known");

350:             require(value == 0, "The value must be zero if we do not call the constructor");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L29-L29) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L77-L81), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L239-L242), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L251-L251), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L264-L264), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L265-L265), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L268-L271), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L273-L273), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L303-L303), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L350-L350)


```solidity

File: contracts/DefaultAccount.sol

100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

160:         require(_signature.length == 65, "Signature length is incorrect");

173:         require(v == 27 || v == 28, "v is neither 27 nor 28");

184:         require(uint256(s) <= 0x7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF5D576E7357A4501DDFE92F46681B20A0, "Invalid s");

202:         require(success, "Failed to pay the fee to the operator");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L100-L100) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L160-L160), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L173-L173), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L184-L184), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L202-L202)


```solidity

File: contracts/ImmutableSimulator.sol

35:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L35-L35) 


```solidity

File: contracts/KnownCodesStorage.sol

20:         require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");

76:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");

78:         require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L20-L20) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L76-L76), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L78-L78)


```solidity

File: contracts/L1Messenger.sol

201:         require(numberOfL2ToL1Logs <= L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, "Too many L2->L1 logs");

214:         require(
215:             reconstructedChainedLogsHash == chainedLogsHash,
216:             "reconstructedChainedLogsHash is not equal to chainedLogsHash"
217:         );

245:         require(
246:             reconstructedChainedMessagesHash == chainedMessagesHash,
247:             "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
248:         );

269:         require(
270:             reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
271:             "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
272:         );

279:         require(
280:             uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
281:                 STATE_DIFF_COMPRESSION_VERSION_NUMBER,
282:             "state diff compression version mismatch"
283:         );

298:         require(calldataPtr <= MAX_ALLOWED_PUBDATA_PER_BATCH, "L1 Messenger pubdata is too long");

315:         require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L201-L201) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L214-L217), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L245-L248), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L269-L272), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L279-L283), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L298-L298), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L315-L315)


```solidity

File: contracts/L2BaseToken.sol

33:         require(
34:             msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
35:                 msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
36:                 msg.sender == BOOTLOADER_FORMAL_ADDRESS,
37:             "Only system contracts with special access can call this method"
38:         );

41:         require(fromBalance >= _amount, "Transfer amount exceeds balance");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L33-L38) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L41-L41)


```solidity

File: contracts/MsgValueSimulator.sol

60:         require(to != address(this), "MsgValueSimulator calls itself");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/MsgValueSimulator.sol#L60-L60) 


```solidity

File: contracts/NonceHolder.sol

66:         require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");

85:         require(_value != 0, "Nonce value cannot be set to 0");

89:             require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");

115:         require(oldMinNonce == _expectedNonce, "Incorrect nonce");

136:         require(
137:             msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
138:             "Only the contract deployer can increment the deployment nonce"
139:         );

170:             revert("Reusing the same nonce twice");

172:             revert("The nonce was not set as used");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L66-L66) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L85-L85), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L89-L89), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L115-L115), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L136-L139), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L170-L170), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L172-L172)


```solidity

File: contracts/PubdataChunkPublisher.sol

22:         require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L22-L22) 


```solidity

File: contracts/SystemContext.sol

242:         require(_isFirstInBatch, "Upgrade transaction must be first");

245:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

249:             require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");

287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

351:             require(
352:                 _l2BlockTimestamp >= currentBatchTimestamp,
353:                 "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
354:             );

355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

367:             require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");

368:             require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");

369:             require(
370:                 _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
371:                 "The previous hash of the same L2 block must be same"
372:             );

373:             require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");

385:             require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");

386:             require(
387:                 _l2BlockTimestamp > currentL2BlockTimestamp,
388:                 "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
389:             );

394:             revert("Invalid new L2 block number");

413:         require(currentBatchNumber > 0, "The current batch number must be greater than 0");

429:         require(
430:             _newTimestamp > currentBlockTimestamp,
431:             "The timestamp of the batch must be greater than the timestamp of the previous block"
432:         );

451:         require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");

452:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L242-L242) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L245-L245), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L249-L249), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L287-L287), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L351-L354), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L355-L355), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L367-L367), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L368-L368), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L369-L372), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L373-L373), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L385-L385), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L386-L389), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L394-L394), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L413-L413), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L429-L432), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L451-L451), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L452-L452)


```solidity

File: contracts/interfaces/ISystemContract.sol

21:         require(
22:             SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
23:             "This method require system call flag"
24:         );

31:         require(
32:             SystemContractHelper.isSystemContract(msg.sender),
33:             "This method require the caller to be system contract"
34:         );

41:         require(msg.sender == caller, "Inappropriate caller");

48:         require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");

55:         require(msg.sender == FORCE_DEPLOYER);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L21-L24) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L31-L34), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L41-L41), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L48-L48), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L55-L55)


```solidity

File: contracts/libraries/EfficientCall.sol

38:         require(returnData.length == 32, "keccak256 returned invalid data");

47:         require(returnData.length == 32, "sha returned invalid data");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L38-L38) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L47-L47)


```solidity

File: contracts/libraries/SystemContractHelper.sol

319:         require(index < 10, "There are only 10 accessible registers");

350:         require(precompileCallSuccess, "Failed to charge gas");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L319-L319) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L350-L350)


```solidity

File: contracts/libraries/TransactionHelper.sol

112:             revert("Encoding unsupported tx");

363:         require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");

367:             require(
368:                 _transaction.paymasterInput.length >= 68,
369:                 "The approvalBased paymaster input must be at least 68 bytes long"
370:             );

388:             revert("Unsupported paymaster flow");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L112-L112) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L363-L363), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L367-L370), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L388-L388)


```solidity

File: contracts/libraries/Utils.sol

21:         require(_x <= type(uint128).max, "Overflow");

27:         require(_x <= type(uint32).max, "Overflow");

33:         require(_x <= type(uint24).max, "Overflow");

84:         require(_bytecode.length % 32 == 0, "po");

87:         require(lengthInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words

88:         require(lengthInWords % 2 == 1, "pr"); // bytecode length in words must be odd


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L21-L21) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L27-L27), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L33-L33), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L84-L84), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L87-L87), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L88-L88)


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

64:         require(msg.sender == address(sharedBridge), "Not shared bridge");

66:         require(amount == _amount, "Incorrect amount");

141:         require(_amount != 0, "0T"); // empty deposit

143:         require(amount == _amount, "3T"); // The token has non-standard transfer logic

186:         require(amount != 0, "2T"); // empty deposit

215:         require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L64-L64) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L66-L66), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L141-L141), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L143-L143), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L186-L186), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L215-L215)


```solidity

File: contracts/bridge/L1SharedBridge.sol

69:         require(msg.sender == address(bridgehub), "ShB not BH");

75:         require(
76:             msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
77:             "L1SharedBridge: not bridgehub or era chain"
78:         );

84:         require(msg.sender == address(legacyBridge), "ShB not legacy bridge");

108:         require(_owner != address(0), "ShB owner 0");

121:             require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");

129:             require(amount > 0, "ShB: 0 amount to transfer");

132:             require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");

138:         require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");

155:             require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");

158:             require(msg.value == 0, "ShB m.v > 0 b d.it");

161:             require(amount == _amount, "3T"); // The token has non-standard transfer logic

188:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

194:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");

195:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

200:             require(_depositAmount == 0, "ShB wrong withdraw amount");

202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");

206:             require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic

208:         require(amount != 0, "6T"); // empty deposit amount

237:         require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");

325:             require(proofValid, "yn");

327:         require(_amount > 0, "y1");

342:                 require(dataHash == txDataHash, "ShB: d.it not hap");

349:             require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");

360:             require(callSuccess, "ShB: claimFailedDeposit failed");

396:             require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");

417:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");

427:             require(!alreadyFinalized, "Withdrawal is already finalized 2");

439:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds

449:             require(callSuccess, "ShB: withdraw failed");

484:         require(success, "ShB withd w proof"); // withdrawal wrong proof

501:         require(_l2ToL1message.length >= 56, "ShB wrong msg len"); // wrong messsage length

517:             require(_l2ToL1message.length == 76, "ShB wrong msg len 2");

522:             revert("ShB Incorrect message function selector");

563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L69-L69) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L75-L78), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L84-L84), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L108-L108), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L121-L121), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L129-L129), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L132-L132), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L138-L138), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L155-L155), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L158-L158), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L161-L161), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L188-L188), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L194-L194), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L195-L195), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L200-L200), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L202-L202), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L206-L206), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L208-L208), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L237-L237), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L325-L325), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L327-L327), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L342-L342), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L349-L349), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L360-L360), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L396-L396), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L417-L417), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L427-L427), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L439-L439), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L449-L449), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L484-L484), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L501-L501), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L517-L517), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L522-L522), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L563-L563), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L564-L564)


```solidity

File: contracts/bridgehub/Bridgehub.sol

46:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

62:         require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

83:         require(
84:             !stateTransitionManagerIsRegistered[_stateTransitionManager],
85:             "Bridgehub: state transition already registered"
86:         );

93:         require(
94:             stateTransitionManagerIsRegistered[_stateTransitionManager],
95:             "Bridgehub: state transition not registered yet"
96:         );

102:         require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

122:         require(_chainId != 0, "Bridgehub: chainId cannot be 0");

123:         require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");

125:         require(
126:             stateTransitionManagerIsRegistered[_stateTransitionManager],
127:             "Bridgehub: state transition not registered"
128:         );

129:         require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");

130:         require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

223:                 require(msg.value == _request.mintValue, "Bridgehub: msg.value mismatch 1");

225:                 require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");

269:                 require(
270:                     msg.value == _request.mintValue + _request.secondBridgeValue,
271:                     "Bridgehub: msg.value mismatch 2"
272:                 );

275:                 require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3");

296:         require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch");

300:         require(
301:             _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
302:             "Bridgehub: second bridge address too low"
303:         ); // to avoid calls to precompiles


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L46-L46) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L62-L62), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L83-L86), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L93-L96), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L102-L102), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L122-L122), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L123-L123), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L125-L128), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L129-L129), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L130-L130), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L132-L132), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L223-L223), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L225-L225), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L269-L272), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L275-L275), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L296-L296), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L300-L303)


```solidity

File: contracts/common/ReentrancyGuard.sol

58:         require(lockSlotOldValue == 0, "1B");

75:         require(_status == _NOT_ENTERED, "r1");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/ReentrancyGuard.sol#L58-L58) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/ReentrancyGuard.sol#L75-L75)


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

23:         require(_bytecode.length % 32 == 0, "pq");

26:         require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words

27:         require(bytecodeLenInWords % 2 == 1, "ps"); // bytecode length in words must be odd

41:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash

43:         require(bytecodeLen(_bytecodeHash) % 2 == 1, "uy"); // Code length in words must be odd


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L23-L23) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L26-L26), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L27-L27), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L41-L41), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L43-L43)


```solidity

File: contracts/governance/Governance.sol

42:         require(_admin != address(0), "Admin should be non zero address");

59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

65:         require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

71:         require(
72:             msg.sender == owner() || msg.sender == securityCouncil,
73:             "Only the owner and security council are allowed to call this function"
74:         );

155:         require(isOperationPending(_id), "Operation must be pending");

172:         require(isOperationReady(id), "Operation must be ready before execution");

177:         require(isOperationReady(id), "Operation must be ready after execution");

191:         require(isOperationPending(id), "Operation must be pending before execution");

196:         require(isOperationPending(id), "Operation must be pending after execution");

216:         require(!isOperation(_id), "Operation with this proposal id already exists");

217:         require(_delay >= minDelay, "Proposed delay is less than minimum delay");

240:         require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L42-L42) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L59-L59), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L65-L65), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L71-L74), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L155-L155), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L172-L172), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L177-L177), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L191-L191), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L196-L196), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L216-L216), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L217-L217), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L240-L240)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

64:         require(msg.sender == bridgehub, "StateTransition: only bridgehub");

70:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

82:         require(_initializeData.governor != address(0), "StateTransition: governor zero");

121:         require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

256:         require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L64-L64) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L70-L70), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L82-L82), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L121-L121), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L256-L256)


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

62:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

68:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");

195:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

217:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L62-L62) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L68-L68), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L195-L195), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L217-L217)


```solidity

File: contracts/state-transition/chain-deps/DiamondInit.sol

25:         require(address(_initializeData.verifier) != address(0), "vt");

26:         require(_initializeData.admin != address(0), "vy");

27:         require(_initializeData.validatorTimelock != address(0), "hc");

28:         require(_initializeData.priorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "vu");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondInit.sol#L25-L25) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondInit.sol#L26-L26), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondInit.sol#L27-L27), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondInit.sol#L28-L28)


```solidity

File: contracts/state-transition/chain-deps/DiamondProxy.sol

14:         require(_chainId == block.chainid, "pr");

25:         require(msg.data.length >= 4 || msg.data.length == 0, "Ut");

30:         require(facetAddress != address(0), "F"); // Proxy has no facet for this selector

31:         require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondProxy.sol#L14-L14) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondProxy.sol#L25-L25), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondProxy.sol#L30-L30), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondProxy.sol#L31-L31)


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

34:         require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights

59:         require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");

70:         require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");

90:         require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed

105:         require(
106:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107:             "StateTransition: cutHash mismatch"
108:         );

110:         require(
111:             s.protocolVersion == _oldProtocolVersion,
112:             "StateTransition: protocolVersion mismatch in STC when upgrading"
113:         );

116:         require(
117:             s.protocolVersion > _oldProtocolVersion,
118:             "StateTransition: protocolVersion mismatch in STC after upgrading"
119:         );

136:         require(!diamondStorage.isFrozen, "a9"); // diamond proxy is frozen already

146:         require(diamondStorage.isFrozen, "a7"); // diamond proxy is not frozen


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L34-L34) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L59-L59), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L70-L70), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L90-L90), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L105-L108), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L110-L113), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L116-L119), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L136-L136), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L146-L146)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

37:         require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f"); // only commit next batch

40:         require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us");

50:             require(logOutput.pubdataHash == 0x00, "v0h");

51:             require(_newBatch.pubdataCommitments.length == 1);

61:             require(
62:                 logOutput.pubdataHash ==
63:                     keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),
64:                 "wp"
65:             );

74:         require(_previousBatch.batchHash == logOutput.previousBatchHash, "l");

76:         require(logOutput.chainedPriorityTxsHash == _newBatch.priorityOperationsHash, "t");

78:         require(logOutput.numberOfLayer1Txs == _newBatch.numberOfLayer1Txs, "ta");

110:         require(batchTimestamp == _expectedBatchTimestamp, "tb");

114:         require(_previousBatchTimestamp < batchTimestamp, "h3");

122:         require(block.timestamp - COMMIT_TIMESTAMP_NOT_OLDER <= batchTimestamp, "h1"); // New batch timestamp is too small

123:         require(lastL2BlockTimestamp <= block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA, "h2"); // The last L2 block timestamp is too big

149:             require(!_checkBit(processedLogs, uint8(logKey)), "kp");

154:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");

157:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");

160:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");

163:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");

166:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");

169:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bl");

172:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bk");

175:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");

178:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");

181:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bu");

182:                 require(_expectedSystemContractUpgradeTxHash == logValue, "ut");

184:                 revert("ul");

192:             require(processedLogs == 511, "b7");

194:             require(processedLogs == 1023, "b8");

226:         require(
227:             IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
228:             "Executor facet: wrong protocol version"
229:         );

231:         require(_newBatchesData.length == 1, "e4");

233:         require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data

284:         require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");

323:         require(currentBatchNumber == s.totalBatchesExecuted + _executedBatchIdx + 1, "k"); // Execute batches in order

324:         require(
325:             _hashStoredBatchInfo(_storedBatch) == s.storedBatchHashes[currentBatchNumber],
326:             "exe10" // executing batch should be committed
327:         );

330:         require(priorityOperationsHash == _storedBatch.priorityOperationsHash, "x"); // priority operations hash does not match to expected

358:         require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.

402:         require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");

407:             require(
408:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
409:                 "o1"
410:             );

421:         require(currentTotalBatchesVerified <= s.totalBatchesCommitted, "q");

442:         require(proofPublicInput.length == 1, "t4");

449:         require(successVerifyProof, "p"); // Proof verification fail

482:         require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch

483:         require(_newLastBatch >= s.totalBatchesExecuted, "v2"); // Already executed batches cannot be reverted

543:         require(_batch.systemLogs.length <= MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES, "pu");

567:         require(_blobCommitments.length == MAX_NUMBER_OF_BLOBS, "b10");

568:         require(_blobHashes.length == MAX_NUMBER_OF_BLOBS, "b11");

616:         require(success, "failed to call point evaluation precompile");

618:         require(result == BLS_MODULUS, "precompile unexpected output");

631:         require(_pubdataCommitments.length > 0, "pl");

632:         require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");

633:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");

639:             require(blobVersionedHash != bytes32(0), "vh");

663:         require(versionedHash == bytes32(0), "lh");

668:             require(
669:                 (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
671:                 "bh"
672:             );

681:         require(success, "vc");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L37-L37) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L40-L40), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L50-L50), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L51-L51), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L61-L65), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L74-L74), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L76-L76), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L78-L78), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L110-L110), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L114-L114), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L122-L122), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L123-L123), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L149-L149), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L154-L154), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L157-L157), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L160-L160), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L163-L163), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L166-L166), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L169-L169), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L172-L172), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L175-L175), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L178-L178), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L181-L181), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L182-L182), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L184-L184), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L192-L192), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L194-L194), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L226-L229), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L231-L231), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L233-L233), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L284-L284), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L323-L323), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L324-L327), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L330-L330), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L358-L358), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L402-L402), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L407-L410), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L421-L421), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L442-L442), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L449-L449), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L482-L482), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L483-L483), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L543-L543), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L567-L567), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L568-L568), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L616-L616), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L618-L618), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L631-L631), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L632-L632), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L633-L633), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L639-L639), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L663-L663), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L668-L672), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L681-L681)


```solidity

File: contracts/state-transition/chain-deps/facets/Getters.sol

183:         require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L183-L183) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

39:         require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");

110:         require(_batchNumber <= s.totalBatchesExecuted, "xx");

117:         require(hashedLog != L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH, "tw");

158:         require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

185:         require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");

206:         require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");

243:         require(_request.l2GasPerPubdataByteLimit == REQUIRED_L2_GAS_PRICE_PER_PUBDATA, "qp");

264:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj");

272:         require(_mintValue >= baseCost + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L39-L39) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L110-L110), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L117-L117), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L158-L158), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L185-L185), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L206-L206), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L243-L243), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L264-L264), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L272-L272)


```solidity

File: contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

16:         require(msg.sender == s.admin, "StateTransition Chain: not admin");

22:         require(s.validators[msg.sender], "StateTransition Chain: not validator");

27:         require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

32:         require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

37:         require(
38:             msg.sender == s.admin || msg.sender == s.stateTransitionManager,
39:             "StateTransition Chain: Only by admin or state transition manager"
40:         );

45:         require(
46:             s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
47:             "StateTransition Chain: Only by validator or state transition manager"
48:         );

53:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16-L16) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22-L22), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27-L27), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32-L32), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L37-L40), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45-L48), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53-L53)


```solidity

File: contracts/state-transition/libraries/Diamond.sol

107:             require(selectors.length > 0, "B"); // no functions for diamond cut

116:                 revert("C"); // undefined diamond cut action

132:         require(_facet.code.length > 0, "G");

141:             require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists

155:         require(_facet.code.length > 0, "K");

161:             require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

175:         require(_facet == address(0), "a1"); // facet address must be zero

181:             require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet

215:             require(_isSelectorFreezable == ds.selectorToFacet[selector0].isFreezable, "J1");

280:             require(_calldata.length == 0, "H"); // Non-empty calldata for zero address

287:                     revert("I"); // delegatecall failed

297:             require(data.length == 32, "lp");

298:             require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L107-L107) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L116-L116), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L132-L132), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L141-L141), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L155-L155), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L161-L161), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L175-L175), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L181-L181), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L215-L215), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L280-L280), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L287-L287), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L297-L297), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L298-L298)


```solidity

File: contracts/state-transition/libraries/Merkle.sol

24:         require(pathLength > 0, "xc");

25:         require(pathLength < 256, "bt");

26:         require(_index < (1 << pathLength), "px");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L24-L24) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L25-L25), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L26-L26)


```solidity

File: contracts/state-transition/libraries/PriorityQueue.sol

65:         require(!_queue.isEmpty(), "D"); // priority queue is empty

73:         require(!_queue.isEmpty(), "s"); // priority queue is empty


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/PriorityQueue.sol#L65-L65) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/PriorityQueue.sol#L73-L73)


```solidity

File: contracts/state-transition/libraries/TransactionValidator.sol

28:         require(l2GasForTxBody <= _priorityTxMaxGasLimit, "ui");

30:         require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");

34:         require(
35:             getMinimalPriorityTransactionGasLimit(
36:                 _encoded.length,
37:                 _transaction.factoryDeps.length,
38:                 _transaction.gasPerPubdataByteLimit
39:             ) <= l2GasForTxBody,
40:             "up"
41:         );

48:         require(_transaction.from <= type(uint16).max, "ua");

49:         require(_transaction.to <= type(uint160).max, "ub");

50:         require(_transaction.paymaster == 0, "uc");

51:         require(_transaction.value == 0, "ud");

52:         require(_transaction.maxFeePerGas == 0, "uq");

53:         require(_transaction.maxPriorityFeePerGas == 0, "ux");

54:         require(_transaction.reserved[0] == 0, "ue");

55:         require(_transaction.reserved[1] <= type(uint160).max, "uf");

56:         require(_transaction.reserved[2] == 0, "ug");

57:         require(_transaction.reserved[3] == 0, "uo");

58:         require(_transaction.signature.length == 0, "uh");

59:         require(_transaction.paymasterInput.length == 0, "ul1");

60:         require(_transaction.reservedDynamic.length == 0, "um");

115:         require(_totalGasLimit >= overhead, "my"); // provided gas limit doesn't cover transaction overhead


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L28-L28) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L30-L30), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L34-L41), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L48-L48), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L49-L49), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L50-L50), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L51-L51), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L52-L52), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L53-L53), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L54-L54), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L55-L55), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L56-L56), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L57-L57), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L58-L58), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L59-L59), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L60-L60), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L115-L115)


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

72:         require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

190:         require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");

205:         require(
206:             _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
207:             "The new protocol version should be included in the L2 system upgrade tx"
208:         );

223:         require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");

224:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");

227:             require(
228:                 L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
229:                 "Wrong factory dep hash"
230:             );

238:         require(
239:             _newProtocolVersion > previousProtocolVersion,
240:             "New protocol version is not greater than the current one"
241:         );

242:         require(
243:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
244:             "Too big protocol version difference"
245:         );

249:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

250:         require(
251:             s.l2SystemContractsUpgradeBatchNumber == 0,
252:             "The batch number of the previous upgrade has not been cleaned"
253:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L72-L72) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L190-L190), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L205-L208), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L223-L223), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L224-L224), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L227-L230), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L238-L241), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L242-L245), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L249-L249), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L250-L253)


```solidity

File: contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

22:         require(
23:             // Genesis Upgrade difference: Note this is the only thing change > to >=
24:             _newProtocolVersion >= previousProtocolVersion,
25:             "New protocol version is not greater than the current one"
26:         );

27:         require(
28:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
29:             "Too big protocol version difference"
30:         );

33:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

34:         require(
35:             s.l2SystemContractsUpgradeBatchNumber == 0,
36:             "The batch number of the previous upgrade has not been cleaned"
37:         );

52:         require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22-L26) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L27-L30), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33-L33), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L34-L37), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L52-L52)


```solidity

File: contracts/SystemContractsCaller.sol

28:         require(_x <= type(uint32).max, "Overflow");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L28-L28) 


```solidity

File: contracts/bridge/L2SharedBridge.sol

55:         require(_l1Bridge != address(0), "bf");

56:         require(_l2TokenProxyBytecodeHash != bytes32(0), "df");

57:         require(_aliasedOwner != address(0), "sf");

58:         require(_l2TokenProxyBytecodeHash != bytes32(0), "df");

68:             require(_l1LegecyBridge != address(0), "bf2");

87:         require(
88:             AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
89:                 AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
90:             "mq"
91:         );

92:         require(msg.value == 0, "Value should be 0 for ERC20 bridge");

98:             require(deployedToken == expectedL2Token, "mt");

101:             require(currentL1Token == _l1Token, "gg"); // Double check that the expected value equal to real one

124:         require(_amount > 0, "Amount cannot be zero");

129:         require(l1Token != address(0), "yh");

176:         require(success, "mk");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L55-L55) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L56-L56), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L57-L57), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L58-L58), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L68-L68), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L87-L91), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L92-L92), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L98-L98), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L101-L101), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L124-L124), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L129-L129), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L176-L176)


```solidity

File: contracts/bridge/L2StandardERC20.sol

51:         require(_l1Address != address(0), "in6"); // Should be non-zero address

120:         require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");

130:         require(msg.sender == l2Bridge, "xnt"); // Only L2 bridge can call this method

137:         require(_version == _getInitializedVersion() + 1, "v");

161:         if (availableGetters.ignoreName) revert();

167:         if (availableGetters.ignoreSymbol) revert();

173:         if (availableGetters.ignoreDecimals) revert();


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L51-L51) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L120-L120), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L130-L130), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L137-L137), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L161-L161), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L167-L167), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L173-L173)


</details>


### [GAS&#x2011;15] Divisions which do not divide by -X cannot overflow or overflow so such operations can be unchecked to save gas 
Make such found divisions are unchecked when ensured it is safe to do so


*There are 14 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/Compressor.sol

57:                 dictionary.length / 8 <= encodedData.length / 2,

57:                 dictionary.length / 8 <= encodedData.length / 2,


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L57-L57) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L57-L57)


```solidity

File: contracts/L1Messenger.sol

51:         return KECCAK_ROUND_GAS_COST * (_length / KECCAK_ROUND_NUMBER_OF_BYTES + 1);

62:         return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L51-L51) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L62-L62)


```solidity

File: contracts/NonceHolder.sol

180:         deploymentNonce = _rawMinNonce / DEPLOY_NONCE_MULTIPLIER;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L180-L180) 


```solidity

File: contracts/libraries/Utils.sol

86:         uint256 lengthInWords = _bytecode.length / 32;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L86-L86) 


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

25:         uint256 bytecodeLenInWords = _bytecode.length / 32;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L25-L25) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

159:         uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /

168:             batchOverheadBaseToken /

171:         uint256 l2GasPrice = feeParams.minimalL2GasPrice + batchOverheadBaseToken / uint256(feeParams.maxL2GasPerBatch);

172:         uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L159-L159) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L168-L168), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L171-L171), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L172-L172)


```solidity

File: contracts/state-transition/libraries/LibMap.sol

23:             uint256 mapValue = _map.map[_index / 8];

43:             uint256 mapIndex = _index / 8;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L23-L23) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L43-L43)


```solidity

File: contracts/state-transition/libraries/TransactionValidator.sol

30:         require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L30-L30) 


</details>


### [GAS&#x2011;16] Do not calculate constants 
Due to how constant variables are implemented (replacements at compile-time), an expression assigned to a constant variable is recomputed each time that the variable is used, which wastes some gas.


*There are 12 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/Constants.sol

94: uint256 constant MAX_MSG_VALUE = 2 ** 128 - 1;

135: uint256 constant COMPRESSED_INITIAL_WRITE_SIZE = DERIVED_KEY_LENGTH + VALUE_LENGTH;

137: uint256 constant COMPRESSED_REPEATED_WRITE_SIZE = ENUM_INDEX_LENGTH + VALUE_LENGTH;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Constants.sol#L94-L94) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Constants.sol#L135-L135), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Constants.sol#L137-L137)


```solidity

File: contracts/NonceHolder.sol

28:     uint256 private constant DEPLOY_NONCE_MULTIPLIER = 2 ** 128;

31:     uint256 private constant MAXIMAL_MIN_NONCE_INCREMENT = 2 ** 32;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L28-L28) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L31-L31)


```solidity

File: contracts/libraries/SystemContractsCaller.sol

41: uint256 constant META_GAS_PER_PUBDATA_BYTE_OFFSET = 0 * 8;

42: uint256 constant META_HEAP_SIZE_OFFSET = 8 * 8;

43: uint256 constant META_AUX_HEAP_SIZE_OFFSET = 12 * 8;

44: uint256 constant META_SHARD_ID_OFFSET = 28 * 8;

45: uint256 constant META_CALLER_SHARD_ID_OFFSET = 29 * 8;

46: uint256 constant META_CODE_SHARD_ID_OFFSET = 30 * 8;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L41-L41) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L42-L42), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L43-L43), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L44-L44), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L45-L45), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L46-L46)


```solidity

File: contracts/common/Config.sol

14: uint256 constant MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES = 4 + L2_TO_L1_LOG_SERIALIZE_SIZE * 512;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/Config.sol#L14-L14) 


</details>


### [GAS&#x2011;17] Stack variable cost less while used in emiting event 
Even if the variable is going to be used only one time, caching a state variable and use its cache in an emit would help you reduce the cost by at least ***9 gas***


*There are 14 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/bridgehub/Bridgehub.sol

// @audit `pendingAdmin` is a state variable
69:         emit NewAdmin(previousAdmin, pendingAdmin);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L69-L69) 


```solidity

File: contracts/governance/Governance.sol

// @audit `minDelay` is a state variable
250:         emit ChangeMinDelay(minDelay, _newDelay);

// @audit `securityCouncil` is a state variable
257:         emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L250-L250) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L257-L257)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

// @audit `pendingAdmin` is a state variable
128:         emit NewAdmin(previousAdmin, pendingAdmin);

// @audit `protocolVersion` is a state variable
227:         emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L128-L128) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L227-L227)


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

// @audit `pendingAdmin` is a state variable
40:         emit NewPendingAdmin(pendingAdmin, address(0));

// @audit `pendingAdmin` is a state variable
41:         emit NewAdmin(previousAdmin, pendingAdmin);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L40-L40) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L41-L41)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

// @audit `s` is a state variable
436:         emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

// @audit `s` is a state variable
496:         emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);

// @audit `s` is a state variable
496:         emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);

// @audit `s` is a state variable
496:         emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L436-L436) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L496-L496), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L496-L496), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L496-L496)


```solidity

File: contracts/bridge/L2StandardERC20.sol

// @audit `decimals_` is a state variable
101:         emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);

// @audit `l1Address` is a state variable
126:         emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);

// @audit `decimals_` is a state variable
126:         emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L101-L101) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L126-L126), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L126-L126)


</details>


### [GAS&#x2011;18] Events should be emitted outside of loops 
Emitting an event has an overhead of **375 gas**, which will be incurred on every iteration of the loop. It is cheaper to `emit` only [once](https://github.com/ethereum/EIPs/blob/adad5968fd6de29902174e0cb51c8fc3dceb9ab5/EIPS/eip-1155.md?plain=1#L68) after the loop has finished.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/state-transition/chain-deps/facets/Executor.sol

//@audit BlockCommit is emited inside this loop
257:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
258:             _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));
259: 
260:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
261:             emit BlockCommit(

//@audit BlockCommit is emited inside this loop
289:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
290:             // The upgrade transaction must only be included in the first batch.
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
292:             _lastCommittedBatchData = _commitOneBatch(
293:                 _lastCommittedBatchData,
294:                 _newBatchesData[i],
295:                 expectedUpgradeTxHash
296:             );
297: 
298:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
299:             emit BlockCommit(

//@audit BlockExecution is emited inside this loop
351:         for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
352:             _executeOneBatch(_batchesData[i], i);
353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L257-L261) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L289-L299), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L351-L353)


</details>


### [GAS&#x2011;19] Empty blocks should be removed or emit something 
The code should be refactored such that they no longer exist, or the block should do something useful, such as emitting an event or reverting. If the contract is meant to be extended, the contract should be `abstract` and the function signatures be added without any default implementation. If the block is an empty `if`-statement block to avoid doing subsequent checks in the else-if/else conditions, the else-if/else conditions should be nested under the negation of the if-statement, because they involve different classes of checks, which may lead to the introduction of errors when the code is later modified (`if (x) {...} else if (y) {...} else {...}` => `if (!x) { if (y) {...} else {...} }`). Empty `receive()`/`fallback() payable` functions that are not used, can be removed to save deployment gas.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/bridge/L1ERC20Bridge.sol

60:     function initialize() external reentrancyGuardInitializer {}


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L60-L60) 


</details>


### [GAS&#x2011;20] The result of function calls should be cached rather than re-calling the function 
The instances below point to the second+ call of the function within a single function


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/L1Messenger.sol

// @audit gasleft() is called 2 times in the function `sendToL1`
116:     function sendToL1(bytes calldata _message) external override returns (bytes32 hash) {
117:         uint256 gasBeforeMessageHashing = gasleft();
118:         hash = EfficientCall.keccak(_message);
119:         uint256 gasSpentOnMessageHashing = gasBeforeMessageHashing - gasleft();
120: 
121:         /// Store message record
122:         chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));
123: 
124:         /// Store log record
125:         L2ToL1Log memory l2ToL1Log = L2ToL1Log({
126:             l2ShardId: 0,
127:             isService: true,
128:             txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),
129:             sender: address(this),
130:             key: bytes32(uint256(uint160(msg.sender))),
131:             value: hash
132:         });
133:         _processL2ToL1Log(l2ToL1Log);
134: 
135:         // Get cost of one byte pubdata in gas from context.
136:         uint256 pubdataLen;
137:         unchecked {
138:             // 4 bytes used to encode the length of the message (see `publishPubdataAndClearState`)
139:             // L2_TO_L1_LOG_SERIALIZE_SIZE bytes used to encode L2ToL1Log
140:             pubdataLen = 4 + _message.length + L2_TO_L1_LOG_SERIALIZE_SIZE;
141:         }
142: 
143:         // We need to charge cost of hashing, as it will be used in `publishPubdataAndClearState`:
144:         // - keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) and keccakGasCost(64) when reconstructing L2ToL1Log
145:         // - keccakGasCost(64) and gasSpentOnMessageHashing when reconstructing Messages
146:         // - at most 1 time keccakGasCost(64) when building the Merkle tree (as merkle tree can contain
147:         // ~2*N nodes, where the first N nodes are leaves the hash of which is calculated on the previous step).
148:         uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) +
149:             3 *
150:             keccakGasCost(64) +
151:             gasSpentOnMessageHashing +
152:             COMPUTATIONAL_PRICE_FOR_PUBDATA *
153:             pubdataLen;
154:         SystemContractHelper.burnGas(Utils.safeCastToU32(gasToPay), uint32(pubdataLen));
155: 
156:         emit L1MessageSent(msg.sender, hash, _message);
157:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L116-L157) 


</details>


### [GAS&#x2011;21] Don't initialize `uint` variables with default value 
The default value for variables is zero, so initializing them to zero is superfluous.


*There are 38 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/Compressor.sol

61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {

124:         uint256 numInitialWritesProcessed = 0;

127:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

159:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L61-L61) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L124-L124), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L127-L127), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L159-L159)


```solidity

File: contracts/ContractDeployer.sol

247:         uint256 sumOfValues = 0;

248:         for (uint256 i = 0; i < deploymentsLength; ++i) {

253:         for (uint256 i = 0; i < deploymentsLength; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L247-L247) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L248-L248), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L253-L253)


```solidity

File: contracts/ImmutableSimulator.sol

38:             for (uint256 i = 0; i < immutablesLength; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L38-L38) 


```solidity

File: contracts/KnownCodesStorage.sol

30:             for (uint256 i = 0; i < hashesLen; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L30-L30) 


```solidity

File: contracts/L1Messenger.sol

197:         uint256 calldataPtr = 0;

206:         for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

224:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

236:         for (uint256 i = 0; i < numberOfMessages; ++i) {

254:         for (uint256 i = 0; i < numberOfBytecodes; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L197-L197) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L206-L206), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L224-L224), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L236-L236), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L254-L254)


```solidity

File: contracts/PubdataChunkPublisher.sol

36:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L36-L36) 


```solidity

File: contracts/governance/Governance.sol

225:         for (uint256 i = 0; i < _calls.length; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L225-L225) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

116:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

135:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

185:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

209:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L116-L116) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L135-L135), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L185-L185), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L209-L209)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

142:         for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

257:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

289:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

311:         for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {

351:         for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {

405:         for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {

580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

629:         uint256 versionedHashIndex = 0;

636:         for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {

667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L142-L142) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L257-L257), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L289-L289), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L311-L311), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L351-L351), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L405-L405), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L580-L580), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L629-L629), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L636-L636), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L667-L667)


```solidity

File: contracts/state-transition/chain-deps/facets/Getters.sol

208:         for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L208-L208) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

356:         for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L356-L356) 


```solidity

File: contracts/state-transition/libraries/Diamond.sol

101:         for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {

138:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

158:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

178:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L101-L101) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L138-L138), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L158-L158), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L178-L178)


```solidity

File: contracts/state-transition/libraries/TransactionValidator.sol

92:         uint256 costForPubdata = 0;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L92-L92) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L226-L226) 


</details>


### [GAS&#x2011;22] `require()` or `revert()` statements that check input arguments should be at the top of the function 



*There are 12 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ContractDeployer.sol

238:     function forceDeployOnAddresses(ForceDeployment[] calldata _deployments) external payable {
239:         require(
240:             msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
241:             "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
242:         );
243: 
244:         uint256 deploymentsLength = _deployments.length;
245:         // We need to ensure that the `value` provided by the call is enough to provide `value`
246:         // for all of the deployments
247:         uint256 sumOfValues = 0;
248:         for (uint256 i = 0; i < deploymentsLength; ++i) {
249:             sumOfValues += _deployments[i].value;
250:         }
251:         require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L238-L251) 


```solidity

File: contracts/SystemContext.sol

241:     function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {
242:         require(_isFirstInBatch, "Upgrade transaction must be first");
243: 
244:         // This is how it will be commonly done in practice, but it will simplify some logic later
245:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L241-L245) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

303:     function _claimFailedDeposit(
304:         bool _checkedInLegacyBridge,
305:         uint256 _chainId,
306:         address _depositSender,
307:         address _l1Token,
308:         uint256 _amount,
309:         bytes32 _l2TxHash,
310:         uint256 _l2BatchNumber,
311:         uint256 _l2MessageIndex,
312:         uint16 _l2TxNumberInBatch,
313:         bytes32[] calldata _merkleProof
314:     ) internal nonReentrant {
315:         {
316:             bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
317:                 _chainId,
318:                 _l2TxHash,
319:                 _l2BatchNumber,
320:                 _l2MessageIndex,
321:                 _l2TxNumberInBatch,
322:                 _merkleProof,
323:                 TxStatus.Failure
324:             );
325:             require(proofValid, "yn");
326:         }
327:         require(_amount > 0, "y1");

554:     function depositLegacyErc20Bridge(
555:         address _prevMsgSender,
556:         address _l2Receiver,
557:         address _l1Token,
558:         uint256 _amount,
559:         uint256 _l2TxGasLimit,
560:         uint256 _l2TxGasPerPubdataByte,
561:         address _refundRecipient
562:     ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L303-L327) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L554-L564)


```solidity

File: contracts/governance/Governance.sol

215:     function _schedule(bytes32 _id, uint256 _delay) internal {
216:         require(!isOperation(_id), "Operation with this proposal id already exists");
217:         require(_delay >= minDelay, "Proposed delay is less than minimum delay");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L215-L217) 


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

100:     function upgradeChainFromVersion(
101:         uint256 _oldProtocolVersion,
102:         Diamond.DiamondCutData calldata _diamondCut
103:     ) external onlyAdminOrStateTransitionManager {
104:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
105:         require(
106:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107:             "StateTransition: cutHash mismatch"
108:         );
109: 
110:         require(
111:             s.protocolVersion == _oldProtocolVersion,

100:     function upgradeChainFromVersion(
101:         uint256 _oldProtocolVersion,
102:         Diamond.DiamondCutData calldata _diamondCut
103:     ) external onlyAdminOrStateTransitionManager {
104:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
105:         require(
106:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107:             "StateTransition: cutHash mismatch"
108:         );
109: 
110:         require(
111:             s.protocolVersion == _oldProtocolVersion,
112:             "StateTransition: protocolVersion mismatch in STC when upgrading"
113:         );
114:         Diamond.diamondCut(_diamondCut);
115:         emit ExecuteUpgrade(_diamondCut);
116:         require(
117:             s.protocolVersion > _oldProtocolVersion,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L100-L111) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L100-L117)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

258:     function _requestL2Transaction(
259:         uint256 _mintValue,
260:         WritePriorityOpParams memory _params,
261:         bytes memory _calldata,
262:         bytes[] memory _factoryDeps
263:     ) internal returns (bytes32 canonicalTxHash) {
264:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj");
265:         _params.txId = s.priorityQueue.getTotalPriorityTxs();
266: 
267:         // Checking that the user provided enough ether to pay for the transaction.
268:         // Using a new scope to prevent "stack too deep" error
269: 
270:         _params.l2GasPrice = _deriveL2GasPrice(tx.gasprice, _params.l2GasPricePerPubdata);
271:         uint256 baseCost = _params.l2GasPrice * _params.l2GasLimit;
272:         require(_mintValue >= baseCost + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L258-L272) 


```solidity

File: contracts/state-transition/libraries/Merkle.sol

18:     function calculateRoot(
19:         bytes32[] calldata _path,
20:         uint256 _index,
21:         bytes32 _itemHash
22:     ) internal pure returns (bytes32) {
23:         uint256 pathLength = _path.length;
24:         require(pathLength > 0, "xc");
25:         require(pathLength < 256, "bt");
26:         require(_index < (1 << pathLength), "px");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L18-L26) 


```solidity

File: contracts/state-transition/libraries/TransactionValidator.sol

46:     function validateUpgradeTransaction(L2CanonicalTransaction memory _transaction) internal pure {
47:         // Restrict from to be within system contract range (0...2^16 - 1)
48:         require(_transaction.from <= type(uint16).max, "ua");
49:         require(_transaction.to <= type(uint160).max, "ub");
50:         require(_transaction.paymaster == 0, "uc");
51:         require(_transaction.value == 0, "ud");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L46-L51) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

180:     function _setL2SystemContractUpgrade(
181:         L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
182:         bytes[] calldata _factoryDeps,
183:         uint256 _newProtocolVersion
184:     ) internal returns (bytes32) {
185:         // If the type is 0, it is considered as noop and so will not be required to be executed.
186:         if (_l2ProtocolUpgradeTx.txType == 0) {
187:             return bytes32(0);
188:         }
189: 
190:         require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");
191: 
192:         bytes memory encodedTransaction = abi.encode(_l2ProtocolUpgradeTx);
193: 
194:         TransactionValidator.validateL1ToL2Transaction(
195:             _l2ProtocolUpgradeTx,
196:             encodedTransaction,
197:             s.priorityTxMaxGasLimit,
198:             s.feeParams.priorityTxMaxPubdata
199:         );
200: 
201:         TransactionValidator.validateUpgradeTransaction(_l2ProtocolUpgradeTx);
202: 
203:         // We want the hashes of l2 system upgrade transactions to be unique.
204:         // This is why we require that the `nonce` field is unique to each upgrade.
205:         require(
206:             _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L180-L206) 


```solidity

File: contracts/bridge/L2SharedBridge.sol

79:     function finalizeDeposit(
80:         address _l1Sender,
81:         address _l2Receiver,
82:         address _l1Token,
83:         uint256 _amount,
84:         bytes calldata _data
85:     ) external payable override {
86:         // Only the L1 bridge counterpart can initiate and finalize the deposit.
87:         require(
88:             AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
89:                 AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
90:             "mq"
91:         );
92:         require(msg.value == 0, "Value should be 0 for ERC20 bridge");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L79-L92) 


</details>


### [GAS&#x2011;23] `internal` functions only called once can be inlined to save gas 
Not inlining costs 20 to 40 gas because of two extra JUMP instructions and additional stack operations needed for function calls.


*There are 55 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/BootloaderUtilities.sol

44:     function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {

139:     function encodeEIP2930TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {

229:     function encodeEIP1559TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L44-L44) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L139-L139), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L229-L229)


```solidity

File: contracts/Compressor.sol

197:     function _decodeRawBytecode(
198:         bytes calldata _rawCompressedData
199:     ) internal pure returns (bytes calldata dictionary, bytes calldata encodedData) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L197-L199) 


```solidity

File: contracts/ContractDeployer.sol

283:     function _performDeployOnAddress(
284:         bytes32 _bytecodeHash,
285:         address _newAddress,
286:         AccountAbstractionVersion _aaVersion,
287:         bytes calldata _input
288:     ) internal {

309:     function _storeConstructingByteCodeHashOnAddress(address _newAddress, bytes32 _bytecodeHash) internal {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L283-L288) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L309-L309)


```solidity

File: contracts/DefaultAccount.sol

78:     function _validateTransaction(
79:         bytes32 _suggestedSignedHash,
80:         Transaction calldata _transaction
81:     ) internal returns (bytes4 magic) {

131:     function _execute(Transaction calldata _transaction) internal {

159:     function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L78-L81) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L131-L131), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L159-L159)


```solidity

File: contracts/KnownCodesStorage.sol

74:     function _validateBytecode(bytes32 _bytecodeHash) internal pure {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L74-L74) 


```solidity

File: contracts/L1Messenger.sol

61:     function sha256GasCost(uint256 _length) internal pure returns (uint256) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L61-L61) 


```solidity

File: contracts/L2BaseToken.sol

112:     function _getL1WithdrawMessage(address _to, uint256 _amount) internal pure returns (bytes memory) {

117:     function _getExtendedWithdrawMessage(
118:         address _to,
119:         uint256 _amount,
120:         address _sender,
121:         bytes memory _additionalData
122:     ) internal pure returns (bytes memory) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L112-L112) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L117-L122)


```solidity

File: contracts/MsgValueSimulator.sol

25:     function _getAbiParams() internal view returns (uint256 value, bool isSystemCall, address to) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/MsgValueSimulator.sol#L25-L25) 


```solidity

File: contracts/SystemContext.sol

221:     function _calculateL2BlockHash(
222:         uint128 _blockNumber,
223:         uint128 _blockTimestamp,
224:         bytes32 _prevL2BlockHash,
225:         bytes32 _blockTxsRollingHash
226:     ) internal pure returns (bytes32) {

233:     function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {

241:     function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {

263:     function _setVirtualBlock(
264:         uint128 _l2BlockNumber,
265:         uint128 _maxVirtualBlocksToCreate,
266:         uint128 _newTimestamp
267:     ) internal {

427:     function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L221-L226) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L233-L233), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L241-L241), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L263-L267), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L427-L427)


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

160:     function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L160-L160) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

254:     function _getERC20Getters(address _token) internal view returns (bytes memory) {

458:     function _checkWithdrawal(
459:         uint256 _chainId,
460:         MessageParams memory _messageParams,
461:         bytes calldata _message,
462:         bytes32[] calldata _merkleProof
463:     ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {

487:     function _parseL2WithdrawalMessage(
488:         uint256 _chainId,
489:         bytes memory _l2ToL1message
490:     ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L254-L254) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L458-L463), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L487-L490)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

177:     function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L177-L177) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

103:     function _verifyBatchTimestamp(
104:         uint256 _packedBatchAndL2BlockTimestamp,
105:         uint256 _expectedBatchTimestamp,
106:         uint256 _previousBatchTimestamp
107:     ) internal view {

130:     function _processL2Logs(
131:         CommitBatchInfo calldata _newBatch,
132:         bytes32 _expectedSystemContractUpgradeTxHash
133:     ) internal pure returns (LogProcessingOutput memory logOutput) {

253:     function _commitBatchesWithoutSystemContractsUpgrade(
254:         StoredBatchInfo memory _lastCommittedBatchData,
255:         CommitBatchInfo[] calldata _newBatchesData
256:     ) internal {

273:     function _commitBatchesWithSystemContractsUpgrade(
274:         StoredBatchInfo memory _lastCommittedBatchData,
275:         CommitBatchInfo[] calldata _newBatchesData,
276:         bytes32 _systemContractUpgradeTxHash
277:     ) internal {

308:     function _collectOperationsFromPriorityQueue(uint256 _nPriorityOps) internal returns (bytes32 concatHash) {

321:     function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {

453:     function _getBatchProofPublicInput(
454:         bytes32 _prevBatchCommitment,
455:         bytes32 _currentBatchCommitment,
456:         VerifierParams memory _verifierParams
457:     ) internal pure returns (uint256) {

500:     function _createBatchCommitment(
501:         CommitBatchInfo calldata _newBatchData,
502:         bytes32 _stateDiffHash,
503:         bytes32[] memory _blobCommitments,
504:         bytes32[] memory _blobHashes
505:     ) internal view returns (bytes32) {

515:     function _batchPassThroughData(CommitBatchInfo calldata _batch) internal pure returns (bytes memory) {

525:     function _batchMetaParameters() internal view returns (bytes memory) {

537:     function _batchAuxiliaryOutput(
538:         CommitBatchInfo calldata _batch,
539:         bytes32 _stateDiffHash,
540:         bytes32[] memory _blobCommitments,
541:         bytes32[] memory _blobHashes
542:     ) internal pure returns (bytes memory) {

561:     function _encodeBlobAuxilaryOutput(
562:         bytes32[] memory _blobCommitments,
563:         bytes32[] memory _blobHashes
564:     ) internal pure returns (bytes32[] memory blobAuxOutputWords) {

592:     function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

597:     function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {

605:     function _pointEvaluationPrecompile(
606:         bytes32 _versionedHash,
607:         bytes32 _openingPoint,
608:         bytes calldata _openingValueCommitmentProof
609:     ) internal view {

625:     function _verifyBlobInformation(
626:         bytes calldata _pubdataCommitments,
627:         bytes32[] memory _blobHashes
628:     ) internal view returns (bytes32[] memory blobCommitments) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L103-L107) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L130-L133), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L253-L256), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L273-L277), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L308-L308), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L321-L321), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L453-L457), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L500-L505), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L515-L515), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L525-L525), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L561-L564), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L592-L592), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L597-L597), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L605-L609), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L625-L628)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

130:     function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {

258:     function _requestL2Transaction(
259:         uint256 _mintValue,
260:         WritePriorityOpParams memory _params,
261:         bytes memory _calldata,
262:         bytes[] memory _factoryDeps
263:     ) internal returns (bytes32 canonicalTxHash) {

289:     function _serializeL2Transaction(
290:         WritePriorityOpParams memory _priorityOpParams,
291:         bytes memory _calldata,
292:         bytes[] memory _factoryDeps
293:     ) internal pure returns (L2CanonicalTransaction memory transaction) {

316:     function _writePriorityOp(
317:         WritePriorityOpParams memory _priorityOpParams,
318:         bytes memory _calldata,
319:         bytes[] memory _factoryDeps
320:     ) internal returns (bytes32 canonicalTxHash) {

353:     function _hashFactoryDeps(bytes[] memory _factoryDeps) internal pure returns (uint256[] memory hashedFactoryDeps) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L130-L130) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L258-L263), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L289-L293), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L316-L320), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L353-L353)


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

163:     function _upgradeVerifier(address _newVerifier, VerifierParams calldata _verifierParams) internal {

171:     function _setBaseSystemContracts(bytes32 _bootloaderHash, bytes32 _defaultAccountHash) internal {

180:     function _setL2SystemContractUpgrade(
181:         L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
182:         bytes[] calldata _factoryDeps,
183:         uint256 _newProtocolVersion
184:     ) internal returns (bytes32) {

236:     function _setNewProtocolVersion(uint256 _newProtocolVersion) internal virtual {

263:     function _upgradeL1Contract(bytes calldata _customCallDataForUpgrade) internal virtual {}

269:     function _postUpgrade(bytes calldata _customCallDataForUpgrade) internal virtual {}


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L163-L163) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L171-L171), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L180-L184), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L236-L236), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L263-L263), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L269-L269)


```solidity

File: contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

20:     function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20-L20) 


```solidity

File: contracts/bridge/L2SharedBridge.sol

109:     function _deployL2Token(address _l1Token, bytes calldata _data) internal returns (address) {

138:     function _getL1WithdrawMessage(
139:         address _to,
140:         address _l1Token,
141:         uint256 _amount
142:     ) internal pure returns (bytes memory) {

164:     function _deployBeaconProxy(bytes32 salt) internal returns (BeaconProxy proxy) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L109-L109) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L138-L142), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L164-L164)


</details>


### [GAS&#x2011;24] `require()`/`revert()` strings longer than 32 bytes cost extra gas 
Each extra memory word of bytes past the original 32 [incurs an MSTORE](https://gist.github.com/hrkrshnn/ee8fabd532058307229d65dcd5836ddc#consider-having-short-revert-strings) which costs **3 gas**


*There are 105 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/AccountCodeStorage.sol

26:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
27:         _;

37:         require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");
38:         _storeCodeHash(_address, _hash);

48:         require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");
49:         _storeCodeHash(_address, _hash);

57:         require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");
58: 


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L26-L27) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L37-L38), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L48-L49), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L57-L58)


```solidity

File: contracts/ComplexUpgrader.sol

22:         require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");
23: 


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ComplexUpgrader.sol#L22-L23) 


```solidity

File: contracts/Compressor.sol

51:             require(
52:                 encodedData.length * 4 == _bytecode.length,
53:                 "Encoded data length should be 4 times shorter than the original bytecode"
54:             );

56:             require(
57:                 dictionary.length / 8 <= encodedData.length / 2,
58:                 "Dictionary should have at most the same number of entries as the encoded data"
59:             );

63:                 require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");
64: 

68:                 require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");
69:             }

119:         require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");
120: 

156:         require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");
157: 

187:         require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");
188: 

230:                 require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");
231:             } else if (_operation == 1) {

232:                 require(
233:                     _initialValue + convertedValue == _finalValue,
234:                     "add: initial plus converted not equal to final"
235:                 );

237:                 require(
238:                     _initialValue - convertedValue == _finalValue,
239:                     "sub: initial minus converted not equal to final"
240:                 );


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L51-L54) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L56-L59), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L63-L64), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L68-L69), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L119-L120), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L156-L157), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L187-L188), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L230-L231), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L232-L235), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L237-L240)


```solidity

File: contracts/ContractDeployer.sol

77:         require(
78:             _nonceOrdering == AccountNonceOrdering.Arbitrary &&
79:                 currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
80:             "It is only possible to change from sequential to arbitrary ordering"
81:         );

239:         require(
240:             msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
241:             "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
242:         );

251:         require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");
252: 

265:         require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");
266: 

350:             require(value == 0, "The value must be zero if we do not call the constructor");
351:             // If we do not call the constructor, we need to set the constructed code hash.


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L77-L81) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L239-L242), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L251-L252), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L265-L266), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L350-L351)


```solidity

File: contracts/DefaultAccount.sol

100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");
101: 

202:         require(success, "Failed to pay the fee to the operator");
203:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L100-L101) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L202-L203)


```solidity

File: contracts/ImmutableSimulator.sol

35:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
36:         unchecked {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L35-L36) 


```solidity

File: contracts/KnownCodesStorage.sol

76:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
77: 


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L76-L77) 


```solidity

File: contracts/L1Messenger.sol

214:         require(
215:             reconstructedChainedLogsHash == chainedLogsHash,
216:             "reconstructedChainedLogsHash is not equal to chainedLogsHash"
217:         );

245:         require(
246:             reconstructedChainedMessagesHash == chainedMessagesHash,
247:             "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
248:         );

269:         require(
270:             reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
271:             "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
272:         );

279:         require(
280:             uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
281:                 STATE_DIFF_COMPRESSION_VERSION_NUMBER,
282:             "state diff compression version mismatch"
283:         );

315:         require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");
316: 


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L214-L217) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L245-L248), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L269-L272), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L279-L283), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L315-L316)


```solidity

File: contracts/L2BaseToken.sol

33:         require(
34:             msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
35:                 msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
36:                 msg.sender == BOOTLOADER_FORMAL_ADDRESS,
37:             "Only system contracts with special access can call this method"
38:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L33-L38) 


```solidity

File: contracts/NonceHolder.sol

66:         require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");
67: 

136:         require(
137:             msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
138:             "Only the contract deployer can increment the deployment nonce"
139:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L66-L67) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L136-L139)


```solidity

File: contracts/SystemContext.sol

242:         require(_isFirstInBatch, "Upgrade transaction must be first");
243: 

245:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");
246: 

249:             require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");
250: 

287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");
288:             _maxVirtualBlocksToCreate -= 1;

351:             require(
352:                 _l2BlockTimestamp >= currentBatchTimestamp,
353:                 "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
354:             );

355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");
356:         }

367:             require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");
368:             require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");

368:             require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");
369:             require(

369:             require(
370:                 _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
371:                 "The previous hash of the same L2 block must be same"
372:             );

373:             require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");
374:         } else if (currentL2BlockNumber + 1 == _l2BlockNumber) {

385:             require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");
386:             require(

386:             require(
387:                 _l2BlockTimestamp > currentL2BlockTimestamp,
388:                 "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
389:             );

413:         require(currentBatchNumber > 0, "The current batch number must be greater than 0");
414: 

429:         require(
430:             _newTimestamp > currentBlockTimestamp,
431:             "The timestamp of the batch must be greater than the timestamp of the previous block"
432:         );

452:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
453: 


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L242-L243) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L245-L246), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L249-L250), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L287-L288), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L351-L354), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L355-L356), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L367-L368), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L368-L369), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L369-L372), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L373-L374), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L385-L386), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L386-L389), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L413-L414), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L429-L432), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L452-L453)


```solidity

File: contracts/interfaces/ISystemContract.sol

21:         require(
22:             SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
23:             "This method require system call flag"
24:         );

31:         require(
32:             SystemContractHelper.isSystemContract(msg.sender),
33:             "This method require the caller to be system contract"
34:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L21-L24) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L31-L34)


```solidity

File: contracts/libraries/SystemContractHelper.sol

319:         require(index < 10, "There are only 10 accessible registers");
320: 


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L319-L320) 


```solidity

File: contracts/libraries/TransactionHelper.sol

363:         require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");
364: 

367:             require(
368:                 _transaction.paymasterInput.length >= 68,
369:                 "The approvalBased paymaster input must be at least 68 bytes long"
370:             );


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L363-L364) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L367-L370)


```solidity

File: contracts/bridge/L1SharedBridge.sol

75:         require(
76:             msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
77:             "L1SharedBridge: not bridgehub or era chain"
78:         );

155:             require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");
156:         } else {

195:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");
196: 

427:             require(!alreadyFinalized, "Withdrawal is already finalized 2");
428:         }

522:             revert("ShB Incorrect message function selector");
523:         }

564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
565: 


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L75-L78) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L155-L156), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L195-L196), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L427-L428), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L522-L523), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L564-L565)


```solidity

File: contracts/bridgehub/Bridgehub.sol

83:         require(
84:             !stateTransitionManagerIsRegistered[_stateTransitionManager],
85:             "Bridgehub: state transition already registered"
86:         );

93:         require(
94:             stateTransitionManagerIsRegistered[_stateTransitionManager],
95:             "Bridgehub: state transition not registered yet"
96:         );

102:         require(!tokenIsRegistered[_token], "Bridgehub: token already registered");
103:         tokenIsRegistered[_token] = true;

125:         require(
126:             stateTransitionManagerIsRegistered[_stateTransitionManager],
127:             "Bridgehub: state transition not registered"
128:         );

132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");
133: 

225:                 require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");
226:             }

300:         require(
301:             _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
302:             "Bridgehub: second bridge address too low"
303:         ); // to avoid calls to precompiles


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L83-L86) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L93-L96), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L102-L103), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L125-L128), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L132-L133), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L225-L226), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L300-L303)


```solidity

File: contracts/governance/Governance.sol

59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
60:         _;

65:         require(msg.sender == securityCouncil, "Only security council is allowed to call this function");
66:         _;

71:         require(
72:             msg.sender == owner() || msg.sender == securityCouncil,
73:             "Only the owner and security council are allowed to call this function"
74:         );

172:         require(isOperationReady(id), "Operation must be ready before execution");
173:         // Execute operation.

177:         require(isOperationReady(id), "Operation must be ready after execution");
178:         // Set operation to be done

191:         require(isOperationPending(id), "Operation must be pending before execution");
192:         // Execute operation.

196:         require(isOperationPending(id), "Operation must be pending after execution");
197:         // Set operation to be done

216:         require(!isOperation(_id), "Operation with this proposal id already exists");
217:         require(_delay >= minDelay, "Proposed delay is less than minimum delay");

217:         require(_delay >= minDelay, "Proposed delay is less than minimum delay");
218: 

240:         require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");
241:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L59-L60) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L65-L66), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L71-L74), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L172-L173), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L177-L178), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L191-L192), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L196-L197), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L216-L217), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L217-L218), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L240-L241)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

256:         require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");
257: 


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L256-L257) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

62:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");
63:         _;

68:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
69:         _;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L62-L63) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L68-L69)


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

90:         require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed
91:         s.feeParams.pubdataPricingMode = _validiumMode;

105:         require(
106:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107:             "StateTransition: cutHash mismatch"
108:         );

110:         require(
111:             s.protocolVersion == _oldProtocolVersion,
112:             "StateTransition: protocolVersion mismatch in STC when upgrading"
113:         );

116:         require(
117:             s.protocolVersion > _oldProtocolVersion,
118:             "StateTransition: protocolVersion mismatch in STC after upgrading"
119:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L90-L91) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L105-L108), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L110-L113), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L116-L119)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

226:         require(
227:             IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
228:             "Executor facet: wrong protocol version"
229:         );

616:         require(success, "failed to call point evaluation precompile");
617:         (, uint256 result) = abi.decode(data, (uint256, uint256));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L226-L229) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L616-L617)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

39:         require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");
40: 

158:         require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");
159:         uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /

185:         require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");
186:         IL1SharedBridge(s.baseTokenBridge).finalizeWithdrawal(

206:         require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");
207:         canonicalTxHash = _requestL2TransactionSender(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L39-L40) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L158-L159), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L185-L186), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L206-L207)


```solidity

File: contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

22:         require(s.validators[msg.sender], "StateTransition Chain: not validator");
23:         _;

27:         require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");
28:         _;

32:         require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");
33:         _;

37:         require(
38:             msg.sender == s.admin || msg.sender == s.stateTransitionManager,
39:             "StateTransition Chain: Only by admin or state transition manager"
40:         );

45:         require(
46:             s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
47:             "StateTransition Chain: Only by validator or state transition manager"
48:         );

53:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
54:         _;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22-L23) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27-L28), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32-L33), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L37-L40), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45-L48), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53-L54)


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

190:         require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");
191: 

205:         require(
206:             _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
207:             "The new protocol version should be included in the L2 system upgrade tx"
208:         );

238:         require(
239:             _newProtocolVersion > previousProtocolVersion,
240:             "New protocol version is not greater than the current one"
241:         );

242:         require(
243:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
244:             "Too big protocol version difference"
245:         );

249:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
250:         require(

250:         require(
251:             s.l2SystemContractsUpgradeBatchNumber == 0,
252:             "The batch number of the previous upgrade has not been cleaned"
253:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L190-L191) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L205-L208), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L238-L241), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L242-L245), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L249-L250), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L250-L253)


```solidity

File: contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

22:         require(
23:             // Genesis Upgrade difference: Note this is the only thing change > to >=
24:             _newProtocolVersion >= previousProtocolVersion,
25:             "New protocol version is not greater than the current one"
26:         );

27:         require(
28:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
29:             "Too big protocol version difference"
30:         );

33:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
34:         require(

34:         require(
35:             s.l2SystemContractsUpgradeBatchNumber == 0,
36:             "The batch number of the previous upgrade has not been cleaned"
37:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22-L26) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L27-L30), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33-L34), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L34-L37)


```solidity

File: contracts/bridge/L2SharedBridge.sol

92:         require(msg.value == 0, "Value should be 0 for ERC20 bridge");
93: 


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L92-L93) 


</details>


### [GAS&#x2011;25] Consider merging sequential for loops 
Merging multiple `for` loops within a function in Solidity can enhance efficiency and reduce gas costs, especially when they share a common iterating variable or perform related operations. By minimizing redundant iterations over the same data set, execution becomes more cost-effective. However, while merging can optimize gas usage and simplify logic, it may also increase code complexity. Therefore, careful balance between optimization and maintainability is essential, along with thorough testing to ensure the refactored code behaves as expected.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/Compressor.sol

127:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
128:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
129:             uint64 enumIndex = stateDiff.readUint64(84);
130:             if (enumIndex != 0) {
131:                 // It is a repeated write, so we skip it.
132:                 continue;
133:             }
134: 
135:             numInitialWritesProcessed++;
136: 
137:             bytes32 derivedKey = stateDiff.readBytes32(52);
138:             uint256 initValue = stateDiff.readUint256(92);
139:             uint256 finalValue = stateDiff.readUint256(124);
140:             require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");
141:             stateDiffPtr += 32;
142: 
143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
144:             stateDiffPtr++;
145:             uint8 operation = metadata & OPERATION_BITMASK;
146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
147:             _verifyValueCompression(
148:                 initValue,
149:                 finalValue,
150:                 operation,
151:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
152:             );
153:             stateDiffPtr += len;
154:         }
155: 
156:         require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");
157: 
158:         // Process repeated writes
159:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L127-L159) 


```solidity

File: contracts/ContractDeployer.sol

248:         for (uint256 i = 0; i < deploymentsLength; ++i) {
249:             sumOfValues += _deployments[i].value;
250:         }
251:         require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");
252: 
253:         for (uint256 i = 0; i < deploymentsLength; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L248-L253) 


</details>


### [GAS&#x2011;26] Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct`, where appropriate 
Saves a storage slot for the mapping. Depending on the circumstances and sizes of types, can avoid a Gsset (**20000 gas**) per mapping combined. Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Finally, if both fields are accessed in the same function, can save **~42 gas per access** due to [not having to recalculate the key's keccak256 hash](https://gist.github.com/IllIllI000/ec23a57daa30a8f8ca8b9681c8ccefb0) (Gkeccak256 - 30 gas) and that calculation's associated stack operations.


*There are 6 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/bridge/L1ERC20Bridge.sol

32:     mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))

45:     mapping(address => uint256) private __DEPRECATED_lastWithdrawalLimitReset;

48:     mapping(address => uint256) private __DEPRECATED_withdrawnAmountInWindow;

51:     mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L32-L32) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L45-L45), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L48-L48), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L51-L51)


```solidity

File: contracts/bridgehub/Bridgehub.sol

21:     mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;

23:     mapping(address _token => bool) public tokenIsRegistered;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L21-L21) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L23-L23)


</details>


### [GAS&#x2011;27] Optimize names to save gas 
`public`/`external` function names and `public` member variable names can be optimized to save gas. See [this](https://gist.github.com/IllIllI000/a5d8b486a8259f9f77891a919febd1a9) link for an example of how it works. Below are the interfaces/abstract contracts that can be optimized so that the most frequently-called functions use the least amount of gas possible during method lookup. Method IDs that have two leading zero bytes can save **128 gas** each during deployment, and renaming functions to have lower method IDs will save **22 gas** per call, [per sorted position shifted](https://medium.com/joyso/solidity-how-does-function-name-affect-gas-consumption-in-smart-contract-47d270d8ac92)


*There are 49 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ContractDeployer.sol

// @audit extendedAccountVersion(address) ==> extendedAccountVersion_uaR(address),0000a709
23: contract ContractDeployer is IContractDeployer, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L23-L23) 


```solidity

File: contracts/L1Messenger.sol

// @audit publishPubdataAndClearState(bytes) ==> publishPubdataAndClearState_KeV(bytes),0000cdf3
25: contract L1Messenger is IL1Messenger, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L25-L25) 


```solidity

File: contracts/SystemContext.sol

// @audit setChainId(uint256) ==> setChainId_Neq(uint256),0000f915
// @audit setTxOrigin(address) ==> setTxOrigin_ANR(address),00003c03
// @audit setGasPrice(uint256) ==> setGasPrice_WeF(uint256),00003047
// @audit setPubdataInfo(uint256,uint256) ==> setPubdataInfo_m63(uint256,uint256),0000e57d
// @audit getCurrentPubdataCost() ==> getCurrentPubdataCost_WnL(),00007d98
// @audit setL2Block(uint128,uint128,bytes32,bool,uint128) ==> setL2Block_i4K(uint128,uint128,bytes32,bool,uint128),00002aeb
// @audit appendTransactionToCurrentL2Block(bytes32) ==> appendTransactionToCurrentL2Block_s5L(bytes32),00004c0a
// @audit publishTimestampDataToL1() ==> publishTimestampDataToL1_Bjv(),00008dcb
// @audit setNewBatch(bytes32,uint128,uint128,uint256) ==> setNewBatch_4aU(bytes32,uint128,uint128,uint256),00008bba
// @audit unsafeOverrideBatch(uint256,uint256,uint256) ==> unsafeOverrideBatch_aik(uint256,uint256,uint256),000006f4
// @audit incrementTxNumberInBatch() ==> incrementTxNumberInBatch_lL(),0000ea07
// @audit resetTxNumberInBatch() ==> resetTxNumberInBatch_d6N(),0000bcd1
17: contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L17-L17) 


```solidity

File: contracts/interfaces/IAccountCodeStorage.sol

// @audit storeAccountConstructingCodeHash(address,bytes32) ==> storeAccountConstructingCodeHash_2aF(address,bytes32),0000700d
// @audit storeAccountConstructedCodeHash(address,bytes32) ==> storeAccountConstructedCodeHash_83Z(address,bytes32),0000bfea
// @audit markAccountCodeHashAsConstructed(address) ==> markAccountCodeHashAsConstructed_qBJ(address),000059d0
// @audit getRawCodeHash(address) ==> getRawCodeHash_tyR(address),00004449
// @audit getCodeHash(uint256) ==> getCodeHash_H51q(uint256),00004c7a
5: interface IAccountCodeStorage {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IAccountCodeStorage.sol#L5-L5) 


```solidity

File: contracts/interfaces/IBaseToken.sol

// @audit balanceOf(uint256) ==> balanceOf_ljD(uint256),00000286
// @audit transferFromTo(address,address,uint256) ==> transferFromTo_45m(address,address,uint256),00005f70
// @audit totalSupply() ==> totalSupply_B6A(),00005a30
// @audit name() ==> name_v1V(),00006681
// @audit symbol() ==> symbol_km(),000087e0
// @audit decimals() ==> decimals_ckx(),000000ea
// @audit mint(address,uint256) ==> mint_Qgo(address,uint256),00001784
// @audit withdraw(address) ==> withdraw_rO7(address),00006cce
// @audit withdrawWithMessage(address,bytes) ==> withdrawWithMessage_a5V(address,bytes),0000a82d
5: interface IBaseToken {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IBaseToken.sol#L5-L5) 


```solidity

File: contracts/interfaces/IComplexUpgrader.sol

// @audit upgrade(address,bytes) ==> upgrade_KcF(address,bytes),0000bf82
10: interface IComplexUpgrader {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IComplexUpgrader.sol#L10-L10) 


```solidity

File: contracts/interfaces/ICompressor.sol

// @audit publishCompressedBytecode(bytes,bytes) ==> publishCompressedBytecode_t2J(bytes,bytes),00006cb3
// @audit verifyCompressedStateDiffs(uint256,uint256,bytes,bytes) ==> verifyCompressedStateDiffs_Rbt(uint256,uint256,bytes,bytes),000078ce
18: interface ICompressor {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ICompressor.sol#L18-L18) 


```solidity

File: contracts/interfaces/IContractDeployer.sol

// @audit getNewAddressCreate2(address,bytes32,bytes32,bytes) ==> getNewAddressCreate2_ChE(address,bytes32,bytes32,bytes),00001706
// @audit getNewAddressCreate(address,uint256) ==> getNewAddressCreate_K3h(address,uint256),0000ec72
// @audit create2(bytes32,bytes32,bytes) ==> create2_FoO(bytes32,bytes32,bytes),000004f0
// @audit create(bytes32,bytes32,bytes) ==> create_mU1M(bytes32,bytes32,bytes),00006f40
// @audit getAccountInfo(address) ==> getAccountInfo_tn(address),0000eac4
5: interface IContractDeployer {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IContractDeployer.sol#L5-L5) 


```solidity

File: contracts/interfaces/IImmutableSimulator.sol

// @audit getImmutable(address,uint256) ==> getImmutable_5f6(address,uint256),0000022e
10: interface IImmutableSimulator {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IImmutableSimulator.sol#L10-L10) 


```solidity

File: contracts/interfaces/IKnownCodesStorage.sol

// @audit markFactoryDeps(bool,bytes32[]) ==> markFactoryDeps_HlC(bool,bytes32[]),00003e74
// @audit markBytecodeAsPublished(bytes32) ==> markBytecodeAsPublished_LiC(bytes32),0000a55c
// @audit getMarker(bytes32) ==> getMarker_81H(bytes32),00009524
11: interface IKnownCodesStorage {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IKnownCodesStorage.sol#L11-L11) 


```solidity

File: contracts/interfaces/IL1Messenger.sol

// @audit sendToL1(bytes) ==> sendToL1_W1O(bytes),00002736
// @audit sendL2ToL1Log(bool,bytes32,bytes32) ==> sendL2ToL1Log_XJY(bool,bytes32,bytes32),00006c1f
40: interface IL1Messenger {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IL1Messenger.sol#L40-L40) 


```solidity

File: contracts/interfaces/IL2StandardToken.sol

// @audit bridgeBurn(address,uint256) ==> bridgeBurn_C7z(address,uint256),0000d61d
// @audit l1Address() ==> l1Address_7bQ(),00003741
// @audit l2Bridge() ==> l2Bridge_m2x(),0000227a
5: interface IL2StandardToken {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IL2StandardToken.sol#L5-L5) 


```solidity

File: contracts/interfaces/IMailbox.sol

// @audit finalizeEthWithdrawal(uint256,uint256,uint16,bytes,bytes32[]) ==> finalizeEthWithdrawal_03v(uint256,uint256,uint16,bytes,bytes32[]),00006a0f
5: interface IMailbox {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IMailbox.sol#L5-L5) 


```solidity

File: contracts/interfaces/INonceHolder.sol

// @audit getMinNonce(address) ==> getMinNonce_I3G(address),0000e26b
// @audit getRawNonce(address) ==> getRawNonce_kjd(address),00009242
// @audit increaseMinNonce(uint256) ==> increaseMinNonce_C2N(uint256),00000de6
// @audit setValueUnderNonce(uint256,uint256) ==> setValueUnderNonce_Tne(uint256,uint256),0000e130
// @audit getValueUnderNonce(uint256) ==> getValueUnderNonce_383(uint256),000099d1
// @audit incrementMinNonceIfEquals(uint256) ==> incrementMinNonceIfEquals_O1A(uint256),0000d15e
// @audit getDeploymentNonce(address) ==> getDeploymentNonce_W2s(address),00004438
// @audit incrementDeploymentNonce(address) ==> incrementDeploymentNonce_d5N(address),0000a901
// @audit validateNonceUsage(address,uint256,bool) ==> validateNonceUsage_Y8w(address,uint256,bool),0000c2dc
// @audit isNonceUsed(address,uint256) ==> isNonceUsed_lMS(address,uint256),00005f49
13: interface INonceHolder {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/INonceHolder.sol#L13-L13) 


```solidity

File: contracts/interfaces/IPaymasterFlow.sol

// @audit general(bytes) ==> general_L3I(bytes),00009df8
// @audit approvalBased(address,uint256,bytes) ==> approvalBased_MgP(address,uint256,bytes),000013ad
12: interface IPaymasterFlow {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IPaymasterFlow.sol#L12-L12) 


```solidity

File: contracts/interfaces/IPubdataChunkPublisher.sol

// @audit chunkAndPublishPubdata(bytes) ==> chunkAndPublishPubdata_inX(bytes),00008ad2
9: interface IPubdataChunkPublisher {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IPubdataChunkPublisher.sol#L9-L9) 


```solidity

File: contracts/interfaces/ISystemContext.sol

// @audit chainId() ==> chainId_DeZ(),00005e1e
// @audit origin() ==> origin_S2m(),0000b15e
// @audit gasPrice() ==> gasPrice_81G(),00007fb9
// @audit blockGasLimit() ==> blockGasLimit_G2G(),0000e4c5
// @audit coinbase() ==> coinbase_V96(),0000148f
// @audit difficulty() ==> difficulty_fhV(),00000281
// @audit baseFee() ==> baseFee_xnW(),00001af1
// @audit txNumberInBlock() ==> txNumberInBlock_uqT(),0000a928
// @audit getBlockHashEVM(uint256) ==> getBlockHashEVM_xD8(uint256),00006084
// @audit getBatchHash(uint256) ==> getBatchHash_f3R(uint256),000099a3
// @audit getBlockNumber() ==> getBlockNumber_91N(),00004fae
// @audit getBlockTimestamp() ==> getBlockTimestamp_92X(),000058f6
// @audit getBatchNumberAndTimestamp() ==> getBatchNumberAndTimestamp_GzB(),0000d297
// @audit getL2BlockNumberAndTimestamp() ==> getL2BlockNumberAndTimestamp_B26(),00005c9d
// @audit gasPerPubdataByte() ==> gasPerPubdataByte_PlH(),00004aba
// @audit getCurrentPubdataSpent() ==> getCurrentPubdataSpent_ZAN(),0000a231
11: interface ISystemContext {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContext.sol#L11-L11) 


```solidity

File: contracts/interfaces/ISystemContextDeprecated.sol

// @audit currentBlockInfo() ==> currentBlockInfo_2H5(),00004d55
// @audit getBlockNumberAndTimestamp() ==> getBlockNumberAndTimestamp_Oma(),0000bace
// @audit blockHash(uint256) ==> blockHash_c84(uint256),0000ed7f
10: interface ISystemContextDeprecated {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContextDeprecated.sol#L10-L10) 


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

// @audit initialize() ==> initialize_Gh2(),0000315c
19: contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L19-L19) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

// @audit initialize(address,uint256) ==> initialize_C7f(address,uint256),0000d6a7
// @audit transferFundsFromLegacy(address,address,uint256) ==> transferFundsFromLegacy_DmR(address,address,uint256),0000079e
// @audit initializeChainGovernance(uint256,address) ==> initializeChainGovernance_N8c(uint256,address),00007017
30: contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L30-L30) 


```solidity

File: contracts/bridge/interfaces/IL1ERC20Bridge.sol

// @audit isWithdrawalFinalized(uint256,uint256) ==> isWithdrawalFinalized_23R(uint256,uint256),000051f3
// @audit deposit(address,address,uint256,uint256,uint256,address) ==> deposit_tay(address,address,uint256,uint256,uint256,address),00001dfc
// @audit deposit(address,address,uint256,uint256,uint256) ==> deposit_J9W(address,address,uint256,uint256,uint256),000009fe
// @audit claimFailedDeposit(address,address,bytes32,uint256,uint256,uint16,bytes32[]) ==> claimFailedDeposit_B9M(address,address,bytes32,uint256,uint256,uint16,bytes32[]),0000f22e
// @audit finalizeWithdrawal(uint256,uint256,uint16,bytes,bytes32[]) ==> finalizeWithdrawal_X6T(uint256,uint256,uint16,bytes,bytes32[]),00000481
// @audit l2TokenAddress(address) ==> l2TokenAddress_Ec6(address),0000d47f
// @audit sharedBridge() ==> sharedBridge_96c(),0000094a
// @audit l2TokenBeacon() ==> l2TokenBeacon_sb6(),0000c58f
// @audit l2Bridge() ==> l2Bridge_m2x(),0000227a
// @audit depositAmount(address,address,bytes32) ==> depositAmount_t3W(address,address,bytes32),0000c93c
// @audit tranferTokenToSharedBridge(address,uint256) ==> tranferTokenToSharedBridge_Ijo(address,uint256),00002ac2
11: interface IL1ERC20Bridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11-L11) 


```solidity

File: contracts/bridge/interfaces/IL1SharedBridge.sol

// @audit isWithdrawalFinalized(uint256,uint256,uint256) ==> isWithdrawalFinalized_PuP(uint256,uint256,uint256),0000e319
// @audit depositLegacyErc20Bridge(address,address,address,uint256,uint256,uint256,address) ==> depositLegacyErc20Bridge_qav(address,address,address,uint256,uint256,uint256,address),00003a60
// @audit claimFailedDepositLegacyErc20Bridge(address,address,uint256,bytes32,uint256,uint256,uint16,bytes32[]) ==> claimFailedDepositLegacyErc20Bridge_x13(address,address,uint256,bytes32,uint256,uint256,uint16,bytes32[]),00002aca
// @audit claimFailedDeposit(uint256,address,address,uint256,bytes32,uint256,uint256,uint16,bytes32[]) ==> claimFailedDeposit_Tt1(uint256,address,address,uint256,bytes32,uint256,uint256,uint16,bytes32[]),0000bda9
// @audit finalizeWithdrawalLegacyErc20Bridge(uint256,uint256,uint16,bytes,bytes32[]) ==> finalizeWithdrawalLegacyErc20Bridge_K5B(uint256,uint256,uint16,bytes,bytes32[]),00004ec6
// @audit finalizeWithdrawal(uint256,uint256,uint256,uint16,bytes,bytes32[]) ==> finalizeWithdrawal_Osx(uint256,uint256,uint256,uint16,bytes,bytes32[]),00001042
// @audit l1WethAddress() ==> l1WethAddress_Iam(),0000ed98
// @audit bridgehub() ==> bridgehub_wzy(),00002add
// @audit legacyBridge() ==> legacyBridge_e6t(),000041e6
// @audit l2BridgeAddress(uint256) ==> l2BridgeAddress_fAZ(uint256),00008629
// @audit depositHappened(uint256,bytes32) ==> depositHappened_weP(uint256,bytes32),0000bfbc
// @audit bridgehubDeposit(uint256,address,uint256,bytes) ==> bridgehubDeposit_jBe(uint256,address,uint256,bytes),00007b9b
// @audit bridgehubDepositBaseToken(uint256,address,address,uint256) ==> bridgehubDepositBaseToken_y8V(uint256,address,address,uint256),00007267
// @audit bridgehubConfirmL2Transaction(uint256,bytes32,bytes32) ==> bridgehubConfirmL2Transaction_7id(uint256,bytes32,bytes32),00003b03
// @audit receiveEth(uint256) ==> receiveEth_x9f(uint256),00004d09
12: interface IL1SharedBridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL1SharedBridge.sol#L12-L12) 


```solidity

File: contracts/bridge/interfaces/IL2Bridge.sol

// @audit finalizeDeposit(address,address,address,uint256,bytes) ==> finalizeDeposit_9dK(address,address,address,uint256,bytes),00005523
// @audit withdraw(address,address,uint256) ==> withdraw_ci4(address,address,uint256),00007f2d
// @audit l1TokenAddress(address) ==> l1TokenAddress_VcU(address),0000115d
// @audit l2TokenAddress(address) ==> l2TokenAddress_Ec6(address),0000d47f
// @audit l1Bridge() ==> l1Bridge_X9E(),0000681d
6: interface IL2Bridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL2Bridge.sol#L6-L6) 


```solidity

File: contracts/bridge/interfaces/IWETH9.sol

// @audit deposit() ==> deposit_WjZ(),000061eb
// @audit withdraw(uint256) ==> withdraw_6BK(uint256),0000b293
4: interface IWETH9 {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IWETH9.sol#L4-L4) 


```solidity

File: contracts/bridgehub/Bridgehub.sol

// @audit initialize(address) ==> initialize_G9M(address),00008134
16: contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L16-L16) 


```solidity

File: contracts/bridgehub/IBridgehub.sol

// @audit setPendingAdmin(address) ==> setPendingAdmin_3s5(address),0000cc67
// @audit acceptAdmin() ==> acceptAdmin_YF3(),000091cf
// @audit stateTransitionManagerIsRegistered(address) ==> stateTransitionManagerIsRegistered_F5I(address),0000c17e
// @audit stateTransitionManager(uint256) ==> stateTransitionManager_jz3(uint256),00000c21
// @audit tokenIsRegistered(address) ==> tokenIsRegistered_H8N(address),0000897a
// @audit baseToken(uint256) ==> baseToken_95j(uint256),00000855
// @audit sharedBridge() ==> sharedBridge_96c(),0000094a
// @audit getStateTransition(uint256) ==> getStateTransition_TP(uint256),00008654
// @audit l2TransactionBaseCost(uint256,uint256,uint256,uint256) ==> l2TransactionBaseCost_XIS(uint256,uint256,uint256,uint256),0000e435
// @audit createNewChain(uint256,address,address,uint256,address,bytes) ==> createNewChain_34g(uint256,address,address,uint256,address,bytes),000000b2
// @audit addStateTransitionManager(address) ==> addStateTransitionManager_N95(address),000095e5
// @audit removeStateTransitionManager(address) ==> removeStateTransitionManager_D3H(address),0000df96
// @audit addToken(address) ==> addToken_y3C(address),0000c92c
// @audit setSharedBridge(address) ==> setSharedBridge_mh6(address),0000779a
42: interface IBridgehub {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/IBridgehub.sol#L42-L42) 


```solidity

File: contracts/common/interfaces/IL2ContractDeployer.sol

// @audit create2(bytes32,bytes32,bytes) ==> create2_FoO(bytes32,bytes32,bytes),000004f0
9: interface IL2ContractDeployer {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/interfaces/IL2ContractDeployer.sol#L9-L9) 


```solidity

File: contracts/governance/IGovernance.sol

// @audit isOperation(bytes32) ==> isOperation_jL(bytes32),00008e31
// @audit isOperationPending(bytes32) ==> isOperationPending_e15(bytes32),00006b4c
// @audit isOperationReady(bytes32) ==> isOperationReady_b3g(bytes32),00005bdf
// @audit isOperationDone(bytes32) ==> isOperationDone_slR(bytes32),0000c7f2
// @audit getOperationState(bytes32) ==> getOperationState_tzZ(bytes32),0000e9f4
// @audit scheduleShadow(bytes32,uint256) ==> scheduleShadow_n6r(bytes32,uint256),00008faa
// @audit cancel(bytes32) ==> cancel_Xqu(bytes32),00002dcf
// @audit updateDelay(uint256) ==> updateDelay_0do(uint256),0000a4ca
// @audit updateSecurityCouncil(address) ==> updateSecurityCouncil_h5M(address),0000f456
8: interface IGovernance {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/IGovernance.sol#L8-L8) 


```solidity

File: contracts/state-transition/IStateTransitionManager.sol

// @audit bridgehub() ==> bridgehub_wzy(),00002add
// @audit setPendingAdmin(address) ==> setPendingAdmin_3s5(address),0000cc67
// @audit acceptAdmin() ==> acceptAdmin_YF3(),000091cf
// @audit storedBatchZero() ==> storedBatchZero_hbI(),0000663c
// @audit initialCutHash() ==> initialCutHash_ebI(),00008627
// @audit genesisUpgrade() ==> genesisUpgrade_9gT(),000058a8
// @audit upgradeCutHash(uint256) ==> upgradeCutHash_3fy(uint256),0000ac59
// @audit protocolVersion() ==> protocolVersion_Icn(),0000d638
// @audit setValidatorTimelock(address) ==> setValidatorTimelock_slS(address),00009589
// @audit getChainAdmin(uint256) ==> getChainAdmin_whg(uint256),0000cae7
// @audit createNewChain(uint256,address,address,address,bytes) ==> createNewChain_cjj(uint256,address,address,address,bytes),00005f5c
// @audit registerAlreadyDeployedStateTransition(uint256,address) ==> registerAlreadyDeployedStateTransition_0gv(uint256,address),00007d58
// @audit freezeChain(uint256) ==> freezeChain_rby(uint256),0000c96d
// @audit unfreezeChain(uint256) ==> unfreezeChain_T9F(uint256),0000efa5
26: interface IStateTransitionManager {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/IStateTransitionManager.sol#L26-L26) 


```solidity

File: contracts/state-transition/StateTransitionManager.sol

// @audit revertBatches(uint256,uint256) ==> revertBatches_UlA(uint256,uint256),00002d59
25: contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L25-L25) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

// @audit addValidator(uint256,address) ==> addValidator_r84(uint256,address),00006392
// @audit removeValidator(uint256,address) ==> removeValidator_rgQ(uint256,address),00005453
// @audit setExecutionDelay(uint32) ==> setExecutionDelay_iiw(uint32),0000dda0
// @audit getCommittedBatchTimestamp(uint256,uint256) ==> getCommittedBatchTimestamp_b3p(uint256,uint256),00005cc3
22: contract ValidatorTimelock is IExecutor, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L22-L22) 


```solidity

File: contracts/state-transition/chain-interfaces/IAdmin.sol

// @audit setPendingAdmin(address) ==> setPendingAdmin_3s5(address),0000cc67
// @audit acceptAdmin() ==> acceptAdmin_YF3(),000091cf
// @audit setPorterAvailability(bool) ==> setPorterAvailability_HcG(bool),0000fb3b
// @audit setPriorityTxMaxGasLimit(uint256) ==> setPriorityTxMaxGasLimit_tFZ(uint256),000077cf
// @audit setTokenMultiplier(uint128,uint128) ==> setTokenMultiplier_U5h(uint128,uint128),00001d4c
// @audit freezeDiamond() ==> freezeDiamond_UY(),000055c7
// @audit unfreezeDiamond() ==> unfreezeDiamond_7ct(),00002fd0
13: interface IAdmin is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IAdmin.sol#L13-L13) 


```solidity

File: contracts/state-transition/chain-interfaces/IExecutor.sol

// @audit revertBatchesSharedBridge(uint256,uint256) ==> revertBatchesSharedBridge_hr(uint256,uint256),00009473
73: interface IExecutor is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IExecutor.sol#L73-L73) 


```solidity

File: contracts/state-transition/chain-interfaces/IGetters.sol

// @audit getVerifier() ==> getVerifier_C1d(),0000ba20
// @audit getAdmin() ==> getAdmin_GcZ(),000054f3
// @audit getPendingAdmin() ==> getPendingAdmin_4bC(),00009945
// @audit getBridgehub() ==> getBridgehub_1mR(),0000b6f3
// @audit getStateTransitionManager() ==> getStateTransitionManager_E40(),0000d8d8
// @audit getBaseToken() ==> getBaseToken_Srf(),00003d8c
// @audit getBaseTokenBridge() ==> getBaseTokenBridge_hmf(),0000f2c6
// @audit getTotalBatchesCommitted() ==> getTotalBatchesCommitted_673(),0000793f
// @audit getTotalBatchesVerified() ==> getTotalBatchesVerified_wk7(),0000056a
// @audit getTotalBatchesExecuted() ==> getTotalBatchesExecuted_MkR(),000039e8
// @audit getTotalPriorityTxs() ==> getTotalPriorityTxs_DiV(),0000ab28
// @audit getFirstUnprocessedPriorityTx() ==> getFirstUnprocessedPriorityTx_3f3(),0000412e
// @audit getPriorityQueueSize() ==> getPriorityQueueSize_45J(),000024ec
// @audit priorityQueueFrontOperation() ==> priorityQueueFrontOperation_cnk(),000070e2
// @audit isValidator(address) ==> isValidator_B9D(address),0000df60
// @audit l2LogsRootHash(uint256) ==> l2LogsRootHash_AAk(uint256),00009365
// @audit storedBatchHash(uint256) ==> storedBatchHash_f7z(uint256),00005d98
// @audit getL2BootloaderBytecodeHash() ==> getL2BootloaderBytecodeHash_sbY(),00007d34
// @audit getL2DefaultAccountBytecodeHash() ==> getL2DefaultAccountBytecodeHash_sbn(),00001482
// @audit getVerifierParams() ==> getVerifierParams_049(),00007b0c
// @audit isDiamondStorageFrozen() ==> isDiamondStorageFrozen_Ha9(),0000378f
// @audit getProtocolVersion() ==> getProtocolVersion_ycH(),0000933a
// @audit getL2SystemContractsUpgradeTxHash() ==> getL2SystemContractsUpgradeTxHash_dlY(),0000d7be
// @audit getL2SystemContractsUpgradeBatchNumber() ==> getL2SystemContractsUpgradeBatchNumber_Ng7(),0000b2e5
// @audit getPriorityTxMaxGasLimit() ==> getPriorityTxMaxGasLimit_E3M(),0000fd50
// @audit isEthWithdrawalFinalized(uint256,uint256) ==> isEthWithdrawalFinalized_bo1M(uint256,uint256),0000f456
// @audit getPubdataPricingMode() ==> getPubdataPricingMode_NfU(),0000b2c7
// @audit baseTokenGasPriceMultiplierNominator() ==> baseTokenGasPriceMultiplierNominator_t8j(),00007e7c
// @audit baseTokenGasPriceMultiplierDenominator() ==> baseTokenGasPriceMultiplierDenominator_m4D(),0000faa1
// @audit facets() ==> facets_nkr(),000007f4
// @audit facetFunctionSelectors(address) ==> facetFunctionSelectors_E1e(address),00008e42
// @audit facetAddresses() ==> facetAddresses_Dsu(),00000fc4
// @audit facetAddress(bytes4) ==> facetAddress_JTk(bytes4),00001f7a
// @audit isFunctionFreezable(bytes4) ==> isFunctionFreezable_o4Z(bytes4),00008b54
// @audit isFacetFreezable(address) ==> isFacetFreezable_N1T(address),0000a556
13: interface IGetters is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IGetters.sol#L13-L13) 


```solidity

File: contracts/state-transition/chain-interfaces/ILegacyGetters.sol

// @audit getTotalBlocksCommitted() ==> getTotalBlocksCommitted_N40(),00008ef7
// @audit getTotalBlocksVerified() ==> getTotalBlocksVerified_dOw(),0000743e
// @audit getTotalBlocksExecuted() ==> getTotalBlocksExecuted_Ynk(),00009fd1
// @audit storedBlockHash(uint256) ==> storedBlockHash_9us(uint256),0000325b
// @audit getL2SystemContractsUpgradeBlockNumber() ==> getL2SystemContractsUpgradeBlockNumber_IcI(),000023c1
11: interface ILegacyGetters is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L11-L11) 


```solidity

File: contracts/state-transition/chain-interfaces/IMailbox.sol

// @audit finalizeEthWithdrawal(uint256,uint256,uint16,bytes,bytes32[]) ==> finalizeEthWithdrawal_03v(uint256,uint256,uint16,bytes,bytes32[]),00006a0f
// @audit requestL2Transaction(address,uint256,bytes,uint256,uint256,bytes[],address) ==> requestL2Transaction_3cW(address,uint256,bytes,uint256,uint256,bytes[],address),00009bd2
// @audit l2TransactionBaseCost(uint256,uint256,uint256) ==> l2TransactionBaseCost_m3F(uint256,uint256,uint256),000057e9
// @audit transferEthToSharedBridge() ==> transferEthToSharedBridge_wBB(),00008dc0
11: interface IMailbox is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IMailbox.sol#L11-L11) 


```solidity

File: contracts/state-transition/chain-interfaces/IVerifier.sol

// @audit verify(uint256[],uint256[],uint256[]) ==> verify_42S(uint256[],uint256[],uint256[]),0000ef81
// @audit verificationKeyHash() ==> verificationKeyHash_H3K(),000099a1
15: interface IVerifier {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IVerifier.sol#L15-L15) 


```solidity

File: contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol

// @audit getName() ==> getName_NXz(),00006a46
7: interface IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L7-L7) 


```solidity

File: contracts/state-transition/l2-deps/ISystemContext.sol

// @audit setChainId(uint256) ==> setChainId_Neq(uint256),0000f915
4: interface ISystemContext {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/l2-deps/ISystemContext.sol#L4-L4) 


```solidity

File: contracts/L2ContractHelper.sol

// @audit sendToL1(bytes) ==> sendToL1_W1O(bytes),00002736
18: interface IL2Messenger {

// @audit create2(bytes32,bytes32,bytes) ==> create2_FoO(bytes32,bytes32,bytes),000004f0
30: interface IContractDeployer {

// @audit withdrawWithMessage(address,bytes) ==> withdrawWithMessage_a5V(address,bytes),0000a82d
61: interface IBaseToken {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L18-L18) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L30-L30), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L61-L61)


```solidity

File: contracts/bridge/L2SharedBridge.sol

// @audit initialize(address,address,bytes32,address) ==> initialize_wcW(address,address,bytes32,address),0000ef21
23: contract L2SharedBridge is IL2SharedBridge, Initializable {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L23-L23) 


```solidity

File: contracts/bridge/L2StandardERC20.sol

// @audit bridgeInitialize(address,bytes) ==> bridgeInitialize_Wai(address,bytes),000081fc
// @audit decodeString(bytes) ==> decodeString_reE(bytes),00002e72
// @audit decodeUint8(bytes) ==> decodeUint8_tgl(bytes),0000d0c3
15: contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L15-L15) 


```solidity

File: contracts/bridge/interfaces/IL1ERC20Bridge.sol

// @audit finalizeWithdrawal(uint256,uint256,uint16,bytes,bytes32[]) ==> finalizeWithdrawal_X6T(uint256,uint256,uint16,bytes,bytes32[]),00000481
8: interface IL1ERC20Bridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL1ERC20Bridge.sol#L8-L8) 


```solidity

File: contracts/bridge/interfaces/IL1SharedBridge.sol

// @audit finalizeWithdrawal(uint256,uint256,uint256,uint16,bytes,bytes32[]) ==> finalizeWithdrawal_Osx(uint256,uint256,uint256,uint16,bytes,bytes32[]),00001042
8: interface IL1SharedBridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL1SharedBridge.sol#L8-L8) 


```solidity

File: contracts/bridge/interfaces/IL2SharedBridge.sol

// @audit finalizeDeposit(address,address,address,uint256,bytes) ==> finalizeDeposit_9dK(address,address,address,uint256,bytes),00005523
// @audit withdraw(address,address,uint256) ==> withdraw_ci4(address,address,uint256),00007f2d
// @audit l1TokenAddress(address) ==> l1TokenAddress_VcU(address),0000115d
// @audit l2TokenAddress(address) ==> l2TokenAddress_Ec6(address),0000d47f
// @audit l1Bridge() ==> l1Bridge_X9E(),0000681d
6: interface IL2SharedBridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL2SharedBridge.sol#L6-L6) 


```solidity

File: contracts/bridge/interfaces/IL2StandardToken.sol

// @audit bridgeBurn(address,uint256) ==> bridgeBurn_C7z(address,uint256),0000d61d
// @audit l1Address() ==> l1Address_7bQ(),00003741
// @audit l2Bridge() ==> l2Bridge_m2x(),0000227a
5: interface IL2StandardToken {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL2StandardToken.sol#L5-L5) 


```solidity

File: contracts/interfaces/IPaymasterFlow.sol

// @audit general(bytes) ==> general_L3I(bytes),00009df8
// @audit approvalBased(address,uint256,bytes) ==> approvalBased_MgP(address,uint256,bytes),000013ad
13: interface IPaymasterFlow {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/interfaces/IPaymasterFlow.sol#L13-L13) 


</details>


### [GAS&#x2011;28] Not using the named return variables anywhere in the function wast gas 
Consider changing the variable to be an unnamed one, since the variable is never assigned, nor is it returned by name. If the optimizer is not turned on, leaving the code as it is will also waste gas for the stack variable.


*There are 4 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/BootloaderUtilities.sol

// @audit txHash
44:     function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L44-L44) 


```solidity

File: contracts/ContractDeployer.sol

// @audit info
34:     function getAccountInfo(address _address) external view returns (AccountInfo memory info) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L34-L34) 


```solidity

File: contracts/bridgehub/Bridgehub.sol

// @audit chainId
114:     function createNewChain(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L114-L114) 


```solidity

File: contracts/state-transition/libraries/Diamond.sol

// @audit diamondStorage
87:     function getDiamondStorage() internal pure returns (DiamondStorage storage diamondStorage) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L87-L87) 


</details>


### [GAS&#x2011;29] Enable Solidity's optimizer 
Make sure Solidity's optimizer is enabled. It reduces gas costs. If you want to gas optimize for contract deployment (costs less to deploy a contract) then set the Solidity optimizer at a low number. If you want to optimize for run-time gas costs (when functions are called on a contract) then set the optimizer to a high number.
Set the optimization value higher than 800 in your hardhat.config.ts file.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: hardhat.config.ts

//@audit c4/competitions/2024-03-zksync/code/contracts/zksync/hardhat.config.ts
1: 


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//hardhat.config.ts#L1-L1) 


</details>


### [GAS&#x2011;30] Structs can be packed into fewer storage slots 
Each slot saved can avoid an extra Gsset (**20000 gas**) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/state-transition/IStateTransitionManager.sol

// @audit from 7 to 6 you need to change the structure elements order to: , bytes32, bytes32, uint256, address, address, address, uint64, Diamond.DiamondCutData
15: struct StateTransitionManagerInitializeData {
16:     address governor;
17:     address validatorTimelock;
18:     address genesisUpgrade;
19:     bytes32 genesisBatchHash;
20:     uint64 genesisIndexRepeatedStorageChanges;
21:     bytes32 genesisBatchCommitment;
22:     Diamond.DiamondCutData diamondCut;
23:     uint256 protocolVersion;
24: }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/IStateTransitionManager.sol#L15-L24) 


```solidity

File: contracts/state-transition/chain-interfaces/IExecutor.sol

// @audit from 8 to 7 you need to change the structure elements order to: , bytes32, uint256, bytes32, bytes32, uint256, bytes32, uint64, uint64
83:     struct StoredBatchInfo {
84:         uint64 batchNumber;
85:         bytes32 batchHash;
86:         uint64 indexRepeatedStorageChanges;
87:         uint256 numberOfLayer1Txs;
88:         bytes32 priorityOperationsHash;
89:         bytes32 l2LogsTreeRoot;
90:         uint256 timestamp;
91:         bytes32 commitment;
92:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IExecutor.sol#L83-L92) 


</details>


### [GAS&#x2011;31] Constructors can be marked `payable` 
Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided.A constructor can safely be marked as payable, since only the deployer would be able to pass funds, and the project itself would not pass any funds.


*There are 10 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/bridge/L1ERC20Bridge.sol

55:     constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
56:         sharedBridge = _sharedBridge;
57:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L55-L57) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

90:     constructor(
91:         address _l1WethAddress,
92:         IBridgehub _bridgehub,
93:         IL1ERC20Bridge _legacyBridge
94:     ) reentrancyGuardInitializer {
95:         _disableInitializers();
96:         l1WethAddress = _l1WethAddress;
97:         bridgehub = _bridgehub;
98:         legacyBridge = _legacyBridge;
99:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L90-L99) 


```solidity

File: contracts/bridgehub/Bridgehub.sol

38:     constructor() reentrancyGuardInitializer {}


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L38-L38) 


```solidity

File: contracts/governance/Governance.sol

41:     constructor(address _admin, address _securityCouncil, uint256 _minDelay) {
42:         require(_admin != address(0), "Admin should be non zero address");
43: 
44:         _transferOwnership(_admin);
45: 
46:         securityCouncil = _securityCouncil;
47:         emit ChangeSecurityCouncil(address(0), _securityCouncil);
48: 
49:         minDelay = _minDelay;
50:         emit ChangeMinDelay(0, _minDelay);
51:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L41-L51) 


```solidity

File: contracts/state-transition/StateTransitionManager.sol

58:     constructor(address _bridgehub) reentrancyGuardInitializer {
59:         bridgehub = _bridgehub;
60:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L58-L60) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

55:     constructor(address _initialOwner, uint32 _executionDelay) {
56:         _transferOwnership(_initialOwner);
57:         executionDelay = _executionDelay;
58:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L55-L58) 


```solidity

File: contracts/state-transition/chain-deps/DiamondInit.sol

19:     constructor() reentrancyGuardInitializer {}


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondInit.sol#L19-L19) 


```solidity

File: contracts/state-transition/chain-deps/DiamondProxy.sol

11:     constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
12:         // Check that the contract is deployed on the expected chain.
13:         // Thus, the contract deployed by the same Create2 factory on the different chain will have different addresses!
14:         require(_chainId == block.chainid, "pr");
15:         Diamond.diamondCut(_diamondCut);
16:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondProxy.sol#L11-L16) 


```solidity

File: contracts/bridge/L2SharedBridge.sol

41:     constructor() {
42:         _disableInitializers();
43:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L41-L43) 


```solidity

File: contracts/bridge/L2StandardERC20.sol

40:     constructor() {
41:         // Disable initialization to prevent Parity hack.
42:         _disableInitializers();
43:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L40-L43) 


</details>


### [GAS&#x2011;32] Using `private` rather than `public` for constants, saves gas 
If needed, the values can be read from the verified contract source code, or if there are multiple values there can be a single getter function that [returns a tuple](https://github.com/code-423n4/2022-08-frax/blob/90f55a9ce4e25bceed3a74290b854341d8de6afa/src/contracts/FraxlendPair.sol#L156-L178) of the values of all currently-public constants. Saves **3406-3606 gas** in deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it's used, and not adding another entry to the method ID table


*There are 5 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/state-transition/ValidatorTimelock.sol

26:     string public constant override getName = "ValidatorTimelock";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L26-L26) 


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

20:     string public constant override getName = "AdminFacet";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L20-L20) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

27:     string public constant override getName = "ExecutorFacet";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L27-L27) 


```solidity

File: contracts/state-transition/chain-deps/facets/Getters.sol

25:     string public constant override getName = "GettersFacet";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L25-L25) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

35:     string public constant override getName = "MailboxFacet";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L35-L35) 


</details>


### [GAS&#x2011;33] `private` functions only called once can be inlined to save gas 
Not inlining costs 20 to 40 gas because of two extra JUMP instructions and additional stack operations needed for function calls.


*There are 6 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/common/ReentrancyGuard.sol

46:     function _initializeReentrancyGuard() private {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/ReentrancyGuard.sol#L46-L46) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

92:     function _setL2DefaultAccountBytecodeHash(bytes32 _l2DefaultAccountBytecodeHash) private {

109:     function _setL2BootloaderBytecodeHash(bytes32 _l2BootloaderBytecodeHash) private {

126:     function _setVerifier(IVerifier _newVerifier) private {

142:     function _setVerifierParams(VerifierParams calldata _newVerifierParams) private {

222:     function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L92-L92) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L109-L109), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L126-L126), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L142-L142), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L222-L222)


</details>


### [GAS&#x2011;34] Remove or replace unused state variables 
Saves a storage slot. If the variable is assigned a non-zero value, saves Gsset (**20000 gas**). If it's assigned a zero value, saves Gsreset (**2900 gas**). If the variable remains unassigned, there is no gas savings unless the variable is `public`, in which case the compiler-generated non-payable getter deployment cost is saved. If the state variable is overriding an interface's public function, mark the variable as `constant` or `immutable` so that it does not use a storage slot


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/SystemContext.sol

37:     uint256 public blockGasLimit = type(uint32).max;

41:     address public coinbase = BOOTLOADER_FORMAL_ADDRESS;

44:     uint256 public difficulty = 2.5e15;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L37-L37) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L41-L41), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L44-L44)


</details>


### [GAS&#x2011;35] Redundant else statement 



*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/governance/Governance.sol

111:         } else if (timestamp > block.timestamp) {
112:             return OperationState.Waiting;
113:         } else {
114:             return OperationState.Ready;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L111-L114) 


</details>


### [GAS&#x2011;36] Functions guaranteed to revert when called by normal users can be marked `payable` 
If a function modifier such as `onlyOwner` is used, the function will revert if a normal user tries to pay the function. Marking the function as `payable` will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided.The extra opcodes avoided are `CALLVALUE`(2), `DUP1`(3), `ISZERO`(3), `PUSH2`(3), `JUMPI`(10), `PUSH1`(3), `DUP1`(3), `REVERT`(0), `JUMPDEST`(1), `POP`(2), which costs an average of about ** 21 gas per call ** to the function, in addition to the extra deployment cost


*There are 96 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/AccountCodeStorage.sol

35:     function storeAccountConstructingCodeHash(address _address, bytes32 _hash) external override onlyDeployer {

46:     function storeAccountConstructedCodeHash(address _address, bytes32 _hash) external override onlyDeployer {

54:     function markAccountCodeHashAsConstructed(address _address) external override onlyDeployer {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L35-L35) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L46-L46), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L54-L54)


```solidity

File: contracts/ContractDeployer.sol

65:     function updateAccountVersion(AccountAbstractionVersion _version) external onlySystemCall {

74:     function updateNonceOrdering(AccountNonceOrdering _nonceOrdering) external onlySystemCall {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L65-L65) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L74-L74)


```solidity

File: contracts/ImmutableSimulator.sol

34:     function setImmutables(address _dest, ImmutableData[] calldata _immutables) external override {
35:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L34-L35) 


```solidity

File: contracts/KnownCodesStorage.sol

27:     function markFactoryDeps(bool _shouldSendToL1, bytes32[] calldata _hashes) external onlyCallFromBootloader {

39:     function markBytecodeAsPublished(bytes32 _bytecodeHash) external onlyCompressor {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L27-L27) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L39-L39)


```solidity

File: contracts/L1Messenger.sol

70:     function sendL2ToL1Log(
71:         bool _isService,
72:         bytes32 _key,
73:         bytes32 _value
74:     ) external onlyCallFromSystemContract returns (uint256 logIdInMerkleTree) {

161:     function requestBytecodeL1Publication(
162:         bytes32 _bytecodeHash
163:     ) external override onlyCallFrom(address(KNOWN_CODE_STORAGE_CONTRACT)) {

194:     function publishPubdataAndClearState(
195:         bytes calldata _totalL2ToL1PubdataAndStateDiffs
196:     ) external onlyCallFromBootloader {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L70-L74) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L161-L163), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L194-L196)


```solidity

File: contracts/L2BaseToken.sol

32:     function transferFromTo(address _from, address _to, uint256 _amount) external override {
33:         require(
34:             msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
35:                 msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
36:                 msg.sender == BOOTLOADER_FORMAL_ADDRESS,

64:     function mint(address _account, uint256 _amount) external override onlyCallFromBootloader {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L32-L36) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L64-L64)


```solidity

File: contracts/NonceHolder.sol

65:     function increaseMinNonce(uint256 _value) public onlySystemCall returns (uint256 oldMinNonce) {

82:     function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall {

110:     function incrementMinNonceIfEquals(uint256 _expectedNonce) external onlySystemCall {

135:     function incrementDeploymentNonce(address _address) external returns (uint256 prevDeploymentNonce) {
136:         require(
137:             msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L65-L65) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L82-L82), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L110-L110), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L135-L137)


```solidity

File: contracts/PubdataChunkPublisher.sol

21:     function chunkAndPublishPubdata(bytes calldata _pubdata) external onlyCallFrom(address(L1_MESSENGER_CONTRACT)) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L21-L21) 


```solidity

File: contracts/SystemContext.sol

84:     function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {

99:     function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {

105:     function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {

112:     function setPubdataInfo(uint256 _gasPerPubdataByte, uint256 _basePubdataSpent) external onlyCallFromBootloader {

341:     function setL2Block(
342:         uint128 _l2BlockNumber,
343:         uint128 _l2BlockTimestamp,
344:         bytes32 _expectedPrevL2BlockHash,
345:         bool _isFirstInBatch,
346:         uint128 _maxVirtualBlocksToCreate
347:     ) external onlyCallFromBootloader {

402:     function appendTransactionToCurrentL2Block(bytes32 _txHash) external onlyCallFromBootloader {

408:     function publishTimestampDataToL1() external onlyCallFromBootloader {

444:     function setNewBatch(
445:         bytes32 _prevBatchHash,
446:         uint128 _newTimestamp,
447:         uint128 _expectedNewNumber,
448:         uint256 _baseFee
449:     ) external onlyCallFromBootloader {

471:     function unsafeOverrideBatch(
472:         uint256 _newTimestamp,
473:         uint256 _number,
474:         uint256 _baseFee
475:     ) external onlyCallFromBootloader {

482:     function incrementTxNumberInBatch() external onlyCallFromBootloader {

486:     function resetTxNumberInBatch() external onlyCallFromBootloader {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L84-L84) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L99-L99), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L105-L105), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L112-L112), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L341-L347), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L402-L402), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L408-L408), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L444-L449), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L471-L475), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L482-L482), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L486-L486)


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

63:     function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
64:         require(msg.sender == address(sharedBridge), "Not shared bridge");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L63-L64) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

116:     function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {

142:     function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner {

232:     function bridgehubConfirmL2Transaction(
233:         uint256 _chainId,
234:         bytes32 _txDataHash,
235:         bytes32 _txHash
236:     ) external override onlyBridgehub {

615:     function finalizeWithdrawalLegacyErc20Bridge(
616:         uint256 _l2BatchNumber,
617:         uint256 _l2MessageIndex,
618:         uint16 _l2TxNumberInBatch,
619:         bytes calldata _message,
620:         bytes32[] calldata _merkleProof
621:     ) external override onlyLegacyBridge returns (address l1Receiver, address l1Token, uint256 amount) {

644:     function claimFailedDepositLegacyErc20Bridge(
645:         address _depositSender,
646:         address _l1Token,
647:         uint256 _amount,
648:         bytes32 _l2TxHash,
649:         uint256 _l2BatchNumber,
650:         uint256 _l2MessageIndex,
651:         uint16 _l2TxNumberInBatch,
652:         bytes32[] calldata _merkleProof
653:     ) external override onlyLegacyBridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L116-L116) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L142-L142), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L232-L236), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L615-L621), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L644-L653)


```solidity

File: contracts/bridgehub/Bridgehub.sol

51:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

60:     function acceptAdmin() external {
61:         address currentPendingAdmin = pendingAdmin;
62:         require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

82:     function addStateTransitionManager(address _stateTransitionManager) external onlyOwner {

92:     function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner {

101:     function addToken(address _token) external onlyOwner {

108:     function setSharedBridge(address _sharedBridge) external onlyOwner {

114:     function createNewChain(
115:         uint256 _chainId,
116:         address _stateTransitionManager,
117:         address _baseToken,
118:         uint256, //_salt
119:         address _admin,
120:         bytes calldata _initData
121:     ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {

325:     function _actualRefundRecipient(address _refundRecipient) internal view returns (address _recipient) {
326:         if (_refundRecipient == address(0)) {
327:             // If the `_refundRecipient` is not provided, we use the `msg.sender` as the recipient.
328:             _recipient = msg.sender == tx.origin ? msg.sender : AddressAliasHelper.applyL1ToL2Alias(msg.sender);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L51-L51) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L60-L62), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L82-L82), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L92-L92), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L101-L101), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L108-L108), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L114-L121), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L325-L328)


```solidity

File: contracts/governance/Governance.sol

129:     function scheduleTransparent(Operation calldata _operation, uint256 _delay) external onlyOwner {

142:     function scheduleShadow(bytes32 _id, uint256 _delay) external onlyOwner {

154:     function cancel(bytes32 _id) external onlyOwner {

249:     function updateDelay(uint256 _newDelay) external onlySelf {

256:     function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L129-L129) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L142-L142), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L154-L154), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L249-L249), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L256-L256)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

110:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

119:     function acceptAdmin() external {
120:         address currentPendingAdmin = pendingAdmin;
121:         require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

132:     function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {

137:     function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {

142:     function setNewVersionUpgrade(
143:         Diamond.DiamondCutData calldata _cutData,
144:         uint256 _oldProtocolVersion,
145:         uint256 _newProtocolVersion
146:     ) external onlyOwner {

152:     function setUpgradeDiamondCut(
153:         Diamond.DiamondCutData calldata _cutData,
154:         uint256 _oldProtocolVersion
155:     ) external onlyOwner {

160:     function freezeChain(uint256 _chainId) external onlyOwner {

165:     function unfreezeChain(uint256 _chainId) external onlyOwner {

170:     function revertBatches(uint256 _chainId, uint256 _newLastBatch) external onlyOwnerOrAdmin {

230:     function registerAlreadyDeployedStateTransition(
231:         uint256 _chainId,
232:         address _stateTransitionContract
233:     ) external onlyOwner {

239:     function createNewChain(
240:         uint256 _chainId,
241:         address _baseToken,
242:         address _sharedBridge,
243:         address _admin,
244:         bytes calldata _diamondCut
245:     ) external onlyBridgehub {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L110-L110) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L119-L121), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L132-L132), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L137-L137), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L142-L146), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L152-L155), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L160-L160), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L165-L165), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L170-L170), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L230-L233), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L239-L245)


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

73:     function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {

78:     function addValidator(uint256 _chainId, address _newValidator) external onlyChainAdmin(_chainId) {

87:     function removeValidator(uint256 _chainId, address _validator) external onlyChainAdmin(_chainId) {

96:     function setExecutionDelay(uint32 _executionDelay) external onlyOwner {

108:     function commitBatches(
109:         StoredBatchInfo calldata,
110:         CommitBatchInfo[] calldata _newBatchesData
111:     ) external onlyValidator(ERA_CHAIN_ID) {

126:     function commitBatchesSharedBridge(
127:         uint256 _chainId,
128:         StoredBatchInfo calldata,
129:         CommitBatchInfo[] calldata _newBatchesData
130:     ) external onlyValidator(_chainId) {

146:     function revertBatches(uint256) external onlyValidator(ERA_CHAIN_ID) {

153:     function revertBatchesSharedBridge(uint256 _chainId, uint256) external onlyValidator(_chainId) {

160:     function proveBatches(
161:         StoredBatchInfo calldata,
162:         StoredBatchInfo[] calldata,
163:         ProofInput calldata
164:     ) external onlyValidator(ERA_CHAIN_ID) {

171:     function proveBatchesSharedBridge(
172:         uint256 _chainId,
173:         StoredBatchInfo calldata,
174:         StoredBatchInfo[] calldata,
175:         ProofInput calldata
176:     ) external onlyValidator(_chainId) {

182:     function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {

203:     function executeBatchesSharedBridge(
204:         uint256 _chainId,
205:         StoredBatchInfo[] calldata _newBatchesData
206:     ) external onlyValidator(_chainId) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L73-L73) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L78-L78), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L87-L87), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L96-L96), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L108-L111), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L126-L130), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L146-L146), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L153-L153), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L160-L164), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L171-L176), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L182-L182), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L203-L206)


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

23:     function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {

32:     function acceptAdmin() external {
33:         address pendingAdmin = s.pendingAdmin;
34:         require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights

45:     function setValidator(address _validator, bool _active) external onlyStateTransitionManager {

51:     function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {

58:     function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager {

67:     function changeFeeParams(FeeParams calldata _newFeeParams) external onlyAdminOrStateTransitionManager {

79:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {

89:     function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {

100:     function upgradeChainFromVersion(
101:         uint256 _oldProtocolVersion,
102:         Diamond.DiamondCutData calldata _diamondCut
103:     ) external onlyAdminOrStateTransitionManager {

123:     function executeUpgrade(Diamond.DiamondCutData calldata _diamondCut) external onlyStateTransitionManager {

133:     function freezeDiamond() external onlyAdminOrStateTransitionManager {

143:     function unfreezeDiamond() external onlyAdminOrStateTransitionManager {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L23-L23) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L32-L34), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L45-L45), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L51-L51), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L58-L58), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L67-L67), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L79-L79), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L89-L89), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L100-L103), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L123-L123), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L133-L133), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L143-L143)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

199:     function commitBatches(
200:         StoredBatchInfo memory _lastCommittedBatchData,
201:         CommitBatchInfo[] calldata _newBatchesData
202:     ) external nonReentrant onlyValidator {

207:     function commitBatchesSharedBridge(
208:         uint256, // _chainId
209:         StoredBatchInfo memory _lastCommittedBatchData,
210:         CommitBatchInfo[] calldata _newBatchesData
211:     ) external nonReentrant onlyValidator {

337:     function executeBatchesSharedBridge(
338:         uint256,
339:         StoredBatchInfo[] calldata _batchesData
340:     ) external nonReentrant onlyValidator {

345:     function executeBatches(StoredBatchInfo[] calldata _batchesData) external nonReentrant onlyValidator {

368:     function proveBatches(
369:         StoredBatchInfo calldata _prevBatch,
370:         StoredBatchInfo[] calldata _committedBatches,
371:         ProofInput calldata _proof
372:     ) external nonReentrant onlyValidator {

377:     function proveBatchesSharedBridge(
378:         uint256, // _chainId
379:         StoredBatchInfo calldata _prevBatch,
380:         StoredBatchInfo[] calldata _committedBatches,
381:         ProofInput calldata _proof
382:     ) external nonReentrant onlyValidator {

472:     function revertBatches(uint256 _newLastBatch) external nonReentrant onlyValidatorOrStateTransitionManager {

477:     function revertBatchesSharedBridge(uint256, uint256 _newLastBatch) external nonReentrant onlyValidator {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L199-L202) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L207-L211), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L337-L340), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L345-L345), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L368-L372), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L377-L382), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L472-L472), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L477-L477)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

38:     function transferEthToSharedBridge() external onlyBaseTokenBridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L38-L38) 


```solidity

File: contracts/bridge/L2StandardERC20.sol

111:     function reinitializeToken(
112:         ERC20Getters calldata _availableGetters,
113:         string memory _newName,
114:         string memory _newSymbol,
115:         uint8 _version
116:     ) external onlyNextVersion(_version) reinitializer(_version) {

111:     function reinitializeToken(
112:         ERC20Getters calldata _availableGetters,
113:         string memory _newName,
114:         string memory _newSymbol,
115:         uint8 _version
116:     ) external onlyNextVersion(_version) reinitializer(_version) {
117:         // It is expected that this token is deployed as a beacon proxy, so we'll
118:         // allow the governor of the beacon to reinitialize the token.
119:         address beaconAddress = _getBeacon();
120:         require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");

145:     function bridgeMint(address _to, uint256 _amount) external override onlyBridge {

154:     function bridgeBurn(address _from, uint256 _amount) external override onlyBridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L111-L116) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L111-L120), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L145-L145), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L154-L154)


</details>


### [GAS&#x2011;37] Avoid updating storage when the value hasn't changed to save gas 
If the old value is equal to the new value, not re-storing the value will avoid a Gsreset (**2900 gas**), potentially at the expense of a Gcoldsload (**2100 gas**) or a Gwarmaccess (**100 gas**)


*There are 28 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ContractDeployer.sol

65:     function updateAccountVersion(AccountAbstractionVersion _version) external onlySystemCall {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L65-L65) 


```solidity

File: contracts/SystemContext.sol

84:     function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {

99:     function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {

105:     function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {

112:     function setPubdataInfo(uint256 _gasPerPubdataByte, uint256 _basePubdataSpent) external onlyCallFromBootloader {

486:     function resetTxNumberInBatch() external onlyCallFromBootloader {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L84-L84) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L99-L99), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L105-L105), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L112-L112), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L486-L486)


```solidity

File: contracts/bridgehub/Bridgehub.sol

51:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

108:     function setSharedBridge(address _sharedBridge) external onlyOwner {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L51-L51) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L108-L108)


```solidity

File: contracts/governance/Governance.sol

249:     function updateDelay(uint256 _newDelay) external onlySelf {

256:     function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L249-L249) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L256-L256)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

110:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

132:     function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {

137:     function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {

142:     function setNewVersionUpgrade(

152:     function setUpgradeDiamondCut(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L110-L110) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L132-L132), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L137-L137), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L142-L142), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L152-L152)


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

73:     function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {

96:     function setExecutionDelay(uint32 _executionDelay) external onlyOwner {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L73-L73) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L96-L96)


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

23:     function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {

45:     function setValidator(address _validator, bool _active) external onlyStateTransitionManager {

51:     function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {

58:     function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager {

67:     function changeFeeParams(FeeParams calldata _newFeeParams) external onlyAdminOrStateTransitionManager {

79:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L23-L23) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L45-L45), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L51-L51), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L58-L58), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L67-L67), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L79-L79)


```solidity

File: contracts/state-transition/chain-deps/facets/Getters.sol

57:     function getBaseToken() external view returns (address) {

62:     function getBaseTokenBridge() external view returns (address) {

67:     function baseTokenGasPriceMultiplierNominator() external view returns (uint128) {

72:     function baseTokenGasPriceMultiplierDenominator() external view returns (uint128) {

188:     function isEthWithdrawalFinalized(uint256 _l2BatchNumber, uint256 _l2MessageIndex) external view returns (bool) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L57-L57) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L62-L62), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L67-L67), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L72-L72), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L188-L188)


</details>


### [GAS&#x2011;38] Use shift Right instead of division if possible to save gas 



*There are 4 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/Compressor.sol

57:                 dictionary.length / 8 <= encodedData.length / 2,

57:                 dictionary.length / 8 <= encodedData.length / 2,


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L57-L57) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L57-L57)


```solidity

File: contracts/state-transition/libraries/LibMap.sol

23:             uint256 mapValue = _map.map[_index / 8];

43:             uint256 mapIndex = _index / 8;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L23-L23) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L43-L43)


</details>


### [GAS&#x2011;39] Use shift Left instead of multiplication if possible to save gas 



*There are 19 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/BootloaderUtilities.sol

97:                 vInt += 8 + block.chainid * 2;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L97-L97) 


```solidity

File: contracts/Compressor.sol

52:                 encodedData.length * 4 == _bytecode.length,

62:                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;

66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

203:             dictionary = _rawCompressedData[2:2 + dictionaryLen * 8];

204:             encodedData = _rawCompressedData[2 + dictionaryLen * 8:];

253:         number >>= (256 - (_calldataSlice.length * 8));


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L52-L52) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L62-L62), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L66-L66), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L203-L203), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L204-L204), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L253-L253)


```solidity

File: contracts/L1Messenger.sol

89:         uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) + 2 * keccakGasCost(64);

226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])

226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L89-L89) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L226-L226), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L226-L226)


```solidity

File: contracts/libraries/RLPEncoder.sol

37:                 uint256 shiftedVal = _val << (lbs * 8);

72:                 uint256 shiftedVal = uint256(_len) << (lbs * 8);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L37-L37) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L72-L72)


```solidity

File: contracts/libraries/Utils.sol

87:         require(lengthInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L87-L87) 


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

26:         require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L26-L26) 


```solidity

File: contracts/state-transition/StateTransitionManager.sol

106:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L106-L106) 


```solidity

File: contracts/state-transition/chain-deps/DiamondInit.sol

51:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondInit.sol#L51-L51) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

578:         blobAuxOutputWords = new bytes32[](2 * TOTAL_BLOBS_IN_COMMITMENT);

581:             blobAuxOutputWords[i * 2] = _blobHashes[i];

582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L578-L578) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L581-L581), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L582-L582)


</details>


### [GAS&#x2011;40] Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead 
> When using elements that are smaller than 32 bytes, your contract's gas usage may be higher. This is because the EVM operates on 32 bytes at a time. Therefore, if the element is smaller than that, the EVM must use more operations in order to reduce the size of the element from 32 bytes to the desired size.
https://docs.soliditylang.org/en/v0.8.11/internals/layout_in_storage.html
Each operation involving a `uint8` costs an extra [** 22 - 28 gas **](https://gist.github.com/IllIllI000/9388d20c70f9a4632eb3ca7836f54977) (depending on whether the other operand is also a variable of type `uint8`) as compared to ones involving `uint256`, due to the compiler having to clear the higher bits of the memory word before operating on the `uint8`, as well as the associated stack operations of doing so. Use a larger size then downcast where needed


*There are 178 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/BootloaderUtilities.sol

//@audit `txDataLen` is `uint64`
68:             uint64 txDataLen = uint64(_transaction.data.length);

//@audit `txDataLen` is `uint64`
164:             uint64 txDataLen = uint64(_transaction.data.length);

//@audit `txDataLen` is `uint64`
259:             uint64 txDataLen = uint64(_transaction.data.length);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L68-L68) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L164-L164), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L259-L259)


```solidity

File: contracts/Compressor.sol

//@audit `encodedChunk` is `uint64`
65:                 uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);

//@audit `realChunk` is `uint64`
66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

//@audit `enumIndex` is `uint64`
129:             uint64 enumIndex = stateDiff.readUint64(84);

//@audit `metadata` is `uint8`
143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

//@audit `operation` is `uint8`
145:             uint8 operation = metadata & OPERATION_BITMASK;

//@audit `len` is `uint8`
146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

//@audit `enumIndex` is `uint64`
161:             uint64 enumIndex = stateDiff.readUint64(84);

//@audit `metadata` is `uint8`
174:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

//@audit `operation` is `uint8`
176:             uint8 operation = metadata & OPERATION_BITMASK;

//@audit `len` is `uint8`
177:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L65-L65) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L66-L66), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L129-L129), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L143-L143), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L145-L145), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L146-L146), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L161-L161), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L174-L174), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L176-L176), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L177-L177)


```solidity

File: contracts/DefaultAccount.sol

//@audit `value` is `uint128`
133:         uint128 value = Utils.safeCastToU128(_transaction.value);

//@audit `gas` is `uint32`
135:         uint32 gas = Utils.safeCastToU32(gasleft());

//@audit `v` is `uint8`
161:         uint8 v;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L133-L133) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L135-L135), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L161-L161)


```solidity

File: contracts/KnownCodesStorage.sol

//@audit `version` is `uint8`
75:         uint8 version = uint8(_bytecodeHash[0]);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L75-L75) 


```solidity

File: contracts/L1Messenger.sol

//@audit `numberOfL2ToL1Logs` is `uint32`
200:         uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

//@audit `numberOfMessages` is `uint32`
233:         uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

//@audit `currentMessageLength` is `uint32`
237:             uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

//@audit `numberOfBytecodes` is `uint32`
251:         uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

//@audit `currentBytecodeLength` is `uint32`
255:             uint32 currentBytecodeLength = uint32(

//@audit `compressedStateDiffSize` is `uint24`
286:         uint24 compressedStateDiffSize = uint24(bytes3(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 3]));

//@audit `enumerationIndexSize` is `uint8`
289:         uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));

//@audit `numberOfStateDiffs` is `uint32`
300:         uint32 numberOfStateDiffs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L200-L200) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L233-L233), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L237-L237), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L251-L251), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L255-L255), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L286-L286), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L289-L289), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L300-L300)


```solidity

File: contracts/L2BaseToken.sol

//@audit `` is `uint8`
140:     function decimals() external pure override returns (uint8) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L140-L140) 


```solidity

File: contracts/SystemContext.sol

//@audit `blockNumber` is `uint128`
133:         uint128 blockNumber = currentVirtualL2BlockInfo.number;

//@audit `batchNumber` is `uint128`
172:     function getBatchNumberAndTimestamp() public view returns (uint128 batchNumber, uint128 batchTimestamp) {

//@audit `batchTimestamp` is `uint128`
172:     function getBatchNumberAndTimestamp() public view returns (uint128 batchNumber, uint128 batchTimestamp) {

//@audit `blockNumber` is `uint128`
180:     function getL2BlockNumberAndTimestamp() public view returns (uint128 blockNumber, uint128 blockTimestamp) {

//@audit `blockTimestamp` is `uint128`
180:     function getL2BlockNumberAndTimestamp() public view returns (uint128 blockNumber, uint128 blockTimestamp) {

//@audit `` is `uint128`
190:     function getBlockNumber() public view returns (uint128) {

//@audit `` is `uint128`
198:     function getBlockTimestamp() public view returns (uint128) {

//@audit `_blockNumber` is `uint128`
222:         uint128 _blockNumber,

//@audit `_blockTimestamp` is `uint128`
223:         uint128 _blockTimestamp,

//@audit `_blockNumber` is `uint128`
233:     function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {

//@audit `_l2BlockNumber` is `uint128`
241:     function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {

//@audit `_l2BlockNumber` is `uint128`
264:         uint128 _l2BlockNumber,

//@audit `_maxVirtualBlocksToCreate` is `uint128`
265:         uint128 _maxVirtualBlocksToCreate,

//@audit `_newTimestamp` is `uint128`
266:         uint128 _newTimestamp

//@audit `currentBatchNumber` is `uint128`
278:             uint128 currentBatchNumber = currentBatchInfo.number;

//@audit `_l2BlockNumber` is `uint128`
314:     function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal {

//@audit `_l2BlockTimestamp` is `uint128`
314:     function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal {

//@audit `_l2BlockNumber` is `uint128`
342:         uint128 _l2BlockNumber,

//@audit `_l2BlockTimestamp` is `uint128`
343:         uint128 _l2BlockTimestamp,

//@audit `_maxVirtualBlocksToCreate` is `uint128`
346:         uint128 _maxVirtualBlocksToCreate

//@audit `currentBatchTimestamp` is `uint128`
350:             uint128 currentBatchTimestamp = currentBatchInfo.timestamp;

//@audit `currentL2BlockNumber` is `uint128`
358:         (uint128 currentL2BlockNumber, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();

//@audit `currentL2BlockTimestamp` is `uint128`
358:         (uint128 currentL2BlockNumber, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();

//@audit `currentBatchNumber` is `uint128`
409:         (uint128 currentBatchNumber, uint128 currentBatchTimestamp) = getBatchNumberAndTimestamp();

//@audit `currentBatchTimestamp` is `uint128`
409:         (uint128 currentBatchNumber, uint128 currentBatchTimestamp) = getBatchNumberAndTimestamp();

//@audit `currentL2BlockTimestamp` is `uint128`
410:         (, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();

//@audit `` is `uint128`
427:     function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {

//@audit `currentBlockTimestamp` is `uint128`
428:         uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp;

//@audit `` is `uint128`
446:         uint128 _newTimestamp,

//@audit `` is `uint128`
447:         uint128 _expectedNewNumber,

//@audit `previousBatchNumber` is `uint128`
450:         (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();

//@audit `previousBatchTimestamp` is `uint128`
450:         (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();

//@audit `blockNumber` is `uint128`
497:         (uint128 blockNumber, uint128 blockTimestamp) = getBatchNumberAndTimestamp();

//@audit `blockTimestamp` is `uint128`
497:         (uint128 blockNumber, uint128 blockTimestamp) = getBatchNumberAndTimestamp();


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L133-L133) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L172-L172), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L172-L172), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L180-L180), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L180-L180), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L190-L190), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L198-L198), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L222-L222), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L223-L223), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L233-L233), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L241-L241), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L264-L264), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L265-L265), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L266-L266), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L278-L278), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L314-L314), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L314-L314), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L342-L342), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L343-L343), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L346-L346), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L350-L350), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L358-L358), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L358-L358), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L409-L409), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L409-L409), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L410-L410), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L427-L427), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L428-L428), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L446-L446), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L447-L447), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L450-L450), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L450-L450), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L497-L497), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L497-L497)


```solidity

File: contracts/interfaces/IBaseToken.sol

//@audit `` is `uint8`
16:     function decimals() external pure returns (uint8);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IBaseToken.sol#L16-L16) 


```solidity

File: contracts/interfaces/IMailbox.sol

//@audit `_l2TxNumberInBlock` is `uint16`
9:         uint16 _l2TxNumberInBlock,


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IMailbox.sol#L9-L9) 


```solidity

File: contracts/interfaces/ISystemContext.sol

//@audit `` is `uint16`
44:     function txNumberInBlock() external view returns (uint16);

//@audit `` is `uint128`
50:     function getBlockNumber() external view returns (uint128);

//@audit `` is `uint128`
52:     function getBlockTimestamp() external view returns (uint128);

//@audit `blockNumber` is `uint128`
54:     function getBatchNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);

//@audit `blockTimestamp` is `uint128`
54:     function getBatchNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);

//@audit `blockNumber` is `uint128`
56:     function getL2BlockNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);

//@audit `blockTimestamp` is `uint128`
56:     function getL2BlockNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContext.sol#L44-L44) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContext.sol#L50-L50), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContext.sol#L52-L52), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContext.sol#L54-L54), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContext.sol#L54-L54), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContext.sol#L56-L56), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContext.sol#L56-L56)


```solidity

File: contracts/libraries/EfficientCall.sol

//@audit `shrinkTo` is `uint32`
261:         uint32 shrinkTo = uint32(msg.data.length - (_data.length + dataOffset));

//@audit `gas` is `uint32`
264:         uint32 gas = Utils.safeCastToU32(_gas);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L261-L261) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L264-L264)


```solidity

File: contracts/libraries/RLPEncoder.sol

//@audit `_len` is `uint64`
49:     function encodeNonSingleBytesLen(uint64 _len) internal pure returns (bytes memory) {

//@audit `_len` is `uint64`
56:     function encodeListLen(uint64 _len) internal pure returns (bytes memory) {

//@audit `_len` is `uint64`
60:     function _encodeLength(uint64 _len, uint256 _offset) private pure returns (bytes memory encoded) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L49-L49) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L56-L56), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L60-L60)


```solidity

File: contracts/libraries/SystemContractHelper.sol

//@audit `_value` is `uint32`
94:     function ptrAddIntoActive(uint32 _value) internal view {

//@audit `_shrink` is `uint32`
106:     function ptrShrinkIntoActive(uint32 _shrink) internal view {

//@audit `_inputMemoryOffset` is `uint32`
125:         uint32 _inputMemoryOffset,

//@audit `_inputMemoryLength` is `uint32`
126:         uint32 _inputMemoryLength,

//@audit `_outputMemoryOffset` is `uint32`
127:         uint32 _outputMemoryOffset,

//@audit `_outputMemoryLength` is `uint32`
128:         uint32 _outputMemoryLength,

//@audit `_perPrecompileInterpreted` is `uint64`
129:         uint64 _perPrecompileInterpreted

//@audit `_gasToBurn` is `uint32`
150:         uint32 _gasToBurn,

//@audit `_pubdataToSpend` is `uint32`
151:         uint32 _pubdataToSpend

//@audit `_value` is `uint128`
168:     function setValueForNextFarCall(uint128 _value) internal returns (bool success) {

//@audit `pubdataPublished` is `uint32`
227:     function getPubdataPublishedFromMeta(uint256 meta) internal pure returns (uint32 pubdataPublished) {

//@audit `heapSize` is `uint32`
237:     function getHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 heapSize) {

//@audit `auxHeapSize` is `uint32`
246:     function getAuxHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 auxHeapSize) {

//@audit `shardId` is `uint8`
254:     function getShardIdFromMeta(uint256 meta) internal pure returns (uint8 shardId) {

//@audit `callerShardId` is `uint8`
263:     function getCallerShardIdFromMeta(uint256 meta) internal pure returns (uint8 callerShardId) {

//@audit `codeShardId` is `uint8`
272:     function getCodeShardIdFromMeta(uint256 meta) internal pure returns (uint8 codeShardId) {

//@audit `_gasToPay` is `uint32`
344:     function burnGas(uint32 _gasToPay, uint32 _pubdataToSpend) internal view {

//@audit `_pubdataToSpend` is `uint32`
344:     function burnGas(uint32 _gasToPay, uint32 _pubdataToSpend) internal view {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L94-L94) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L106-L106), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L125-L125), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L126-L126), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L127-L127), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L128-L128), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L129-L129), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L150-L150), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L151-L151), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L168-L168), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L227-L227), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L237-L237), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L246-L246), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L254-L254), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L263-L263), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L272-L272), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L344-L344), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L344-L344)


```solidity

File: contracts/libraries/SystemContractsCaller.sol

//@audit `gasLimit` is `uint32`
76:     function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

//@audit `dataStart` is `uint32`
79:         uint32 dataStart;

//@audit `dataLength` is `uint32`
83:         uint32 dataLength = uint32(Utils.safeCastToU32(data.length));

//@audit `gasLimit` is `uint32`
124:         uint32 gasLimit,

//@audit `value` is `uint128`
126:         uint128 value,

//@audit `gasLimit` is `uint32`
151:         uint32 gasLimit,

//@audit `value` is `uint128`
153:         uint128 value,

//@audit `dataOffset` is `uint32`
215:         uint32 dataOffset,

//@audit `memoryPage` is `uint32`
216:         uint32 memoryPage,

//@audit `dataStart` is `uint32`
217:         uint32 dataStart,

//@audit `dataLength` is `uint32`
218:         uint32 dataLength,

//@audit `gasPassed` is `uint32`
219:         uint32 gasPassed,

//@audit `shardId` is `uint8`
220:         uint8 shardId,

//@audit `gasPassed` is `uint32`
251:         uint32 gasPassed,

//@audit `shardId` is `uint8`
252:         uint8 shardId,


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L76-L76) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L79-L79), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L83-L83), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L124-L124), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L126-L126), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L151-L151), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L153-L153), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L215-L215), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L216-L216), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L217-L217), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L218-L218), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L219-L219), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L220-L220), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L251-L251), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L252-L252)


```solidity

File: contracts/libraries/TransactionHelper.sol

//@audit `txDataLen` is `uint64`
171:             uint64 txDataLen = uint64(_transaction.data.length);

//@audit `txDataLen` is `uint64`
249:             uint64 txDataLen = uint64(_transaction.data.length);

//@audit `txDataLen` is `uint64`
321:             uint64 txDataLen = uint64(_transaction.data.length);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L171-L171) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L249-L249), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L321-L321)


```solidity

File: contracts/libraries/UnsafeBytesCalldata.sol

//@audit `result` is `uint16`
19:     function readUint16(bytes calldata _bytes, uint256 _start) internal pure returns (uint16 result) {

//@audit `result` is `uint32`
26:     function readUint32(bytes calldata _bytes, uint256 _start) internal pure returns (uint32 result) {

//@audit `result` is `uint64`
33:     function readUint64(bytes calldata _bytes, uint256 _start) internal pure returns (uint64 result) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L19-L19) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L26-L26), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L33-L33)


```solidity

File: contracts/libraries/Utils.sol

//@audit `` is `uint128`
20:     function safeCastToU128(uint256 _x) internal pure returns (uint128) {

//@audit `` is `uint32`
26:     function safeCastToU32(uint256 _x) internal pure returns (uint32) {

//@audit `` is `uint24`
32:     function safeCastToU24(uint256 _x) internal pure returns (uint24) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L20-L20) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L26-L26), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L32-L32)


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

//@audit `_l2TxNumberInBatch` is `uint16`
182:         uint16 _l2TxNumberInBatch,

//@audit `_l2TxNumberInBatch` is `uint16`
211:         uint16 _l2TxNumberInBatch,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L182-L182) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L211-L211)


```solidity

File: contracts/bridge/L1SharedBridge.sol

//@audit `_l2TxNumberInBatch` is `uint16`
285:         uint16 _l2TxNumberInBatch,

//@audit `_l2TxNumberInBatch` is `uint16`
312:         uint16 _l2TxNumberInBatch,

//@audit `_l2TxNumberInBatch` is `uint16`
389:         uint16 _l2TxNumberInBatch,

//@audit `_l2TxNumberInBatch` is `uint16`
413:         uint16 _l2TxNumberInBatch,

//@audit `functionSignature` is `uint32`
503:         (uint32 functionSignature, uint256 offset) = UnsafeBytes.readUint32(_l2ToL1message, 0);

//@audit `_l2TxNumberInBatch` is `uint16`
618:         uint16 _l2TxNumberInBatch,

//@audit `_l2TxNumberInBatch` is `uint16`
651:         uint16 _l2TxNumberInBatch,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L285-L285) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L312-L312), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L389-L389), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L413-L413), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L503-L503), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L618-L618), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L651-L651)


```solidity

File: contracts/bridge/interfaces/IL1ERC20Bridge.sol

//@audit `_l2TxNumberInBatch` is `uint16`
49:         uint16 _l2TxNumberInBatch,

//@audit `_l2TxNumberInBatch` is `uint16`
56:         uint16 _l2TxNumberInBatch,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL1ERC20Bridge.sol#L49-L49) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL1ERC20Bridge.sol#L56-L56)


```solidity

File: contracts/bridge/interfaces/IL1SharedBridge.sol

//@audit `_l2TxNumberInBatch` is `uint16`
81:         uint16 _l2TxNumberInBatch,

//@audit `_l2TxNumberInBatch` is `uint16`
93:         uint16 _l2TxNumberInBatch,

//@audit `_l2TxNumberInBatch` is `uint16`
100:         uint16 _l2TxNumberInBatch,

//@audit `_l2TxNumberInBatch` is `uint16`
109:         uint16 _l2TxNumberInBatch,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL1SharedBridge.sol#L81-L81) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL1SharedBridge.sol#L93-L93), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL1SharedBridge.sol#L100-L100), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL1SharedBridge.sol#L109-L109)


```solidity

File: contracts/bridgehub/Bridgehub.sol

//@audit `_l2TxNumberInBatch` is `uint16`
181:         uint16 _l2TxNumberInBatch,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L181-L181) 


```solidity

File: contracts/bridgehub/IBridgehub.sol

//@audit `_l2TxNumberInBatch` is `uint16`
94:         uint16 _l2TxNumberInBatch,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/IBridgehub.sol#L94-L94) 


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

//@audit `version` is `uint8`
40:         uint8 version = uint8(_bytecodeHash[0]);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L40-L40) 


```solidity

File: contracts/common/libraries/UnsafeBytes.sol

//@audit `result` is `uint32`
19:     function readUint32(bytes memory _bytes, uint256 _start) internal pure returns (uint32 result, uint256 offset) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UnsafeBytes.sol#L19-L19) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

//@audit `_executionDelay` is `uint32`
55:     constructor(address _initialOwner, uint32 _executionDelay) {

//@audit `_executionDelay` is `uint32`
96:     function setExecutionDelay(uint32 _executionDelay) external onlyOwner {

//@audit `timestamp` is `uint32`
115:             uint32 timestamp = uint32(block.timestamp);

//@audit `timestamp` is `uint32`
134:             uint32 timestamp = uint32(block.timestamp);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L55-L55) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L96-L96), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L115-L115), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L134-L134)


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

//@audit `_nominator` is `uint128`
79:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {

//@audit `_denominator` is `uint128`
79:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {

//@audit `oldNominator` is `uint128`
80:         uint128 oldNominator = s.baseTokenGasPriceMultiplierNominator;

//@audit `oldDenominator` is `uint128`
81:         uint128 oldDenominator = s.baseTokenGasPriceMultiplierDenominator;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L79-L79) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L79-L79), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L80-L80), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L81-L81)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

//@audit `pubdataSource` is `uint8`
39:         uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));

//@audit `_index` is `uint8`
592:     function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

//@audit `_index` is `uint8`
597:     function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L39-L39) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L592-L592), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L597-L597)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

//@audit `_l2TxNumberInBatch` is `uint16`
78:         uint16 _l2TxNumberInBatch,

//@audit `_l2TxNumberInBatch` is `uint16`
181:         uint16 _l2TxNumberInBatch,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L78-L78) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L181-L181)


```solidity

File: contracts/state-transition/chain-interfaces/IAdmin.sol

//@audit `_nominator` is `uint128`
40:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external;

//@audit `_denominator` is `uint128`
40:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IAdmin.sol#L40-L40) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IAdmin.sol#L40-L40)


```solidity

File: contracts/state-transition/chain-interfaces/IMailbox.sol

//@audit `_l2TxNumberInBatch` is `uint16`
51:         uint16 _l2TxNumberInBatch,

//@audit `_l2TxNumberInBatch` is `uint16`
65:         uint16 _l2TxNumberInBatch,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IMailbox.sol#L51-L51) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IMailbox.sol#L65-L65)


```solidity

File: contracts/state-transition/libraries/Diamond.sol

//@audit `selectorPosition` is `uint16`
208:         uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16();


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L208-L208) 


```solidity

File: contracts/state-transition/libraries/LibMap.sol

//@audit `_map` is `uint32map`
18:     function get(Uint32Map storage _map, uint256 _index) internal view returns (uint32 result) {

//@audit `result` is `uint32`
18:     function get(Uint32Map storage _map, uint256 _index) internal view returns (uint32 result) {

//@audit `_map` is `uint32map`
38:     function set(Uint32Map storage _map, uint256 _index, uint32 _value) internal {

//@audit `_value` is `uint32`
38:     function set(Uint32Map storage _map, uint256 _index, uint32 _value) internal {

//@audit `oldValue` is `uint32`
54:             uint32 oldValue = uint32(mapValue >> bitOffset);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L18-L18) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L18-L18), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L38-L38), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L38-L38), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L54-L54)


```solidity

File: contracts/SystemContractsCaller.sol

//@audit `` is `uint32`
27:     function safeCastToU32(uint256 _x) internal pure returns (uint32) {

//@audit `gasLimit` is `uint32`
37:     function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

//@audit `dataStart` is `uint32`
40:         uint32 dataStart;

//@audit `dataLength` is `uint32`
44:         uint32 dataLength = uint32(Utils.safeCastToU32(data.length));

//@audit `gasLimit` is `uint32`
77:         uint32 gasLimit,

//@audit `value` is `uint128`
79:         uint128 value,

//@audit `dataOffset` is `uint32`
96:         uint32 dataOffset,

//@audit `memoryPage` is `uint32`
97:         uint32 memoryPage,

//@audit `dataStart` is `uint32`
98:         uint32 dataStart,

//@audit `dataLength` is `uint32`
99:         uint32 dataLength,

//@audit `gasPassed` is `uint32`
100:         uint32 gasPassed,

//@audit `shardId` is `uint8`
101:         uint8 shardId,

//@audit `gasPassed` is `uint32`
122:         uint32 gasPassed,

//@audit `shardId` is `uint8`
123:         uint8 shardId,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L27-L27) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L37-L37), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L40-L40), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L44-L44), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L77-L77), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L79-L79), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L96-L96), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L97-L97), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L98-L98), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L99-L99), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L100-L100), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L101-L101), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L122-L122), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L123-L123)


```solidity

File: contracts/bridge/L2StandardERC20.sol

//@audit `decimalsUint8` is `uint8`
93:         try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {

//@audit `_version` is `uint8`
115:         uint8 _version

//@audit `` is `uint8`
171:     function decimals() public view override returns (uint8) {

//@audit `result` is `uint8`
183:     function decodeUint8(bytes memory _input) external pure returns (uint8 result) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L93-L93) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L115-L115), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L171-L171), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L183-L183)


```solidity

File: contracts/bridge/interfaces/IL1ERC20Bridge.sol

//@audit `_l2TxNumberInBatch` is `uint16`
12:         uint16 _l2TxNumberInBatch,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL1ERC20Bridge.sol#L12-L12) 


```solidity

File: contracts/bridge/interfaces/IL1SharedBridge.sol

//@audit `_l2TxNumberInBatch` is `uint16`
13:         uint16 _l2TxNumberInBatch,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL1SharedBridge.sol#L13-L13) 


</details>


### [GAS&#x2011;41] The use of a logical AND in place of double if is slightly less gas efficient in instances where there isn't a corresponding else statement for the given if statement 
Using a double if statement instead of logical AND (&&) can provide similar short-circuiting behavior whereas double if is slightly more efficient.


*There are 7 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/AccountCodeStorage.sol

131:         if (
132:             uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS &&
133:             codeHash != 0x00 &&
134:             !Utils.isContractConstructing(codeHash)
135:         ) {
136:             codeSize = Utils.bytecodeLenInBytes(codeHash);
137:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L131-L137) 


```solidity

File: contracts/ContractDeployer.sol

47:         if (
48:             _address > address(MAX_SYSTEM_CONTRACT_ADDRESS) &&
49:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getRawCodeHash(_address) == 0
50:         ) {
51:             return AccountAbstractionVersion.Version1;
52:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L47-L52) 


```solidity

File: contracts/DefaultAccount.sol

139:         if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) {
140:             bytes4 selector = bytes4(data[:4]);
141:             // Check that called function is the deployment method,
142:             // the others deployer method is not supposed to be called from the default account.
143:             isSystemCall =
144:                 selector == DEPLOYER_SYSTEM_CONTRACT.create.selector ||
145:                 selector == DEPLOYER_SYSTEM_CONTRACT.create2.selector ||
146:                 selector == DEPLOYER_SYSTEM_CONTRACT.createAccount.selector ||
147:                 selector == DEPLOYER_SYSTEM_CONTRACT.create2Account.selector;
148:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L139-L148) 


```solidity

File: contracts/NonceHolder.sol

88:         if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {
89:             require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");
90:         }

171:         } else if (!isUsed && _shouldBeUsed) {
172:             revert("The nonce was not set as used");
173:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L88-L90) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L171-L173)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

361:         if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {
362:             delete s.l2SystemContractsUpgradeTxHash;
363:             delete s.l2SystemContractsUpgradeBatchNumber;
364:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L361-L364) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

147:         if (
148:             _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) &&
149:             _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) &&
150:             _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)
151:         ) {
152:             return;
153:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L147-L153) 


</details>


### [GAS&#x2011;42] Splitting `require()` statements that use `&&` saves gas 
See [this issue](https://github.com/code-423n4/2022-01-xdefi-findings/issues/128) which describes the fact that there is a larger deployment gas cost, but with enough runtime calls, the change ends up being cheaper by **3 gas**


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ContractDeployer.sol

77:         require(
78:             _nonceOrdering == AccountNonceOrdering.Arbitrary &&
79:                 currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
80:             "It is only possible to change from sequential to arbitrary ordering"
81:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L77-L81) 


```solidity

File: contracts/KnownCodesStorage.sol

76:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L76-L76) 


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

41:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L41-L41) 


</details>


### [GAS&#x2011;43] Stack variable used as a cheaper cache for a state variable is only used once 
If the variable is only accessed once, it's cheaper to use the state variable directly that one time, and save the **3 gas** the extra stack assignment would spend. However, if it used as a parameter in an event emit, then caching it will help reduce gas by at least ***10 gas***


*There are 312 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/AccountCodeStorage.sol

/// @audit `constructedBytecodeHash`,  are used only once
60:         bytes32 constructedBytecodeHash = Utils.constructedBytecodeHash(codeHash);

/// @audit `addressAsKey`,  are used only once
69:         uint256 addressAsKey = uint256(uint160(_address));

/// @audit `addressAsKey`,  are used only once
79:         uint256 addressAsKey = uint256(uint160(_address));


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L60-L60) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L69-L69), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L79-L79)


```solidity

File: contracts/BootloaderUtilities.sol

/// @audit `encodedGasPrice`,  are used only once
56:             bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);

/// @audit `encodedGasLimit`,  are used only once
57:             bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

/// @audit `rInt`,  are used only once
81:             uint256 rInt = uint256(bytes32(_transaction.signature[0:32]));

/// @audit `sInt`,  are used only once
86:             uint256 sInt = uint256(bytes32(_transaction.signature[32:64]));

/// @audit `listLength`,  are used only once
105:             uint256 listLength = encodedNonce.length +
106:                 encodedGasParam.length +
107:                 encodedTo.length +
108:                 encodedValue.length +
109:                 encodedDataLength.length +
110:                 _transaction.data.length +
111:                 rEncoded.length +
112:                 sEncoded.length +
113:                 vEncoded.length;

/// @audit `encodedChainId`,  are used only once
143:             bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);

/// @audit `encodedNonce`,  are used only once
144:             bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);

/// @audit `encodedGasPrice`,  are used only once
145:             bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);

/// @audit `encodedGasLimit`,  are used only once
146:             bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

/// @audit `encodedTo`,  are used only once
147:             bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

/// @audit `encodedValue`,  are used only once
148:             bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);

/// @audit `rInt`,  are used only once
180:             uint256 rInt = uint256(bytes32(_transaction.signature[0:32]));

/// @audit `sInt`,  are used only once
185:             uint256 sInt = uint256(bytes32(_transaction.signature[32:64]));

/// @audit `listLength`,  are used only once
198:             uint256 listLength = encodedFixedLengthParams.length +
199:                 encodedDataLength.length +
200:                 _transaction.data.length +
201:                 encodedAccessListLength.length +
202:                 rEncoded.length +
203:                 sEncoded.length +
204:                 vEncoded.length;

/// @audit `encodedChainId`,  are used only once
236:             bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);

/// @audit `encodedNonce`,  are used only once
237:             bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);

/// @audit `encodedMaxPriorityFeePerGas`,  are used only once
238:             bytes memory encodedMaxPriorityFeePerGas = RLPEncoder.encodeUint256(_transaction.maxPriorityFeePerGas);

/// @audit `encodedMaxFeePerGas`,  are used only once
239:             bytes memory encodedMaxFeePerGas = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);

/// @audit `encodedGasLimit`,  are used only once
240:             bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

/// @audit `encodedTo`,  are used only once
241:             bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

/// @audit `encodedValue`,  are used only once
242:             bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);

/// @audit `rInt`,  are used only once
275:             uint256 rInt = uint256(bytes32(_transaction.signature[0:32]));

/// @audit `sInt`,  are used only once
280:             uint256 sInt = uint256(bytes32(_transaction.signature[32:64]));

/// @audit `listLength`,  are used only once
293:             uint256 listLength = encodedFixedLengthParams.length +
294:                 encodedDataLength.length +
295:                 _transaction.data.length +
296:                 encodedAccessListLength.length +
297:                 rEncoded.length +
298:                 sEncoded.length +
299:                 vEncoded.length;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L56-L56) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L57-L57), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L81-L81), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L86-L86), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L105-L113), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L143-L143), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L144-L144), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L145-L145), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L146-L146), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L147-L147), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L148-L148), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L180-L180), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L185-L185), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L198-L204), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L236-L236), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L237-L237), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L238-L238), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L239-L239), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L240-L240), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L241-L241), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L242-L242), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L275-L275), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L280-L280), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L293-L299)


```solidity

File: contracts/ComplexUpgrader.sol

/// @audit `success`, `returnData`,  are used only once
25:         (bool success, bytes memory returnData) = _delegateTo.delegatecall(_calldata);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ComplexUpgrader.sol#L25-L25) 


```solidity

File: contracts/Compressor.sol

/// @audit `encodedChunk`,  are used only once
65:                 uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);

/// @audit `realChunk`,  are used only once
66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

/// @audit `numberOfInitialWrites`,  are used only once
121:         uint256 numberOfInitialWrites = uint256(_compressedStateDiffs.readUint16(0));

/// @audit `derivedKey`,  are used only once
137:             bytes32 derivedKey = stateDiff.readBytes32(52);

/// @audit `compressedEnumIndex`,  are used only once
168:             uint256 compressedEnumIndex = _sliceToUint256(
169:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + _enumerationIndexSize]
170:             );


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L65-L65) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L66-L66), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L121-L121), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L137-L137), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L168-L170)


```solidity

File: contracts/ContractDeployer.sol

/// @audit `constructorInputHash`,  are used only once
103:         bytes32 constructorInputHash = EfficientCall.keccak(_input);

/// @audit `hash`,  are used only once
105:         bytes32 hash = keccak256(
106:             bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, constructorInputHash)
107:         );

/// @audit `hash`,  are used only once
121:         bytes32 hash = keccak256(
122:             bytes.concat(CREATE_PREFIX, bytes32(uint256(uint160(_sender))), bytes32(_senderNonce))
123:         );

/// @audit `senderNonce`,  are used only once
188:         uint256 senderNonce = NONCE_HOLDER_SYSTEM_CONTRACT.incrementDeploymentNonce(msg.sender);

/// @audit `knownCodeMarker`,  are used only once
302:         uint256 knownCodeMarker = KNOWN_CODE_STORAGE_CONTRACT.getMarker(_bytecodeHash);

/// @audit `constructingBytecodeHash`,  are used only once
311:         bytes32 constructingBytecodeHash = Utils.constructingBytecodeHash(_bytecodeHash);

/// @audit `returnData`,  are used only once
343:             bytes memory returnData = EfficientCall.mimicCall(gasleft(), _newAddress, _input, _sender, true, _isSystem);

/// @audit `immutables`,  are used only once
347:             ImmutableData[] memory immutables = abi.decode(returnData, (ImmutableData[]));


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L103-L103) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L105-L107), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L121-L123), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L188-L188), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L302-L302), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L311-L311), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L343-L343), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L347-L347)


```solidity

File: contracts/DefaultAccount.sol

/// @audit `txHash`,  are used only once
94:         bytes32 txHash = _suggestedSignedHash != bytes32(0) ? _suggestedSignedHash : _transaction.encodeHash();

/// @audit `totalRequiredBalance`,  are used only once
99:         uint256 totalRequiredBalance = _transaction.totalRequiredBalance();

/// @audit `value`,  are used only once
133:         uint128 value = Utils.safeCastToU128(_transaction.value);

/// @audit `gas`,  are used only once
135:         uint32 gas = Utils.safeCastToU32(gasleft());

/// @audit `success`,  are used only once
149:         bool success = EfficientCall.rawCall(gas, to, value, data, isSystemCall);

/// @audit `r`,  are used only once
162:         bytes32 r;

/// @audit `success`,  are used only once
201:         bool success = _transaction.payToTheBootloader();


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L94-L94) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L99-L99), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L133-L133), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L135-L135), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L149-L149), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L162-L162), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L201-L201)


```solidity

File: contracts/ImmutableSimulator.sol

/// @audit `immutablesLength`,  are used only once
37:             uint256 immutablesLength = _immutables.length;

/// @audit `index`,  are used only once
39:                 uint256 index = _immutables[i].index;

/// @audit `value`,  are used only once
40:                 bytes32 value = _immutables[i].value;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L37-L37) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L39-L39), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L40-L40)


```solidity

File: contracts/KnownCodesStorage.sol

/// @audit `hashesLen`,  are used only once
29:             uint256 hashesLen = _hashes.length;

/// @audit `version`,  are used only once
75:         uint8 version = uint8(_bytecodeHash[0]);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L29-L29) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L75-L75)


```solidity

File: contracts/L1Messenger.sol

/// @audit `l2ToL1Log`,  are used only once
75:         L2ToL1Log memory l2ToL1Log = L2ToL1Log({
76:             l2ShardId: 0,
77:             isService: _isService,
78:             txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),
79:             sender: msg.sender,
80:             key: _key,
81:             value: _value
82:         });

/// @audit `gasToPay`,  are used only once
89:         uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) + 2 * keccakGasCost(64);

/// @audit `hashedLog`,  are used only once
095:         bytes32 hashedLog = keccak256(
096:             abi.encodePacked(
097:                 _l2ToL1Log.l2ShardId,
098:                 _l2ToL1Log.isService,
099:                 _l2ToL1Log.txNumberInBlock,
100:                 _l2ToL1Log.sender,
101:                 _l2ToL1Log.key,
102:                 _l2ToL1Log.value
103:             )
104:         );

/// @audit `gasBeforeMessageHashing`,  are used only once
117:         uint256 gasBeforeMessageHashing = gasleft();

/// @audit `gasSpentOnMessageHashing`,  are used only once
119:         uint256 gasSpentOnMessageHashing = gasBeforeMessageHashing - gasleft();

/// @audit `l2ToL1Log`,  are used only once
125:         L2ToL1Log memory l2ToL1Log = L2ToL1Log({
126:             l2ShardId: 0,
127:             isService: true,
128:             txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),
129:             sender: address(this),
130:             key: bytes32(uint256(uint160(msg.sender))),
131:             value: hash
132:         });

/// @audit `gasToPay`,  are used only once
148:         uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) +
149:             3 *
150:             keccakGasCost(64) +
151:             gasSpentOnMessageHashing +
152:             COMPUTATIONAL_PRICE_FOR_PUBDATA *
153:             pubdataLen;

/// @audit `gasToPay`,  are used only once
175:         uint256 gasToPay = sha256GasCost(bytecodeLen) +
176:             keccakGasCost(64) +
177:             COMPUTATIONAL_PRICE_FOR_PUBDATA *
178:             pubdataLen;

/// @audit `l2ToL1LogsTreeRoot`,  are used only once
230:         bytes32 l2ToL1LogsTreeRoot = l2ToL1LogsTreeArray[0];

/// @audit `numberOfMessages`,  are used only once
233:         uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

/// @audit `hashedMessage`,  are used only once
239:             bytes32 hashedMessage = EfficientCall.keccak(
240:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentMessageLength]
241:             );

/// @audit `numberOfBytecodes`,  are used only once
251:         uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

/// @audit `enumerationIndexSize`,  are used only once
289:         uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));

/// @audit `compressedStateDiffs`,  are used only once
292:         bytes calldata compressedStateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr +
293:             compressedStateDiffSize];

/// @audit `stateDiffs`,  are used only once
303:         bytes calldata stateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr +
304:             (numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE)];

/// @audit `stateDiffHash`,  are used only once
307:         bytes32 stateDiffHash = COMPRESSOR_CONTRACT.verifyCompressedStateDiffs(
308:             numberOfStateDiffs,
309:             enumerationIndexSize,
310:             stateDiffs,
311:             compressedStateDiffs
312:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L75-L82) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L89-L89), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L95-L104), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L117-L117), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L119-L119), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L125-L132), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L148-L153), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L175-L178), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L230-L230), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L233-L233), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L239-L241), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L251-L251), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L289-L289), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L292-L293), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L303-L304), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L307-L312)


```solidity

File: contracts/L2BaseToken.sol

/// @audit `message`,  are used only once
76:         bytes memory message = _getL1WithdrawMessage(_l1Receiver, amount);

/// @audit `message`,  are used only once
89:         bytes memory message = _getExtendedWithdrawMessage(_l1Receiver, amount, msg.sender, _additionalData);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L76-L76) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L89-L89)


```solidity

File: contracts/MsgValueSimulator.sol

/// @audit `addressAsUint`,  are used only once
27:         uint256 addressAsUint = SystemContractHelper.getExtraAbiData(1);

/// @audit `mask`,  are used only once
28:         uint256 mask = SystemContractHelper.getExtraAbiData(2);

/// @audit `isSystemCall`,  are used only once
57:         (uint256 value, bool isSystemCall, address to) = _getAbiParams();

/// @audit `success`,  are used only once
63:             (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call(
64:                 abi.encodeCall(REAL_BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo, (msg.sender, to, value))
65:             );


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/MsgValueSimulator.sol#L27-L27) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/MsgValueSimulator.sol#L28-L28), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/MsgValueSimulator.sol#L57-L57), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/MsgValueSimulator.sol#L63-L65)


```solidity

File: contracts/NonceHolder.sol

/// @audit `addressAsKey`,  are used only once
47:         uint256 addressAsKey = uint256(uint160(_address));

/// @audit `addressAsKey`,  are used only once
58:         uint256 addressAsKey = uint256(uint160(_address));

/// @audit `accountInfo`,  are used only once
83:         IContractDeployer.AccountInfo memory accountInfo = DEPLOYER_SYSTEM_CONTRACT.getAccountInfo(msg.sender);

/// @audit `addressAsKey`,  are used only once
92:         uint256 addressAsKey = uint256(uint160(msg.sender));

/// @audit `addressAsKey`,  are used only once
103:         uint256 addressAsKey = uint256(uint160(msg.sender));

/// @audit `addressAsKey`,  are used only once
126:         uint256 addressAsKey = uint256(uint160(_address));

/// @audit `addressAsKey`,  are used only once
155:         uint256 addressAsKey = uint256(uint160(_address));


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L47-L47) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L58-L58), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L83-L83), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L92-L92), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L103-L103), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L126-L126), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L155-L155)


```solidity

File: contracts/PubdataChunkPublisher.sol

/// @audit `totalBlobs`,  are used only once
28:         bytes memory totalBlobs = new bytes(BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS);

/// @audit `start`,  are used only once
37:             uint256 start = BLOB_SIZE_BYTES * i;

/// @audit `blobHash`,  are used only once
45:             bytes32 blobHash;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L28-L28) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L37-L37), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L45-L45)


```solidity

File: contracts/SystemContext.sol

/// @audit `currentBatchTimestamp`,  are used only once
350:             uint128 currentBatchTimestamp = currentBatchInfo.timestamp;

/// @audit `prevL2BlockHash`,  are used only once
376:             bytes32 prevL2BlockHash = _getLatest257L2blockHash(currentL2BlockNumber - 1);

/// @audit `pendingL2BlockHash`,  are used only once
378:             bytes32 pendingL2BlockHash = _calculateL2BlockHash(
379:                 currentL2BlockNumber,
380:                 currentL2BlockTimestamp,
381:                 prevL2BlockHash,
382:                 currentL2BlockTxsRollingHash
383:             );

/// @audit `currentBatchNumber`, `currentBatchTimestamp`,  are used only once
409:         (uint128 currentBatchNumber, uint128 currentBatchTimestamp) = getBatchNumberAndTimestamp();

/// @audit `packedTimestamps`,  are used only once
416:         uint256 packedTimestamps = (uint256(currentBatchTimestamp) << 128) | currentL2BlockTimestamp;

/// @audit `currentBlockTimestamp`,  are used only once
428:         uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp;

/// @audit `previousBatchTimestamp`,  are used only once
450:         (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();

/// @audit `newBlockInfo`,  are used only once
459:         BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp});

/// @audit `newBlockInfo`,  are used only once
476:         BlockInfo memory newBlockInfo = BlockInfo({number: uint128(_number), timestamp: uint128(_newTimestamp)});

/// @audit `blockNumber`, `blockTimestamp`,  are used only once
497:         (uint128 blockNumber, uint128 blockTimestamp) = getBatchNumberAndTimestamp();


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L350-L350) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L376-L376), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L378-L383), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L409-L409), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L416-L416), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L428-L428), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L450-L450), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L459-L459), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L476-L476), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L497-L497)


```solidity

File: contracts/libraries/EfficientCall.sol

/// @audit `success`,  are used only once
65:         bool success = rawCall(_gas, _address, _value, _data, _isSystem);

/// @audit `success`,  are used only once
79:         bool success = rawStaticCall(_gas, _address, _data);

/// @audit `success`,  are used only once
93:         bool success = rawDelegateCall(_gas, _address, _data);

/// @audit `success`,  are used only once
113:         bool success = rawMimicCall(_gas, _address, _data, _whoToMimic, _isConstructor, _isSystem);

/// @audit `callAddr`,  are used only once
134:             address callAddr = RAW_FAR_CALL_BY_REF_CALL_ADDRESS;

/// @audit `msgValueSimulator`,  are used only once
142:             address msgValueSimulator = MSG_VALUE_SYSTEM_CONTRACT;

/// @audit `callAddr`,  are used only once
143:             address callAddr = SYSTEM_CALL_BY_REF_CALL_ADDRESS;

/// @audit `forwardMask`,  are used only once
146:             uint256 forwardMask = _isSystem ? MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT : 0;

/// @audit `callAddr`,  are used only once
162:         address callAddr = RAW_FAR_CALL_BY_REF_CALL_ADDRESS;

/// @audit `callAddr`,  are used only once
176:         address callAddr = RAW_FAR_CALL_BY_REF_CALL_ADDRESS;

/// @audit `callAddr`,  are used only once
201:         address callAddr = MIMIC_CALL_BY_REF_CALL_ADDRESS;

/// @audit `cleanupMask`,  are used only once
202:         uint256 cleanupMask = ADDRESS_MASK;

/// @audit `size`,  are used only once
217:             uint256 size;

/// @audit `shrinkTo`,  are used only once
261:         uint32 shrinkTo = uint32(msg.data.length - (_data.length + dataOffset));

/// @audit `gas`,  are used only once
264:         uint32 gas = Utils.safeCastToU32(_gas);

/// @audit `farCallAbi`,  are used only once
265:         uint256 farCallAbi = SystemContractsCaller.getFarCallABIWithEmptyFatPointer(
266:             gas,
267:             // Only rollup is supported for now
268:             0,
269:             CalldataForwardingMode.ForwardFatPointer,
270:             _isConstructor,
271:             _isSystem
272:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L65-L65) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L79-L79), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L93-L93), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L113-L113), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L134-L134), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L142-L142), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L143-L143), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L146-L146), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L162-L162), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L176-L176), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L201-L201), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L202-L202), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L217-L217), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L261-L261), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L264-L264), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L265-L272)


```solidity

File: contracts/libraries/RLPEncoder.sol

/// @audit `shiftedVal`,  are used only once
15:         bytes20 shiftedVal = bytes20(_val);

/// @audit `lbs`,  are used only once
36:                 uint256 lbs = 31 - hbs;

/// @audit `shiftedVal`,  are used only once
37:                 uint256 shiftedVal = _val << (lbs * 8);

/// @audit `lbs`,  are used only once
71:                 uint256 lbs = 31 - hbs;

/// @audit `shiftedVal`,  are used only once
72:                 uint256 shiftedVal = uint256(_len) << (lbs * 8);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L15-L15) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L36-L36), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L37-L37), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L71-L71), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L72-L72)


```solidity

File: contracts/libraries/SystemContractHelper.sol

/// @audit `callAddr`,  are used only once
49:         address callAddr = TO_L1_CALL_ADDRESS;

/// @audit `callAddr`,  are used only once
64:         address callAddr = CODE_ADDRESS_CALL_ADDRESS;

/// @audit `callAddr`,  are used only once
75:         address callAddr = LOAD_CALLDATA_INTO_ACTIVE_PTR_CALL_ADDRESS;

/// @audit `callAddr`,  are used only once
86:         address callAddr = PTR_PACK_INTO_ACTIVE_CALL_ADDRESS;

/// @audit `callAddr`,  are used only once
95:         address callAddr = PTR_ADD_INTO_ACTIVE_CALL_ADDRESS;

/// @audit `cleanupMask`,  are used only once
96:         uint256 cleanupMask = UINT32_MASK;

/// @audit `callAddr`,  are used only once
107:         address callAddr = PTR_SHRINK_INTO_ACTIVE_CALL_ADDRESS;

/// @audit `cleanupMask`,  are used only once
108:         uint256 cleanupMask = UINT32_MASK;

/// @audit `callAddr`,  are used only once
153:         address callAddr = PRECOMPILE_CALL_ADDRESS;

/// @audit `params`,  are used only once
155:         uint256 params = uint256(_gasToBurn) + (uint256(_pubdataToSpend) << 32);

/// @audit `cleanupMask`,  are used only once
157:         uint256 cleanupMask = UINT64_MASK;

/// @audit `cleanupMask`,  are used only once
169:         uint256 cleanupMask = UINT128_MASK;

/// @audit `callAddr`,  are used only once
170:         address callAddr = SET_CONTEXT_VALUE_CALL_ADDRESS;

/// @audit `callAddr`,  are used only once
182:         address callAddr = EVENT_INITIALIZE_ADDRESS;

/// @audit `callAddr`,  are used only once
192:         address callAddr = EVENT_WRITE_ADDRESS;

/// @audit `callAddr`,  are used only once
204:         address callAddr = META_CALL_ADDRESS;

/// @audit `shifted`,  are used only once
217:         uint256 shifted = (meta << (256 - size - offset));

/// @audit `callAddr`,  are used only once
297:         address callAddr = CALLFLAGS_CALL_ADDRESS;

/// @audit `callAddr`,  are used only once
308:         address callAddr = PTR_CALLDATA_CALL_ADDRESS;

/// @audit `callAddr`,  are used only once
321:         address callAddr = GET_EXTRA_ABI_DATA_ADDRESS;

/// @audit `callFlags`,  are used only once
330:         uint256 callFlags = getCallFlags();

/// @audit `precompileCallSuccess`,  are used only once
345:         bool precompileCallSuccess = unsafePrecompileCall(
346:             0, // The precompile parameters are formal ones. We only need the precompile call to burn gas.
347:             _gasToPay,
348:             _pubdataToSpend
349:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L49-L49) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L64-L64), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L75-L75), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L86-L86), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L95-L95), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L96-L96), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L107-L107), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L108-L108), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L153-L153), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L155-L155), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L157-L157), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L169-L169), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L170-L170), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L182-L182), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L192-L192), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L204-L204), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L217-L217), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L297-L297), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L308-L308), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L321-L321), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L330-L330), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L345-L349)


```solidity

File: contracts/libraries/SystemContractsCaller.sol

/// @audit `callAddr`,  are used only once
77:         address callAddr = SYSTEM_CALL_CALL_ADDRESS;

/// @audit `dataStart`,  are used only once
79:         uint32 dataStart;

/// @audit `dataLength`,  are used only once
83:         uint32 dataLength = uint32(Utils.safeCastToU32(data.length));

/// @audit `farCallAbi`,  are used only once
85:         uint256 farCallAbi = SystemContractsCaller.getFarCallABI(
86:             0,
87:             0,
88:             dataStart,
89:             dataLength,
90:             gasLimit,
91:             // Only rollup is supported for now
92:             0,
93:             CalldataForwardingMode.UseHeap,
94:             false,
95:             true
96:         );

/// @audit `msgValueSimulator`,  are used only once
104:             address msgValueSimulator = MSG_VALUE_SYSTEM_CONTRACT;

/// @audit `forwardMask`,  are used only once
107:             uint256 forwardMask = MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT;

/// @audit `size`,  are used only once
131:         uint256 size;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L77-L77) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L79-L79), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L83-L83), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L85-L96), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L104-L104), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L107-L107), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L131-L131)


```solidity

File: contracts/libraries/TransactionHelper.sol

/// @audit `structHash`,  are used only once
119:         bytes32 structHash = keccak256(
120:             abi.encode(
121:                 EIP712_TRANSACTION_TYPE_HASH,
122:                 _transaction.txType,
123:                 _transaction.from,
124:                 _transaction.to,
125:                 _transaction.gasLimit,
126:                 _transaction.gasPerPubdataByteLimit,
127:                 _transaction.maxFeePerGas,
128:                 _transaction.maxPriorityFeePerGas,
129:                 _transaction.paymaster,
130:                 _transaction.nonce,
131:                 _transaction.value,
132:                 EfficientCall.keccak(_transaction.data),
133:                 keccak256(abi.encodePacked(_transaction.factoryDeps)),
134:                 EfficientCall.keccak(_transaction.paymasterInput)
135:             )
136:         );

/// @audit `domainSeparator`,  are used only once
138:         bytes32 domainSeparator = keccak256(
139:             abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
140:         );

/// @audit `encodedGasPrice`,  are used only once
159:             bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);

/// @audit `encodedGasLimit`,  are used only once
160:             bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

/// @audit `listLength`,  are used only once
190:             uint256 listLength = encodedNonce.length +
191:                 encodedGasParam.length +
192:                 encodedTo.length +
193:                 encodedValue.length +
194:                 encodedDataLength.length +
195:                 _transaction.data.length +
196:                 encodedChainId.length;

/// @audit `encodedChainId`,  are used only once
228:             bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);

/// @audit `encodedNonce`,  are used only once
229:             bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);

/// @audit `encodedGasPrice`,  are used only once
230:             bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);

/// @audit `encodedGasLimit`,  are used only once
231:             bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

/// @audit `encodedTo`,  are used only once
232:             bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

/// @audit `encodedValue`,  are used only once
233:             bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);

/// @audit `listLength`,  are used only once
265:             uint256 listLength = encodedFixedLengthParams.length +
266:                 encodedDataLength.length +
267:                 _transaction.data.length +
268:                 encodedAccessListLength.length;

/// @audit `encodedChainId`,  are used only once
298:             bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);

/// @audit `encodedNonce`,  are used only once
299:             bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);

/// @audit `encodedMaxPriorityFeePerGas`,  are used only once
300:             bytes memory encodedMaxPriorityFeePerGas = RLPEncoder.encodeUint256(_transaction.maxPriorityFeePerGas);

/// @audit `encodedMaxFeePerGas`,  are used only once
301:             bytes memory encodedMaxFeePerGas = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);

/// @audit `encodedGasLimit`,  are used only once
302:             bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

/// @audit `encodedTo`,  are used only once
303:             bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));

/// @audit `encodedValue`,  are used only once
304:             bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);

/// @audit `listLength`,  are used only once
337:             uint256 listLength = encodedFixedLengthParams.length +
338:                 encodedDataLength.length +
339:                 _transaction.data.length +
340:                 encodedAccessListLength.length;

/// @audit `currentAllowance`,  are used only once
377:             uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);

/// @audit `bootloaderAddr`,  are used only once
396:         address bootloaderAddr = BOOTLOADER_FORMAL_ADDRESS;

/// @audit `amount`,  are used only once
397:         uint256 amount = _transaction.maxFeePerGas * _transaction.gasLimit;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L119-L136) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L138-L140), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L159-L159), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L160-L160), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L190-L196), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L228-L228), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L229-L229), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L230-L230), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L231-L231), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L232-L232), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L233-L233), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L265-L268), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L298-L298), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L299-L299), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L300-L300), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L301-L301), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L302-L302), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L303-L303), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L304-L304), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L337-L340), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L377-L377), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L396-L396), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L397-L397)


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

/// @audit `constructorInputHash`,  are used only once
76:         bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));

/// @audit `salt`,  are used only once
77:         bytes32 salt = bytes32(uint256(uint160(_l1Token)));

/// @audit `amount`,  are used only once
142:         uint256 amount = _depositFundsToSharedBridge(msg.sender, IERC20(_l1Token), _amount);

/// @audit `balanceBefore`,  are used only once
161:         uint256 balanceBefore = _token.balanceOf(address(sharedBridge));

/// @audit `balanceAfter`,  are used only once
163:         uint256 balanceAfter = _token.balanceOf(address(sharedBridge));

/// @audit `l1Receiver`, `l1Token`, `amount`,  are used only once
218:         (address l1Receiver, address l1Token, uint256 amount) = sharedBridge.finalizeWithdrawalLegacyErc20Bridge(
219:             _l2BatchNumber,
220:             _l2MessageIndex,
221:             _l2TxNumberInBatch,
222:             _message,
223:             _merkleProof
224:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L76-L76) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L77-L77), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L142-L142), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L161-L161), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L163-L163), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L218-L224)


```solidity

File: contracts/bridge/L1SharedBridge.sol

/// @audit `amount`,  are used only once
160:             uint256 amount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _amount); // note if _prevMsgSender is this contract, this will return 0. This does not happen.

/// @audit `balanceBefore`,  are used only once
174:         uint256 balanceBefore = _token.balanceOf(address(this));

/// @audit `balanceAfter`,  are used only once
176:         uint256 balanceAfter = _token.balanceOf(address(this));

/// @audit `withdrawAmount`,  are used only once
205:             uint256 withdrawAmount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount);

/// @audit `l2TxCalldata`,  are used only once
217:             bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, amount);

/// @audit `gettersData`,  are used only once
249:         bytes memory gettersData = _getERC20Getters(_l1Token);

/// @audit `name`,  are used only once
256:             bytes memory name = bytes("Ether");

/// @audit `symbol`,  are used only once
257:             bytes memory symbol = bytes("ETH");

/// @audit `decimals`,  are used only once
258:             bytes memory decimals = abi.encode(uint8(18));

/// @audit `proofValid`,  are used only once
316:             bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
317:                 _chainId,
318:                 _l2TxHash,
319:                 _l2BatchNumber,
320:                 _l2MessageIndex,
321:                 _l2TxNumberInBatch,
322:                 _merkleProof,
323:                 TxStatus.Failure
324:             );

/// @audit `weCanCheckDepositHere`,  are used only once
333:                 bool weCanCheckDepositHere = !_isEraLegacyWithdrawal(_chainId, _l2BatchNumber);

/// @audit `dataHash`,  are used only once
340:                 bytes32 dataHash = depositHappened[_chainId][_l2TxHash];

/// @audit `txDataHash`,  are used only once
341:                 bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));

/// @audit `callSuccess`,  are used only once
355:             bool callSuccess;

/// @audit `alreadyFinalized`,  are used only once
423:             bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
424:                 _l2BatchNumber,
425:                 _l2MessageIndex
426:             );

/// @audit `messageParams`,  are used only once
430:         MessageParams memory messageParams = MessageParams({
431:             l2BatchNumber: _l2BatchNumber,
432:             l2MessageIndex: _l2MessageIndex,
433:             l2TxNumberInBatch: _l2TxNumberInBatch
434:         });

/// @audit `callSuccess`,  are used only once
444:             bool callSuccess;

/// @audit `baseTokenWithdrawal`,  are used only once
467:             bool baseTokenWithdrawal = (l1Token == bridgehub.baseToken(_chainId));

/// @audit `l2Sender`,  are used only once
468:             address l2Sender = baseTokenWithdrawal ? L2_BASE_TOKEN_SYSTEM_CONTRACT_ADDR : l2BridgeAddress[_chainId];

/// @audit `success`,  are used only once
477:         bool success = bridgehub.proveL2MessageInclusion(
478:             _chainId,
479:             _messageParams.l2BatchNumber,
480:             _messageParams.l2MessageIndex,
481:             l2ToL1Message,
482:             _merkleProof
483:         );

/// @audit `l2TxCalldata`,  are used only once
571:         bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);

/// @audit `request`,  are used only once
584:             L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
585:                 chainId: ERA_CHAIN_ID,
586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
587:                 mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
588:                 l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
589:                 l2Calldata: l2TxCalldata,
590:                 l2GasLimit: _l2TxGasLimit,
591:                 l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
592:                 factoryDeps: new bytes[](0),
593:                 refundRecipient: refundRecipient
594:             });

/// @audit `txDataHash`,  are used only once
598:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L160-L160) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L174-L174), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L176-L176), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L205-L205), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L217-L217), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L249-L249), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L256-L256), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L257-L257), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L258-L258), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L316-L324), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L333-L333), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L340-L340), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L341-L341), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L355-L355), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L423-L426), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L430-L434), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L444-L444), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L467-L467), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L468-L468), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L477-L483), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L571-L571), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L584-L594), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L598-L598)


```solidity

File: contracts/bridgehub/Bridgehub.sol

/// @audit `oldPendingAdmin`,  are used only once
53:         address oldPendingAdmin = pendingAdmin;

/// @audit `previousAdmin`,  are used only once
64:         address previousAdmin = admin;

/// @audit `stateTransition`,  are used only once
159:         address stateTransition = getStateTransition(_chainId);

/// @audit `stateTransition`,  are used only once
171:         address stateTransition = getStateTransition(_chainId);

/// @audit `stateTransition`,  are used only once
185:         address stateTransition = getStateTransition(_chainId);

/// @audit `stateTransition`,  are used only once
204:         address stateTransition = getStateTransition(_chainId);

/// @audit `stateTransition`,  are used only once
236:         address stateTransition = getStateTransition(_request.chainId);

/// @audit `refundRecipient`,  are used only once
237:         address refundRecipient = _actualRefundRecipient(_request.refundRecipient);

/// @audit `stateTransition`,  are used only once
286:         address stateTransition = getStateTransition(_request.chainId);

/// @audit `refundRecipient`,  are used only once
298:         address refundRecipient = _actualRefundRecipient(_request.refundRecipient);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L53-L53) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L64-L64), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L159-L159), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L171-L171), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L185-L185), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L204-L204), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L236-L236), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L237-L237), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L286-L286), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L298-L298)


```solidity

File: contracts/common/ReentrancyGuard.sol

/// @audit `lockSlotOldValue`,  are used only once
47:         uint256 lockSlotOldValue;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/ReentrancyGuard.sol#L47-L47) 


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

/// @audit `version`,  are used only once
40:         uint8 version = uint8(_bytecodeHash[0]);

/// @audit `senderBytes`,  are used only once
66:         bytes32 senderBytes = bytes32(uint256(uint160(_sender)));

/// @audit `data`,  are used only once
67:         bytes32 data = keccak256(
68:             bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
69:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L40-L40) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L66-L66), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L67-L69)


```solidity

File: contracts/governance/Governance.sol

/// @audit `success`, `returnData`,  are used only once
226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L226-L226) 


```solidity

File: contracts/state-transition/StateTransitionManager.sol

/// @audit `batchZero`,  are used only once
90:         IExecutor.StoredBatchInfo memory batchZero = IExecutor.StoredBatchInfo(
91:             0,
92:             _initializeData.genesisBatchHash,
93:             _initializeData.genesisIndexRepeatedStorageChanges,
94:             0,
95:             EMPTY_STRING_KECCAK,
96:             DEFAULT_L2_LOGS_TREE_ROOT_HASH,
97:             0,
98:             _initializeData.genesisBatchCommitment
99:         );

/// @audit `oldPendingAdmin`,  are used only once
112:         address oldPendingAdmin = pendingAdmin;

/// @audit `previousAdmin`,  are used only once
123:         address previousAdmin = admin;

/// @audit `systemContextCalldata`,  are used only once
178:         bytes memory systemContextCalldata = abi.encodeCall(ISystemContext.setChainId, (_chainId));

/// @audit `uintEmptyArray`,  are used only once
179:         uint256[] memory uintEmptyArray;

/// @audit `bytesEmptyArray`,  are used only once
180:         bytes[] memory bytesEmptyArray;

/// @audit `proposedUpgrade`,  are used only once
202:         ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
203:             l2ProtocolUpgradeTx: l2ProtocolUpgradeTx,
204:             factoryDeps: bytesEmptyArray,
205:             bootloaderHash: bytes32(0),
206:             defaultAccountHash: bytes32(0),
207:             verifier: address(0),
208:             verifierParams: VerifierParams({
209:                 recursionNodeLevelVkHash: bytes32(0),
210:                 recursionLeafLevelVkHash: bytes32(0),
211:                 recursionCircuitsSetVksHash: bytes32(0)
212:             }),
213:             l1ContractsUpgradeCalldata: new bytes(0),
214:             postUpgradeCalldata: new bytes(0),
215:             upgradeTimestamp: 0,
216:             newProtocolVersion: protocolVersion
217:         });

/// @audit `emptyArray`,  are used only once
219:         Diamond.FacetCut[] memory emptyArray;

/// @audit `cutData`,  are used only once
220:         Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({
221:             facetCuts: emptyArray,
222:             initAddress: genesisUpgrade,
223:             initCalldata: abi.encodeCall(IDefaultUpgrade.upgrade, (proposedUpgrade))
224:         });

/// @audit `cutHashInput`,  are used only once
255:         bytes32 cutHashInput = keccak256(_diamondCut);

/// @audit `stateTransitionContract`,  are used only once
277:         DiamondProxy stateTransitionContract = new DiamondProxy{salt: bytes32(0)}(block.chainid, diamondCut);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L90-L99) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L112-L112), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L123-L123), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L178-L178), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L179-L179), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L180-L180), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L202-L217), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L219-L219), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L220-L224), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L255-L255), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L277-L277)


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

/// @audit `timestamp`,  are used only once
115:             uint32 timestamp = uint32(block.timestamp);

/// @audit `timestamp`,  are used only once
134:             uint32 timestamp = uint32(block.timestamp);

/// @audit `delay`,  are used only once
183:         uint256 delay = executionDelay; // uint32

/// @audit `commitBatchTimestamp`,  are used only once
186:                 uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
187:                     _newBatchesData[i].batchNumber
188:                 );

/// @audit `delay`,  are used only once
207:         uint256 delay = executionDelay; // uint32

/// @audit `commitBatchTimestamp`,  are used only once
210:                 uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);

/// @audit `contractAddress`,  are used only once
226:         address contractAddress = stateTransitionManager.stateTransition(_chainId);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L115-L115) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L134-L134), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L183-L183), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L186-L188), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L207-L207), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L210-L210), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L226-L226)


```solidity

File: contracts/state-transition/chain-deps/DiamondProxy.sol

/// @audit `facetAddress`,  are used only once
28:         address facetAddress = facet.facetAddress;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondProxy.sol#L28-L28) 


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

/// @audit `oldPendingAdmin`,  are used only once
25:         address oldPendingAdmin = s.pendingAdmin;

/// @audit `previousAdmin`,  are used only once
36:         address previousAdmin = s.admin;

/// @audit `oldPriorityTxMaxGasLimit`,  are used only once
61:         uint256 oldPriorityTxMaxGasLimit = s.priorityTxMaxGasLimit;

/// @audit `oldFeeParams`,  are used only once
72:         FeeParams memory oldFeeParams = s.feeParams;

/// @audit `oldNominator`,  are used only once
80:         uint128 oldNominator = s.baseTokenGasPriceMultiplierNominator;

/// @audit `oldDenominator`,  are used only once
81:         uint128 oldDenominator = s.baseTokenGasPriceMultiplierDenominator;

/// @audit `cutHashInput`,  are used only once
104:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L25-L25) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L36-L36), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L61-L61), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L72-L72), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L80-L80), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L81-L81), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L104-L104)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

/// @audit `commitment`,  are used only once
84:         bytes32 commitment = _createBatchCommitment(_newBatch, logOutput.stateDiffHash, blobCommitments, blobHashes);

/// @audit `lastL2BlockTimestamp`,  are used only once
116:         uint256 lastL2BlockTimestamp = _packedBatchAndL2BlockTimestamp & PACKED_L2_BLOCK_TIMESTAMP_MASK;

/// @audit `expectedUpgradeTxHash`,  are used only once
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);

/// @audit `priorityOp`,  are used only once
312:             PriorityOperation memory priorityOp = s.priorityQueue.popFront();

/// @audit `priorityOperationsHash`,  are used only once
329:         bytes32 priorityOperationsHash = _collectOperationsFromPriorityQueue(_storedBatch.numberOfLayer1Txs);

/// @audit `verifierParams`,  are used only once
396:         VerifierParams memory verifierParams = s.verifierParams;

/// @audit `successVerifyProof`,  are used only once
444:         bool successVerifyProof = s.verifier.verify(
445:             proofPublicInput,
446:             _proof.serializedProof,
447:             _proof.recursiveAggregationInput
448:         );

/// @audit `passThroughDataHash`,  are used only once
506:         bytes32 passThroughDataHash = keccak256(_batchPassThroughData(_newBatchData));

/// @audit `metadataHash`,  are used only once
507:         bytes32 metadataHash = keccak256(_batchMetaParameters());

/// @audit `auxiliaryOutputHash`,  are used only once
508:         bytes32 auxiliaryOutputHash = keccak256(
509:             _batchAuxiliaryOutput(_newBatchData, _stateDiffHash, _blobCommitments, _blobHashes)
510:         );

/// @audit `l2ToL1LogsHash`,  are used only once
545:         bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs);

/// @audit `precompileInput`,  are used only once
610:         bytes memory precompileInput = abi.encodePacked(_versionedHash, _openingPoint, _openingValueCommitmentProof);

/// @audit `success`, `data`,  are used only once
612:         (bool success, bytes memory data) = POINT_EVALUATION_PRECOMPILE_ADDR.staticcall(precompileInput);

/// @audit `openingPoint`,  are used only once
643:             bytes32 openingPoint = bytes32(
644:                 uint256(uint128(bytes16(_pubdataCommitments[i:i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET])))
645:             );

/// @audit `versionedHash`,  are used only once
662:         bytes32 versionedHash = _getBlobVersionedHash(versionedHashIndex);

/// @audit `success`, `data`,  are used only once
680:         (bool success, bytes memory data) = s.blobVersionedHashRetriever.staticcall(abi.encode(_index));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L84-L84) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L116-L116), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L291-L291), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L312-L312), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L329-L329), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L396-L396), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L444-L448), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L506-L506), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L507-L507), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L508-L510), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L545-L545), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L610-L610), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L612-L612), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L643-L645), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L662-L662), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L680-L680)


```solidity

File: contracts/state-transition/chain-deps/facets/Getters.sol

/// @audit `ds`,  are used only once
158:         Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();

/// @audit `selectorsArrayLen`,  are used only once
168:         uint256 selectorsArrayLen = ds.facetToSelectors[_facet].selectors.length;

/// @audit `selector0`,  are used only once
170:             bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];

/// @audit `facetToSelectors`,  are used only once
210:             Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];

/// @audit `ds`,  are used only once
218:         Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();

/// @audit `ds`,  are used only once
224:         Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();

/// @audit `ds`,  are used only once
230:         Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L158-L158) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L168-L168), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L170-L170), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L210-L210), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L218-L218), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L224-L224), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L230-L230)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

/// @audit `amount`,  are used only once
41:         uint256 amount = address(this).balance;

/// @audit `sharedBridgeAddress`,  are used only once
42:         address sharedBridgeAddress = s.baseTokenBridge;

/// @audit `l2Log`,  are used only once
92:         L2Log memory l2Log = L2Log({
93:             l2ShardId: 0,
94:             isService: true,
95:             txNumberInBatch: _l2TxNumberInBatch,
96:             sender: L2_BOOTLOADER_ADDRESS,
97:             key: _l2TxHash,
98:             value: bytes32(uint256(_status))
99:         });

/// @audit `calculatedRootHash`,  are used only once
123:         bytes32 calculatedRootHash = Merkle.calculateRoot(_proof, _index, hashedLog);

/// @audit `actualRootHash`,  are used only once
124:         bytes32 actualRootHash = s.l2LogsRootHashes[_batchNumber];

/// @audit `l2GasPrice`,  are used only once
148:         uint256 l2GasPrice = _deriveL2GasPrice(_gasPrice, _l2GasPerPubdataByteLimit);

/// @audit `fullPubdataPriceBaseToken`,  are used only once
167:         uint256 fullPubdataPriceBaseToken = pubdataPriceBaseToken +
168:             batchOverheadBaseToken /
169:             uint256(feeParams.maxPubdataPerBatch);

/// @audit `l2GasPrice`,  are used only once
171:         uint256 l2GasPrice = feeParams.minimalL2GasPrice + batchOverheadBaseToken / uint256(feeParams.maxL2GasPerBatch);

/// @audit `minL2GasPriceBaseToken`,  are used only once
172:         uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata;

/// @audit `baseCost`,  are used only once
271:         uint256 baseCost = _params.l2GasPrice * _params.l2GasLimit;

/// @audit `hashedBytecode`,  are used only once
357:             bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L41-L41) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L42-L42), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L92-L99), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L123-L123), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L124-L124), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L148-L148), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L167-L169), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L171-L171), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L172-L172), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L271-L271), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L357-L357)


```solidity

File: contracts/state-transition/libraries/Diamond.sol

/// @audit `position`,  are used only once
88:         bytes32 position = DIAMOND_STORAGE_POSITION;

/// @audit `facetCutsLength`,  are used only once
100:         uint256 facetCutsLength = facetCuts.length;

/// @audit `ds`,  are used only once
127:         DiamondStorage storage ds = getDiamondStorage();

/// @audit `selectorsLength`,  are used only once
137:         uint256 selectorsLength = _selectors.length;

/// @audit `oldFacet`,  are used only once
140:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

/// @audit `ds`,  are used only once
150:         DiamondStorage storage ds = getDiamondStorage();

/// @audit `selectorsLength`,  are used only once
157:         uint256 selectorsLength = _selectors.length;

/// @audit `ds`,  are used only once
173:         DiamondStorage storage ds = getDiamondStorage();

/// @audit `selectorsLength`,  are used only once
177:         uint256 selectorsLength = _selectors.length;

/// @audit `selectorsLength`,  are used only once
192:         uint256 selectorsLength = ds.facetToSelectors[_facet].selectors.length;

/// @audit `selector0`,  are used only once
214:             bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];

/// @audit `success`,  are used only once
283:             (bool success, bytes memory data) = _init.delegatecall(_calldata);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L88-L88) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L100-L100), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L127-L127), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L137-L137), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L140-L140), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L150-L150), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L157-L157), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L173-L173), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L177-L177), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L192-L192), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L214-L214), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L283-L283)


```solidity

File: contracts/state-transition/libraries/LibMap.sol

/// @audit `mapValue`,  are used only once
23:             uint256 mapValue = _map.map[_index / 8];

/// @audit `bitOffset`,  are used only once
27:             uint256 bitOffset = (_index & 7) * 32;

/// @audit `oldValue`,  are used only once
54:             uint32 oldValue = uint32(mapValue >> bitOffset);

/// @audit `newValueXorOldValue`,  are used only once
57:             uint256 newValueXorOldValue = uint256(oldValue ^ _value);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L23-L23) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L27-L27), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L54-L54), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L57-L57)


```solidity

File: contracts/state-transition/libraries/TransactionValidator.sol

/// @audit `overheadForLength`,  are used only once
135:         uint256 overheadForLength = MEMORY_OVERHEAD_GAS * _encodingLength;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L135-L135) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

/// @audit `previousDefaultAccountBytecodeHash`,  are used only once
100:         bytes32 previousDefaultAccountBytecodeHash = s.l2DefaultAccountBytecodeHash;

/// @audit `previousBootloaderBytecodeHash`,  are used only once
117:         bytes32 previousBootloaderBytecodeHash = s.l2BootloaderBytecodeHash;

/// @audit `oldVerifier`,  are used only once
135:         IVerifier oldVerifier = s.verifier;

/// @audit `oldVerifierParams`,  are used only once
155:         VerifierParams memory oldVerifierParams = s.verifierParams;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L100-L100) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L117-L117), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L135-L135), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L155-L155)


```solidity

File: contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

/// @audit `txHash`,  are used only once
59:         bytes32 txHash = _setL2SystemContractUpgrade(
60:             _proposedUpgrade.l2ProtocolUpgradeTx,
61:             _proposedUpgrade.factoryDeps,
62:             _proposedUpgrade.newProtocolVersion
63:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L59-L63) 


```solidity

File: contracts/L2ContractHelper.sol

/// @audit `senderBytes`,  are used only once
107:         bytes32 senderBytes = bytes32(uint256(uint160(_sender)));

/// @audit `data`,  are used only once
108:         bytes32 data = keccak256(
109:             bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
110:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L107-L107) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L108-L110)


```solidity

File: contracts/SystemContractsCaller.sol

/// @audit `callAddr`,  are used only once
38:         address callAddr = SYSTEM_CALL_CALL_ADDRESS;

/// @audit `dataStart`,  are used only once
40:         uint32 dataStart;

/// @audit `dataLength`,  are used only once
44:         uint32 dataLength = uint32(Utils.safeCastToU32(data.length));

/// @audit `farCallAbi`,  are used only once
46:         uint256 farCallAbi = getFarCallABI(
47:             0,
48:             0,
49:             dataStart,
50:             dataLength,
51:             gasLimit,
52:             // Only rollup is supported for now
53:             0,
54:             CalldataForwardingMode.UseHeap,
55:             false,
56:             true
57:         );

/// @audit `msgValueSimulator`,  are used only once
65:             address msgValueSimulator = MSG_VALUE_SYSTEM_CONTRACT;

/// @audit `forwardMask`,  are used only once
68:             uint256 forwardMask = MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT;

/// @audit `size`,  are used only once
84:         uint256 size;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L38-L38) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L40-L40), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L44-L44), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L46-L57), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L65-L65), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L68-L68), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L84-L84)


```solidity

File: contracts/bridge/L2SharedBridge.sol

/// @audit `l2StandardToken`,  are used only once
64:             address l2StandardToken = address(new L2StandardERC20{salt: bytes32(0)}());

/// @audit `deployedToken`,  are used only once
97:             address deployedToken = _deployL2Token(_l1Token, _data);

/// @audit `salt`,  are used only once
110:         bytes32 salt = _getCreate2Salt(_l1Token);

/// @audit `message`,  are used only once
131:         bytes memory message = _getL1WithdrawMessage(_l1Receiver, l1Token, _amount);

/// @audit `constructorInputHash`,  are used only once
150:         bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""));

/// @audit `salt`,  are used only once
151:         bytes32 salt = _getCreate2Salt(_l1Token);

/// @audit `success`, `returndata`,  are used only once
165:         (bool success, bytes memory returndata) = SystemContractsCaller.systemCallWithReturndata(
166:             uint32(gasleft()),
167:             DEPLOYER_SYSTEM_CONTRACT,
168:             0,
169:             abi.encodeCall(
170:                 IContractDeployer.create2,
171:                 (salt, l2TokenProxyBytecodeHash, abi.encode(address(l2TokenBeacon), ""))
172:             )
173:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L64-L64) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L97-L97), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L110-L110), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L131-L131), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L150-L150), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L151-L151), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L165-L173)


```solidity

File: contracts/bridge/L2StandardERC20.sol

/// @audit `nameBytes`, `symbolBytes`, `decimalsBytes`,  are used only once
57:         (bytes memory nameBytes, bytes memory symbolBytes, bytes memory decimalsBytes) = abi.decode(
58:             _data,
59:             (bytes, bytes, bytes)
60:         );

/// @audit `beaconAddress`,  are used only once
119:         address beaconAddress = _getBeacon();


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L57-L60) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L119-L119)


</details>


### [GAS&#x2011;44] Using `storage` instead of `memory` for structs/arrays saves gas 
When fetching data from a storage location, assigning the data to a `memory` variable causes all fields of the struct/array to be read from storage, which incurs a Gcoldsload (**2100 gas**) for *each* field of the struct/array. If the fields are read from the new memory variable, they incur an additional `MLOAD` rather than a cheap stack read. Instead of declearing the variable with the `memory` keyword, declaring the variable with the `storage` keyword and caching any fields that need to be re-read in stack variables, will be much cheaper, only incuring the Gcoldsload for the fields actually read. The only time it makes sense to read the whole struct/array into a `memory` variable, is if the full struct/array is being returned by the function, is being passed to a function that requires `memory`, or if the array/struct is being read from another `memory` array/struct


*There are 11 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ContractDeployer.sol

41:         AccountInfo memory info = accountInfo[_address];


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L41-L41) 


```solidity

File: contracts/SystemContext.sol

135:         VirtualBlockUpgradeInfo memory currentVirtualBlockUpgradeInfo = virtualBlockUpgradeInfo;

173:         BlockInfo memory batchInfo = currentBatchInfo;

181:         BlockInfo memory blockInfo = currentL2BlockInfo;

275:         BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L135-L135) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L173-L173), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L181-L181), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L275-L275)


```solidity

File: contracts/state-transition/chain-deps/DiamondProxy.sol

27:         Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondProxy.sol#L27-L27) 


```solidity

File: contracts/state-transition/chain-deps/facets/Getters.sol

210:             Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L210-L210) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

157:         FeeParams memory feeParams = s.feeParams;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L157-L157) 


```solidity

File: contracts/state-transition/libraries/Diamond.sol

140:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

160:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

180:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L140-L140) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L160-L160), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L180-L180)


</details>


### [GAS&#x2011;45] `>=`/`<=` costs less gas than `>`/`<` 
The compiler uses opcodes `GT` and `ISZERO` for solidity code that uses `>`, but only requires `LT` for `>=`, [which saves **3 gas**](https://gist.github.com/IllIllI000/3dc79d25acccfa16dee4e83ffdc6ffde)


*There are 60 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/AccountCodeStorage.sol

102:         if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {

132:             uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS &&


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L102-L102) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L132-L132)


```solidity

File: contracts/ComplexUpgrader.sol

24:         require(_delegateTo.code.length > 0, "Delegatee is an EOA");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ComplexUpgrader.sol#L24-L24) 


```solidity

File: contracts/Compressor.sol

63:                 require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L63-L63) 


```solidity

File: contracts/ContractDeployer.sol

48:             _address > address(MAX_SYSTEM_CONTRACT_ADDRESS) &&

265:         require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

303:         require(knownCodeMarker > 0, "The code hash is not known");

332:             if (value > 0) {

339:             if (value > 0) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L48-L48) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L265-L265), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L303-L303), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L332-L332), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L339-L339)


```solidity

File: contracts/L1Messenger.sol

222:         while (nodesOnCurrentLevel > 1) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L222-L222) 


```solidity

File: contracts/MsgValueSimulator.sol

53:         uint256 userGas = gasInContext > MSG_VALUE_SIMULATOR_STIPEND_GAS


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/MsgValueSimulator.sol#L53-L53) 


```solidity

File: contracts/NonceHolder.sol

156:         return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);

156:         return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L156-L156) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L156-L156)


```solidity

File: contracts/SystemContext.sol

119:         return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;

144:         if (blockNumber <= _block || blockNumber - _block > 256) {

146:         } else if (_block < currentVirtualBlockUpgradeInfo.virtualBlockStartBatch) {

152:             currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0

245:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

387:                 _l2BlockTimestamp > currentL2BlockTimestamp,

413:         require(currentBatchNumber > 0, "The current batch number must be greater than 0");

430:             _newTimestamp > currentBlockTimestamp,

451:         require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L119-L119) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L144-L144), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L146-L146), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L152-L152), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L245-L245), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L287-L287), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L355-L355), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L387-L387), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L413-L413), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L430-L430), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L451-L451)


```solidity

File: contracts/libraries/RLPEncoder.sol

26:             if (_val < 128) {

62:             if (_len < 56) {

86:             if (_number > type(uint128).max) {

90:             if (_number > type(uint64).max) {

94:             if (_number > type(uint32).max) {

98:             if (_number > type(uint16).max) {

102:             if (_number > type(uint8).max) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L26-L26) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L62-L62), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L86-L86), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L90-L90), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L94-L94), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L98-L98), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L102-L102)


```solidity

File: contracts/libraries/SystemContractHelper.sol

319:         require(index < 10, "There are only 10 accessible registers");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L319-L319) 


```solidity

File: contracts/libraries/TransactionHelper.sol

378:             if (currentAllowance < minAllowance) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L378-L378) 


```solidity

File: contracts/libraries/Utils.sol

87:         require(lengthInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L87-L87) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

121:             require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");

129:             require(amount > 0, "ShB: 0 amount to transfer");

327:         require(_amount > 0, "y1");

375:         return (_chainId == ERA_CHAIN_ID) && (_l2BatchNumber < eraFirstPostUpgradeBatch);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L121-L121) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L129-L129), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L327-L327), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L375-L375)


```solidity

File: contracts/bridgehub/Bridgehub.sol

301:             _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,

329:         } else if (_refundRecipient.code.length > 0) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L301-L301) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L329-L329)


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

26:         require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L26-L26) 


```solidity

File: contracts/governance/Governance.sol

111:         } else if (timestamp > block.timestamp) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L111-L111) 


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

117:             s.protocolVersion > _oldProtocolVersion,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L117-L117) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

114:         require(_previousBatchTimestamp < batchTimestamp, "h3");

429:         if (_proof.serializedProof.length > 0) {

482:         require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch

485:         if (_newLastBatch < s.totalBatchesVerified) {

492:         if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) {

593:         return (_bitMap & (1 << _index)) > 0;

631:         require(_pubdataCommitments.length > 0, "pl");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L114-L114) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L429-L429), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L482-L482), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L485-L485), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L492-L492), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L593-L593), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L631-L631)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

158:         require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

277:         if (refundRecipient.code.length > 0) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L158-L158) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L277-L277)


```solidity

File: contracts/state-transition/libraries/Diamond.sol

107:             require(selectors.length > 0, "B"); // no functions for diamond cut

132:         require(_facet.code.length > 0, "G");

155:         require(_facet.code.length > 0, "K");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L107-L107) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L132-L132), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L155-L155)


```solidity

File: contracts/state-transition/libraries/Merkle.sol

24:         require(pathLength > 0, "xc");

25:         require(pathLength < 256, "bt");

26:         require(_index < (1 << pathLength), "px");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L24-L24) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L25-L25), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L26-L26)


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

239:             _newProtocolVersion > previousProtocolVersion,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L239-L239) 


```solidity

File: contracts/bridge/L2SharedBridge.sol

124:         require(_amount > 0, "Amount cannot be zero");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L124-L124) 


</details>


### [GAS&#x2011;46] Using `this.<fn>()` wastes gas 
Calling an external function internally, through the use of `this` wastes the gas overhead of calling an external function (**100 gas**). Instead, change the function from `external` to `public`, and remove the `this`


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/bridge/L2StandardERC20.sol

75:         try this.decodeString(nameBytes) returns (string memory nameString) {

81:         try this.decodeString(symbolBytes) returns (string memory symbolString) {

93:         try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L75-L75) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L81-L81), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L93-L93)


</details>


### [GAS&#x2011;47] Use assembly to validate `msg.sender` 
We can use assembly to efficiently validate msg.sender with the least amount of opcodes necessary. For more details check the following report [Here](https://code4rena.com/reports/2023-05-juicebox#g-06-use-assembly-to-validate-msgsender)


*There are 36 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/AccountCodeStorage.sol

26:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L26-L26) 


```solidity

File: contracts/ComplexUpgrader.sol

22:         require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ComplexUpgrader.sol#L22-L22) 


```solidity

File: contracts/ContractDeployer.sol

29:         require(msg.sender == address(this), "Callable only by self");

240:             msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L29-L29) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L240-L240)


```solidity

File: contracts/DefaultAccount.sol

29:         if (msg.sender != BOOTLOADER_FORMAL_ADDRESS) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L29-L29) 


```solidity

File: contracts/ImmutableSimulator.sol

35:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L35-L35) 


```solidity

File: contracts/KnownCodesStorage.sol

20:         require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L20-L20) 


```solidity

File: contracts/L2BaseToken.sol

36:                 msg.sender == BOOTLOADER_FORMAL_ADDRESS,


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L36-L36) 


```solidity

File: contracts/NonceHolder.sol

137:             msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L137-L137) 


```solidity

File: contracts/interfaces/ISystemContract.sol

41:         require(msg.sender == caller, "Inappropriate caller");

48:         require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");

55:         require(msg.sender == FORCE_DEPLOYER);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L41-L41) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L48-L48), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L55-L55)


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

64:         require(msg.sender == address(sharedBridge), "Not shared bridge");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L64-L64) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

69:         require(msg.sender == address(bridgehub), "ShB not BH");

76:             msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),

84:         require(msg.sender == address(legacyBridge), "ShB not legacy bridge");

138:         require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L69-L69) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L76-L76), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L84-L84), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L138-L138)


```solidity

File: contracts/bridgehub/Bridgehub.sol

46:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

62:         require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

328:             _recipient = msg.sender == tx.origin ? msg.sender : AddressAliasHelper.applyL1ToL2Alias(msg.sender);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L46-L46) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L62-L62), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L328-L328)


```solidity

File: contracts/governance/Governance.sol

59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

65:         require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

72:             msg.sender == owner() || msg.sender == securityCouncil,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L59-L59) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L65-L65), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L72-L72)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

64:         require(msg.sender == bridgehub, "StateTransition: only bridgehub");

70:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

121:         require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L64-L64) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L70-L70), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L121-L121)


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

62:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L62-L62) 


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

34:         require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L34-L34) 


```solidity

File: contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

16:         require(msg.sender == s.admin, "StateTransition Chain: not admin");

27:         require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

32:         require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

38:             msg.sender == s.admin || msg.sender == s.stateTransitionManager,

46:             s.validators[msg.sender] || msg.sender == s.stateTransitionManager,

53:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16-L16) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27-L27), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32-L32), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L38-L38), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L46-L46), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53-L53)


```solidity

File: contracts/bridge/L2StandardERC20.sol

120:         require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");

130:         require(msg.sender == l2Bridge, "xnt"); // Only L2 bridge can call this method


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L120-L120) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L130-L130)


</details>


### [GAS&#x2011;48] Can make the variable outside the loop to save gas 
Creating variables inside the loop consum more gas compared to declaring them outside and just reaffecting values to them inside the loop.


*There are 53 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/Compressor.sol

//@audit variable `indexOfEncodedChunk` is created inside a loop.
62:                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;

//@audit variable `encodedChunk` is created inside a loop.
65:                 uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);

//@audit variable `realChunk` is created inside a loop.
66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

//@audit variable `stateDiff` is created inside a loop.
128:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];

//@audit variable `enumIndex` is created inside a loop.
129:             uint64 enumIndex = stateDiff.readUint64(84);

//@audit variable `derivedKey` is created inside a loop.
137:             bytes32 derivedKey = stateDiff.readBytes32(52);

//@audit variable `initValue` is created inside a loop.
138:             uint256 initValue = stateDiff.readUint256(92);

//@audit variable `finalValue` is created inside a loop.
139:             uint256 finalValue = stateDiff.readUint256(124);

//@audit variable `metadata` is created inside a loop.
143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

//@audit variable `operation` is created inside a loop.
145:             uint8 operation = metadata & OPERATION_BITMASK;

//@audit variable `len` is created inside a loop.
146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

//@audit variable `stateDiff` is created inside a loop.
160:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];

//@audit variable `enumIndex` is created inside a loop.
161:             uint64 enumIndex = stateDiff.readUint64(84);

//@audit variable `initValue` is created inside a loop.
166:             uint256 initValue = stateDiff.readUint256(92);

//@audit variable `finalValue` is created inside a loop.
167:             uint256 finalValue = stateDiff.readUint256(124);

//@audit variable `compressedEnumIndex` is created inside a loop.
168:             uint256 compressedEnumIndex = _sliceToUint256(

//@audit variable `metadata` is created inside a loop.
174:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

//@audit variable `operation` is created inside a loop.
176:             uint8 operation = metadata & OPERATION_BITMASK;

//@audit variable `len` is created inside a loop.
177:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L62-L62) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L65-L65), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L66-L66), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L128-L128), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L129-L129), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L137-L137), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L138-L138), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L139-L139), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L143-L143), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L145-L145), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L146-L146), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L160-L160), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L161-L161), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L166-L166), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L167-L167), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L168-L168), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L174-L174), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L176-L176), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L177-L177)


```solidity

File: contracts/ImmutableSimulator.sol

//@audit variable `index` is created inside a loop.
39:                 uint256 index = _immutables[i].index;

//@audit variable `value` is created inside a loop.
40:                 bytes32 value = _immutables[i].value;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L39-L39) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L40-L40)


```solidity

File: contracts/L1Messenger.sol

//@audit variable `hashedLog` is created inside a loop.
207:             bytes32 hashedLog = EfficientCall.keccak(

//@audit variable `i` is created inside a loop.
224:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

//@audit variable `currentMessageLength` is created inside a loop.
237:             uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

//@audit variable `hashedMessage` is created inside a loop.
239:             bytes32 hashedMessage = EfficientCall.keccak(

//@audit variable `currentBytecodeLength` is created inside a loop.
255:             uint32 currentBytecodeLength = uint32(


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L207-L207) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L224-L224), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L237-L237), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L239-L239), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L255-L255)


```solidity

File: contracts/PubdataChunkPublisher.sol

//@audit variable `start` is created inside a loop.
37:             uint256 start = BLOB_SIZE_BYTES * i;

//@audit variable `blobHash` is created inside a loop.
45:             bytes32 blobHash;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L37-L37) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L45-L45)


```solidity

File: contracts/governance/Governance.sol

//@audit variable `success` is created inside a loop.
226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

//@audit variable `returnData` is created inside a loop.
226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L226-L226) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L226-L226)


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

//@audit variable `commitBatchTimestamp` is created inside a loop.
186:                 uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(

//@audit variable `commitBatchTimestamp` is created inside a loop.
210:                 uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L186-L186) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L210-L210)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

//@audit variable `logSender` is created inside a loop.
144:             (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);

//@audit variable `logKey` is created inside a loop.
145:             (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);

//@audit variable `logValue` is created inside a loop.
146:             (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);

//@audit variable `expectedUpgradeTxHash` is created inside a loop.
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);

//@audit variable `priorityOp` is created inside a loop.
312:             PriorityOperation memory priorityOp = s.priorityQueue.popFront();

//@audit variable `currentBatchCommitment` is created inside a loop.
412:             bytes32 currentBatchCommitment = _committedBatches[i].commitment;

//@audit variable `blobVersionedHash` is created inside a loop.
637:             bytes32 blobVersionedHash = _getBlobVersionedHash(versionedHashIndex);

//@audit variable `openingPoint` is created inside a loop.
643:             bytes32 openingPoint = bytes32(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L144-L144) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L145-L145), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L146-L146), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L291-L291), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L312-L312), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L412-L412), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L637-L637), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L643-L643)


```solidity

File: contracts/state-transition/chain-deps/facets/Getters.sol

//@audit variable `facetAddr` is created inside a loop.
209:             address facetAddr = ds.facets[i];

//@audit variable `facetToSelectors` is created inside a loop.
210:             Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L209-L209) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L210-L210)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

//@audit variable `hashedBytecode` is created inside a loop.
357:             bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L357-L357) 


```solidity

File: contracts/state-transition/libraries/Diamond.sol

//@audit variable `action` is created inside a loop.
102:             Action action = facetCuts[i].action;

//@audit variable `facet` is created inside a loop.
103:             address facet = facetCuts[i].facet;

//@audit variable `isFacetFreezable` is created inside a loop.
104:             bool isFacetFreezable = facetCuts[i].isFreezable;

//@audit variable `selectors` is created inside a loop.
105:             bytes4[] memory selectors = facetCuts[i].selectors;

//@audit variable `selector` is created inside a loop.
139:             bytes4 selector = _selectors[i];

//@audit variable `oldFacet` is created inside a loop.
140:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

//@audit variable `selector` is created inside a loop.
159:             bytes4 selector = _selectors[i];

//@audit variable `oldFacet` is created inside a loop.
160:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

//@audit variable `selector` is created inside a loop.
179:             bytes4 selector = _selectors[i];

//@audit variable `oldFacet` is created inside a loop.
180:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L102-L102) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L103-L103), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L104-L104), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L105-L105), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L139-L139), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L140-L140), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L159-L159), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L160-L160), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L179-L179), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L180-L180)


</details>


### [GAS&#x2011;49] Consider activating via-ir for deploying 
The Solidity compiler's Intermediate Representation (IR) based code generator, which can be activated using --via-ir on the command line or {""viaIR"": true} in the options, serves a dual purpose. Firstly, it boosts the transparency and audibility of code generation, which enhances developers' comprehension and control over the contract's final bytecode. Secondly, it enables more sophisticated optimization passes that span multiple functions, thereby potentially leading to more efficient bytecode.
It's important to note that using the IR- based code generator may lengthen compile times due to the extra optimization steps.Therefore, it's advised to test your contract with and without this option enabled to measure the performance and gas cost implications.If the IR- based code generator significantly enhances your contract's performance or reduces gas costs, consider using the --via-ir flag during deployment.This way, you can leverage more advanced compiler optimizations without hindering your development workflow.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: hardhat.config.ts

//@audit /2024-03-zksync/code/system-contracts/hardhat.config.ts
1: 

//@audit /2024-03-zksync/code/contracts/ethereum/hardhat.config.ts
1: 

//@audit /2024-03-zksync/code/contracts/zksync/hardhat.config.ts
1: 


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//hardhat.config.ts#L1-L1) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//hardhat.config.ts#L1-L1), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//hardhat.config.ts#L1-L1)


</details>


### [GAS&#x2011;50] `++i` costs less gas than `i++`, especially when it's used in `for`-loops (`--i`/`i--` too) 
*Saves 5 gas per loop*


*There are 8 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/Compressor.sol

135:             numInitialWritesProcessed++;

144:             stateDiffPtr++;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L135-L135) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L144-L144)


```solidity

File: contracts/L1Messenger.sol

109:         numberOfLogsToProcess++;

284:         calldataPtr++;

290:         calldataPtr++;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L109-L109) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L284-L284), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L290-L290)


```solidity

File: contracts/PubdataChunkPublisher.sol

36:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L36-L36) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L580-L580) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L667-L667)


</details>


### [GAS&#x2011;51] Unnecessary casting as variable is already of the same type 



*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/libraries/SystemContractHelper.sol

//@audit `MAX_SYSTEM_CONTRACT_ADDRESS` is getting converted from `uint160` to `uint160`
339:         return uint160(_address) <= uint160(MAX_SYSTEM_CONTRACT_ADDRESS);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L339-L339) 


```solidity

File: contracts/state-transition/StateTransitionManager.sol

//@audit `protocolVersion` is getting converted from `uint256` to `uint256`
266:             bytes32(uint256(protocolVersion)),

//@audit `storedBatchZero` is getting converted from `bytes32` to `bytes32`
271:             bytes32(storedBatchZero),


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L266-L266) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L271-L271)


</details>


### [GAS&#x2011;52] Structs can be packed into fewer storage slots by truncating timestamp bytes 
By using a `uint32` rather than a larger type for variables that track timestamps, one can save gas by using fewer storage slots per struct, at the expense of the protocol breaking after the year 2106 (when `uint32` wraps). If this is an acceptable tradeoff, each slot saved can avoid an extra Gsset (**20000 gas**) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/state-transition/chain-interfaces/IExecutor.sol

//@audit the following variables: timestamp,  could be packed
83:     struct StoredBatchInfo {
84:         uint64 batchNumber;
85:         bytes32 batchHash;
86:         uint64 indexRepeatedStorageChanges;
87:         uint256 numberOfLayer1Txs;
88:         bytes32 priorityOperationsHash;
89:         bytes32 l2LogsTreeRoot;
90:         uint256 timestamp;
91:         bytes32 commitment;
92:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IExecutor.sol#L83-L92) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

//@audit the following variables: upgradeTimestamp,  could be packed
28: struct ProposedUpgrade {
29:     L2CanonicalTransaction l2ProtocolUpgradeTx;
30:     bytes[] factoryDeps;
31:     bytes32 bootloaderHash;
32:     bytes32 defaultAccountHash;
33:     address verifier;
34:     VerifierParams verifierParams;
35:     bytes l1ContractsUpgradeCalldata;
36:     bytes postUpgradeCalldata;
37:     uint256 upgradeTimestamp;
38:     uint256 newProtocolVersion;
39: }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L28-L39) 


</details>


### [GAS&#x2011;53] Stat variables can be packed into fewer storage slots by truncating timestamp bytes 
By using a `uint32` rather than a larger type for variables that track timestamps, one can save gas by using fewer storage slots per struct, at the expense of the protocol breaking after the year 2106 (when `uint32` wraps). If this is an acceptable tradeoff, each slot saved can avoid an extra Gsset (**20000 gas**) for the first setting of the stat variable. Subsequent reads as well as writes have smaller gas savings


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/governance/Governance.sol

//@audit the following variables could be packed: 
    uint256 public minDelay;
 
20: contract Governance is IGovernance, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L20-L20) 


</details>


### [GAS&#x2011;54] State variables can be packed into fewer storage slots 
If variables occupying the same slot are both written the same function or by the constructor, avoids a separate Gsset (**20000 gas**). Reads of the variables can also be cheaper


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/SystemContext.sol

// @audit from 12 to 11 you need to change the structure elements order to: , uint256, uint256, uint256, uint256, uint256, mapping, bytes32, uint256, uint256, address, address, uint16, BlockInfo, VirtualBlockUpgradeInfo, BlockInfo, BlockInfo, array
017: contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract {
018:     /// @notice The number of latest L2 blocks to store.
019:     /// @dev EVM requires us to be able to query the hashes of previous 256 blocks.
020:     /// We could either:
021:     /// - Store the latest 256 hashes (and strictly rely that we do not accidentally override the hash of the block 256 blocks ago)
022:     /// - Store the latest 257 blocks' hashes.
023:     uint256 internal constant MINIBLOCK_HASHES_TO_STORE = 257;
024: 
025:     /// @notice The chainId of the network. It is set at the genesis.
026:     uint256 public chainId;
027: 
028:     /// @notice The `tx.origin` in the current transaction.
029:     /// @dev It is updated before each transaction by the bootloader
030:     address public origin;
031: 
032:     /// @notice The `tx.gasPrice` in the current transaction.
033:     /// @dev It is updated before each transaction by the bootloader
034:     uint256 public gasPrice;
035: 
036:     /// @notice The current block's gasLimit.
037:     uint256 public blockGasLimit = type(uint32).max;
038: 
039:     /// @notice The `block.coinbase` in the current transaction.
040:     /// @dev For the support of coinbase, we will use the bootloader formal address for now
041:     address public coinbase = BOOTLOADER_FORMAL_ADDRESS;
042: 
043:     /// @notice Formal `block.difficulty` parameter.
044:     uint256 public difficulty = 2.5e15;
045: 
046:     /// @notice The `block.basefee`.
047:     /// @dev It is currently a constant.
048:     uint256 public baseFee;
049: 
050:     /// @notice The number and the timestamp of the current L1 batch stored packed.
051:     BlockInfo internal currentBatchInfo;
052: 
053:     /// @notice The hashes of batches.
054:     /// @dev It stores batch hashes for all previous batches.
055:     mapping(uint256 batchNumber => bytes32 batchHash) internal batchHashes;
056: 
057:     /// @notice The number and the timestamp of the current L2 block.
058:     BlockInfo internal currentL2BlockInfo;
059: 
060:     /// @notice The rolling hash of the transactions in the current L2 block.
061:     bytes32 internal currentL2BlockTxsRollingHash;
062: 
063:     /// @notice The hashes of L2 blocks.
064:     /// @dev It stores block hashes for previous L2 blocks. Note, in order to make publishing the hashes
065:     /// of the miniblocks cheaper, we only store the previous MINIBLOCK_HASHES_TO_STORE ones. Since whenever we need to publish a state
066:     /// diff, a pair of <key, value> is published and for cached keys only 8-byte id is used instead of 32 bytes.
067:     /// By having this data in a cyclic array of MINIBLOCK_HASHES_TO_STORE blocks, we bring the costs down by 40% (i.e. 40 bytes per miniblock instead of 64 bytes).
068:     /// @dev The hash of a miniblock with number N would be stored under slot N%MINIBLOCK_HASHES_TO_STORE.
069:     /// @dev Hashes of the blocks older than the ones which are stored here can be calculated as _calculateLegacyL2BlockHash(blockNumber).
070:     bytes32[MINIBLOCK_HASHES_TO_STORE] internal l2BlockHash;
071: 
072:     /// @notice To make migration to L2 blocks smoother, we introduce a temporary concept of virtual L2 blocks, the data
073:     /// about which will be returned by the EVM-like methods: block.number/block.timestamp/blockhash.
074:     /// - Their number will start from being equal to the number of the batch and it will increase until it reaches the L2 block number.
075:     /// - Their timestamp is updated each time a new virtual block is created.
076:     /// - Their hash is calculated as `keccak256(uint256(number))`
077:     BlockInfo internal currentVirtualL2BlockInfo;
078: 
079:     /// @notice The information about the virtual blocks upgrade, which tracks when the migration to the L2 blocks has started and finished.
080:     VirtualBlockUpgradeInfo internal virtualBlockUpgradeInfo;
081: 
082:     /// @notice Set the chainId origin.
083:     /// @param _newChainId The chainId
084:     function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {
085:         chainId = _newChainId;
086:     }
087: 
088:     /// @notice Number of current transaction in block.
089:     uint16 public txNumberInBlock;
090: 
091:     /// @notice The current gas per pubdata byte
092:     uint256 public gasPerPubdataByte;
093: 
094:     /// @notice The number of pubdata spent as of the start of the transaction
095:     uint256 internal basePubdataSpent;
096: 
097:     /// @notice Set the current tx origin.
098:     /// @param _newOrigin The new tx origin.
099:     function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {
100:         origin = _newOrigin;
101:     }
102: 
103:     /// @notice Set the the current gas price.
104:     /// @param _gasPrice The new tx gasPrice.
105:     function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {
106:         gasPrice = _gasPrice;
107:     }
108: 
109:     /// @notice Sets the number of L2 gas that is needed to pay a single byte of pubdata.
110:     /// @dev This value does not have any impact on the execution and purely serves as a way for users
111:     /// to access the current gas price for the pubdata.
112:     function setPubdataInfo(uint256 _gasPerPubdataByte, uint256 _basePubdataSpent) external onlyCallFromBootloader {
113:         basePubdataSpent = _basePubdataSpent;
114:         gasPerPubdataByte = _gasPerPubdataByte;
115:     }
116: 
117:     function getCurrentPubdataSpent() public view returns (uint256) {
118:         uint256 pubdataPublished = SystemContractHelper.getZkSyncMeta().pubdataPublished;
119:         return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;
120:     }
121: 
122:     function getCurrentPubdataCost() external view returns (uint256) {
123:         return gasPerPubdataByte * getCurrentPubdataSpent();
124:     }
125: 
126:     /// @notice The method that emulates `blockhash` opcode in EVM.
127:     /// @dev Just like the blockhash in the EVM, it returns bytes32(0),
128:     /// when queried about hashes that are older than 256 blocks ago.
129:     /// @dev Since zksolc compiler calls this method to emulate `blockhash`,
130:     /// its signature can not be changed to `getL2BlockHashEVM`.
131:     /// @return hash The blockhash of the block with the given number.
132:     function getBlockHashEVM(uint256 _block) external view returns (bytes32 hash) {
133:         uint128 blockNumber = currentVirtualL2BlockInfo.number;
134: 
135:         VirtualBlockUpgradeInfo memory currentVirtualBlockUpgradeInfo = virtualBlockUpgradeInfo;
136: 
137:         // Due to virtual blocks upgrade, we'll have to use the following logic for retreiving the blockhash:
138:         // 1. If the block number is out of the 256-block supported range, return 0.
139:         // 2. If the block was created before the upgrade for the virtual blocks (i.e. there we used to use hashes of the batches),
140:         // we return the hash of the batch.
141:         // 3. If the block was created after the day when the virtual blocks have caught up with the L2 blocks, i.e.
142:         // all the information which is returned for users should be for L2 blocks, we return the hash of the corresponding L2 block.
143:         // 4. If the block queried is a virtual blocks, calculate it on the fly.
144:         if (blockNumber <= _block || blockNumber - _block > 256) {
145:             hash = bytes32(0);
146:         } else if (_block < currentVirtualBlockUpgradeInfo.virtualBlockStartBatch) {
147:             // Note, that we will get into this branch only for a brief moment of time, right after the upgrade
148:             // for virtual blocks before 256 virtual blocks are produced.
149:             hash = batchHashes[_block];
150:         } else if (
151:             _block >= currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block &&
152:             currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0
153:         ) {
154:             hash = _getLatest257L2blockHash(_block);
155:         } else {
156:             // Important: we do not want this number to ever collide with the L2 block hash (either new or old one) and so
157:             // that's why the legacy L2 blocks' hashes are keccak256(abi.encodePacked(uint32(_block))), while these are equivalent to
158:             // keccak256(abi.encodePacked(_block))
159:             hash = keccak256(abi.encode(_block));
160:         }
161:     }
162: 
163:     /// @notice Returns the hash of the given batch.
164:     /// @param _batchNumber The number of the batch.
165:     /// @return hash The hash of the batch.
166:     function getBatchHash(uint256 _batchNumber) external view returns (bytes32 hash) {
167:         hash = batchHashes[_batchNumber];
168:     }
169: 
170:     /// @notice Returns the current batch's number and timestamp.
171:     /// @return batchNumber and batchTimestamp tuple of the current batch's number and the current batch's timestamp
172:     function getBatchNumberAndTimestamp() public view returns (uint128 batchNumber, uint128 batchTimestamp) {
173:         BlockInfo memory batchInfo = currentBatchInfo;
174:         batchNumber = batchInfo.number;
175:         batchTimestamp = batchInfo.timestamp;
176:     }
177: 
178:     /// @notice Returns the current block's number and timestamp.
179:     /// @return blockNumber and blockTimestamp tuple of the current L2 block's number and the current block's timestamp
180:     function getL2BlockNumberAndTimestamp() public view returns (uint128 blockNumber, uint128 blockTimestamp) {
181:         BlockInfo memory blockInfo = currentL2BlockInfo;
182:         blockNumber = blockInfo.number;
183:         blockTimestamp = blockInfo.timestamp;
184:     }
185: 
186:     /// @notice Returns the current L2 block's number.
187:     /// @dev Since zksolc compiler calls this method to emulate `block.number`,
188:     /// its signature can not be changed to `getL2BlockNumber`.
189:     /// @return blockNumber The current L2 block's number.
190:     function getBlockNumber() public view returns (uint128) {
191:         return currentVirtualL2BlockInfo.number;
192:     }
193: 
194:     /// @notice Returns the current L2 block's timestamp.
195:     /// @dev Since zksolc compiler calls this method to emulate `block.timestamp`,
196:     /// its signature can not be changed to `getL2BlockTimestamp`.
197:     /// @return timestamp The current L2 block's timestamp.
198:     function getBlockTimestamp() public view returns (uint128) {
199:         return currentVirtualL2BlockInfo.timestamp;
200:     }
201: 
202:     /// @notice Assuming that block is one of the last MINIBLOCK_HASHES_TO_STORE ones, returns its hash.
203:     /// @param _block The number of the block.
204:     /// @return hash The hash of the block.
205:     function _getLatest257L2blockHash(uint256 _block) internal view returns (bytes32) {
206:         return l2BlockHash[_block % MINIBLOCK_HASHES_TO_STORE];
207:     }
208: 
209:     /// @notice Assuming that the block is one of the last MINIBLOCK_HASHES_TO_STORE ones, sets its hash.
210:     /// @param _block The number of the block.
211:     /// @param _hash The hash of the block.
212:     function _setL2BlockHash(uint256 _block, bytes32 _hash) internal {
213:         l2BlockHash[_block % MINIBLOCK_HASHES_TO_STORE] = _hash;
214:     }
215: 
216:     /// @notice Calculates the hash of an L2 block.
217:     /// @param _blockNumber The number of the L2 block.
218:     /// @param _blockTimestamp The timestamp of the L2 block.
219:     /// @param _prevL2BlockHash The hash of the previous L2 block.
220:     /// @param _blockTxsRollingHash The rolling hash of the transactions in the L2 block.
221:     function _calculateL2BlockHash(
222:         uint128 _blockNumber,
223:         uint128 _blockTimestamp,
224:         bytes32 _prevL2BlockHash,
225:         bytes32 _blockTxsRollingHash
226:     ) internal pure returns (bytes32) {
227:         return keccak256(abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash));
228:     }
229: 
230:     /// @notice Calculates the legacy block hash of L2 block, which were used before the upgrade where
231:     /// the advanced block hashes were introduced.
232:     /// @param _blockNumber The number of the L2 block.
233:     function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {
234:         return keccak256(abi.encodePacked(uint32(_blockNumber)));
235:     }
236: 
237:     /// @notice Performs the upgrade where we transition to the L2 blocks.
238:     /// @param _l2BlockNumber The number of the new L2 block.
239:     /// @param _expectedPrevL2BlockHash The expected hash of the previous L2 block.
240:     /// @param _isFirstInBatch Whether this method is called for the first time in the batch.
241:     function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {
242:         require(_isFirstInBatch, "Upgrade transaction must be first");
243: 
244:         // This is how it will be commonly done in practice, but it will simplify some logic later
245:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");
246: 
247:         unchecked {
248:             bytes32 correctPrevBlockHash = _calculateLegacyL2BlockHash(_l2BlockNumber - 1);
249:             require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");
250: 
251:             // Whenever we'll be queried about the hashes of the blocks before the upgrade,
252:             // we'll use batches' hashes, so we don't need to store 256 previous hashes.
253:             // However, we do need to store the last previous hash in order to be able to correctly calculate the
254:             // hash of the new L2 block.
255:             _setL2BlockHash(_l2BlockNumber - 1, correctPrevBlockHash);
256:         }
257:     }
258: 
259:     /// @notice Creates new virtual blocks, while ensuring they don't exceed the L2 block number.
260:     /// @param _l2BlockNumber The number of the new L2 block.
261:     /// @param _maxVirtualBlocksToCreate The maximum number of virtual blocks to create with this L2 block.
262:     /// @param _newTimestamp The timestamp of the new L2 block, which is also the timestamp of the new virtual block.
263:     function _setVirtualBlock(
264:         uint128 _l2BlockNumber,
265:         uint128 _maxVirtualBlocksToCreate,
266:         uint128 _newTimestamp
267:     ) internal {
268:         if (virtualBlockUpgradeInfo.virtualBlockFinishL2Block != 0) {
269:             // No need to to do anything about virtual blocks anymore
270:             // All the info is the same as for L2 blocks.
271:             currentVirtualL2BlockInfo = currentL2BlockInfo;
272:             return;
273:         }
274: 
275:         BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;
276: 
277:         if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
278:             uint128 currentBatchNumber = currentBatchInfo.number;
279: 
280:             // The virtual block is set for the first time. We can count it as 1 creation of a virtual block.
281:             // Note, that when setting the virtual block number we use the batch number to make a smoother upgrade from batch number to
282:             // the L2 block number.
283:             virtualBlockInfo.number = currentBatchNumber;
284:             // Remembering the batch number on which the upgrade to the virtual blocks has been done.
285:             virtualBlockUpgradeInfo.virtualBlockStartBatch = currentBatchNumber;
286: 
287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");
288:             _maxVirtualBlocksToCreate -= 1;
289:         } else if (_maxVirtualBlocksToCreate == 0) {
290:             // The virtual blocks have been already initialized, but the operator didn't ask to create
291:             // any new virtual blocks. So we can just return.
292:             return;
293:         }
294: 
295:         virtualBlockInfo.number += _maxVirtualBlocksToCreate;
296:         virtualBlockInfo.timestamp = _newTimestamp;
297: 
298:         // The virtual block number must never exceed the L2 block number.
299:         // We do not use a `require` here, since the virtual blocks are a temporary solution to let the Solidity's `block.number`
300:         // catch up with the L2 block number and so the situation where virtualBlockInfo.number starts getting larger
301:         // than _l2BlockNumber is expected once virtual blocks have caught up the L2 blocks.
302:         if (virtualBlockInfo.number >= _l2BlockNumber) {
303:             virtualBlockUpgradeInfo.virtualBlockFinishL2Block = _l2BlockNumber;
304:             virtualBlockInfo.number = _l2BlockNumber;
305:         }
306: 
307:         currentVirtualL2BlockInfo = virtualBlockInfo;
308:     }
309: 
310:     /// @notice Sets the current block number and timestamp of the L2 block.
311:     /// @param _l2BlockNumber The number of the new L2 block.
312:     /// @param _l2BlockTimestamp The timestamp of the new L2 block.
313:     /// @param _prevL2BlockHash The hash of the previous L2 block.
314:     function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal {
315:         // In the unsafe version we do not check that the block data is correct
316:         currentL2BlockInfo = BlockInfo({number: _l2BlockNumber, timestamp: _l2BlockTimestamp});
317: 
318:         // It is always assumed in production that _l2BlockNumber > 0
319:         _setL2BlockHash(_l2BlockNumber - 1, _prevL2BlockHash);
320: 
321:         // Reseting the rolling hash
322:         currentL2BlockTxsRollingHash = bytes32(0);
323:     }
324: 
325:     /// @notice Sets the current block number and timestamp of the L2 block.
326:     /// @dev Called by the bootloader before each transaction. This is needed to ensure
327:     /// that the data about the block is consistent with the sequencer.
328:     /// @dev If the new block number is the same as the current one, we ensure that the block's data is
329:     /// consistent with the one in the current block.
330:     /// @dev If the new block number is greater than the current one by 1,
331:     /// then we ensure that timestamp has increased.
332:     /// @dev If the currently stored number is 0, we assume that it is the first upgrade transaction
333:     /// and so we will fill up the old data.
334:     /// @param _l2BlockNumber The number of the new L2 block.
335:     /// @param _l2BlockTimestamp The timestamp of the new L2 block.
336:     /// @param _expectedPrevL2BlockHash The expected hash of the previous L2 block.
337:     /// @param _isFirstInBatch Whether this method is called for the first time in the batch.
338:     /// @param _maxVirtualBlocksToCreate The maximum number of virtual block to create with this L2 block.
339:     /// @dev It is a strict requirement that a new virtual block is created at the start of the batch.
340:     /// @dev It is also enforced that the number of the current virtual L2 block can not exceed the number of the L2 block.
341:     function setL2Block(
342:         uint128 _l2BlockNumber,
343:         uint128 _l2BlockTimestamp,
344:         bytes32 _expectedPrevL2BlockHash,
345:         bool _isFirstInBatch,
346:         uint128 _maxVirtualBlocksToCreate
347:     ) external onlyCallFromBootloader {
348:         // We check that the timestamp of the L2 block is consistent with the timestamp of the batch.
349:         if (_isFirstInBatch) {
350:             uint128 currentBatchTimestamp = currentBatchInfo.timestamp;
351:             require(
352:                 _l2BlockTimestamp >= currentBatchTimestamp,
353:                 "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
354:             );
355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");
356:         }
357: 
358:         (uint128 currentL2BlockNumber, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();
359: 
360:         if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {
361:             // Since currentL2BlockNumber and currentL2BlockTimestamp are zero it means that it is
362:             // the first ever batch with L2 blocks, so we need to initialize those.
363:             _upgradeL2Blocks(_l2BlockNumber, _expectedPrevL2BlockHash, _isFirstInBatch);
364: 
365:             _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);
366:         } else if (currentL2BlockNumber == _l2BlockNumber) {
367:             require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");
368:             require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");
369:             require(
370:                 _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
371:                 "The previous hash of the same L2 block must be same"
372:             );
373:             require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");
374:         } else if (currentL2BlockNumber + 1 == _l2BlockNumber) {
375:             // From the checks in _upgradeL2Blocks it is known that currentL2BlockNumber can not be 0
376:             bytes32 prevL2BlockHash = _getLatest257L2blockHash(currentL2BlockNumber - 1);
377: 
378:             bytes32 pendingL2BlockHash = _calculateL2BlockHash(
379:                 currentL2BlockNumber,
380:                 currentL2BlockTimestamp,
381:                 prevL2BlockHash,
382:                 currentL2BlockTxsRollingHash
383:             );
384: 
385:             require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");
386:             require(
387:                 _l2BlockTimestamp > currentL2BlockTimestamp,
388:                 "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
389:             );
390: 
391:             // Since the new block is created, we'll clear out the rolling hash
392:             _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);
393:         } else {
394:             revert("Invalid new L2 block number");
395:         }
396: 
397:         _setVirtualBlock(_l2BlockNumber, _maxVirtualBlocksToCreate, _l2BlockTimestamp);
398:     }
399: 
400:     /// @notice Appends the transaction hash to the rolling hash of the current L2 block.
401:     /// @param _txHash The hash of the transaction.
402:     function appendTransactionToCurrentL2Block(bytes32 _txHash) external onlyCallFromBootloader {
403:         currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));
404:     }
405: 
406:     /// @notice Publishes L2->L1 logs needed to verify the validity of this batch on L1.
407:     /// @dev Should be called at the end of the current batch.
408:     function publishTimestampDataToL1() external onlyCallFromBootloader {
409:         (uint128 currentBatchNumber, uint128 currentBatchTimestamp) = getBatchNumberAndTimestamp();
410:         (, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();
411: 
412:         // The structure of the "setNewBatch" implies that currentBatchNumber > 0, but we still double check it
413:         require(currentBatchNumber > 0, "The current batch number must be greater than 0");
414: 
415:         // In order to spend less pubdata, the packed version is published
416:         uint256 packedTimestamps = (uint256(currentBatchTimestamp) << 128) | currentL2BlockTimestamp;
417: 
418:         SystemContractHelper.toL1(
419:             false,
420:             bytes32(uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)),
421:             bytes32(packedTimestamps)
422:         );
423:     }
424: 
425:     /// @notice Ensures that the timestamp of the batch is greater than the timestamp of the last L2 block.
426:     /// @param _newTimestamp The timestamp of the new batch.
427:     function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {
428:         uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp;
429:         require(
430:             _newTimestamp > currentBlockTimestamp,
431:             "The timestamp of the batch must be greater than the timestamp of the previous block"
432:         );
433:     }
434: 
435:     /// @notice Increments the current batch number and sets the new timestamp
436:     /// @dev Called by the bootloader at the start of the batch.
437:     /// @param _prevBatchHash The hash of the previous batch.
438:     /// @param _newTimestamp The timestamp of the new batch.
439:     /// @param _expectedNewNumber The new batch's number.
440:     /// @param _baseFee The new batch's base fee
441:     /// @dev While _expectedNewNumber can be derived as prevBatchNumber + 1, we still
442:     /// manually supply it here for consistency checks.
443:     /// @dev The correctness of the _prevBatchHash and _newTimestamp should be enforced on L1.
444:     function setNewBatch(
445:         bytes32 _prevBatchHash,
446:         uint128 _newTimestamp,
447:         uint128 _expectedNewNumber,
448:         uint256 _baseFee
449:     ) external onlyCallFromBootloader {
450:         (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();
451:         require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");
452:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
453: 
454:         _ensureBatchConsistentWithL2Block(_newTimestamp);
455: 
456:         batchHashes[previousBatchNumber] = _prevBatchHash;
457: 
458:         // Setting new block number and timestamp
459:         BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp});
460: 
461:         currentBatchInfo = newBlockInfo;
462: 
463:         baseFee = _baseFee;
464: 
465:         // The correctness of this block hash:
466:         SystemContractHelper.toL1(false, bytes32(uint256(SystemLogKey.PREV_BATCH_HASH_KEY)), _prevBatchHash);
467:     }
468: 
469:     /// @notice A testing method that manually sets the current blocks' number and timestamp.
470:     /// @dev Should be used only for testing / ethCalls and should never be used in production.
471:     function unsafeOverrideBatch(
472:         uint256 _newTimestamp,
473:         uint256 _number,
474:         uint256 _baseFee
475:     ) external onlyCallFromBootloader {
476:         BlockInfo memory newBlockInfo = BlockInfo({number: uint128(_number), timestamp: uint128(_newTimestamp)});
477:         currentBatchInfo = newBlockInfo;
478: 
479:         baseFee = _baseFee;
480:     }
481: 
482:     function incrementTxNumberInBatch() external onlyCallFromBootloader {
483:         txNumberInBlock += 1;
484:     }
485: 
486:     function resetTxNumberInBatch() external onlyCallFromBootloader {
487:         txNumberInBlock = 0;
488:     }
489: 
490:     /*//////////////////////////////////////////////////////////////
491:                         DEPRECATED METHODS
492:     //////////////////////////////////////////////////////////////*/
493: 
494:     /// @notice Returns the current batch's number and timestamp.
495:     /// @dev Deprecated in favor of getBatchNumberAndTimestamp.
496:     function currentBlockInfo() external view returns (uint256 blockInfo) {
497:         (uint128 blockNumber, uint128 blockTimestamp) = getBatchNumberAndTimestamp();
498:         blockInfo = (uint256(blockNumber) << 128) | uint256(blockTimestamp);
499:     }
500: 
501:     /// @notice Returns the current batch's number and timestamp.
502:     /// @dev Deprecated in favor of getBatchNumberAndTimestamp.
503:     function getBlockNumberAndTimestamp() external view returns (uint256 blockNumber, uint256 blockTimestamp) {
504:         (blockNumber, blockTimestamp) = getBatchNumberAndTimestamp();
505:     }
506: 
507:     /// @notice Returns the hash of the given batch.
508:     /// @dev Deprecated in favor of getBatchHash.
509:     function blockHash(uint256 _blockNumber) external view returns (bytes32 hash) {
510:         hash = batchHashes[_blockNumber];
511:     }
512: }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L17-L512) 


</details>


### [GAS&#x2011;55] Use `do while` loops instead of `for` loops 
A `do while` loop will cost less gas since the condition is not being checked for the first iteration, Check my example on [github](https://github.com/he110-1/gasOptimization/blob/main/forToDoWhileOptimizationProof.sol). Actually, `do while` alwayse cast less gas compared to `For` check my second example [github](https://github.com/he110-1/gasOptimization/blob/main/forToDoWhileOptimizationProof2.sol)


*There are 35 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/Compressor.sol

61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {

127:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

159:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L61-L61) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L127-L127), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L159-L159)


```solidity

File: contracts/ContractDeployer.sol

248:         for (uint256 i = 0; i < deploymentsLength; ++i) {

253:         for (uint256 i = 0; i < deploymentsLength; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L248-L248) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L253-L253)


```solidity

File: contracts/ImmutableSimulator.sol

38:             for (uint256 i = 0; i < immutablesLength; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L38-L38) 


```solidity

File: contracts/KnownCodesStorage.sol

30:             for (uint256 i = 0; i < hashesLen; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L30-L30) 


```solidity

File: contracts/L1Messenger.sol

206:         for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

218:         for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

224:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

236:         for (uint256 i = 0; i < numberOfMessages; ++i) {

254:         for (uint256 i = 0; i < numberOfBytecodes; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L206-L206) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L218-L218), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L224-L224), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L236-L236), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L254-L254)


```solidity

File: contracts/PubdataChunkPublisher.sol

36:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L36-L36) 


```solidity

File: contracts/governance/Governance.sol

225:         for (uint256 i = 0; i < _calls.length; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L225-L225) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

116:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

135:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

185:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

209:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L116-L116) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L135-L135), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L185-L185), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L209-L209)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

142:         for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

257:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

289:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

311:         for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {

351:         for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {

405:         for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {

580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

636:         for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {

667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L142-L142) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L257-L257), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L289-L289), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L311-L311), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L351-L351), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L405-L405), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L580-L580), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L636-L636), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L667-L667)


```solidity

File: contracts/state-transition/chain-deps/facets/Getters.sol

208:         for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L208-L208) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

356:         for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L356-L356) 


```solidity

File: contracts/state-transition/libraries/Diamond.sol

101:         for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {

138:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

158:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

178:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L101-L101) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L138-L138), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L158-L158), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L178-L178)


```solidity

File: contracts/state-transition/libraries/Merkle.sol

29:         for (uint256 i; i < pathLength; i = i.uncheckedInc()) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L29-L29) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L226-L226) 


</details>


### [GAS&#x2011;56] Use `+=` for `mapping`s 
Using `+=` for mappings saves **[40 gas](https://gist.github.com/IllIllI000/4fc5f83a9edc6ed16677258bf58f32a5)** due to not having to recalculate the mapping's value's hash


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/bridge/L1SharedBridge.sol

133:             chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L133-L133) 


</details>


### [GAS&#x2011;57] Avoid transferring amounts of zero in order to save gas 
Skipping the external call when nothing will be transferred, will save at least **100 gas**


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/bridge/L1ERC20Bridge.sol

162:         _token.safeTransferFrom(_from, address(sharedBridge), _amount);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L162-L162) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

175:         _token.safeTransferFrom(_from, address(this), _amount);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L175-L175) 


</details>


### [GAS&#x2011;58] When no `addresses` are used `abi.encodepacked()` Outperforms `abi.encode()` in Efficiency 
when dealing with non address type parameters `encodepacked()` function less gas than `encode()`. For more details check the following [comparison](https://github.com/ConnorBlockchain/Solidity-Encode-Gas-Comparison)


*There are 28 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/L1Messenger.sol

106:         chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

122:         chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

164:         chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

212:             reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));

226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])

243:             reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));

260:                 abi.encode(


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L106-L106) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L122-L122), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L164-L164), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L212-L212), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L226-L226), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L243-L243), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L260-L260)


```solidity

File: contracts/SystemContext.sol

159:             hash = keccak256(abi.encode(_block));

227:         return keccak256(abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash));

403:         currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L159-L159) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L227-L227), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L403-L403)


```solidity

File: contracts/libraries/TransactionHelper.sol

120:             abi.encode(

139:             abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L120-L120) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L139-L139)


```solidity

File: contracts/bridge/L1SharedBridge.sol

258:             bytes memory decimals = abi.encode(uint8(18));

259:             return abi.encode(name, symbol, decimals); // when depositing eth to a non-eth based chain it is an ERC20

265:         return abi.encode(data1, data2, data3);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L258-L258) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L259-L259), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L265-L265)


```solidity

File: contracts/governance/Governance.sol

205:         return keccak256(abi.encode(_operation));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L205-L205) 


```solidity

File: contracts/state-transition/StateTransitionManager.sol

100:         storedBatchZero = keccak256(abi.encode(batchZero));

102:         initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

138:         initialCutHash = keccak256(abi.encode(_diamondCut));

147:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

156:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L100-L100) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L102-L102), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L138-L138), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L147-L147), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L156-L156)


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

104:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L104-L104) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

313:             concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));

512:         return keccak256(abi.encode(passThroughDataHash, metadataHash, auxiliaryOutputHash));

588:         return keccak256(abi.encode(_storedBatchInfo));

680:         (bool success, bytes memory data) = s.blobVersionedHashRetriever.staticcall(abi.encode(_index));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L313-L313) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L512-L512), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L588-L588), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L680-L680)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

323:         bytes memory transactionEncoding = abi.encode(transaction);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L323-L323) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

192:         bytes memory encodedTransaction = abi.encode(_l2ProtocolUpgradeTx);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L192-L192) 


</details>


### [GAS&#x2011;59] A `modifier` used only once and not being inherited should be inlined to save gas 



*There are 7 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ContractDeployer.sol

28:     modifier onlySelf() {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L28-L28) 


```solidity

File: contracts/KnownCodesStorage.sol

19:     modifier onlyCompressor() {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L19-L19) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

74:     modifier onlyBridgehubOrEra(uint256 _chainId) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L74-L74) 


```solidity

File: contracts/governance/Governance.sol

64:     modifier onlySecurityCouncil() {

70:     modifier onlyOwnerOrSecurityCouncil() {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L64-L64) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L70-L70)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

63:     modifier onlyBridgehub() {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L63-L63) 


```solidity

File: contracts/bridge/L2StandardERC20.sol

134:     modifier onlyNextVersion(uint8 _version) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L134-L134) 


</details>


### [GAS&#x2011;60] Simple checks for zero `uint` can be done using assembly to save gas 



*There are 48 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/Compressor.sol

146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

162:             if (enumIndex == 0) {

177:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

229:             if (_operation == 0 || _operation == 3) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L146-L146) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L162-L162), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L177-L177), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L229-L229)


```solidity

File: contracts/ContractDeployer.sol

350:             require(value == 0, "The value must be zero if we do not call the constructor");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L350-L350) 


```solidity

File: contracts/KnownCodesStorage.sol

47:         if (getMarker(_bytecodeHash) == 0) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L47-L47) 


```solidity

File: contracts/SystemContext.sol

277:         if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {

277:         if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {

289:         } else if (_maxVirtualBlocksToCreate == 0) {

360:         if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {

360:         if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {

373:             require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L277-L277) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L277-L277), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L289-L289), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L360-L360), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L360-L360), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L373-L373)


```solidity

File: contracts/libraries/EfficientCall.sol

131:         if (_value == 0) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L131-L131) 


```solidity

File: contracts/libraries/RLPEncoder.sol

29:                 encoded[0] = (_val == 0) ? bytes1(uint8(128)) : bytes1(uint8(_val));


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L29-L29) 


```solidity

File: contracts/libraries/SystemContractsCaller.sol

98:         if (value == 0) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L98-L98) 


```solidity

File: contracts/libraries/TransactionHelper.sol

95:         return _addr == uint256(uint160(address(BASE_TOKEN_SYSTEM_CONTRACT))) || _addr == 0;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L95-L95) 


```solidity

File: contracts/libraries/Utils.sol

84:         require(_bytecode.length % 32 == 0, "po");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L84-L84) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

158:             require(msg.value == 0, "ShB m.v > 0 b d.it");

200:             require(_depositAmount == 0, "ShB wrong withdraw amount");

202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L158-L158) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L200-L200), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L202-L202)


```solidity

File: contracts/bridgehub/Bridgehub.sol

225:                 require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L225-L225) 


```solidity

File: contracts/common/ReentrancyGuard.sol

58:         require(lockSlotOldValue == 0, "1B");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/ReentrancyGuard.sol#L58-L58) 


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

23:         require(_bytecode.length % 32 == 0, "pq");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L23-L23) 


```solidity

File: contracts/governance/Governance.sol

107:         if (timestamp == 0) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L107-L107) 


```solidity

File: contracts/state-transition/chain-deps/DiamondProxy.sol

25:         require(msg.data.length >= 4 || msg.data.length == 0, "Ut");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondProxy.sol#L25-L25) 


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

90:         require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L90-L90) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

284:         require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");

291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);

633:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L284-L284) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L291-L291), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L633-L633)


```solidity

File: contracts/state-transition/libraries/Diamond.sol

194:         if (selectorsLength == 0) {

250:         if (lastSelectorPosition == 0) {

280:             require(_calldata.length == 0, "H"); // Non-empty calldata for zero address


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L194-L194) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L250-L250), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L280-L280)


```solidity

File: contracts/state-transition/libraries/Merkle.sol

30:             currentHash = (_index % 2 == 0)


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L30-L30) 


```solidity

File: contracts/state-transition/libraries/TransactionValidator.sol

50:         require(_transaction.paymaster == 0, "uc");

51:         require(_transaction.value == 0, "ud");

52:         require(_transaction.maxFeePerGas == 0, "uq");

53:         require(_transaction.maxPriorityFeePerGas == 0, "ux");

54:         require(_transaction.reserved[0] == 0, "ue");

56:         require(_transaction.reserved[2] == 0, "ug");

57:         require(_transaction.reserved[3] == 0, "uo");

58:         require(_transaction.signature.length == 0, "uh");

59:         require(_transaction.paymasterInput.length == 0, "ul1");

60:         require(_transaction.reservedDynamic.length == 0, "um");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L50-L50) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L51-L51), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L52-L52), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L53-L53), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L54-L54), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L56-L56), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L57-L57), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L58-L58), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L59-L59), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L60-L60)


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

186:         if (_l2ProtocolUpgradeTx.txType == 0) {

251:             s.l2SystemContractsUpgradeBatchNumber == 0,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L186-L186) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L251-L251)


```solidity

File: contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

35:             s.l2SystemContractsUpgradeBatchNumber == 0,


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L35-L35) 


```solidity

File: contracts/SystemContractsCaller.sol

59:         if (value == 0) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L59-L59) 


```solidity

File: contracts/bridge/L2SharedBridge.sol

92:         require(msg.value == 0, "Value should be 0 for ERC20 bridge");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L92-L92) 


</details>


### [GAS&#x2011;61] `++i`/`i++` should be `unchecked{++i}`/`unchecked{i++}` when it is not possible for them to overflow, as is the case when used in `for`- and `while`-loops 
The `unchecked` keyword is new in solidity version 0.8.0, so this only applies to that version or higher, which these instances are. This saves **30-40 gas [per loop](https://gist.github.com/hrkrshnn/ee8fabd532058307229d65dcd5836ddc#the-increment-in-for-loop-post-condition-can-be-made-unchecked)**


*There are 12 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ContractDeployer.sol

248:         for (uint256 i = 0; i < deploymentsLength; ++i) {

253:         for (uint256 i = 0; i < deploymentsLength; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L248-L248) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L253-L253)


```solidity

File: contracts/L1Messenger.sol

206:         for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

218:         for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

224:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

236:         for (uint256 i = 0; i < numberOfMessages; ++i) {

254:         for (uint256 i = 0; i < numberOfBytecodes; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L206-L206) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L218-L218), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L224-L224), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L236-L236), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L254-L254)


```solidity

File: contracts/PubdataChunkPublisher.sol

36:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L36-L36) 


```solidity

File: contracts/governance/Governance.sol

225:         for (uint256 i = 0; i < _calls.length; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L225-L225) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L580-L580) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L667-L667)


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L226-L226) 


</details>


### [GAS&#x2011;62] Do not cache constants to save gas 



*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/state-transition/libraries/Diamond.sol

88:         bytes32 position = DIAMOND_STORAGE_POSITION;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L88-L88) 


</details>


### [GAS&#x2011;63] Using `private` for constants saves gas 
If needed, the values can be read from the verified contract source code, or if there are multiple values there can be a single getter function that [returns a tuple](https://github.com/code-423n4/2022-08-frax/blob/90f55a9ce4e25bceed3a74290b854341d8de6afa/src/contracts/FraxlendPair.sol#L156-L178) of the values of all currently-public constants. Saves **3406-3606 gas** in deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it's used, and not adding another entry to the method ID table


*There are 10 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/bridge/L1ERC20Bridge.sol

23:     IL1SharedBridge public immutable override sharedBridge;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L23-L23) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

34:     address public immutable override l1WethAddress;

37:     IBridgehub public immutable override bridgehub;

40:     IL1ERC20Bridge public immutable override legacyBridge;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L34-L34) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L37-L37), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L40-L40)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

27:     address public immutable bridgehub;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L27-L27) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

26:     string public constant override getName = "ValidatorTimelock";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L26-L26) 


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

20:     string public constant override getName = "AdminFacet";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L20-L20) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

27:     string public constant override getName = "ExecutorFacet";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L27-L27) 


```solidity

File: contracts/state-transition/chain-deps/facets/Getters.sol

25:     string public constant override getName = "GettersFacet";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L25-L25) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

35:     string public constant override getName = "MailboxFacet";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L35-L35) 


</details>


### [GAS&#x2011;64] Initializer can be marked `payable` 
Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided.An Initializer can safely be marked as payable, since only the allowed user would be able to pass funds, and the project itself would not pass any funds.


*There are 9 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/bridge/L1ERC20Bridge.sol

60:     function initialize() external reentrancyGuardInitializer {}
61: 


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L60-L61) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

104:     function initialize(
105:         address _owner,
106:         uint256 _eraFirstPostUpgradeBatch
107:     ) external reentrancyGuardInitializer initializer {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L104-L107) 


```solidity

File: contracts/bridgehub/Bridgehub.sol

41:     function initialize(address _owner) external reentrancyGuardInitializer {
42:         _transferOwnership(_owner);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L41-L42) 


```solidity

File: contracts/state-transition/IStateTransitionManager.sol

65:     function initialize(StateTransitionManagerInitializeData calldata _initalizeData) external;
66: 
67:     function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external;
68: 
69:     function setValidatorTimelock(address _validatorTimelock) external;
70: 
71:     function getChainAdmin(uint256 _chainId) external view returns (address);
72: 
73:     /// @notice
74:     function createNewChain(
75:         uint256 _chainId,
76:         address _baseToken,
77:         address _sharedBridge,
78:         address _admin,
79:         bytes calldata _diamondCut
80:     ) external;
81: 
82:     function registerAlreadyDeployedStateTransition(uint256 _chainId, address _stateTransitionContract) external;
83: 
84:     function setNewVersionUpgrade(
85:         Diamond.DiamondCutData calldata _cutData,
86:         uint256 _oldProtocolVersion,
87:         uint256 _newProtocolVersion
88:     ) external;
89: 
90:     function setUpgradeDiamondCut(Diamond.DiamondCutData calldata _cutData, uint256 _oldProtocolVersion) external;
91: 
92:     function freezeChain(uint256 _chainId) external;
93: 
94:     function unfreezeChain(uint256 _chainId) external;
95: }
96: 


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/IStateTransitionManager.sol#L65-L96) 


```solidity

File: contracts/state-transition/StateTransitionManager.sol

79:     function initialize(
80:         StateTransitionManagerInitializeData calldata _initializeData
81:     ) external reentrancyGuardInitializer {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L79-L81) 


```solidity

File: contracts/state-transition/chain-deps/DiamondInit.sol

24:     function initialize(InitializeData calldata _initializeData) external reentrancyGuardInitializer returns (bytes32) {
25:         require(address(_initializeData.verifier) != address(0), "vt");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondInit.sol#L24-L25) 


```solidity

File: contracts/state-transition/chain-interfaces/IDiamondInit.sol

62:     function initialize(InitializeData calldata _initData) external returns (bytes32);
63: }
64: 


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IDiamondInit.sol#L62-L64) 


```solidity

File: contracts/bridge/L2SharedBridge.sol

49:     function initialize(
50:         address _l1Bridge,
51:         address _l1LegecyBridge,
52:         bytes32 _l2TokenProxyBytecodeHash,
53:         address _aliasedOwner
54:     ) external reinitializer(2) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L49-L54) 


```solidity

File: contracts/bridge/L2StandardERC20.sol

50:     function bridgeInitialize(address _l1Address, bytes memory _data) external initializer {
51:         require(_l1Address != address(0), "in6"); // Should be non-zero address


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L50-L51) 


</details>


### [GAS&#x2011;65] Avoid caching global special variables 
It's better not to cache the global special variables, because it's cheaper to use them directly (e.g. `msg.sender`).


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ContractDeployer.sol

329:         uint256 value = msg.value;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L329-L329) 


</details>


### [GAS&#x2011;66] Use `s.x = s.x + y` instead of `s.x += y` for memory structs 
Using the `s.x = s.x + y` instead of `s.x += y` for memory structs can save **100 gas**. The same applies to `-=`, `*=`, etc.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/SystemContext.sol

295:         virtualBlockInfo.number += _maxVirtualBlocksToCreate;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L295-L295) 


</details>


### [GAS&#x2011;67] Using `constant`s instead of `enum` can save gas 
`Enum` is expensive and it is [more efficient to use constants](https://www.codehawks.com/finding/clm84992q02j9w9ruebun36d9) instead. An illustrative example of this approach can be found in the [ReentrancyGuard.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/181d518609a9f006fcb97af63e6952e603cf100e/contracts/utils/ReentrancyGuard.sol#L34-L35).


*There are 15 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/Constants.sol

110: enum SystemLogKey {
111:     L2_TO_L1_LOGS_TREE_ROOT_KEY,
112:     TOTAL_L2_TO_L1_PUBDATA_KEY,
113:     STATE_DIFF_HASH_KEY,
114:     PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY,
115:     PREV_BATCH_HASH_KEY,
116:     CHAINED_PRIORITY_TXN_HASH_KEY,
117:     NUMBER_OF_LAYER_1_TXS_KEY,
118:     BLOB_ONE_HASH_KEY,
119:     BLOB_TWO_HASH_KEY,
120:     EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY
121: }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Constants.sol#L110-L121) 


```solidity

File: contracts/interfaces/IContractDeployer.sol

11:     enum AccountAbstractionVersion {
12:         None,
13:         Version1
14:     }

23:     enum AccountNonceOrdering {
24:         Sequential,
25:         Arbitrary
26:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IContractDeployer.sol#L11-L14) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IContractDeployer.sol#L23-L26)


```solidity

File: contracts/interfaces/IPaymaster.sol

07: enum ExecutionResult {
08:     Revert,
09:     Success
10: }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IPaymaster.sol#L7-L10) 


```solidity

File: contracts/libraries/SystemContractHelper.sol

24: enum Global {
25:     CalldataPtr,
26:     CallFlags,
27:     ExtraABIData1,
28:     ExtraABIData2,
29:     ReturndataPtr
30: }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L24-L30) 


```solidity

File: contracts/libraries/SystemContractsCaller.sol

56: enum CalldataForwardingMode {
57:     UseHeap,
58:     ForwardFatPointer,
59:     UseAuxHeap
60: }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L56-L60) 


```solidity

File: contracts/common/Messaging.sol

08: enum TxStatus {
09:     Failure,
10:     Success
11: }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/Messaging.sol#L8-L11) 


```solidity

File: contracts/governance/IGovernance.sol

14:     enum OperationState {
15:         Unset,
16:         Waiting,
17:         Ready,
18:         Done
19:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/IGovernance.sol#L14-L19) 


```solidity

File: contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

12: enum UpgradeState {
13:     None,
14:     Transparent,
15:     Shadow
16: }

39: enum PubdataPricingMode {
40:     Rollup,
41:     Validium
42: }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L12-L16) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L39-L42)


```solidity

File: contracts/state-transition/chain-interfaces/IExecutor.sol

08: enum SystemLogKey {
09:     L2_TO_L1_LOGS_TREE_ROOT_KEY,
10:     TOTAL_L2_TO_L1_PUBDATA_KEY,
11:     STATE_DIFF_HASH_KEY,
12:     PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY,
13:     PREV_BATCH_HASH_KEY,
14:     CHAINED_PRIORITY_TXN_HASH_KEY,
15:     NUMBER_OF_LAYER_1_TXS_KEY,
16:     BLOB_ONE_HASH_KEY,
17:     BLOB_TWO_HASH_KEY,
18:     EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY
19: }

22: enum PubdataSource {
23:     Calldata,
24:     Blob
25: }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IExecutor.sol#L8-L19) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IExecutor.sol#L22-L25)


```solidity

File: contracts/state-transition/libraries/Diamond.sol

80:     enum Action {
81:         Add,
82:         Replace,
83:         Remove
84:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L80-L84) 


```solidity

File: contracts/SystemContractsCaller.sol

20: enum CalldataForwardingMode {
21:     UseHeap,
22:     ForwardFatPointer,
23:     UseAuxHeap
24: }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L20-L24) 


```solidity

File: contracts/interfaces/IPaymaster.sol

07: enum ExecutionResult {
08:     Revert,
09:     Success
10: }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/interfaces/IPaymaster.sol#L7-L10) 


</details>


### [GAS&#x2011;68] Gas savings can be achieved by changing the model for assigning value to the structure ***123 gas*** 
Change this `structName a = structName({item1: val1,item2: val2}); ==> structName a; a.item1 = val1; a.item2 = val2;`


*There are 17 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/L1Messenger.sol

75:         L2ToL1Log memory l2ToL1Log = L2ToL1Log({
76:             l2ShardId: 0,
77:             isService: _isService,
78:             txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),
79:             sender: msg.sender,
80:             key: _key,
81:             value: _value
82:         });

125:         L2ToL1Log memory l2ToL1Log = L2ToL1Log({
126:             l2ShardId: 0,
127:             isService: true,
128:             txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),
129:             sender: address(this),
130:             key: bytes32(uint256(uint160(msg.sender))),
131:             value: hash
132:         });


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L75-L82) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L125-L132)


```solidity

File: contracts/SystemContext.sol

316:         currentL2BlockInfo = BlockInfo({number: _l2BlockNumber, timestamp: _l2BlockTimestamp});

459:         BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp});

476:         BlockInfo memory newBlockInfo = BlockInfo({number: uint128(_number), timestamp: uint128(_newTimestamp)});


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L316-L316) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L459-L459), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L476-L476)


```solidity

File: contracts/bridge/L1SharedBridge.sol

219:             request = L2TransactionRequestTwoBridgesInner({
220:                 magicValue: TWO_BRIDGES_MAGIC_VALUE,
221:                 l2Contract: l2BridgeAddress[_chainId],
222:                 l2Calldata: l2TxCalldata,
223:                 factoryDeps: new bytes[](0),
224:                 txDataHash: txDataHash
225:             });

430:         MessageParams memory messageParams = MessageParams({
431:             l2BatchNumber: _l2BatchNumber,
432:             l2MessageIndex: _l2MessageIndex,
433:             l2TxNumberInBatch: _l2TxNumberInBatch
434:         });

470:             l2ToL1Message = L2Message({
471:                 txNumberInBatch: _messageParams.l2TxNumberInBatch,
472:                 sender: l2Sender,
473:                 data: _message
474:             });

584:             L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
585:                 chainId: ERA_CHAIN_ID,
586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
587:                 mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
588:                 l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
589:                 l2Calldata: l2TxCalldata,
590:                 l2GasLimit: _l2TxGasLimit,
591:                 l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
592:                 factoryDeps: new bytes[](0),
593:                 refundRecipient: refundRecipient
594:             });


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L219-L225) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L430-L434), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L470-L474), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L584-L594)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

90:         IExecutor.StoredBatchInfo memory batchZero = IExecutor.StoredBatchInfo(
91:             0,
92:             _initializeData.genesisBatchHash,
93:             _initializeData.genesisIndexRepeatedStorageChanges,
94:             0,
95:             EMPTY_STRING_KECCAK,
96:             DEFAULT_L2_LOGS_TREE_ROOT_HASH,
97:             0,
98:             _initializeData.genesisBatchCommitment
99:         );

182:         L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
183:             txType: SYSTEM_UPGRADE_L2_TX_TYPE,
184:             from: uint256(uint160(L2_FORCE_DEPLOYER_ADDR)),
185:             to: uint256(uint160(L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR)),
186:             gasLimit: 1,//$(PRIORITY_TX_MAX_GAS_LIMIT),
187:             gasPerPubdataByteLimit: REQUIRED_L2_GAS_PRICE_PER_PUBDATA,
188:             maxFeePerGas: uint256(0),
189:             maxPriorityFeePerGas: uint256(0),
190:             paymaster: uint256(0),
191:             // Note, that the priority operation id is used as "nonce" for L1->L2 transactions
192:             nonce: protocolVersion,
193:             value: 0,
194:             reserved: [uint256(0), 0, 0, 0],
195:             data: systemContextCalldata,
196:             signature: new bytes(0),
197:             factoryDeps: uintEmptyArray,
198:             paymasterInput: new bytes(0),
199:             reservedDynamic: new bytes(0)
200:         });

202:         ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
203:             l2ProtocolUpgradeTx: l2ProtocolUpgradeTx,
204:             factoryDeps: bytesEmptyArray,
205:             bootloaderHash: bytes32(0),
206:             defaultAccountHash: bytes32(0),
207:             verifier: address(0),
208:             verifierParams: VerifierParams({
209:                 recursionNodeLevelVkHash: bytes32(0),
210:                 recursionLeafLevelVkHash: bytes32(0),
211:                 recursionCircuitsSetVksHash: bytes32(0)
212:             }),
213:             l1ContractsUpgradeCalldata: new bytes(0),
214:             postUpgradeCalldata: new bytes(0),
215:             upgradeTimestamp: 0,
216:             newProtocolVersion: protocolVersion
217:         });

220:         Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({
221:             facetCuts: emptyArray,
222:             initAddress: genesisUpgrade,
223:             initCalldata: abi.encodeCall(IDefaultUpgrade.upgrade, (proposedUpgrade))
224:         });


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L90-L99) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L182-L200), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L202-L217), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L220-L224)


```solidity

File: contracts/state-transition/chain-deps/facets/Getters.sol

212:             result[i] = Facet(facetAddr, facetToSelectors.selectors);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L212-L212) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

92:         L2Log memory l2Log = L2Log({
93:             l2ShardId: 0,
94:             isService: true,
95:             txNumberInBatch: _l2TxNumberInBatch,
96:             sender: L2_BOOTLOADER_ADDRESS,
97:             key: _l2TxHash,
98:             value: bytes32(uint256(_status))
99:         });

294:         transaction = L2CanonicalTransaction({
295:             txType: PRIORITY_OPERATION_L2_TX_TYPE,
296:             from: uint256(uint160(_priorityOpParams.sender)),
297:             to: uint256(uint160(_priorityOpParams.contractAddressL2)),
298:             gasLimit: _priorityOpParams.l2GasLimit,
299:             gasPerPubdataByteLimit: _priorityOpParams.l2GasPricePerPubdata,
300:             maxFeePerGas: uint256(_priorityOpParams.l2GasPrice),
301:             maxPriorityFeePerGas: uint256(0),
302:             paymaster: uint256(0),
303:             // Note, that the priority operation id is used as "nonce" for L1->L2 transactions
304:             nonce: uint256(_priorityOpParams.txId),
305:             value: _priorityOpParams.l2Value,
306:             reserved: [_priorityOpParams.valueToMint, uint256(uint160(_priorityOpParams.refundRecipient)), 0, 0],
307:             data: _calldata,
308:             signature: new bytes(0),
309:             factoryDeps: _hashFactoryDeps(_factoryDeps),
310:             paymasterInput: new bytes(0),
311:             reservedDynamic: new bytes(0)
312:         });


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L92-L99) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L294-L312)


```solidity

File: contracts/state-transition/libraries/Diamond.sol

218:         ds.selectorToFacet[_selector] = SelectorToFacet({
219:             facetAddress: _facet,
220:             selectorPosition: selectorPosition,
221:             isFreezable: _isSelectorFreezable
222:         });


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L218-L222) 


</details>


### [GAS&#x2011;69] Refactor modifiers to call a local function 
Modifiers code is copied in all instances where it's used, increasing bytecode size. By doing a refractor to the internal function, one can reduce bytecode size significantly at the cost of one JUMP.


*There are 14 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/interfaces/ISystemContract.sol

20:     modifier onlySystemCall() {
21:         require(
22:             SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
23:             "This method require system call flag"
24:         );
25:         _;
26:     }

30:     modifier onlyCallFromSystemContract() {
31:         require(
32:             SystemContractHelper.isSystemContract(msg.sender),
33:             "This method require the caller to be system contract"
34:         );
35:         _;
36:     }

40:     modifier onlyCallFrom(address caller) {
41:         require(msg.sender == caller, "Inappropriate caller");
42:         _;
43:     }

47:     modifier onlyCallFromBootloader() {
48:         require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");
49:         _;
50:     }

54:     modifier onlyCallFromForceDeployer() {
55:         require(msg.sender == FORCE_DEPLOYER);
56:         _;
57:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L20-L26) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L30-L36), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L40-L43), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L47-L50), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L54-L57)


```solidity

File: contracts/common/ReentrancyGuard.sol

41:     modifier reentrancyGuardInitializer() {
42:         _initializeReentrancyGuard();
43:         _;
44:     }

68:     modifier nonReentrant() {
69:         uint256 _status;
70:         assembly {
71:             _status := sload(LOCK_FLAG_ADDRESS)
72:         }
73: 
74:         // On the first call to nonReentrant, _notEntered will be true
75:         require(_status == _NOT_ENTERED, "r1");
76: 
77:         // Any calls to nonReentrant after this point will fail
78:         assembly {
79:             sstore(LOCK_FLAG_ADDRESS, _ENTERED)
80:         }
81: 
82:         _;
83: 
84:         // By storing the original value once again, a refund is triggered (see
85:         // https://eips.ethereum.org/EIPS/eip-2200)
86:         assembly {
87:             sstore(LOCK_FLAG_ADDRESS, _NOT_ENTERED)
88:         }
89:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/ReentrancyGuard.sol#L41-L44) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/ReentrancyGuard.sol#L68-L89)


```solidity

File: contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

15:     modifier onlyAdmin() {
16:         require(msg.sender == s.admin, "StateTransition Chain: not admin");
17:         _;
18:     }

21:     modifier onlyValidator() {
22:         require(s.validators[msg.sender], "StateTransition Chain: not validator");
23:         _;
24:     }

26:     modifier onlyStateTransitionManager() {
27:         require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");
28:         _;
29:     }

31:     modifier onlyBridgehub() {
32:         require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");
33:         _;
34:     }

36:     modifier onlyAdminOrStateTransitionManager() {
37:         require(
38:             msg.sender == s.admin || msg.sender == s.stateTransitionManager,
39:             "StateTransition Chain: Only by admin or state transition manager"
40:         );
41:         _;
42:     }

44:     modifier onlyValidatorOrStateTransitionManager() {
45:         require(
46:             s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
47:             "StateTransition Chain: Only by validator or state transition manager"
48:         );
49:         _;
50:     }

52:     modifier onlyBaseTokenBridge() {
53:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
54:         _;
55:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L15-L18) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L21-L24), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L26-L29), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L31-L34), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L36-L42), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L44-L50), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L52-L55)


</details>


### [GAS&#x2011;70] Use `solady` library where possible to save gas 
[Solady](https://github.com/Vectorized/solady) is a Solidity library inspired by [Solmate](https://github.com/rari-capital/solmate), optimized heavily for gas optimizations and battle tested by [hundreds of developers](https://www.alchemy.com/dapps/solady). Consider implementing solady contracts where possible to reduce runtime gas fees.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/state-transition/ValidatorTimelock.sol

6: import {LibMap} from "./libraries/LibMap.sol";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L6-L6) 


</details>


### [GAS&#x2011;71] Consider using OZ EnumerateSet in place of nested mappings 
Nested mappings and multi-dimensional arrays in Solidity operate through a process of double hashing, wherein the original storage slot and the first key are concatenated and hashed, and then this hash is again concatenated with the second key and hashed. This process can be quite gas expensive due to the double-hashing operation and subsequent storage operation (sstore).\n\nA possible optimization involves manually concatenating the keys followed by a single hash operation and an sstore.However, this technique introduces the risk of storage collision, especially when there are other nested hash maps in the contract that use the same key types.Because Solidity is unaware of the number and structure of nested hash maps in a contract, it follows a conservative approach in computing the storage slot to avoid possible collisions.\n\nOpenZeppelin's EnumerableSet provides a potential solution to this problem. It creates a data structure that combines the benefits of set operations with the ability to enumerate stored elements, which is not natively available in Solidity. EnumerableSet handles the element uniqueness internally and can therefore provide a more gas-efficient and collision-resistant alternative to nested mappings or multi-dimensional arrays in certain scenarios.


*There are 9 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ImmutableSimulator.sol

21:     mapping(uint256 contractAddress => mapping(uint256 index => bytes32 value)) internal immutableDataStorage;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L21-L21) 


```solidity

File: contracts/NonceHolder.sol

41:     mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L41-L41) 


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

27:     mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
28:         public isWithdrawalFinalized;

32:     mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
33:         public depositAmount;

51:     mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L27-L28) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L32-L33), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L51-L51)


```solidity

File: contracts/bridge/L1SharedBridge.sol

52:     mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
53:         public
54:         override depositHappened;

57:     mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
58:         public isWithdrawalFinalized;

65:     mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L52-L54) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L57-L58), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L65-L65)


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

50:     mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L50-L50) 


</details>


### [GAS&#x2011;72] Consider using solady's 'FixedPointMathLib' 
Using Solady's 'FixedPointMathLib' for multiplication or division operations in Solidity can lead to significant gas savings. This library is designed to optimize fixed-point arithmetic operations, which are common in financial calculations involving tokens or currencies. By implementing more efficient algorithms and assembly optimizations, 'FixedPointMathLib' minimizes the computational resources required for these operations. For contracts that frequently perform such calculations, integrating this library can reduce transaction costs, thereby enhancing overall performance and cost-effectiveness. However, developers must ensure compatibility with their existing codebase and thoroughly test for accuracy and expected behavior to avoid any unintended consequences.


*There are 69 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/BootloaderUtilities.sol

//@audit for: `*`
97:                 vInt += 8 + block.chainid * 2;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L97-L97) 


```solidity

File: contracts/Compressor.sol

//@audit for: `*`
52:                 encodedData.length * 4 == _bytecode.length,

//@audit for: `/`
57:                 dictionary.length / 8 <= encodedData.length / 2,

//@audit for: `/`
57:                 dictionary.length / 8 <= encodedData.length / 2,

//@audit for: `*`
62:                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;

//@audit for: `*`
66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

//@audit for: `*`
127:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

//@audit for: `*`
159:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

//@audit for: `*`
203:             dictionary = _rawCompressedData[2:2 + dictionaryLen * 8];

//@audit for: `*`
204:             encodedData = _rawCompressedData[2 + dictionaryLen * 8:];

//@audit for: `*`
253:         number >>= (256 - (_calldataSlice.length * 8));


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L52-L52) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L57-L57), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L57-L57), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L62-L62), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L66-L66), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L127-L127), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L159-L159), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L203-L203), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L204-L204), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L253-L253)


```solidity

File: contracts/L1Messenger.sol

//@audit for: `*`
51:         return KECCAK_ROUND_GAS_COST * (_length / KECCAK_ROUND_NUMBER_OF_BYTES + 1);

//@audit for: `/`
51:         return KECCAK_ROUND_GAS_COST * (_length / KECCAK_ROUND_NUMBER_OF_BYTES + 1);

//@audit for: `*`
62:         return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1);

//@audit for: `/`
62:         return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1);

//@audit for: `*`
89:         uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) + 2 * keccakGasCost(64);

//@audit for: `*`
149:             3 *
150:             keccakGasCost(64) +

//@audit for: `*`
152:             COMPUTATIONAL_PRICE_FOR_PUBDATA *
153:             pubdataLen;

//@audit for: `*`
177:             COMPUTATIONAL_PRICE_FOR_PUBDATA *
178:             pubdataLen;

//@audit for: `*`
226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])

//@audit for: `*`
226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])

//@audit for: `*`
304:             (numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE)];

//@audit for: `*`
305:         calldataPtr += numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L51-L51) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L51-L51), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L62-L62), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L62-L62), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L89-L89), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L149-L150), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L152-L153), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L177-L178), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L226-L226), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L226-L226), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L304-L304), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L305-L305)


```solidity

File: contracts/NonceHolder.sol

//@audit for: `/`
180:         deploymentNonce = _rawMinNonce / DEPLOY_NONCE_MULTIPLIER;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L180-L180) 


```solidity

File: contracts/PubdataChunkPublisher.sol

//@audit for: `*`
22:         require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");

//@audit for: `*`
28:         bytes memory totalBlobs = new bytes(BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS);

//@audit for: `*`
37:             uint256 start = BLOB_SIZE_BYTES * i;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L22-L22) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L28-L28), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L37-L37)


```solidity

File: contracts/SystemContext.sol

//@audit for: `*`
123:         return gasPerPubdataByte * getCurrentPubdataSpent();


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L123-L123) 


```solidity

File: contracts/libraries/RLPEncoder.sol

//@audit for: `*`
37:                 uint256 shiftedVal = _val << (lbs * 8);

//@audit for: `*`
72:                 uint256 shiftedVal = uint256(_len) << (lbs * 8);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L37-L37) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L72-L72)


```solidity

File: contracts/libraries/SystemContractsCaller.sol

//@audit for: `*`
41: uint256 constant META_GAS_PER_PUBDATA_BYTE_OFFSET = 0 * 8;

//@audit for: `*`
42: uint256 constant META_HEAP_SIZE_OFFSET = 8 * 8;

//@audit for: `*`
43: uint256 constant META_AUX_HEAP_SIZE_OFFSET = 12 * 8;

//@audit for: `*`
44: uint256 constant META_SHARD_ID_OFFSET = 28 * 8;

//@audit for: `*`
45: uint256 constant META_CALLER_SHARD_ID_OFFSET = 29 * 8;

//@audit for: `*`
46: uint256 constant META_CODE_SHARD_ID_OFFSET = 30 * 8;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L41-L41) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L42-L42), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L43-L43), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L44-L44), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L45-L45), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L46-L46)


```solidity

File: contracts/libraries/TransactionHelper.sol

//@audit for: `*`
397:         uint256 amount = _transaction.maxFeePerGas * _transaction.gasLimit;

//@audit for: `*`
411:             requiredBalance = _transaction.maxFeePerGas * _transaction.gasLimit + _transaction.value;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L397-L397) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L411-L411)


```solidity

File: contracts/libraries/Utils.sol

//@audit for: `*`
46:             codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));

//@audit for: `/`
86:         uint256 lengthInWords = _bytecode.length / 32;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L46-L46) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L86-L86)


```solidity

File: contracts/common/Config.sol

//@audit for: `*`
14: uint256 constant MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES = 4 + L2_TO_L1_LOG_SERIALIZE_SIZE * 512;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/Config.sol#L14-L14) 


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

//@audit for: `/`
25:         uint256 bytecodeLenInWords = _bytecode.length / 32;

//@audit for: `*`
50:         codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L25-L25) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L50-L50)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

//@audit for: `*`
106:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L106-L106) 


```solidity

File: contracts/state-transition/chain-deps/DiamondInit.sol

//@audit for: `*`
51:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondInit.sol#L51-L51) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

//@audit for: `*`
578:         blobAuxOutputWords = new bytes32[](2 * TOTAL_BLOBS_IN_COMMITMENT);

//@audit for: `*`
581:             blobAuxOutputWords[i * 2] = _blobHashes[i];

//@audit for: `*`
582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];

//@audit for: `*`
632:         require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L578-L578) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L581-L581), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L582-L582), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L632-L632)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

//@audit for: `*`
149:         return l2GasPrice * _l2GasLimit;

//@audit for: `/`
159:         uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
160:             s.baseTokenGasPriceMultiplierDenominator;

//@audit for: `*`
159:         uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /

//@audit for: `*`
163:             pubdataPriceBaseToken = L1_GAS_PER_PUBDATA_BYTE * l1GasPriceConverted;

//@audit for: `*`
166:         uint256 batchOverheadBaseToken = uint256(feeParams.batchOverheadL1Gas) * l1GasPriceConverted;

//@audit for: `/`
168:             batchOverheadBaseToken /
169:             uint256(feeParams.maxPubdataPerBatch);

//@audit for: `/`
171:         uint256 l2GasPrice = feeParams.minimalL2GasPrice + batchOverheadBaseToken / uint256(feeParams.maxL2GasPerBatch);

//@audit for: `/`
172:         uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata;

//@audit for: `*`
271:         uint256 baseCost = _params.l2GasPrice * _params.l2GasLimit;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L149-L149) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L159-L160), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L159-L159), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L163-L163), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L166-L166), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L168-L169), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L171-L171), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L172-L172), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L271-L271)


```solidity

File: contracts/state-transition/libraries/LibMap.sol

//@audit for: `/`
23:             uint256 mapValue = _map.map[_index / 8];

//@audit for: `*`
27:             uint256 bitOffset = (_index & 7) * 32;

//@audit for: `/`
43:             uint256 mapIndex = _index / 8;

//@audit for: `*`
48:             uint256 bitOffset = (_index & 7) * 32;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L23-L23) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L27-L27), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L43-L43), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L48-L48)


```solidity

File: contracts/state-transition/libraries/TransactionValidator.sol

//@audit for: `/`
30:         require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");

//@audit for: `*`
83:             costForComputation += Math.ceilDiv(_encodingLength * L1_TX_DELTA_544_ENCODING_BYTES, 544);

//@audit for: `*`
86:             costForComputation += _numberOfFactoryDependencies * L1_TX_DELTA_FACTORY_DEPS_L2_GAS;

//@audit for: `*`
95:             costForPubdata = L1_TX_INTRINSIC_PUBDATA * _l2GasPricePerPubdata;

//@audit for: `*`
98:             costForPubdata += _numberOfFactoryDependencies * L1_TX_DELTA_FACTORY_DEPS_PUBDATA * _l2GasPricePerPubdata;

//@audit for: `*`
98:             costForPubdata += _numberOfFactoryDependencies * L1_TX_DELTA_FACTORY_DEPS_PUBDATA * _l2GasPricePerPubdata;

//@audit for: `*`
135:         uint256 overheadForLength = MEMORY_OVERHEAD_GAS * _encodingLength;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L30-L30) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L83-L83), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L86-L86), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L95-L95), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L98-L98), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L98-L98), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L135-L135)


</details>


### [GAS&#x2011;73] Counting down in for statements is more gas efficient 
Looping downwards in Solidity is more gas efficient due to how the EVM compares variables. In a 'for' loop that counts down, the end condition is usually to compare with zero, which is cheaper than comparing with another number. As such, restructure your loops to count downwards where possible.


*There are 18 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ContractDeployer.sol

248:         for (uint256 i = 0; i < deploymentsLength; ++i) {
249:             sumOfValues += _deployments[i].value;
250:         }

253:         for (uint256 i = 0; i < deploymentsLength; ++i) {
254:             this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
255:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L248-L250) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L253-L255)


```solidity

File: contracts/ImmutableSimulator.sol

38:             for (uint256 i = 0; i < immutablesLength; ++i) {
39:                 uint256 index = _immutables[i].index;
40:                 bytes32 value = _immutables[i].value;
41:                 immutableDataStorage[uint256(uint160(_dest))][index] = value;
42:             }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L38-L42) 


```solidity

File: contracts/KnownCodesStorage.sol

30:             for (uint256 i = 0; i < hashesLen; ++i) {
31:                 _markBytecodeAsPublished(_hashes[i], _shouldSendToL1);
32:             }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L30-L32) 


```solidity

File: contracts/L1Messenger.sol

206:         for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {
207:             bytes32 hashedLog = EfficientCall.keccak(
208:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + L2_TO_L1_LOG_SERIALIZE_SIZE]
209:             );
210:             calldataPtr += L2_TO_L1_LOG_SERIALIZE_SIZE;
211:             l2ToL1LogsTreeArray[i] = hashedLog;
212:             reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));
213:         }

218:         for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {
219:             l2ToL1LogsTreeArray[i] = L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH;
220:         }

224:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {
225:                 l2ToL1LogsTreeArray[i] = keccak256(
226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
227:                 );
228:             }

236:         for (uint256 i = 0; i < numberOfMessages; ++i) {
237:             uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
238:             calldataPtr += 4;
239:             bytes32 hashedMessage = EfficientCall.keccak(
240:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentMessageLength]
241:             );
242:             calldataPtr += currentMessageLength;
243:             reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));
244:         }

254:         for (uint256 i = 0; i < numberOfBytecodes; ++i) {
255:             uint32 currentBytecodeLength = uint32(
256:                 bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])
257:             );
258:             calldataPtr += 4;
259:             reconstructedChainedL1BytecodesRevealDataHash = keccak256(
260:                 abi.encode(
261:                     reconstructedChainedL1BytecodesRevealDataHash,
262:                     Utils.hashL2Bytecode(
263:                         _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
264:                     )
265:                 )
266:             );
267:             calldataPtr += currentBytecodeLength;
268:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L206-L213) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L218-L220), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L224-L228), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L236-L244), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L254-L268)


```solidity

File: contracts/PubdataChunkPublisher.sol

36:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
37:             uint256 start = BLOB_SIZE_BYTES * i;
38: 
39:             // We break if the pubdata isn't enough to cover 2 blobs. On L1 it is expected that the hash
40:             // will be bytes32(0) if a blob isn't going to be used.
41:             if (start >= _pubdata.length) {
42:                 break;
43:             }
44: 
45:             bytes32 blobHash;
46:             assembly {
47:                 // The pointer to the allocated memory above skipping the length.
48:                 let ptr := add(totalBlobs, 0x20)
49:                 blobHash := keccak256(add(ptr, start), BLOB_SIZE_BYTES)
50:             }
51: 
52:             blobHashes[i] = blobHash;
53:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L36-L53) 


```solidity

File: contracts/governance/Governance.sol

225:         for (uint256 i = 0; i < _calls.length; ++i) {
226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
227:             if (!success) {
228:                 // Propagate an error if the call fails.
229:                 assembly {
230:                     revert(add(returnData, 0x20), mload(returnData))
231:                 }
232:             }
233:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L225-L233) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

116:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
117:                 committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);
118:             }

135:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
136:                 committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);
137:             }

185:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
186:                 uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
187:                     _newBatchesData[i].batchNumber
188:                 );
189: 
190:                 // Note: if the `commitBatchTimestamp` is zero, that means either:
191:                 // * The batch was committed, but not through this contract.
192:                 // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
193:                 // We allow executing such batches.
194: 
195:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
196:             }

209:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
210:                 uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
211: 
212:                 // Note: if the `commitBatchTimestamp` is zero, that means either:
213:                 // * The batch was committed, but not through this contract.
214:                 // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
215:                 // We allow executing such batches.
216: 
217:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
218:             }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L116-L118) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L135-L137), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L185-L196), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L209-L218)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
581:             blobAuxOutputWords[i * 2] = _blobHashes[i];
582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
583:         }

667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
668:             require(
669:                 (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
671:                 "bh"
672:             );
673:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L580-L583) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L667-L673)


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {
227:             require(
228:                 L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
229:                 "Wrong factory dep hash"
230:             );
231:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L226-L231) 


</details>


### [GAS&#x2011;74] Trade-offs Between Modifiers and Internal Functions 
In Solidity, both modifiers and internal functions can be used to modularize and reuse code, but they have different trade-offs.\n\nModifiers are primarily used to augment the behavior of functions, often for checks or validations.They can access parameters of the function they modify and are integrated into the function’s code at compile time.This makes them syntactically cleaner for repetitive precondition checks.However, modifiers can sometimes lead to less readable code, especially when the logic is complex or when multiple modifiers are used on a single function.\n\nInternal functions, on the other hand, offer more flexibility.They can contain complex logic, return values, and be called from other functions.This makes them more suitable for reusable chunks of business logic.Since internal functions are separate entities, they can be more readable and easier to test in isolation compared to modifiers.\n\nUsing internal functions can result in slightly more gas consumption, as it involves an internal function call.However, this cost is usually minimal and can be a worthwhile trade- off for increased code clarity and maintainability.\n\nIn summary, while modifiers offer a concise way to include checks and simple logic across multiple functions, internal functions provide more flexibility and are better suited for complex and reusable code.The choice between the two should be based on the specific use case, considering factors like code complexity, readability, and gas efficiency.


*There are 196 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/AccountCodeStorage.sol

68:     function _storeCodeHash(address _address, bytes32 _hash) internal {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L68-L68) 


```solidity

File: contracts/BootloaderUtilities.sol

44:     function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {

139:     function encodeEIP2930TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {

229:     function encodeEIP1559TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L44-L44) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L139-L139), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L229-L229)


```solidity

File: contracts/Compressor.sol

197:     function _decodeRawBytecode(

220:     function _verifyValueCompression(

251:     function _sliceToUint256(bytes calldata _calldataSlice) internal pure returns (uint256 number) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L197-L197) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L220-L220), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L251-L251)


```solidity

File: contracts/ContractDeployer.sol

58:     function _storeAccountInfo(address _address, AccountInfo memory _newInfo) internal {

258:     function _nonSystemDeployOnAddress(

283:     function _performDeployOnAddress(

301:     function _ensureBytecodeIsKnown(bytes32 _bytecodeHash) internal view {

309:     function _storeConstructingByteCodeHashOnAddress(address _newAddress, bytes32 _bytecodeHash) internal {

321:     function _constructContract(


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L58-L58) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L258-L258), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L283-L283), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L301-L301), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L309-L309), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L321-L321)


```solidity

File: contracts/DefaultAccount.sol

78:     function _validateTransaction(

131:     function _execute(Transaction calldata _transaction) internal {

159:     function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L78-L78) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L131-L131), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L159-L159)


```solidity

File: contracts/KnownCodesStorage.sol

46:     function _markBytecodeAsPublished(bytes32 _bytecodeHash, bool _shouldSendToL1) internal {

74:     function _validateBytecode(bytes32 _bytecodeHash) internal pure {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L46-L46) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L74-L74)


```solidity

File: contracts/L1Messenger.sol

50:     function keccakGasCost(uint256 _length) internal pure returns (uint256) {

61:     function sha256GasCost(uint256 _length) internal pure returns (uint256) {

94:     function _processL2ToL1Log(L2ToL1Log memory _l2ToL1Log) internal returns (uint256 logIdInMerkleTree) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L50-L50) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L61-L61), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L94-L94)


```solidity

File: contracts/L2BaseToken.sol

99:     function _burnMsgValue() internal returns (uint256 amount) {

112:     function _getL1WithdrawMessage(address _to, uint256 _amount) internal pure returns (bytes memory) {

117:     function _getExtendedWithdrawMessage(


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L99-L99) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L112-L112), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L117-L117)


```solidity

File: contracts/MsgValueSimulator.sol

25:     function _getAbiParams() internal view returns (uint256 value, bool isSystemCall, address to) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/MsgValueSimulator.sol#L25-L25) 


```solidity

File: contracts/NonceHolder.sol

179:     function _splitRawNonce(uint256 _rawMinNonce) internal pure returns (uint256 deploymentNonce, uint256 minNonce) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L179-L179) 


```solidity

File: contracts/SystemContext.sol

205:     function _getLatest257L2blockHash(uint256 _block) internal view returns (bytes32) {

212:     function _setL2BlockHash(uint256 _block, bytes32 _hash) internal {

221:     function _calculateL2BlockHash(

233:     function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {

241:     function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {

263:     function _setVirtualBlock(

314:     function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal {

427:     function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L205-L205) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L212-L212), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L221-L221), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L233-L233), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L241-L241), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L263-L263), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L314-L314), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L427-L427)


```solidity

File: contracts/libraries/EfficientCall.sol

36:     function keccak(bytes calldata _data) internal view returns (bytes32) {

45:     function sha(bytes calldata _data) internal view returns (bytes32) {

58:     function call(

74:     function staticCall(

88:     function delegateCall(

105:     function mimicCall(

124:     function rawCall(

159:     function rawStaticCall(uint256 _gas, address _address, bytes calldata _data) internal view returns (bool success) {

173:     function rawDelegateCall(uint256 _gas, address _address, bytes calldata _data) internal returns (bool success) {

191:     function rawMimicCall(

232:     function propagateRevert() internal pure {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L36-L36) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L45-L45), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L58-L58), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L74-L74), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L88-L88), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L105-L105), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L124-L124), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L159-L159), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L173-L173), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L191-L191), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L232-L232)


```solidity

File: contracts/libraries/RLPEncoder.sol

11:     function encodeAddress(address _val) internal pure returns (bytes memory encoded) {

24:     function encodeUint256(uint256 _val) internal pure returns (bytes memory encoded) {

49:     function encodeNonSingleBytesLen(uint64 _len) internal pure returns (bytes memory) {

56:     function encodeListLen(uint64 _len) internal pure returns (bytes memory) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L11-L11) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L24-L24), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L49-L49), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L56-L56)


```solidity

File: contracts/libraries/SystemContractHelper.sol

48:     function toL1(bool _isService, bytes32 _key, bytes32 _value) internal {

63:     function getCodeAddress() internal view returns (address addr) {

74:     function loadCalldataIntoActivePtr() internal view {

85:     function ptrPackIntoActivePtr(uint256 _farCallAbi) internal view {

94:     function ptrAddIntoActive(uint32 _value) internal view {

106:     function ptrShrinkIntoActive(uint32 _shrink) internal view {

124:     function packPrecompileParams(

148:     function unsafePrecompileCall(

168:     function setValueForNextFarCall(uint128 _value) internal returns (bool success) {

181:     function eventInitialize(uint256 initializer, uint256 value1) internal {

191:     function eventWrite(uint256 value1, uint256 value2) internal {

203:     function getZkSyncMetaBytes() internal view returns (uint256 meta) {

215:     function extractNumberFromMeta(uint256 meta, uint256 offset, uint256 size) internal pure returns (uint256 result) {

227:     function getPubdataPublishedFromMeta(uint256 meta) internal pure returns (uint32 pubdataPublished) {

237:     function getHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 heapSize) {

246:     function getAuxHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 auxHeapSize) {

254:     function getShardIdFromMeta(uint256 meta) internal pure returns (uint8 shardId) {

263:     function getCallerShardIdFromMeta(uint256 meta) internal pure returns (uint8 callerShardId) {

272:     function getCodeShardIdFromMeta(uint256 meta) internal pure returns (uint8 codeShardId) {

279:     function getZkSyncMeta() internal view returns (ZkSyncMeta memory meta) {

296:     function getCallFlags() internal view returns (uint256 callFlags) {

307:     function getCalldataPtr() internal view returns (uint256 ptr) {

318:     function getExtraAbiData(uint256 index) internal view returns (uint256 extraAbiData) {

329:     function isSystemCall() internal view returns (bool) {

338:     function isSystemContract(address _address) internal pure returns (bool) {

344:     function burnGas(uint32 _gasToPay, uint32 _pubdataToSpend) internal view {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L48-L48) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L63-L63), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L74-L74), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L85-L85), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L94-L94), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L106-L106), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L124-L124), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L148-L148), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L168-L168), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L181-L181), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L191-L191), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L203-L203), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L215-L215), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L227-L227), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L237-L237), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L246-L246), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L254-L254), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L263-L263), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L272-L272), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L279-L279), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L296-L296), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L307-L307), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L318-L318), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L329-L329), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L338-L338), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L344-L344)


```solidity

File: contracts/libraries/SystemContractsCaller.sol

76:     function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

123:     function systemCallWithReturndata(

150:     function systemCallWithPropagatedRevert(

214:     function getFarCallABI(

250:     function getFarCallABIWithEmptyFatPointer(


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L76-L76) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L123-L123), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L150-L150), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L214-L214), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L250-L250)


```solidity

File: contracts/libraries/TransactionHelper.sol

94:     function isEthToken(uint256 _addr) internal pure returns (bool) {

100:     function encodeHash(Transaction calldata _transaction) internal view returns (bytes32 resultHash) {

362:     function processPaymasterInput(Transaction calldata _transaction) internal {

395:     function payToTheBootloader(Transaction calldata _transaction) internal returns (bool success) {

405:     function totalRequiredBalance(Transaction calldata _transaction) internal pure returns (uint256 requiredBalance) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L94-L94) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L100-L100), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L362-L362), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L395-L395), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L405-L405)


```solidity

File: contracts/libraries/UnsafeBytesCalldata.sol

19:     function readUint16(bytes calldata _bytes, uint256 _start) internal pure returns (uint16 result) {

26:     function readUint32(bytes calldata _bytes, uint256 _start) internal pure returns (uint32 result) {

33:     function readUint64(bytes calldata _bytes, uint256 _start) internal pure returns (uint64 result) {

40:     function readBytes32(bytes calldata _bytes, uint256 _start) internal pure returns (bytes32 result) {

46:     function readUint256(bytes calldata _bytes, uint256 _start) internal pure returns (uint256 result) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L19-L19) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L26-L26), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L33-L33), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L40-L40), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L46-L46)


```solidity

File: contracts/libraries/Utils.sol

20:     function safeCastToU128(uint256 _x) internal pure returns (uint128) {

26:     function safeCastToU32(uint256 _x) internal pure returns (uint32) {

32:     function safeCastToU24(uint256 _x) internal pure returns (uint24) {

39:     function bytecodeLenInBytes(bytes32 _bytecodeHash) internal pure returns (uint256 codeLength) {

44:     function bytecodeLenInWords(bytes32 _bytecodeHash) internal pure returns (uint256 codeLengthInWords) {

51:     function isContractConstructed(bytes32 _bytecodeHash) internal pure returns (bool) {

56:     function isContractConstructing(bytes32 _bytecodeHash) internal pure returns (bool) {

63:     function constructingBytecodeHash(bytes32 _bytecodeHash) internal pure returns (bytes32) {

71:     function constructedBytecodeHash(bytes32 _bytecodeHash) internal pure returns (bytes32) {

82:     function hashL2Bytecode(bytes calldata _bytecode) internal view returns (bytes32 hashedBytecode) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L20-L20) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L26-L26), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L32-L32), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L39-L39), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L44-L44), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L51-L51), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L56-L56), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L63-L63), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L71-L71), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L82-L82)


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

160:     function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L160-L160) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

173:     function _depositFunds(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {

243:     function _getDepositL2Calldata(

254:     function _getERC20Getters(address _token) internal view returns (bytes memory) {

303:     function _claimFailedDeposit(

374:     function _isEraLegacyWithdrawal(uint256 _chainId, uint256 _l2BatchNumber) internal view returns (bool) {

409:     function _finalizeWithdrawal(

458:     function _checkWithdrawal(

487:     function _parseL2WithdrawalMessage(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L173-L173) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L243-L243), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L254-L254), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L303-L303), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L374-L374), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L409-L409), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L458-L458), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L487-L487)


```solidity

File: contracts/bridgehub/Bridgehub.sol

325:     function _actualRefundRecipient(address _refundRecipient) internal view returns (address _recipient) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L325-L325) 


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

21:     function hashL2Bytecode(bytes memory _bytecode) internal pure returns (bytes32 hashedBytecode) {

39:     function validateBytecodeHash(bytes32 _bytecodeHash) internal pure {

49:     function bytecodeLen(bytes32 _bytecodeHash) internal pure returns (uint256 codeLengthInWords) {

60:     function computeCreate2Address(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L21-L21) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L39-L39), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L49-L49), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L60-L60)


```solidity

File: contracts/common/libraries/UncheckedMath.sol

11:     function uncheckedInc(uint256 _number) internal pure returns (uint256) {

17:     function uncheckedAdd(uint256 _lhs, uint256 _rhs) internal pure returns (uint256) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UncheckedMath.sol#L11-L11) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UncheckedMath.sol#L17-L17)


```solidity

File: contracts/common/libraries/UnsafeBytes.sol

19:     function readUint32(bytes memory _bytes, uint256 _start) internal pure returns (uint32 result, uint256 offset) {

26:     function readAddress(bytes memory _bytes, uint256 _start) internal pure returns (address result, uint256 offset) {

33:     function readUint256(bytes memory _bytes, uint256 _start) internal pure returns (uint256 result, uint256 offset) {

40:     function readBytes32(bytes memory _bytes, uint256 _start) internal pure returns (bytes32 result, uint256 offset) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UnsafeBytes.sol#L19-L19) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UnsafeBytes.sol#L26-L26), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UnsafeBytes.sol#L33-L33), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UnsafeBytes.sol#L40-L40)


```solidity

File: contracts/governance/Governance.sol

215:     function _schedule(bytes32 _id, uint256 _delay) internal {

224:     function _execute(Call[] calldata _calls) internal {

239:     function _checkPredecessorDone(bytes32 _predecessorId) internal view {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L215-L215) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L224-L224), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L239-L239)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

177:     function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L177-L177) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

225:     function _propagateToZkSyncStateTransition(uint256 _chainId) internal {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L225-L225) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

32:     function _commitOneBatch(

103:     function _verifyBatchTimestamp(

130:     function _processL2Logs(

215:     function _commitBatches(

253:     function _commitBatchesWithoutSystemContractsUpgrade(

273:     function _commitBatchesWithSystemContractsUpgrade(

308:     function _collectOperationsFromPriorityQueue(uint256 _nPriorityOps) internal returns (bytes32 concatHash) {

321:     function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {

349:     function _executeBatches(StoredBatchInfo[] calldata _batchesData) internal {

386:     function _proveBatches(

440:     function _verifyProof(uint256[] memory proofPublicInput, ProofInput calldata _proof) internal view {

453:     function _getBatchProofPublicInput(

481:     function _revertBatches(uint256 _newLastBatch) internal {

500:     function _createBatchCommitment(

515:     function _batchPassThroughData(CommitBatchInfo calldata _batch) internal pure returns (bytes memory) {

525:     function _batchMetaParameters() internal view returns (bytes memory) {

537:     function _batchAuxiliaryOutput(

561:     function _encodeBlobAuxilaryOutput(

587:     function _hashStoredBatchInfo(StoredBatchInfo memory _storedBatchInfo) internal pure returns (bytes32) {

592:     function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

597:     function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {

605:     function _pointEvaluationPrecompile(

625:     function _verifyBlobInformation(

679:     function _getBlobVersionedHash(uint256 _index) internal view returns (bytes32 versionedHash) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L32-L32) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L103-L103), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L130-L130), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L215-L215), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L253-L253), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L273-L273), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L308-L308), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L321-L321), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L349-L349), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L386-L386), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L440-L440), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L453-L453), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L481-L481), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L500-L500), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L515-L515), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L525-L525), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L537-L537), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L561-L561), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L587-L587), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L592-L592), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L597-L597), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L605-L605), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L625-L625), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L679-L679)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

104:     function _proveL2LogInclusion(

130:     function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {

156:     function _deriveL2GasPrice(uint256 _l1GasPrice, uint256 _gasPerPubdata) internal view returns (uint256) {

228:     function _requestL2TransactionSender(

258:     function _requestL2Transaction(

289:     function _serializeL2Transaction(

316:     function _writePriorityOp(

353:     function _hashFactoryDeps(bytes[] memory _factoryDeps) internal pure returns (uint256[] memory hashedFactoryDeps) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L104-L104) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L130-L130), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L156-L156), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L228-L228), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L258-L258), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L289-L289), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L316-L316), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L353-L353)


```solidity

File: contracts/state-transition/libraries/Diamond.sol

87:     function getDiamondStorage() internal pure returns (DiamondStorage storage diamondStorage) {

96:     function diamondCut(DiamondCutData memory _diamondCut) internal {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L87-L87) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L96-L96)


```solidity

File: contracts/state-transition/libraries/LibMap.sol

18:     function get(Uint32Map storage _map, uint256 _index) internal view returns (uint32 result) {

38:     function set(Uint32Map storage _map, uint256 _index, uint32 _value) internal {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L18-L18) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L38-L38)


```solidity

File: contracts/state-transition/libraries/Merkle.sol

18:     function calculateRoot(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L18-L18) 


```solidity

File: contracts/state-transition/libraries/PriorityQueue.sol

35:     function getFirstUnprocessedPriorityTx(Queue storage _queue) internal view returns (uint256) {

40:     function getTotalPriorityTxs(Queue storage _queue) internal view returns (uint256) {

45:     function getSize(Queue storage _queue) internal view returns (uint256) {

50:     function isEmpty(Queue storage _queue) internal view returns (bool) {

55:     function pushBack(Queue storage _queue, PriorityOperation memory _operation) internal {

64:     function front(Queue storage _queue) internal view returns (PriorityOperation memory) {

72:     function popFront(Queue storage _queue) internal returns (PriorityOperation memory priorityOperation) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/PriorityQueue.sol#L35-L35) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/PriorityQueue.sol#L40-L40), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/PriorityQueue.sol#L45-L45), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/PriorityQueue.sol#L50-L50), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/PriorityQueue.sol#L55-L55), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/PriorityQueue.sol#L64-L64), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/PriorityQueue.sol#L72-L72)


```solidity

File: contracts/state-transition/libraries/TransactionValidator.sol

19:     function validateL1ToL2Transaction(

46:     function validateUpgradeTransaction(L2CanonicalTransaction memory _transaction) internal pure {

69:     function getMinimalPriorityTransactionGasLimit(

109:     function getTransactionBodyGasLimit(

128:     function getOverheadForTransaction(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L19-L19) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L46-L46), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L69-L69), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L109-L109), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L128-L128)


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

163:     function _upgradeVerifier(address _newVerifier, VerifierParams calldata _verifierParams) internal {

171:     function _setBaseSystemContracts(bytes32 _bootloaderHash, bytes32 _defaultAccountHash) internal {

180:     function _setL2SystemContractUpgrade(

236:     function _setNewProtocolVersion(uint256 _newProtocolVersion) internal virtual {

263:     function _upgradeL1Contract(bytes calldata _customCallDataForUpgrade) internal virtual {}

269:     function _postUpgrade(bytes calldata _customCallDataForUpgrade) internal virtual {}


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L163-L163) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L171-L171), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L180-L180), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L236-L236), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L263-L263), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L269-L269)


```solidity

File: contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

20:     function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20-L20) 


```solidity

File: contracts/vendor/AddressAliasHelper.sol

28:     function applyL1ToL2Alias(address l1Address) internal pure returns (address l2Address) {

38:     function undoL1ToL2Alias(address l2Address) internal pure returns (address l1Address) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/vendor/AddressAliasHelper.sol#L28-L28) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/vendor/AddressAliasHelper.sol#L38-L38)


```solidity

File: contracts/L2ContractHelper.sol

90:     function sendMessageToL1(bytes memory _message) internal returns (bytes32) {

101:     function computeCreate2Address(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L90-L90) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L101-L101)


```solidity

File: contracts/SystemContractsCaller.sol

27:     function safeCastToU32(uint256 _x) internal pure returns (uint32) {

37:     function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

76:     function systemCallWithReturndata(

95:     function getFarCallABI(

121:     function getFarCallABIWithEmptyFatPointer(


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L27-L27) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L37-L37), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L76-L76), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L95-L95), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L121-L121)


```solidity

File: contracts/bridge/L2SharedBridge.sol

109:     function _deployL2Token(address _l1Token, bytes calldata _data) internal returns (address) {

138:     function _getL1WithdrawMessage(

157:     function _getCreate2Salt(address _l1Token) internal pure returns (bytes32 salt) {

164:     function _deployBeaconProxy(bytes32 salt) internal returns (BeaconProxy proxy) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L109-L109) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L138-L138), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L157-L157), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L164-L164)


```solidity

File: contracts/vendor/AddressAliasHelper.sol

28:     function applyL1ToL2Alias(address l1Address) internal pure returns (address l2Address) {

38:     function undoL1ToL2Alias(address l2Address) internal pure returns (address l1Address) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/vendor/AddressAliasHelper.sol#L28-L28) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/vendor/AddressAliasHelper.sol#L38-L38)


</details>


### [GAS&#x2011;75] Optimize Deployment Size by Fine-tuning IPFS Hash 
Optimizing the deployment size of a smart contract is vital to minimize gas costs, and one way to achieve this is by fine-tuning the IPFS hash appended by the Solidity compiler as metadata. This metadata, consisting of 53 bytes, increases the gas required for contract deployment by approximately 10,600 gas due to bytecode costs, and additionally, up to 848 gas due to calldata costs, depending on the proportion of zero and non-zero bytes. Utilize the --no-cbor-metadata compiler flag to prevent the compiler from appending metadata. However, this approach has a drawback as it can complicate the contract verification process on block explorers like Etherscan, potentially reducing transparency.


*There are 103 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/AccountCodeStorage.sol

22: contract AccountCodeStorage is IAccountCodeStorage {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L22-L22) 


```solidity

File: contracts/BootloaderUtilities.sol

16: contract BootloaderUtilities is IBootloaderUtilities {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L16-L16) 


```solidity

File: contracts/ComplexUpgrader.sol

14: contract ComplexUpgrader is IComplexUpgrader {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ComplexUpgrader.sol#L14-L14) 


```solidity

File: contracts/Compressor.sol

22: contract Compressor is ICompressor, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L22-L22) 


```solidity

File: contracts/ContractDeployer.sol

23: contract ContractDeployer is IContractDeployer, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L23-L23) 


```solidity

File: contracts/DefaultAccount.sol

19: contract DefaultAccount is IAccount {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L19-L19) 


```solidity

File: contracts/EmptyContract.sol

10: contract EmptyContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/EmptyContract.sol#L10-L10) 


```solidity

File: contracts/ImmutableSimulator.sol

18: contract ImmutableSimulator is IImmutableSimulator {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L18-L18) 


```solidity

File: contracts/KnownCodesStorage.sol

18: contract KnownCodesStorage is IKnownCodesStorage, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L18-L18) 


```solidity

File: contracts/L1Messenger.sol

25: contract L1Messenger is IL1Messenger, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L25-L25) 


```solidity

File: contracts/L2BaseToken.sol

18: contract L2BaseToken is IBaseToken, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L18-L18) 


```solidity

File: contracts/MsgValueSimulator.sol

19: contract MsgValueSimulator is ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/MsgValueSimulator.sol#L19-L19) 


```solidity

File: contracts/NonceHolder.sol

27: contract NonceHolder is INonceHolder, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L27-L27) 


```solidity

File: contracts/PubdataChunkPublisher.sol

16: contract PubdataChunkPublisher is IPubdataChunkPublisher, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L16-L16) 


```solidity

File: contracts/SystemContext.sol

17: contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L17-L17) 


```solidity

File: contracts/interfaces/IAccount.sol

9: interface IAccount {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IAccount.sol#L9-L9) 


```solidity

File: contracts/interfaces/IAccountCodeStorage.sol

5: interface IAccountCodeStorage {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IAccountCodeStorage.sol#L5-L5) 


```solidity

File: contracts/interfaces/IBaseToken.sol

5: interface IBaseToken {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IBaseToken.sol#L5-L5) 


```solidity

File: contracts/interfaces/IBootloaderUtilities.sol

7: interface IBootloaderUtilities {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IBootloaderUtilities.sol#L7-L7) 


```solidity

File: contracts/interfaces/IComplexUpgrader.sol

10: interface IComplexUpgrader {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IComplexUpgrader.sol#L10-L10) 


```solidity

File: contracts/interfaces/ICompressor.sol

18: interface ICompressor {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ICompressor.sol#L18-L18) 


```solidity

File: contracts/interfaces/IContractDeployer.sol

5: interface IContractDeployer {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IContractDeployer.sol#L5-L5) 


```solidity

File: contracts/interfaces/IImmutableSimulator.sol

10: interface IImmutableSimulator {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IImmutableSimulator.sol#L10-L10) 


```solidity

File: contracts/interfaces/IKnownCodesStorage.sol

11: interface IKnownCodesStorage {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IKnownCodesStorage.sol#L11-L11) 


```solidity

File: contracts/interfaces/IL1Messenger.sol

40: interface IL1Messenger {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IL1Messenger.sol#L40-L40) 


```solidity

File: contracts/interfaces/IL2StandardToken.sol

5: interface IL2StandardToken {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IL2StandardToken.sol#L5-L5) 


```solidity

File: contracts/interfaces/IMailbox.sol

5: interface IMailbox {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IMailbox.sol#L5-L5) 


```solidity

File: contracts/interfaces/INonceHolder.sol

13: interface INonceHolder {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/INonceHolder.sol#L13-L13) 


```solidity

File: contracts/interfaces/IPaymaster.sol

14: interface IPaymaster {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IPaymaster.sol#L14-L14) 


```solidity

File: contracts/interfaces/IPaymasterFlow.sol

12: interface IPaymasterFlow {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IPaymasterFlow.sol#L12-L12) 


```solidity

File: contracts/interfaces/IPubdataChunkPublisher.sol

9: interface IPubdataChunkPublisher {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IPubdataChunkPublisher.sol#L9-L9) 


```solidity

File: contracts/interfaces/ISystemContext.sol

11: interface ISystemContext {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContext.sol#L11-L11) 


```solidity

File: contracts/interfaces/ISystemContextDeprecated.sol

10: interface ISystemContextDeprecated {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContextDeprecated.sol#L10-L10) 


```solidity

File: contracts/interfaces/ISystemContract.sol

17: abstract contract ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L17-L17) 


```solidity

File: contracts/libraries/EfficientCall.sol

32: library EfficientCall {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L32-L32) 


```solidity

File: contracts/libraries/RLPEncoder.sol

10: library RLPEncoder {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L10-L10) 


```solidity

File: contracts/libraries/SystemContractHelper.sol

41: library SystemContractHelper {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L41-L41) 


```solidity

File: contracts/libraries/SystemContractsCaller.sol

68: library SystemContractsCaller {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L68-L68) 


```solidity

File: contracts/libraries/TransactionHelper.sol

78: library TransactionHelper {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L78-L78) 


```solidity

File: contracts/libraries/UnsafeBytesCalldata.sol

18: library UnsafeBytesCalldata {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L18-L18) 


```solidity

File: contracts/libraries/Utils.sol

11: library Utils {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L11-L11) 


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

19: contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L19-L19) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

30: contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L30-L30) 


```solidity

File: contracts/bridge/interfaces/IL1ERC20Bridge.sol

11: interface IL1ERC20Bridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11-L11) 


```solidity

File: contracts/bridge/interfaces/IL1SharedBridge.sol

12: interface IL1SharedBridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL1SharedBridge.sol#L12-L12) 


```solidity

File: contracts/bridge/interfaces/IL2Bridge.sol

6: interface IL2Bridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL2Bridge.sol#L6-L6) 


```solidity

File: contracts/bridge/interfaces/IWETH9.sol

4: interface IWETH9 {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IWETH9.sol#L4-L4) 


```solidity

File: contracts/bridgehub/Bridgehub.sol

16: contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L16-L16) 


```solidity

File: contracts/bridgehub/IBridgehub.sol

42: interface IBridgehub {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/IBridgehub.sol#L42-L42) 


```solidity

File: contracts/common/ReentrancyGuard.sol

25: abstract contract ReentrancyGuard {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/ReentrancyGuard.sol#L25-L25) 


```solidity

File: contracts/common/interfaces/IL2ContractDeployer.sol

9: interface IL2ContractDeployer {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/interfaces/IL2ContractDeployer.sol#L9-L9) 


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

10: library L2ContractHelper {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L10-L10) 


```solidity

File: contracts/common/libraries/UncheckedMath.sol

10: library UncheckedMath {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UncheckedMath.sol#L10-L10) 


```solidity

File: contracts/common/libraries/UnsafeBytes.sol

18: library UnsafeBytes {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UnsafeBytes.sol#L18-L18) 


```solidity

File: contracts/governance/Governance.sol

20: contract Governance is IGovernance, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L20-L20) 


```solidity

File: contracts/governance/IGovernance.sol

8: interface IGovernance {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/IGovernance.sol#L8-L8) 


```solidity

File: contracts/state-transition/IStateTransitionManager.sol

26: interface IStateTransitionManager {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/IStateTransitionManager.sol#L26-L26) 


```solidity

File: contracts/state-transition/StateTransitionManager.sol

25: contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L25-L25) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

22: contract ValidatorTimelock is IExecutor, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L22-L22) 


```solidity

File: contracts/state-transition/chain-deps/DiamondInit.sol

17: contract DiamondInit is ZkSyncStateTransitionBase, IDiamondInit {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondInit.sol#L17-L17) 


```solidity

File: contracts/state-transition/chain-deps/DiamondProxy.sol

10: contract DiamondProxy {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondProxy.sol#L10-L10) 


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

18: contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L18-L18) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

22: contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L22-L22) 


```solidity

File: contracts/state-transition/chain-deps/facets/Getters.sol

20: contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L20-L20) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

30: contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L30-L30) 


```solidity

File: contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

11: contract ZkSyncStateTransitionBase is ReentrancyGuard {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L11-L11) 


```solidity

File: contracts/state-transition/chain-interfaces/IAdmin.sol

13: interface IAdmin is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IAdmin.sol#L13-L13) 


```solidity

File: contracts/state-transition/chain-interfaces/IDiamondInit.sol

61: interface IDiamondInit {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IDiamondInit.sol#L61-L61) 


```solidity

File: contracts/state-transition/chain-interfaces/IExecutor.sol

73: interface IExecutor is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IExecutor.sol#L73-L73) 


```solidity

File: contracts/state-transition/chain-interfaces/IGetters.sol

13: interface IGetters is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IGetters.sol#L13-L13) 


```solidity

File: contracts/state-transition/chain-interfaces/ILegacyGetters.sol

11: interface ILegacyGetters is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L11-L11) 


```solidity

File: contracts/state-transition/chain-interfaces/IMailbox.sol

11: interface IMailbox is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IMailbox.sol#L11-L11) 


```solidity

File: contracts/state-transition/chain-interfaces/IVerifier.sol

15: interface IVerifier {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IVerifier.sol#L15-L15) 


```solidity

File: contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol

15: interface IZkSyncStateTransition is IAdmin, IExecutor, IGetters, IMailbox {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L15-L15) 


```solidity

File: contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol

7: interface IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L7-L7) 


```solidity

File: contracts/state-transition/l2-deps/ISystemContext.sol

4: interface ISystemContext {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/l2-deps/ISystemContext.sol#L4-L4) 


```solidity

File: contracts/state-transition/libraries/Diamond.sol

11: library Diamond {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L11-L11) 


```solidity

File: contracts/state-transition/libraries/LibMap.sol

8: library LibMap {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L8-L8) 


```solidity

File: contracts/state-transition/libraries/Merkle.sol

9: library Merkle {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L9-L9) 


```solidity

File: contracts/state-transition/libraries/PriorityQueue.sol

20: library PriorityQueue {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/PriorityQueue.sol#L20-L20) 


```solidity

File: contracts/state-transition/libraries/TransactionValidator.sol

13: library TransactionValidator {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L13-L13) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

44: abstract contract BaseZkSyncUpgrade is ZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L44-L44) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

17: abstract contract BaseZkSyncUpgradeGenesis is BaseZkSyncUpgrade {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L17-L17) 


```solidity

File: contracts/upgrades/DefaultUpgrade.sol

10: contract DefaultUpgrade is BaseZkSyncUpgrade {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/DefaultUpgrade.sol#L10-L10) 


```solidity

File: contracts/upgrades/GenesisUpgrade.sol

11: contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/GenesisUpgrade.sol#L11-L11) 


```solidity

File: contracts/upgrades/IDefaultUpgrade.sol

7: interface IDefaultUpgrade {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/IDefaultUpgrade.sol#L7-L7) 


```solidity

File: contracts/vendor/AddressAliasHelper.sol

21: library AddressAliasHelper {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/vendor/AddressAliasHelper.sol#L21-L21) 


```solidity

File: contracts/ForceDeployUpgrader.sol

10: contract ForceDeployUpgrader {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/ForceDeployUpgrader.sol#L10-L10) 


```solidity

File: contracts/L2ContractHelper.sol

18: interface IL2Messenger {

30: interface IContractDeployer {

61: interface IBaseToken {

83: library L2ContractHelper {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L18-L18) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L30-L30), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L61-L61), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L83-L83)


```solidity

File: contracts/SystemContractsCaller.sol

26: library Utils {

36: library SystemContractsCaller {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L26-L26) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L36-L36)


```solidity

File: contracts/bridge/L2SharedBridge.sol

23: contract L2SharedBridge is IL2SharedBridge, Initializable {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L23-L23) 


```solidity

File: contracts/bridge/L2StandardERC20.sol

15: contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L15-L15) 


```solidity

File: contracts/bridge/interfaces/IL1ERC20Bridge.sol

8: interface IL1ERC20Bridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL1ERC20Bridge.sol#L8-L8) 


```solidity

File: contracts/bridge/interfaces/IL1SharedBridge.sol

8: interface IL1SharedBridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL1SharedBridge.sol#L8-L8) 


```solidity

File: contracts/bridge/interfaces/IL2SharedBridge.sol

6: interface IL2SharedBridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL2SharedBridge.sol#L6-L6) 


```solidity

File: contracts/bridge/interfaces/IL2StandardToken.sol

5: interface IL2StandardToken {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL2StandardToken.sol#L5-L5) 


```solidity

File: contracts/interfaces/IPaymaster.sol

14: interface IPaymaster {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/interfaces/IPaymaster.sol#L14-L14) 


```solidity

File: contracts/interfaces/IPaymasterFlow.sol

13: interface IPaymasterFlow {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/interfaces/IPaymasterFlow.sol#L13-L13) 


```solidity

File: contracts/vendor/AddressAliasHelper.sol

21: library AddressAliasHelper {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/vendor/AddressAliasHelper.sol#L21-L21) 


</details>


### [GAS&#x2011;76] Use assembly scratch space to build calldata for external calls 
Using Solidity's assembly scratch space for constructing calldata in external calls with one or two arguments can be a gas-efficient approach. This method leverages the designated memory area (the first 64 bytes of memory) for temporary data storage during assembly operations. By directly writing arguments into this scratch space, it eliminates the need for additional memory allocation typically required for calldata preparation. This technique can lead to notable gas savings, especially in high-frequency or gas-sensitive operations. However, it requires careful implementation to avoid data corruption and should be used with a thorough understanding of low-level EVM operations and memory handling. Proper testing and validation are crucial when employing such optimizations.


*There are 57 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/AccountCodeStorage.sol

102:         if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L102-L102) 


```solidity

File: contracts/Compressor.sol

73:         L1_MESSENGER_CONTRACT.sendToL1(_rawCompressedData);

74:         KNOWN_CODE_STORAGE_CONTRACT.markBytecodeAsPublished(bytecodeHash);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L73-L73) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L74-L74)


```solidity

File: contracts/ContractDeployer.sol

49:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getRawCodeHash(_address) == 0

168:         NONCE_HOLDER_SYSTEM_CONTRACT.incrementDeploymentNonce(msg.sender);

188:         uint256 senderNonce = NONCE_HOLDER_SYSTEM_CONTRACT.incrementDeploymentNonce(msg.sender);

269:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0,

273:         require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied");

302:         uint256 knownCodeMarker = KNOWN_CODE_STORAGE_CONTRACT.getMarker(_bytecodeHash);

312:         ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.storeAccountConstructingCodeHash(_newAddress, constructingBytecodeHash);

345:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.markAccountCodeHashAsConstructed(_newAddress);

348:             IMMUTABLE_SIMULATOR_SYSTEM_CONTRACT.setImmutables(_newAddress, immutables);

352:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.storeAccountConstructedCodeHash(_newAddress, _bytecodeHash);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L49-L49) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L168-L168), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L188-L188), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L269-L269), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L273-L273), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L302-L302), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L312-L312), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L345-L345), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L348-L348), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L352-L352)


```solidity

File: contracts/KnownCodesStorage.sol

51:                 L1_MESSENGER_CONTRACT.requestBytecodeL1Publication(_bytecodeHash);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L51-L51) 


```solidity

File: contracts/L1Messenger.sol

317:         PUBDATA_CHUNK_PUBLISHER.chunkAndPublishPubdata(totalL2ToL1Pubdata);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L317-L317) 


```solidity

File: contracts/L2BaseToken.sol

77:         L1_MESSENGER_CONTRACT.sendToL1(message);

90:         L1_MESSENGER_CONTRACT.sendToL1(message);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L77-L77) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L90-L90)


```solidity

File: contracts/NonceHolder.sol

83:         IContractDeployer.AccountInfo memory accountInfo = DEPLOYER_SYSTEM_CONTRACT.getAccountInfo(msg.sender);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L83-L83) 


```solidity

File: contracts/libraries/TransactionHelper.sol

377:             uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);

382:                 IERC20(token).safeApprove(paymaster, 0);

383:                 IERC20(token).safeApprove(paymaster, minAllowance);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L377-L377) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L382-L382), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L383-L383)


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

65:         uint256 amount = IERC20(_token).balanceOf(address(this));

67:         IERC20(_token).safeTransfer(address(sharedBridge), amount);

161:         uint256 balanceBefore = _token.balanceOf(address(sharedBridge));

163:         uint256 balanceAfter = _token.balanceOf(address(sharedBridge));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L65-L65) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L67-L67), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L161-L161), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L163-L163)


```solidity

File: contracts/bridge/L1SharedBridge.sol

127:             uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

128:             uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));

130:             IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);

131:             uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

138:         require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");

174:         uint256 balanceBefore = _token.balanceOf(address(this));

176:         uint256 balanceAfter = _token.balanceOf(address(this));

195:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

362:             IERC20(_l1Token).safeTransfer(_depositSender, _amount);

396:             require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");

423:             bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
424:                 _l2BatchNumber,
425:                 _l2MessageIndex
426:             );

452:             IERC20(l1Token).safeTransfer(l1Receiver, amount);

467:             bool baseTokenWithdrawal = (l1Token == bridgehub.baseToken(_chainId));

508:             l1Token = bridgehub.baseToken(_chainId);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L127-L127) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L128-L128), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L130-L130), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L131-L131), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L138-L138), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L174-L174), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L176-L176), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L195-L195), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L362-L362), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L396-L396), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L423-L426), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L452-L452), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L467-L467), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L508-L508)


```solidity

File: contracts/bridgehub/Bridgehub.sol

76:         return IStateTransitionManager(stateTransitionManager[_chainId]).stateTransition(_chainId);

238:         canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction(
239:             BridgehubL2TransactionRequest({
240:                 sender: msg.sender,
241:                 contractL2: _request.l2Contract,
242:                 mintValue: _request.mintValue,
243:                 l2Value: _request.l2Value,
244:                 l2Calldata: _request.l2Calldata,
245:                 l2GasLimit: _request.l2GasLimit,
246:                 l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
247:                 factoryDeps: _request.factoryDeps,
248:                 refundRecipient: refundRecipient
249:             })
250:         );

304:         canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction(
305:             BridgehubL2TransactionRequest({
306:                 sender: _request.secondBridgeAddress,
307:                 contractL2: outputRequest.l2Contract,
308:                 mintValue: _request.mintValue,
309:                 l2Value: _request.l2Value,
310:                 l2Calldata: outputRequest.l2Calldata,
311:                 l2GasLimit: _request.l2GasLimit,
312:                 l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
313:                 factoryDeps: outputRequest.factoryDeps,
314:                 refundRecipient: refundRecipient
315:             })
316:         );


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L76-L76) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L238-L250), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L304-L316)


```solidity

File: contracts/state-transition/StateTransitionManager.sol

171:         IZkSyncStateTransition(stateTransition[_chainId]).revertBatches(_newLastBatch);

226:         IAdmin(_chainContract).executeUpgrade(cutData);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L171-L171) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L226-L226)


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

62:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

226:         address contractAddress = stateTransitionManager.stateTransition(_chainId);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L62-L62) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L226-L226)


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

106:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L106-L106) 


```solidity

File: contracts/upgrades/DefaultUpgrade.sol

14:         super.upgrade(_proposedUpgrade);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/DefaultUpgrade.sol#L14-L14) 


```solidity

File: contracts/upgrades/GenesisUpgrade.sol

15:         super.upgrade(_proposedUpgrade);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/GenesisUpgrade.sol#L15-L15) 


```solidity

File: contracts/L2ContractHelper.sol

91:         return L2_MESSENGER.sendToL1(_message);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L91-L91) 


```solidity

File: contracts/bridge/L2SharedBridge.sol

66:             l2TokenBeacon.transferOwnership(_aliasedOwner);

104:         IL2StandardToken(expectedL2Token).bridgeMint(_l2Receiver, _amount);

113:         L2StandardERC20(address(l2Token)).bridgeInitialize(_l1Token, _data);

126:         IL2StandardToken(_l2Token).bridgeBurn(msg.sender, _amount);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L66-L66) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L104-L104), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L113-L113), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L126-L126)


```solidity

File: contracts/bridge/L2StandardERC20.sol

75:         try this.decodeString(nameBytes) returns (string memory nameString) {

81:         try this.decodeString(symbolBytes) returns (string memory symbolString) {

93:         try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L75-L75) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L81-L81), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L93-L93)


</details>


### [GAS&#x2011;77] Use more recent OpenZeppelin version for gas boost 
Every release contains new gas optimizations. Use the latest version to take advantage of this.


*There are 21 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/bridge/L1ERC20Bridge.sol

5: import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";

6: import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L5-L5) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L6-L6)


```solidity

File: contracts/bridge/L1SharedBridge.sol

5: import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";

6: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";

8: import {IERC20Metadata} from "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";

9: import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";

10: import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L5-L5) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L6-L6), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L8-L8), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L9-L9), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L10-L10)


```solidity

File: contracts/bridgehub/Bridgehub.sol

5: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L5-L5) 


```solidity

File: contracts/governance/Governance.sol

5: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L5-L5) 


```solidity

File: contracts/state-transition/StateTransitionManager.sol

16: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L16-L16) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

5: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L5-L5) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

5: import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L5-L5) 


```solidity

File: contracts/state-transition/libraries/Diamond.sol

5: import {SafeCast} from "@openzeppelin/contracts/utils/math/SafeCast.sol";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L5-L5) 


```solidity

File: contracts/state-transition/libraries/TransactionValidator.sol

5: import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L5-L5) 


```solidity

File: contracts/bridge/L2SharedBridge.sol

5: import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";

6: import {BeaconProxy} from "@openzeppelin/contracts/proxy/beacon/BeaconProxy.sol";

7: import {UpgradeableBeacon} from "@openzeppelin/contracts/proxy/beacon/UpgradeableBeacon.sol";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L5-L5) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L6-L6), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L7-L7)


```solidity

File: contracts/bridge/L2StandardERC20.sol

5: import {ERC20PermitUpgradeable} from "@openzeppelin/contracts-upgradeable/token/ERC20/extensions/draft-ERC20PermitUpgradeable.sol";

5: import {ERC20PermitUpgradeable} from "@openzeppelin/contracts-upgradeable/token/ERC20/extensions/draft-ERC20PermitUpgradeable.sol";

6: import {UpgradeableBeacon} from "@openzeppelin/contracts/proxy/beacon/UpgradeableBeacon.sol";

7: import {ERC1967Upgrade} from "@openzeppelin/contracts/proxy/ERC1967/ERC1967Upgrade.sol";


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L5-L5) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L5-L5), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L6-L6), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L7-L7)


</details>


### [GAS&#x2011;78] Use Array.unsafeAccess() to avoid repeated array length checks 
When using storage arrays, solidity adds an internal lookup of the array's length (a Gcoldsload 2100 gas) to ensure you don't read past the array's end. You can avoid this lookup by using `Array.unsafeAccess()` in cases where the length has already been checked, as is the case with the instances below


*There are 40 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/Compressor.sol

143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

174:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L143-L143) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L174-L174)


```solidity

File: contracts/ContractDeployer.sol

249:             sumOfValues += _deployments[i].value;

254:             this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);

254:             this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L249-L249) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L254-L254), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L254-L254)


```solidity

File: contracts/ImmutableSimulator.sol

39:                 uint256 index = _immutables[i].index;

40:                 bytes32 value = _immutables[i].value;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L39-L39) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L40-L40)


```solidity

File: contracts/KnownCodesStorage.sol

31:                 _markBytecodeAsPublished(_hashes[i], _shouldSendToL1);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L31-L31) 


```solidity

File: contracts/L1Messenger.sol

280:             uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==

289:         uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L280-L280) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L289-L289)


```solidity

File: contracts/governance/Governance.sol

226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L226-L226) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L226-L226), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L226-L226)


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

117:                 committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);

136:                 committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);

187:                     _newBatchesData[i].batchNumber

210:                 uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L117-L117) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L136-L136), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L187-L187), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L210-L210)


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

258:             _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));

287:         s.l2SystemContractsUpgradeBatchNumber = _newBatchesData[0].batchNumber;

294:                 _newBatchesData[i],

352:             _executeOneBatch(_batchesData[i], i);

353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

408:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],

412:             bytes32 currentBatchCommitment = _committedBatches[i].commitment;

581:             blobAuxOutputWords[i * 2] = _blobHashes[i];

582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L258-L258) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L287-L287), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L294-L294), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L352-L352), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L353-L353), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L353-L353), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L353-L353), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L408-L408), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L412-L412), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L581-L581), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L582-L582)


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

357:             bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L357-L357) 


```solidity

File: contracts/state-transition/libraries/Diamond.sol

102:             Action action = facetCuts[i].action;

103:             address facet = facetCuts[i].facet;

104:             bool isFacetFreezable = facetCuts[i].isFreezable;

105:             bytes4[] memory selectors = facetCuts[i].selectors;

139:             bytes4 selector = _selectors[i];

159:             bytes4 selector = _selectors[i];

179:             bytes4 selector = _selectors[i];


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L102-L102) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L103-L103), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L104-L104), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L105-L105), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L139-L139), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L159-L159), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L179-L179)


```solidity

File: contracts/state-transition/libraries/Merkle.sol

31:                 ? _efficientHash(currentHash, _path[i])

32:                 : _efficientHash(_path[i], currentHash);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L31-L31) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L32-L32)


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

228:                 L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),

228:                 L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L228-L228) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L228-L228)


</details>


### [GAS&#x2011;79] State variables only set in their definitions should be declared constant 
Avoids a Gsset (20000 gas) at deployment, and replaces the first access in each transaction (Gcoldsload - 2100 gas) and each access thereafter (Gwarmacces - 100 gas) with a `PUSH32` (3 gas).


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/SystemContext.sol

37:     uint256 public blockGasLimit = type(uint32).max;

41:     address public coinbase = BOOTLOADER_FORMAL_ADDRESS;

44:     uint256 public difficulty = 2.5e15;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L37-L37) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L41-L41), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L44-L44)


</details>


### [GAS&#x2011;80] Combine `mapping`s referenced in the same function by the same key 
Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot (i.e. runtime gas savings). Even if the values can't be packed, if both fields are accessed in the same function (as is the case for these instances), combining them can save **~42 gas per access** due to [not having to recalculate the key's keccak256 hash](https://gist.github.com/IllIllI000/639032d73e35d7e968ff58d8784bc445) (Gkeccak256 - 30 gas) and that calculation's associated stack operations.


*There are 17 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/bridge/L1SharedBridge.sol

//@audit the following two maps should be combined : `hyperbridgingEnabled` and `chainBalance`
148:     function bridgehubDepositBaseToken(
149:         uint256 _chainId,
150:         address _prevMsgSender,
151:         address _l1Token,
152:         uint256 _amount
153:     ) external payable virtual onlyBridgehubOrEra(_chainId) {
154:         if (_l1Token == ETH_TOKEN_ADDRESS) {
155:             require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");
156:         } else {
157:             // The Bridgehub also checks this, but we want to be sure
158:             require(msg.value == 0, "ShB m.v > 0 b d.it");
159: 
160:             uint256 amount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _amount); // note if _prevMsgSender is this contract, this will return 0. This does not happen.
161:             require(amount == _amount, "3T"); // The token has non-standard transfer logic
162:         }
163: 
164:         if (!hyperbridgingEnabled[_chainId]) {
165:             chainBalance[_chainId][_l1Token] += _amount;
166:         }
167:         // Note that we don't save the deposited amount, as this is for the base token, which gets sent to the refundRecipient if the tx fails
168:         emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);
169:     }

//@audit the following two maps should be combined : `hyperbridgingEnabled` and `l2BridgeAddress`
182:     function bridgehubDeposit(
183:         uint256 _chainId,
184:         address _prevMsgSender,
185:         uint256, // l2Value, needed for Weth deposits in the future
186:         bytes calldata _data
187:     ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
188:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
189: 
190:         (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
191:             _data,
192:             (address, uint256, address)
193:         );
194:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");
195:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");
196: 
197:         uint256 amount;
198:         if (_l1Token == ETH_TOKEN_ADDRESS) {
199:             amount = msg.value;
200:             require(_depositAmount == 0, "ShB wrong withdraw amount");
201:         } else {
202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
203:             amount = _depositAmount;
204: 
205:             uint256 withdrawAmount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount);
206:             require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic
207:         }
208:         require(amount != 0, "6T"); // empty deposit amount
209: 
210:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));
211:         if (!hyperbridgingEnabled[_chainId]) {
212:             chainBalance[_chainId][_l1Token] += amount;
213:         }
214: 
215:         {
216:             // Request the finalization of the deposit on the L2 side
217:             bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, amount);
218: 
219:             request = L2TransactionRequestTwoBridgesInner({
220:                 magicValue: TWO_BRIDGES_MAGIC_VALUE,
221:                 l2Contract: l2BridgeAddress[_chainId],
222:                 l2Calldata: l2TxCalldata,
223:                 factoryDeps: new bytes[](0),
224:                 txDataHash: txDataHash
225:             });
226:         }
227:         emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);
228:     }

//@audit the following two maps should be combined : `hyperbridgingEnabled` and `chainBalance`
182:     function bridgehubDeposit(
183:         uint256 _chainId,
184:         address _prevMsgSender,
185:         uint256, // l2Value, needed for Weth deposits in the future
186:         bytes calldata _data
187:     ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
188:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
189: 
190:         (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
191:             _data,
192:             (address, uint256, address)
193:         );
194:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");
195:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");
196: 
197:         uint256 amount;
198:         if (_l1Token == ETH_TOKEN_ADDRESS) {
199:             amount = msg.value;
200:             require(_depositAmount == 0, "ShB wrong withdraw amount");
201:         } else {
202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
203:             amount = _depositAmount;
204: 
205:             uint256 withdrawAmount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount);
206:             require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic
207:         }
208:         require(amount != 0, "6T"); // empty deposit amount
209: 
210:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));
211:         if (!hyperbridgingEnabled[_chainId]) {
212:             chainBalance[_chainId][_l1Token] += amount;
213:         }
214: 
215:         {
216:             // Request the finalization of the deposit on the L2 side
217:             bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, amount);
218: 
219:             request = L2TransactionRequestTwoBridgesInner({
220:                 magicValue: TWO_BRIDGES_MAGIC_VALUE,
221:                 l2Contract: l2BridgeAddress[_chainId],
222:                 l2Calldata: l2TxCalldata,
223:                 factoryDeps: new bytes[](0),
224:                 txDataHash: txDataHash
225:             });
226:         }
227:         emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);
228:     }

//@audit the following two maps should be combined : `l2BridgeAddress` and `chainBalance`
182:     function bridgehubDeposit(
183:         uint256 _chainId,
184:         address _prevMsgSender,
185:         uint256, // l2Value, needed for Weth deposits in the future
186:         bytes calldata _data
187:     ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
188:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
189: 
190:         (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
191:             _data,
192:             (address, uint256, address)
193:         );
194:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");
195:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");
196: 
197:         uint256 amount;
198:         if (_l1Token == ETH_TOKEN_ADDRESS) {
199:             amount = msg.value;
200:             require(_depositAmount == 0, "ShB wrong withdraw amount");
201:         } else {
202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
203:             amount = _depositAmount;
204: 
205:             uint256 withdrawAmount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount);
206:             require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic
207:         }
208:         require(amount != 0, "6T"); // empty deposit amount
209: 
210:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));
211:         if (!hyperbridgingEnabled[_chainId]) {
212:             chainBalance[_chainId][_l1Token] += amount;
213:         }
214: 
215:         {
216:             // Request the finalization of the deposit on the L2 side
217:             bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, amount);
218: 
219:             request = L2TransactionRequestTwoBridgesInner({
220:                 magicValue: TWO_BRIDGES_MAGIC_VALUE,
221:                 l2Contract: l2BridgeAddress[_chainId],
222:                 l2Calldata: l2TxCalldata,
223:                 factoryDeps: new bytes[](0),
224:                 txDataHash: txDataHash
225:             });
226:         }
227:         emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);
228:     }

//@audit the following two maps should be combined : `hyperbridgingEnabled` and `depositHappened`
303:     function _claimFailedDeposit(
304:         bool _checkedInLegacyBridge,
305:         uint256 _chainId,
306:         address _depositSender,
307:         address _l1Token,
308:         uint256 _amount,
309:         bytes32 _l2TxHash,
310:         uint256 _l2BatchNumber,
311:         uint256 _l2MessageIndex,
312:         uint16 _l2TxNumberInBatch,
313:         bytes32[] calldata _merkleProof
314:     ) internal nonReentrant {
315:         {
316:             bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
317:                 _chainId,
318:                 _l2TxHash,
319:                 _l2BatchNumber,
320:                 _l2MessageIndex,
321:                 _l2TxNumberInBatch,
322:                 _merkleProof,
323:                 TxStatus.Failure
324:             );
325:             require(proofValid, "yn");
326:         }
327:         require(_amount > 0, "y1");
328: 
329:         {
330:             bool notCheckedInLegacyBridgeOrWeCanCheckDeposit;
331:             {
332:                 // Deposits that happened before the upgrade cannot be checked here, they have to be claimed and checked in the legacyBridge
333:                 bool weCanCheckDepositHere = !_isEraLegacyWithdrawal(_chainId, _l2BatchNumber);
334:                 // Double claims are not possible, as we this check except for legacy bridge withdrawals
335:                 // Funds claimed before the update will still be recorded in the legacy bridge
336:                 // Note we double check NEW deposits if they are called from the legacy bridge
337:                 notCheckedInLegacyBridgeOrWeCanCheckDeposit = (!_checkedInLegacyBridge) || weCanCheckDepositHere;
338:             }
339:             if (notCheckedInLegacyBridgeOrWeCanCheckDeposit) {
340:                 bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
341:                 bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));
342:                 require(dataHash == txDataHash, "ShB: d.it not hap");
343:                 delete depositHappened[_chainId][_l2TxHash];
344:             }
345:         }
346: 
347:         if (!hyperbridgingEnabled[_chainId]) {
348:             // check that the chain has sufficient balance
349:             require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
350:             chainBalance[_chainId][_l1Token] -= _amount;
351:         }
352: 
353:         // Withdraw funds
354:         if (_l1Token == ETH_TOKEN_ADDRESS) {
355:             bool callSuccess;
356:             // Low-level assembly call, to avoid any memory copying (save gas)
357:             assembly {
358:                 callSuccess := call(gas(), _depositSender, _amount, 0, 0, 0, 0)
359:             }
360:             require(callSuccess, "ShB: claimFailedDeposit failed");
361:         } else {
362:             IERC20(_l1Token).safeTransfer(_depositSender, _amount);
363:             // Note we don't allow weth deposits anymore, but there might be legacy weth deposits.
364:             // until we add Weth bridging capabilities, we don't wrap/unwrap weth to ether.
365:         }
366: 
367:         emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);
368:     }

//@audit the following two maps should be combined : `hyperbridgingEnabled` and `chainBalance`
303:     function _claimFailedDeposit(
304:         bool _checkedInLegacyBridge,
305:         uint256 _chainId,
306:         address _depositSender,
307:         address _l1Token,
308:         uint256 _amount,
309:         bytes32 _l2TxHash,
310:         uint256 _l2BatchNumber,
311:         uint256 _l2MessageIndex,
312:         uint16 _l2TxNumberInBatch,
313:         bytes32[] calldata _merkleProof
314:     ) internal nonReentrant {
315:         {
316:             bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
317:                 _chainId,
318:                 _l2TxHash,
319:                 _l2BatchNumber,
320:                 _l2MessageIndex,
321:                 _l2TxNumberInBatch,
322:                 _merkleProof,
323:                 TxStatus.Failure
324:             );
325:             require(proofValid, "yn");
326:         }
327:         require(_amount > 0, "y1");
328: 
329:         {
330:             bool notCheckedInLegacyBridgeOrWeCanCheckDeposit;
331:             {
332:                 // Deposits that happened before the upgrade cannot be checked here, they have to be claimed and checked in the legacyBridge
333:                 bool weCanCheckDepositHere = !_isEraLegacyWithdrawal(_chainId, _l2BatchNumber);
334:                 // Double claims are not possible, as we this check except for legacy bridge withdrawals
335:                 // Funds claimed before the update will still be recorded in the legacy bridge
336:                 // Note we double check NEW deposits if they are called from the legacy bridge
337:                 notCheckedInLegacyBridgeOrWeCanCheckDeposit = (!_checkedInLegacyBridge) || weCanCheckDepositHere;
338:             }
339:             if (notCheckedInLegacyBridgeOrWeCanCheckDeposit) {
340:                 bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
341:                 bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));
342:                 require(dataHash == txDataHash, "ShB: d.it not hap");
343:                 delete depositHappened[_chainId][_l2TxHash];
344:             }
345:         }
346: 
347:         if (!hyperbridgingEnabled[_chainId]) {
348:             // check that the chain has sufficient balance
349:             require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
350:             chainBalance[_chainId][_l1Token] -= _amount;
351:         }
352: 
353:         // Withdraw funds
354:         if (_l1Token == ETH_TOKEN_ADDRESS) {
355:             bool callSuccess;
356:             // Low-level assembly call, to avoid any memory copying (save gas)
357:             assembly {
358:                 callSuccess := call(gas(), _depositSender, _amount, 0, 0, 0, 0)
359:             }
360:             require(callSuccess, "ShB: claimFailedDeposit failed");
361:         } else {
362:             IERC20(_l1Token).safeTransfer(_depositSender, _amount);
363:             // Note we don't allow weth deposits anymore, but there might be legacy weth deposits.
364:             // until we add Weth bridging capabilities, we don't wrap/unwrap weth to ether.
365:         }
366: 
367:         emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);
368:     }

//@audit the following two maps should be combined : `depositHappened` and `chainBalance`
303:     function _claimFailedDeposit(
304:         bool _checkedInLegacyBridge,
305:         uint256 _chainId,
306:         address _depositSender,
307:         address _l1Token,
308:         uint256 _amount,
309:         bytes32 _l2TxHash,
310:         uint256 _l2BatchNumber,
311:         uint256 _l2MessageIndex,
312:         uint16 _l2TxNumberInBatch,
313:         bytes32[] calldata _merkleProof
314:     ) internal nonReentrant {
315:         {
316:             bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
317:                 _chainId,
318:                 _l2TxHash,
319:                 _l2BatchNumber,
320:                 _l2MessageIndex,
321:                 _l2TxNumberInBatch,
322:                 _merkleProof,
323:                 TxStatus.Failure
324:             );
325:             require(proofValid, "yn");
326:         }
327:         require(_amount > 0, "y1");
328: 
329:         {
330:             bool notCheckedInLegacyBridgeOrWeCanCheckDeposit;
331:             {
332:                 // Deposits that happened before the upgrade cannot be checked here, they have to be claimed and checked in the legacyBridge
333:                 bool weCanCheckDepositHere = !_isEraLegacyWithdrawal(_chainId, _l2BatchNumber);
334:                 // Double claims are not possible, as we this check except for legacy bridge withdrawals
335:                 // Funds claimed before the update will still be recorded in the legacy bridge
336:                 // Note we double check NEW deposits if they are called from the legacy bridge
337:                 notCheckedInLegacyBridgeOrWeCanCheckDeposit = (!_checkedInLegacyBridge) || weCanCheckDepositHere;
338:             }
339:             if (notCheckedInLegacyBridgeOrWeCanCheckDeposit) {
340:                 bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
341:                 bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));
342:                 require(dataHash == txDataHash, "ShB: d.it not hap");
343:                 delete depositHappened[_chainId][_l2TxHash];
344:             }
345:         }
346: 
347:         if (!hyperbridgingEnabled[_chainId]) {
348:             // check that the chain has sufficient balance
349:             require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
350:             chainBalance[_chainId][_l1Token] -= _amount;
351:         }
352: 
353:         // Withdraw funds
354:         if (_l1Token == ETH_TOKEN_ADDRESS) {
355:             bool callSuccess;
356:             // Low-level assembly call, to avoid any memory copying (save gas)
357:             assembly {
358:                 callSuccess := call(gas(), _depositSender, _amount, 0, 0, 0, 0)
359:             }
360:             require(callSuccess, "ShB: claimFailedDeposit failed");
361:         } else {
362:             IERC20(_l1Token).safeTransfer(_depositSender, _amount);
363:             // Note we don't allow weth deposits anymore, but there might be legacy weth deposits.
364:             // until we add Weth bridging capabilities, we don't wrap/unwrap weth to ether.
365:         }
366: 
367:         emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);
368:     }

//@audit the following two maps should be combined : `hyperbridgingEnabled` and `isWithdrawalFinalized`
409:     function _finalizeWithdrawal(
410:         uint256 _chainId,
411:         uint256 _l2BatchNumber,
412:         uint256 _l2MessageIndex,
413:         uint16 _l2TxNumberInBatch,
414:         bytes calldata _message,
415:         bytes32[] calldata _merkleProof
416:     ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
417:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");
418:         isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true;
419: 
420:         // Handling special case for withdrawal from zkSync Era initiated before Shared Bridge.
421:         if (_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)) {
422:             // Checks that the withdrawal wasn't finalized already.
423:             bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
424:                 _l2BatchNumber,
425:                 _l2MessageIndex
426:             );
427:             require(!alreadyFinalized, "Withdrawal is already finalized 2");
428:         }
429: 
430:         MessageParams memory messageParams = MessageParams({
431:             l2BatchNumber: _l2BatchNumber,
432:             l2MessageIndex: _l2MessageIndex,
433:             l2TxNumberInBatch: _l2TxNumberInBatch
434:         });
435:         (l1Receiver, l1Token, amount) = _checkWithdrawal(_chainId, messageParams, _message, _merkleProof);
436: 
437:         if (!hyperbridgingEnabled[_chainId]) {
438:             // Check that the chain has sufficient balance
439:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds
440:             chainBalance[_chainId][l1Token] -= amount;
441:         }
442: 
443:         if (l1Token == ETH_TOKEN_ADDRESS) {
444:             bool callSuccess;
445:             // Low-level assembly call, to avoid any memory copying (save gas)
446:             assembly {
447:                 callSuccess := call(gas(), l1Receiver, amount, 0, 0, 0, 0)
448:             }
449:             require(callSuccess, "ShB: withdraw failed");
450:         } else {
451:             // Withdraw funds
452:             IERC20(l1Token).safeTransfer(l1Receiver, amount);
453:         }
454:         emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);
455:     }

//@audit the following two maps should be combined : `hyperbridgingEnabled` and `chainBalance`
409:     function _finalizeWithdrawal(
410:         uint256 _chainId,
411:         uint256 _l2BatchNumber,
412:         uint256 _l2MessageIndex,
413:         uint16 _l2TxNumberInBatch,
414:         bytes calldata _message,
415:         bytes32[] calldata _merkleProof
416:     ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
417:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");
418:         isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true;
419: 
420:         // Handling special case for withdrawal from zkSync Era initiated before Shared Bridge.
421:         if (_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)) {
422:             // Checks that the withdrawal wasn't finalized already.
423:             bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
424:                 _l2BatchNumber,
425:                 _l2MessageIndex
426:             );
427:             require(!alreadyFinalized, "Withdrawal is already finalized 2");
428:         }
429: 
430:         MessageParams memory messageParams = MessageParams({
431:             l2BatchNumber: _l2BatchNumber,
432:             l2MessageIndex: _l2MessageIndex,
433:             l2TxNumberInBatch: _l2TxNumberInBatch
434:         });
435:         (l1Receiver, l1Token, amount) = _checkWithdrawal(_chainId, messageParams, _message, _merkleProof);
436: 
437:         if (!hyperbridgingEnabled[_chainId]) {
438:             // Check that the chain has sufficient balance
439:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds
440:             chainBalance[_chainId][l1Token] -= amount;
441:         }
442: 
443:         if (l1Token == ETH_TOKEN_ADDRESS) {
444:             bool callSuccess;
445:             // Low-level assembly call, to avoid any memory copying (save gas)
446:             assembly {
447:                 callSuccess := call(gas(), l1Receiver, amount, 0, 0, 0, 0)
448:             }
449:             require(callSuccess, "ShB: withdraw failed");
450:         } else {
451:             // Withdraw funds
452:             IERC20(l1Token).safeTransfer(l1Receiver, amount);
453:         }
454:         emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);
455:     }

//@audit the following two maps should be combined : `isWithdrawalFinalized` and `chainBalance`
409:     function _finalizeWithdrawal(
410:         uint256 _chainId,
411:         uint256 _l2BatchNumber,
412:         uint256 _l2MessageIndex,
413:         uint16 _l2TxNumberInBatch,
414:         bytes calldata _message,
415:         bytes32[] calldata _merkleProof
416:     ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
417:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");
418:         isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true;
419: 
420:         // Handling special case for withdrawal from zkSync Era initiated before Shared Bridge.
421:         if (_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)) {
422:             // Checks that the withdrawal wasn't finalized already.
423:             bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
424:                 _l2BatchNumber,
425:                 _l2MessageIndex
426:             );
427:             require(!alreadyFinalized, "Withdrawal is already finalized 2");
428:         }
429: 
430:         MessageParams memory messageParams = MessageParams({
431:             l2BatchNumber: _l2BatchNumber,
432:             l2MessageIndex: _l2MessageIndex,
433:             l2TxNumberInBatch: _l2TxNumberInBatch
434:         });
435:         (l1Receiver, l1Token, amount) = _checkWithdrawal(_chainId, messageParams, _message, _merkleProof);
436: 
437:         if (!hyperbridgingEnabled[_chainId]) {
438:             // Check that the chain has sufficient balance
439:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds
440:             chainBalance[_chainId][l1Token] -= amount;
441:         }
442: 
443:         if (l1Token == ETH_TOKEN_ADDRESS) {
444:             bool callSuccess;
445:             // Low-level assembly call, to avoid any memory copying (save gas)
446:             assembly {
447:                 callSuccess := call(gas(), l1Receiver, amount, 0, 0, 0, 0)
448:             }
449:             require(callSuccess, "ShB: withdraw failed");
450:         } else {
451:             // Withdraw funds
452:             IERC20(l1Token).safeTransfer(l1Receiver, amount);
453:         }
454:         emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);
455:     }

//@audit the following two maps should be combined : `hyperbridgingEnabled` and `l2BridgeAddress`
554:     function depositLegacyErc20Bridge(
555:         address _prevMsgSender,
556:         address _l2Receiver,
557:         address _l1Token,
558:         uint256 _amount,
559:         uint256 _l2TxGasLimit,
560:         uint256 _l2TxGasPerPubdataByte,
561:         address _refundRecipient
562:     ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
565: 
566:         // Note that funds have been transferred to this contract in the legacy ERC20 bridge.
567:         if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {
568:             chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
569:         }
570: 
571:         bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);
572: 
573:         {
574:             // If the refund recipient is not specified, the refund will be sent to the sender of the transaction.
575:             // Otherwise, the refund will be sent to the specified address.
576:             // If the recipient is a contract on L1, the address alias will be applied.
577:             address refundRecipient = _refundRecipient;
578:             if (_refundRecipient == address(0)) {
579:                 refundRecipient = _prevMsgSender != tx.origin
580:                     ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
581:                     : _prevMsgSender;
582:             }
583: 
584:             L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
585:                 chainId: ERA_CHAIN_ID,
586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
587:                 mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
588:                 l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
589:                 l2Calldata: l2TxCalldata,
590:                 l2GasLimit: _l2TxGasLimit,
591:                 l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
592:                 factoryDeps: new bytes[](0),
593:                 refundRecipient: refundRecipient
594:             });
595:             l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
596:         }
597: 
598:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
599:         // Save the deposited amount to claim funds on L1 if the deposit failed on L2
600:         depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;
601: 
602:         emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
603:     }

//@audit the following two maps should be combined : `hyperbridgingEnabled` and `depositHappened`
554:     function depositLegacyErc20Bridge(
555:         address _prevMsgSender,
556:         address _l2Receiver,
557:         address _l1Token,
558:         uint256 _amount,
559:         uint256 _l2TxGasLimit,
560:         uint256 _l2TxGasPerPubdataByte,
561:         address _refundRecipient
562:     ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
565: 
566:         // Note that funds have been transferred to this contract in the legacy ERC20 bridge.
567:         if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {
568:             chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
569:         }
570: 
571:         bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);
572: 
573:         {
574:             // If the refund recipient is not specified, the refund will be sent to the sender of the transaction.
575:             // Otherwise, the refund will be sent to the specified address.
576:             // If the recipient is a contract on L1, the address alias will be applied.
577:             address refundRecipient = _refundRecipient;
578:             if (_refundRecipient == address(0)) {
579:                 refundRecipient = _prevMsgSender != tx.origin
580:                     ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
581:                     : _prevMsgSender;
582:             }
583: 
584:             L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
585:                 chainId: ERA_CHAIN_ID,
586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
587:                 mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
588:                 l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
589:                 l2Calldata: l2TxCalldata,
590:                 l2GasLimit: _l2TxGasLimit,
591:                 l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
592:                 factoryDeps: new bytes[](0),
593:                 refundRecipient: refundRecipient
594:             });
595:             l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
596:         }
597: 
598:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
599:         // Save the deposited amount to claim funds on L1 if the deposit failed on L2
600:         depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;
601: 
602:         emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
603:     }

//@audit the following two maps should be combined : `hyperbridgingEnabled` and `chainBalance`
554:     function depositLegacyErc20Bridge(
555:         address _prevMsgSender,
556:         address _l2Receiver,
557:         address _l1Token,
558:         uint256 _amount,
559:         uint256 _l2TxGasLimit,
560:         uint256 _l2TxGasPerPubdataByte,
561:         address _refundRecipient
562:     ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
565: 
566:         // Note that funds have been transferred to this contract in the legacy ERC20 bridge.
567:         if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {
568:             chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
569:         }
570: 
571:         bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);
572: 
573:         {
574:             // If the refund recipient is not specified, the refund will be sent to the sender of the transaction.
575:             // Otherwise, the refund will be sent to the specified address.
576:             // If the recipient is a contract on L1, the address alias will be applied.
577:             address refundRecipient = _refundRecipient;
578:             if (_refundRecipient == address(0)) {
579:                 refundRecipient = _prevMsgSender != tx.origin
580:                     ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
581:                     : _prevMsgSender;
582:             }
583: 
584:             L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
585:                 chainId: ERA_CHAIN_ID,
586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
587:                 mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
588:                 l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
589:                 l2Calldata: l2TxCalldata,
590:                 l2GasLimit: _l2TxGasLimit,
591:                 l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
592:                 factoryDeps: new bytes[](0),
593:                 refundRecipient: refundRecipient
594:             });
595:             l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
596:         }
597: 
598:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
599:         // Save the deposited amount to claim funds on L1 if the deposit failed on L2
600:         depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;
601: 
602:         emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
603:     }

//@audit the following two maps should be combined : `l2BridgeAddress` and `depositHappened`
554:     function depositLegacyErc20Bridge(
555:         address _prevMsgSender,
556:         address _l2Receiver,
557:         address _l1Token,
558:         uint256 _amount,
559:         uint256 _l2TxGasLimit,
560:         uint256 _l2TxGasPerPubdataByte,
561:         address _refundRecipient
562:     ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
565: 
566:         // Note that funds have been transferred to this contract in the legacy ERC20 bridge.
567:         if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {
568:             chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
569:         }
570: 
571:         bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);
572: 
573:         {
574:             // If the refund recipient is not specified, the refund will be sent to the sender of the transaction.
575:             // Otherwise, the refund will be sent to the specified address.
576:             // If the recipient is a contract on L1, the address alias will be applied.
577:             address refundRecipient = _refundRecipient;
578:             if (_refundRecipient == address(0)) {
579:                 refundRecipient = _prevMsgSender != tx.origin
580:                     ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
581:                     : _prevMsgSender;
582:             }
583: 
584:             L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
585:                 chainId: ERA_CHAIN_ID,
586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
587:                 mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
588:                 l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
589:                 l2Calldata: l2TxCalldata,
590:                 l2GasLimit: _l2TxGasLimit,
591:                 l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
592:                 factoryDeps: new bytes[](0),
593:                 refundRecipient: refundRecipient
594:             });
595:             l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
596:         }
597: 
598:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
599:         // Save the deposited amount to claim funds on L1 if the deposit failed on L2
600:         depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;
601: 
602:         emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
603:     }

//@audit the following two maps should be combined : `l2BridgeAddress` and `chainBalance`
554:     function depositLegacyErc20Bridge(
555:         address _prevMsgSender,
556:         address _l2Receiver,
557:         address _l1Token,
558:         uint256 _amount,
559:         uint256 _l2TxGasLimit,
560:         uint256 _l2TxGasPerPubdataByte,
561:         address _refundRecipient
562:     ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
565: 
566:         // Note that funds have been transferred to this contract in the legacy ERC20 bridge.
567:         if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {
568:             chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
569:         }
570: 
571:         bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);
572: 
573:         {
574:             // If the refund recipient is not specified, the refund will be sent to the sender of the transaction.
575:             // Otherwise, the refund will be sent to the specified address.
576:             // If the recipient is a contract on L1, the address alias will be applied.
577:             address refundRecipient = _refundRecipient;
578:             if (_refundRecipient == address(0)) {
579:                 refundRecipient = _prevMsgSender != tx.origin
580:                     ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
581:                     : _prevMsgSender;
582:             }
583: 
584:             L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
585:                 chainId: ERA_CHAIN_ID,
586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
587:                 mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
588:                 l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
589:                 l2Calldata: l2TxCalldata,
590:                 l2GasLimit: _l2TxGasLimit,
591:                 l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
592:                 factoryDeps: new bytes[](0),
593:                 refundRecipient: refundRecipient
594:             });
595:             l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
596:         }
597: 
598:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
599:         // Save the deposited amount to claim funds on L1 if the deposit failed on L2
600:         depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;
601: 
602:         emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
603:     }

//@audit the following two maps should be combined : `depositHappened` and `chainBalance`
554:     function depositLegacyErc20Bridge(
555:         address _prevMsgSender,
556:         address _l2Receiver,
557:         address _l1Token,
558:         uint256 _amount,
559:         uint256 _l2TxGasLimit,
560:         uint256 _l2TxGasPerPubdataByte,
561:         address _refundRecipient
562:     ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
565: 
566:         // Note that funds have been transferred to this contract in the legacy ERC20 bridge.
567:         if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {
568:             chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
569:         }
570: 
571:         bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);
572: 
573:         {
574:             // If the refund recipient is not specified, the refund will be sent to the sender of the transaction.
575:             // Otherwise, the refund will be sent to the specified address.
576:             // If the recipient is a contract on L1, the address alias will be applied.
577:             address refundRecipient = _refundRecipient;
578:             if (_refundRecipient == address(0)) {
579:                 refundRecipient = _prevMsgSender != tx.origin
580:                     ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
581:                     : _prevMsgSender;
582:             }
583: 
584:             L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
585:                 chainId: ERA_CHAIN_ID,
586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
587:                 mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
588:                 l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
589:                 l2Calldata: l2TxCalldata,
590:                 l2GasLimit: _l2TxGasLimit,
591:                 l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
592:                 factoryDeps: new bytes[](0),
593:                 refundRecipient: refundRecipient
594:             });
595:             l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
596:         }
597: 
598:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
599:         // Save the deposited amount to claim funds on L1 if the deposit failed on L2
600:         depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;
601: 
602:         emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
603:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L148-L169) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L182-L228), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L182-L228), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L182-L228), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L303-L368), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L303-L368), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L303-L368), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L409-L455), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L409-L455), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L409-L455), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L554-L603), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L554-L603), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L554-L603), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L554-L603), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L554-L603), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L554-L603)


```solidity

File: contracts/bridgehub/Bridgehub.sol

//@audit the following two maps should be combined : `stateTransitionManager` and `baseToken`
114:     function createNewChain(
115:         uint256 _chainId,
116:         address _stateTransitionManager,
117:         address _baseToken,
118:         uint256, //_salt
119:         address _admin,
120:         bytes calldata _initData
121:     ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
122:         require(_chainId != 0, "Bridgehub: chainId cannot be 0");
123:         require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");
124: 
125:         require(
126:             stateTransitionManagerIsRegistered[_stateTransitionManager],
127:             "Bridgehub: state transition not registered"
128:         );
129:         require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");
130:         require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
131: 
132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");
133: 
134:         stateTransitionManager[_chainId] = _stateTransitionManager;
135:         baseToken[_chainId] = _baseToken;
136: 
137:         IStateTransitionManager(_stateTransitionManager).createNewChain(
138:             _chainId,
139:             _baseToken,
140:             address(sharedBridge),
141:             _admin,
142:             _initData
143:         );
144: 
145:         emit NewChain(_chainId, _stateTransitionManager, _admin);
146:         return _chainId;
147:     }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L114-L147) 


</details>


### [GAS&#x2011;81] Consider pre-calculating the address of `address(this)` to save gas 
Use `foundry`'s [`script.sol`](https://book.getfoundry.sh/reference/forge-std/compute-create-address) or `solady`'s [`LibRlp.sol`](https://github.com/Vectorized/solady/blob/main/src/utils/LibRLP.sol) to save the value in a constant, which will avoid having to spend gas to push the value on the stack every time it's used.


*There are 21 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/ContractDeployer.sol

29:         require(msg.sender == address(this), "Callable only by self");

333:                 BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo(address(this), _newAddress, value);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L29-L29) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L333-L333)


```solidity

File: contracts/DefaultAccount.sol

47:         if (codeAddress != address(this)) {

100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

188:         return recoveredAddress == address(this) && recoveredAddress != address(0);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L47-L47) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L100-L100), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L188-L188)


```solidity

File: contracts/L1Messenger.sol

129:             sender: address(this),


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L129-L129) 


```solidity

File: contracts/L2BaseToken.sol

106:             balance[address(this)] -= amount;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L106-L106) 


```solidity

File: contracts/MsgValueSimulator.sol

60:         require(to != address(this), "MsgValueSimulator calls itself");


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/MsgValueSimulator.sol#L60-L60) 


```solidity

File: contracts/libraries/TransactionHelper.sol

377:             uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L377-L377) 


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

65:         uint256 amount = IERC20(_token).balanceOf(address(this));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L65-L65) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

118:             uint256 balanceBefore = address(this).balance;

120:             uint256 balanceAfter = address(this).balance;

127:             uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

131:             uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

174:         uint256 balanceBefore = _token.balanceOf(address(this));

175:         _token.safeTransferFrom(_from, address(this), _amount);

176:         uint256 balanceAfter = _token.balanceOf(address(this));


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L118-L118) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L120-L120), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L127-L127), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L131-L131), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L174-L174), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L175-L175), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L176-L176)


```solidity

File: contracts/governance/Governance.sol

59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L59-L59) 


```solidity

File: contracts/state-transition/StateTransitionManager.sol

265:             bytes32(uint256(uint160(address(this)))),


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L265-L265) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

41:         uint256 amount = address(this).balance;


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L41-L41) 


```solidity

File: contracts/bridge/L2SharedBridge.sol

153:             L2ContractHelper.computeCreate2Address(address(this), salt, l2TokenProxyBytecodeHash, constructorInputHash);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L153-L153) 


</details>


### [GAS&#x2011;82] Avoid emitting event on every iteration 
Emitting events within a loop can cause significant gas consumption due to repeated I/O operations. Instead, accumulate changes in memory and emit a single event post-loop with aggregated data. This approach improves contract efficiency, reduces gas costs, and simplifies event tracking for event listeners.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/state-transition/chain-deps/facets/Executor.sol

257:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
258:             _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));
259: 
260:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
261:             emit BlockCommit(
262:                 _lastCommittedBatchData.batchNumber,
263:                 _lastCommittedBatchData.batchHash,
264:                 _lastCommittedBatchData.commitment
265:             );
266:         }

289:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
290:             // The upgrade transaction must only be included in the first batch.
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
292:             _lastCommittedBatchData = _commitOneBatch(
293:                 _lastCommittedBatchData,
294:                 _newBatchesData[i],
295:                 expectedUpgradeTxHash
296:             );
297: 
298:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
299:             emit BlockCommit(
300:                 _lastCommittedBatchData.batchNumber,
301:                 _lastCommittedBatchData.batchHash,
302:                 _lastCommittedBatchData.commitment
303:             );
304:         }

351:         for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
352:             _executeOneBatch(_batchesData[i], i);
353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
354:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L257-L266) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L289-L304), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L351-L354)


</details>


### [GAS&#x2011;83] Memory-safe annotation missing 
Use `assembly (\"memory- safe\") { ... }` for the assembly blocks below since they dont't read or modify memory, and therefore are [memory-safe](https://docs.soliditylang.org/en/latest/assembly.html#memory-safety). This will help the optimizer to create more optimal gas-efficient code. Use the comment variant if prior to Solidity version 0.8.13


*There are 71 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/AccountCodeStorage.sol

70:         assembly {
71:             sstore(addressAsKey, _hash)
72:         }

81:         assembly {
82:             codeHash := sload(addressAsKey)
83:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L70-L72) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L81-L83)


```solidity

File: contracts/ComplexUpgrader.sol

26:         assembly {
27:             if iszero(success) {
28:                 revert(add(returnData, 0x20), mload(returnData))
29:             }
30:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ComplexUpgrader.sol#L26-L30) 


```solidity

File: contracts/DefaultAccount.sol

31:             assembly {
32:                 return(0, 0)
33:             }

49:             assembly {
50:                 return(0, 0)
51:             }

168:         assembly {
169:             r := mload(add(_signature, 0x20))
170:             s := mload(add(_signature, 0x40))
171:             v := and(mload(add(_signature, 0x41)), 0xff)
172:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L31-L33) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L49-L51), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L168-L172)


```solidity

File: contracts/KnownCodesStorage.sol

55:             assembly {
56:                 sstore(_bytecodeHash, 1)
57:             }

66:         assembly {
67:             marker := sload(_hash)
68:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L55-L57) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L66-L68)


```solidity

File: contracts/MsgValueSimulator.sol

69:                 assembly {
70:                     revert(0, 0)
71:                 }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/MsgValueSimulator.sol#L69-L71) 


```solidity

File: contracts/PubdataChunkPublisher.sol

30:         assembly {
31:             // The pointer to the allocated memory above. We skip 32 bytes to avoid overwriting the length.
32:             let ptr := add(totalBlobs, 0x20)
33:             calldatacopy(ptr, _pubdata.offset, _pubdata.length)
34:         }

46:             assembly {
47:                 // The pointer to the allocated memory above skipping the length.
48:                 let ptr := add(totalBlobs, 0x20)
49:                 blobHash := keccak256(add(ptr, start), BLOB_SIZE_BYTES)
50:             }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L30-L34) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L46-L50)


```solidity

File: contracts/libraries/EfficientCall.sol

135:             assembly {
136:                 success := call(_address, callAddr, 0, 0, 0xFFFF, 0, 0)
137:             }

148:             assembly {
149:                 success := call(msgValueSimulator, callAddr, _value, _address, 0xFFFF, forwardMask, 0)
150:             }

163:         assembly {
164:             success := staticcall(_address, callAddr, 0, 0xFFFF, 0, 0)
165:         }

177:         assembly {
178:             success := delegatecall(_address, callAddr, 0, 0xFFFF, 0, 0)
179:         }

203:         assembly {
204:             // Clearing values before usage in assembly, since Solidity
205:             // doesn't do it by default
206:             _whoToMimic := and(_whoToMimic, cleanupMask)
207: 
208:             success := call(_address, callAddr, 0, 0, _whoToMimic, 0, 0)
209:         }

218:             assembly {
219:                 size := returndatasize()
220:             }

223:             assembly {
224:                 returndatacopy(add(returnData, 0x20), 0, size)
225:             }

233:         assembly {
234:             let size := returndatasize()
235:             returndatacopy(0, 0, size)
236:             revert(0, size)
237:         }

254:         assembly {
255:             dataOffset := _data.offset
256:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L135-L137) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L148-L150), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L163-L165), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L177-L179), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L203-L209), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L218-L220), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L223-L225), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L233-L237), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L254-L256)


```solidity

File: contracts/libraries/RLPEncoder.sol

16:         assembly {
17:             // In the first byte we write the encoded length as 0x80 + 0x14 == 0x94.
18:             mstore(add(encoded, 0x20), 0x9400000000000000000000000000000000000000000000000000000000000000)
19:             // Write address data without stripping zeros.
20:             mstore(add(encoded, 0x21), shiftedVal)
21:         }

39:                 assembly {
40:                     mstore(add(encoded, 0x21), shiftedVal)
41:                 }

74:                 assembly {
75:                     mstore(add(encoded, 0x21), shiftedVal)
76:                 }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L16-L21) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L39-L41), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L74-L76)


```solidity

File: contracts/libraries/SystemContractHelper.sol

50:         assembly {
51:             // Ensuring that the type is bool
52:             _isService := and(_isService, 1)
53:             // This `success` is always 0, but the method always succeeds
54:             // (except for the cases when there is not enough gas)
55:             let success := call(_isService, callAddr, _key, _value, 0xFFFF, 0, 0)
56:         }

65:         assembly {
66:             addr := staticcall(0, callAddr, 0, 0xFFFF, 0, 0)
67:         }

76:         assembly {
77:             pop(staticcall(0, callAddr, 0, 0xFFFF, 0, 0))
78:         }

87:         assembly {
88:             pop(staticcall(_farCallAbi, callAddr, 0, 0xFFFF, 0, 0))
89:         }

097:         assembly {
098:             // Clearing input params as they are not cleaned by Solidity by default
099:             _value := and(_value, cleanupMask)
100:             pop(staticcall(_value, callAddr, 0, 0xFFFF, 0, 0))
101:         }

109:         assembly {
110:             // Clearing input params as they are not cleaned by Solidity by default
111:             _shrink := and(_shrink, cleanupMask)
112:             pop(staticcall(_shrink, callAddr, 0, 0xFFFF, 0, 0))
113:         }

158:         assembly {
159:             // Clearing input params as they are not cleaned by Solidity by default
160:             params := and(params, cleanupMask)
161:             success := staticcall(_rawParams, callAddr, params, 0xFFFF, 0, 0)
162:         }

171:         assembly {
172:             // Clearing input params as they are not cleaned by Solidity by default
173:             _value := and(_value, cleanupMask)
174:             success := call(0, callAddr, _value, 0, 0xFFFF, 0, 0)
175:         }

183:         assembly {
184:             pop(call(initializer, callAddr, value1, 0, 0xFFFF, 0, 0))
185:         }

193:         assembly {
194:             pop(call(value1, callAddr, value2, 0, 0xFFFF, 0, 0))
195:         }

205:         assembly {
206:             meta := staticcall(0, callAddr, 0, 0xFFFF, 0, 0)
207:         }

298:         assembly {
299:             callFlags := staticcall(0, callAddr, 0, 0xFFFF, 0, 0)
300:         }

309:         assembly {
310:             ptr := staticcall(0, callAddr, 0, 0xFFFF, 0, 0)
311:         }

322:         assembly {
323:             extraAbiData := staticcall(index, callAddr, 0, 0xFFFF, 0, 0)
324:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L50-L56) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L65-L67), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L76-L78), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L87-L89), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L97-L101), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L109-L113), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L158-L162), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L171-L175), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L183-L185), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L193-L195), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L205-L207), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L298-L300), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L309-L311), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L322-L324)


```solidity

File: contracts/libraries/SystemContractsCaller.sol

80:         assembly {
81:             dataStart := add(data, 0x20)
82:         }

100:             assembly {
101:                 success := call(to, callAddr, 0, 0, farCallAbi, 0, 0)
102:             }

109:             assembly {
110:                 success := call(msgValueSimulator, callAddr, value, to, farCallAbi, forwardMask, 0)
111:             }

132:         assembly {
133:             size := returndatasize()
134:         }

137:         assembly {
138:             returndatacopy(add(returnData, 0x20), 0, size)
139:         }

160:             assembly {
161:                 let size := mload(returnData)
162:                 revert(add(returnData, 0x20), size)
163:             }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L80-L82) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L100-L102), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L109-L111), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L132-L134), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L137-L139), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L160-L163)


```solidity

File: contracts/libraries/TransactionHelper.sol

399:         assembly {
400:             success := call(gas(), bootloaderAddr, amount, 0, 0, 0, 0)
401:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L399-L401) 


```solidity

File: contracts/libraries/UnsafeBytesCalldata.sol

20:         assembly {
21:             let offset := sub(_bytes.offset, 30)
22:             result := calldataload(add(offset, _start))
23:         }

27:         assembly {
28:             let offset := sub(_bytes.offset, 28)
29:             result := calldataload(add(offset, _start))
30:         }

34:         assembly {
35:             let offset := sub(_bytes.offset, 24)
36:             result := calldataload(add(offset, _start))
37:         }

41:         assembly {
42:             result := calldataload(add(_bytes.offset, _start))
43:         }

47:         assembly {
48:             result := calldataload(add(_bytes.offset, _start))
49:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L20-L23) , [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L27-L30), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L34-L37), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L41-L43), [link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L47-L49)


```solidity

File: contracts/bridge/L1SharedBridge.sol

357:             assembly {
358:                 callSuccess := call(gas(), _depositSender, _amount, 0, 0, 0, 0)
359:             }

446:             assembly {
447:                 callSuccess := call(gas(), l1Receiver, amount, 0, 0, 0, 0)
448:             }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L357-L359) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L446-L448)


```solidity

File: contracts/common/ReentrancyGuard.sol

52:         assembly {
53:             lockSlotOldValue := sload(LOCK_FLAG_ADDRESS)
54:             sstore(LOCK_FLAG_ADDRESS, _NOT_ENTERED)
55:         }

70:         assembly {
71:             _status := sload(LOCK_FLAG_ADDRESS)
72:         }

78:         assembly {
79:             sstore(LOCK_FLAG_ADDRESS, _ENTERED)
80:         }

86:         assembly {
87:             sstore(LOCK_FLAG_ADDRESS, _NOT_ENTERED)
88:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/ReentrancyGuard.sol#L52-L55) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/ReentrancyGuard.sol#L70-L72), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/ReentrancyGuard.sol#L78-L80), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/ReentrancyGuard.sol#L86-L88)


```solidity

File: contracts/common/libraries/UnsafeBytes.sol

20:         assembly {
21:             offset := add(_start, 4)
22:             result := mload(add(_bytes, offset))
23:         }

27:         assembly {
28:             offset := add(_start, 20)
29:             result := mload(add(_bytes, offset))
30:         }

34:         assembly {
35:             offset := add(_start, 32)
36:             result := mload(add(_bytes, offset))
37:         }

41:         assembly {
42:             offset := add(_start, 32)
43:             result := mload(add(_bytes, offset))
44:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UnsafeBytes.sol#L20-L23) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UnsafeBytes.sol#L27-L30), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UnsafeBytes.sol#L34-L37), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UnsafeBytes.sol#L41-L44)


```solidity

File: contracts/governance/Governance.sol

229:                 assembly {
230:                     revert(add(returnData, 0x20), mload(returnData))
231:                 }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L229-L231) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

227:         assembly {
228:             // Copy function signature and arguments from calldata at zero position into memory at pointer position
229:             calldatacopy(0, 0, calldatasize())
230:             // Call method of the hyperchain diamond contract returns 0 on error
231:             let result := call(gas(), contractAddress, 0, 0, calldatasize(), 0, 0)
232:             // Get the size of the last return data
233:             let size := returndatasize()
234:             // Copy the size length of bytes from return data at zero position to pointer position
235:             returndatacopy(0, 0, size)
236:             // Depending on the result value
237:             switch result
238:             case 0 {
239:                 // End execution and revert state changes
240:                 revert(0, size)
241:             }
242:             default {
243:                 // Return data with length of size at pointers position
244:                 return(0, size)
245:             }
246:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L227-L246) 


```solidity

File: contracts/state-transition/chain-deps/DiamondProxy.sol

33:         assembly {
34:             // The pointer to the free memory slot
35:             let ptr := mload(0x40)
36:             // Copy function signature and arguments from calldata at zero position into memory at pointer position
37:             calldatacopy(ptr, 0, calldatasize())
38:             // Delegatecall method of the implementation contract returns 0 on error
39:             let result := delegatecall(gas(), facetAddress, ptr, calldatasize(), 0, 0)
40:             // Get the size of the last return data
41:             let size := returndatasize()
42:             // Copy the size length of bytes from return data at zero position to pointer position
43:             returndatacopy(ptr, 0, size)
44:             // Depending on the result value
45:             switch result
46:             case 0 {
47:                 // End execution and revert state changes
48:                 revert(ptr, size)
49:             }
50:             default {
51:                 // Return data with length of size at pointers position
52:                 return(ptr, size)
53:             }
54:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondProxy.sol#L33-L54) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

360:             assembly {
361:                 mstore(add(hashedFactoryDeps, mul(add(i, 1), 32)), hashedBytecode)
362:             }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L360-L362) 


```solidity

File: contracts/state-transition/libraries/Diamond.sol

89:         assembly {
90:             diamondStorage.slot := position
91:         }

290:                 assembly {
291:                     revert(add(data, 0x20), mload(data))
292:                 }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L89-L91) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L290-L292)


```solidity

File: contracts/state-transition/libraries/Merkle.sol

41:         assembly {
42:             mstore(0x00, _lhs)
43:             mstore(0x20, _rhs)
44:             result := keccak256(0x00, 0x40)
45:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L41-L45) 


```solidity

File: contracts/SystemContractsCaller.sol

41:         assembly {
42:             dataStart := add(data, 0x20)
43:         }

61:             assembly {
62:                 success := call(to, callAddr, 0, 0, farCallAbi, 0, 0)
63:             }

70:             assembly {
71:                 success := call(msgValueSimulator, callAddr, value, to, farCallAbi, forwardMask, 0)
72:             }

85:         assembly {
86:             size := returndatasize()
87:         }

90:         assembly {
91:             returndatacopy(add(returnData, 0x20), 0, size)
92:         }


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L41-L43) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L61-L63), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L70-L72), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L85-L87), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L90-L92)


</details>


### [GAS&#x2011;84] Reduce deployment costs by tweaking contracts' metadata 
See [this](https://www.rareskills.io/post/solidity-metadata) link, at its bottom, for full details


*There are 103 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/AccountCodeStorage.sol

22: contract AccountCodeStorage is IAccountCodeStorage {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/AccountCodeStorage.sol#L22-L22) 


```solidity

File: contracts/BootloaderUtilities.sol

16: contract BootloaderUtilities is IBootloaderUtilities {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/BootloaderUtilities.sol#L16-L16) 


```solidity

File: contracts/ComplexUpgrader.sol

14: contract ComplexUpgrader is IComplexUpgrader {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ComplexUpgrader.sol#L14-L14) 


```solidity

File: contracts/Compressor.sol

22: contract Compressor is ICompressor, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/Compressor.sol#L22-L22) 


```solidity

File: contracts/ContractDeployer.sol

23: contract ContractDeployer is IContractDeployer, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ContractDeployer.sol#L23-L23) 


```solidity

File: contracts/DefaultAccount.sol

19: contract DefaultAccount is IAccount {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/DefaultAccount.sol#L19-L19) 


```solidity

File: contracts/EmptyContract.sol

10: contract EmptyContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/EmptyContract.sol#L10-L10) 


```solidity

File: contracts/ImmutableSimulator.sol

18: contract ImmutableSimulator is IImmutableSimulator {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/ImmutableSimulator.sol#L18-L18) 


```solidity

File: contracts/KnownCodesStorage.sol

18: contract KnownCodesStorage is IKnownCodesStorage, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/KnownCodesStorage.sol#L18-L18) 


```solidity

File: contracts/L1Messenger.sol

25: contract L1Messenger is IL1Messenger, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L1Messenger.sol#L25-L25) 


```solidity

File: contracts/L2BaseToken.sol

18: contract L2BaseToken is IBaseToken, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/L2BaseToken.sol#L18-L18) 


```solidity

File: contracts/MsgValueSimulator.sol

19: contract MsgValueSimulator is ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/MsgValueSimulator.sol#L19-L19) 


```solidity

File: contracts/NonceHolder.sol

27: contract NonceHolder is INonceHolder, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/NonceHolder.sol#L27-L27) 


```solidity

File: contracts/PubdataChunkPublisher.sol

16: contract PubdataChunkPublisher is IPubdataChunkPublisher, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/PubdataChunkPublisher.sol#L16-L16) 


```solidity

File: contracts/SystemContext.sol

17: contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L17-L17) 


```solidity

File: contracts/interfaces/IAccount.sol

9: interface IAccount {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IAccount.sol#L9-L9) 


```solidity

File: contracts/interfaces/IAccountCodeStorage.sol

5: interface IAccountCodeStorage {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IAccountCodeStorage.sol#L5-L5) 


```solidity

File: contracts/interfaces/IBaseToken.sol

5: interface IBaseToken {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IBaseToken.sol#L5-L5) 


```solidity

File: contracts/interfaces/IBootloaderUtilities.sol

7: interface IBootloaderUtilities {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IBootloaderUtilities.sol#L7-L7) 


```solidity

File: contracts/interfaces/IComplexUpgrader.sol

10: interface IComplexUpgrader {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IComplexUpgrader.sol#L10-L10) 


```solidity

File: contracts/interfaces/ICompressor.sol

18: interface ICompressor {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ICompressor.sol#L18-L18) 


```solidity

File: contracts/interfaces/IContractDeployer.sol

5: interface IContractDeployer {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IContractDeployer.sol#L5-L5) 


```solidity

File: contracts/interfaces/IImmutableSimulator.sol

10: interface IImmutableSimulator {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IImmutableSimulator.sol#L10-L10) 


```solidity

File: contracts/interfaces/IKnownCodesStorage.sol

11: interface IKnownCodesStorage {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IKnownCodesStorage.sol#L11-L11) 


```solidity

File: contracts/interfaces/IL1Messenger.sol

40: interface IL1Messenger {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IL1Messenger.sol#L40-L40) 


```solidity

File: contracts/interfaces/IL2StandardToken.sol

5: interface IL2StandardToken {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IL2StandardToken.sol#L5-L5) 


```solidity

File: contracts/interfaces/IMailbox.sol

5: interface IMailbox {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IMailbox.sol#L5-L5) 


```solidity

File: contracts/interfaces/INonceHolder.sol

13: interface INonceHolder {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/INonceHolder.sol#L13-L13) 


```solidity

File: contracts/interfaces/IPaymaster.sol

14: interface IPaymaster {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IPaymaster.sol#L14-L14) 


```solidity

File: contracts/interfaces/IPaymasterFlow.sol

12: interface IPaymasterFlow {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IPaymasterFlow.sol#L12-L12) 


```solidity

File: contracts/interfaces/IPubdataChunkPublisher.sol

9: interface IPubdataChunkPublisher {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/IPubdataChunkPublisher.sol#L9-L9) 


```solidity

File: contracts/interfaces/ISystemContext.sol

11: interface ISystemContext {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContext.sol#L11-L11) 


```solidity

File: contracts/interfaces/ISystemContextDeprecated.sol

10: interface ISystemContextDeprecated {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContextDeprecated.sol#L10-L10) 


```solidity

File: contracts/interfaces/ISystemContract.sol

17: abstract contract ISystemContract {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/interfaces/ISystemContract.sol#L17-L17) 


```solidity

File: contracts/libraries/EfficientCall.sol

32: library EfficientCall {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/EfficientCall.sol#L32-L32) 


```solidity

File: contracts/libraries/RLPEncoder.sol

10: library RLPEncoder {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/RLPEncoder.sol#L10-L10) 


```solidity

File: contracts/libraries/SystemContractHelper.sol

41: library SystemContractHelper {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractHelper.sol#L41-L41) 


```solidity

File: contracts/libraries/SystemContractsCaller.sol

68: library SystemContractsCaller {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/SystemContractsCaller.sol#L68-L68) 


```solidity

File: contracts/libraries/TransactionHelper.sol

78: library TransactionHelper {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/TransactionHelper.sol#L78-L78) 


```solidity

File: contracts/libraries/UnsafeBytesCalldata.sol

18: library UnsafeBytesCalldata {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/UnsafeBytesCalldata.sol#L18-L18) 


```solidity

File: contracts/libraries/Utils.sol

11: library Utils {


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/libraries/Utils.sol#L11-L11) 


```solidity

File: contracts/bridge/L1ERC20Bridge.sol

19: contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1ERC20Bridge.sol#L19-L19) 


```solidity

File: contracts/bridge/L1SharedBridge.sol

30: contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/L1SharedBridge.sol#L30-L30) 


```solidity

File: contracts/bridge/interfaces/IL1ERC20Bridge.sol

11: interface IL1ERC20Bridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11-L11) 


```solidity

File: contracts/bridge/interfaces/IL1SharedBridge.sol

12: interface IL1SharedBridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL1SharedBridge.sol#L12-L12) 


```solidity

File: contracts/bridge/interfaces/IL2Bridge.sol

6: interface IL2Bridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IL2Bridge.sol#L6-L6) 


```solidity

File: contracts/bridge/interfaces/IWETH9.sol

4: interface IWETH9 {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridge/interfaces/IWETH9.sol#L4-L4) 


```solidity

File: contracts/bridgehub/Bridgehub.sol

16: contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/Bridgehub.sol#L16-L16) 


```solidity

File: contracts/bridgehub/IBridgehub.sol

42: interface IBridgehub {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/bridgehub/IBridgehub.sol#L42-L42) 


```solidity

File: contracts/common/ReentrancyGuard.sol

25: abstract contract ReentrancyGuard {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/ReentrancyGuard.sol#L25-L25) 


```solidity

File: contracts/common/interfaces/IL2ContractDeployer.sol

9: interface IL2ContractDeployer {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/interfaces/IL2ContractDeployer.sol#L9-L9) 


```solidity

File: contracts/common/libraries/L2ContractHelper.sol

10: library L2ContractHelper {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/L2ContractHelper.sol#L10-L10) 


```solidity

File: contracts/common/libraries/UncheckedMath.sol

10: library UncheckedMath {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UncheckedMath.sol#L10-L10) 


```solidity

File: contracts/common/libraries/UnsafeBytes.sol

18: library UnsafeBytes {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/common/libraries/UnsafeBytes.sol#L18-L18) 


```solidity

File: contracts/governance/Governance.sol

20: contract Governance is IGovernance, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/Governance.sol#L20-L20) 


```solidity

File: contracts/governance/IGovernance.sol

8: interface IGovernance {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/governance/IGovernance.sol#L8-L8) 


```solidity

File: contracts/state-transition/IStateTransitionManager.sol

26: interface IStateTransitionManager {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/IStateTransitionManager.sol#L26-L26) 


```solidity

File: contracts/state-transition/StateTransitionManager.sol

25: contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/StateTransitionManager.sol#L25-L25) 


```solidity

File: contracts/state-transition/ValidatorTimelock.sol

22: contract ValidatorTimelock is IExecutor, Ownable2Step {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/ValidatorTimelock.sol#L22-L22) 


```solidity

File: contracts/state-transition/chain-deps/DiamondInit.sol

17: contract DiamondInit is ZkSyncStateTransitionBase, IDiamondInit {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondInit.sol#L17-L17) 


```solidity

File: contracts/state-transition/chain-deps/DiamondProxy.sol

10: contract DiamondProxy {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/DiamondProxy.sol#L10-L10) 


```solidity

File: contracts/state-transition/chain-deps/facets/Admin.sol

18: contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Admin.sol#L18-L18) 


```solidity

File: contracts/state-transition/chain-deps/facets/Executor.sol

22: contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Executor.sol#L22-L22) 


```solidity

File: contracts/state-transition/chain-deps/facets/Getters.sol

20: contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Getters.sol#L20-L20) 


```solidity

File: contracts/state-transition/chain-deps/facets/Mailbox.sol

30: contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/Mailbox.sol#L30-L30) 


```solidity

File: contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

11: contract ZkSyncStateTransitionBase is ReentrancyGuard {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L11-L11) 


```solidity

File: contracts/state-transition/chain-interfaces/IAdmin.sol

13: interface IAdmin is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IAdmin.sol#L13-L13) 


```solidity

File: contracts/state-transition/chain-interfaces/IDiamondInit.sol

61: interface IDiamondInit {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IDiamondInit.sol#L61-L61) 


```solidity

File: contracts/state-transition/chain-interfaces/IExecutor.sol

73: interface IExecutor is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IExecutor.sol#L73-L73) 


```solidity

File: contracts/state-transition/chain-interfaces/IGetters.sol

13: interface IGetters is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IGetters.sol#L13-L13) 


```solidity

File: contracts/state-transition/chain-interfaces/ILegacyGetters.sol

11: interface ILegacyGetters is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L11-L11) 


```solidity

File: contracts/state-transition/chain-interfaces/IMailbox.sol

11: interface IMailbox is IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IMailbox.sol#L11-L11) 


```solidity

File: contracts/state-transition/chain-interfaces/IVerifier.sol

15: interface IVerifier {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IVerifier.sol#L15-L15) 


```solidity

File: contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol

15: interface IZkSyncStateTransition is IAdmin, IExecutor, IGetters, IMailbox {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L15-L15) 


```solidity

File: contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol

7: interface IZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L7-L7) 


```solidity

File: contracts/state-transition/l2-deps/ISystemContext.sol

4: interface ISystemContext {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/l2-deps/ISystemContext.sol#L4-L4) 


```solidity

File: contracts/state-transition/libraries/Diamond.sol

11: library Diamond {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Diamond.sol#L11-L11) 


```solidity

File: contracts/state-transition/libraries/LibMap.sol

8: library LibMap {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/LibMap.sol#L8-L8) 


```solidity

File: contracts/state-transition/libraries/Merkle.sol

9: library Merkle {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/Merkle.sol#L9-L9) 


```solidity

File: contracts/state-transition/libraries/PriorityQueue.sol

20: library PriorityQueue {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/PriorityQueue.sol#L20-L20) 


```solidity

File: contracts/state-transition/libraries/TransactionValidator.sol

13: library TransactionValidator {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/state-transition/libraries/TransactionValidator.sol#L13-L13) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgrade.sol

44: abstract contract BaseZkSyncUpgrade is ZkSyncStateTransitionBase {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgrade.sol#L44-L44) 


```solidity

File: contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

17: abstract contract BaseZkSyncUpgradeGenesis is BaseZkSyncUpgrade {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L17-L17) 


```solidity

File: contracts/upgrades/DefaultUpgrade.sol

10: contract DefaultUpgrade is BaseZkSyncUpgrade {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/DefaultUpgrade.sol#L10-L10) 


```solidity

File: contracts/upgrades/GenesisUpgrade.sol

11: contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/GenesisUpgrade.sol#L11-L11) 


```solidity

File: contracts/upgrades/IDefaultUpgrade.sol

7: interface IDefaultUpgrade {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/upgrades/IDefaultUpgrade.sol#L7-L7) 


```solidity

File: contracts/vendor/AddressAliasHelper.sol

21: library AddressAliasHelper {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum//contracts/vendor/AddressAliasHelper.sol#L21-L21) 


```solidity

File: contracts/ForceDeployUpgrader.sol

10: contract ForceDeployUpgrader {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/ForceDeployUpgrader.sol#L10-L10) 


```solidity

File: contracts/L2ContractHelper.sol

18: interface IL2Messenger {

30: interface IContractDeployer {

61: interface IBaseToken {

83: library L2ContractHelper {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L18-L18) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L30-L30), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L61-L61), [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/L2ContractHelper.sol#L83-L83)


```solidity

File: contracts/SystemContractsCaller.sol

26: library Utils {

36: library SystemContractsCaller {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L26-L26) , [link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/SystemContractsCaller.sol#L36-L36)


```solidity

File: contracts/bridge/L2SharedBridge.sol

23: contract L2SharedBridge is IL2SharedBridge, Initializable {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L23-L23) 


```solidity

File: contracts/bridge/L2StandardERC20.sol

15: contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L15-L15) 


```solidity

File: contracts/bridge/interfaces/IL1ERC20Bridge.sol

8: interface IL1ERC20Bridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL1ERC20Bridge.sol#L8-L8) 


```solidity

File: contracts/bridge/interfaces/IL1SharedBridge.sol

8: interface IL1SharedBridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL1SharedBridge.sol#L8-L8) 


```solidity

File: contracts/bridge/interfaces/IL2SharedBridge.sol

6: interface IL2SharedBridge {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL2SharedBridge.sol#L6-L6) 


```solidity

File: contracts/bridge/interfaces/IL2StandardToken.sol

5: interface IL2StandardToken {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/interfaces/IL2StandardToken.sol#L5-L5) 


```solidity

File: contracts/interfaces/IPaymaster.sol

14: interface IPaymaster {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/interfaces/IPaymaster.sol#L14-L14) 


```solidity

File: contracts/interfaces/IPaymasterFlow.sol

13: interface IPaymasterFlow {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/interfaces/IPaymasterFlow.sol#L13-L13) 


```solidity

File: contracts/vendor/AddressAliasHelper.sol

21: library AddressAliasHelper {


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/vendor/AddressAliasHelper.sol#L21-L21) 


</details>


### [GAS&#x2011;85] Use the inputs/results of assignments rather than re-reading state variables 
When a state variable is assigned, it saves gas to use the value being assigned, later in the function, rather than re-reading the state variable itself. If needed, it can also be stored to a local variable, and be used in that way. Both options avoid a Gwarmaccess (**100 gas**). Note that if the operation is, say `+=`, the assignment also results in a value which can be used. The instances below point to the first reference after the assignment, since later references are already covered by issues describing the caching of state variable values.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: contracts/SystemContext.sol

//@audit use result of assignment of currentVirtualL2BlockInfo, here
275:         BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;


```

[link](https://github.com/code-423n4/2024-03-zksync/tree/main/code/system-contracts//contracts/SystemContext.sol#L275-L275) 


```solidity

File: contracts/bridge/L2SharedBridge.sol

//@audit use result of assignment of l2TokenBeacon, here
66:             l2TokenBeacon.transferOwnership(_aliasedOwner);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2SharedBridge.sol#L66-L66) 


```solidity

File: contracts/bridge/L2StandardERC20.sol

//@audit use result of assignment of decimals_, here
101:         emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);


```

[link](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync//contracts/bridge/L2StandardERC20.sol#L101-L101) 


</details>
