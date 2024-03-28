
The content section shows only 10 examples, subsequent cases are listed as links.

## Summary

### Low Risk Issues

| |Issue|Instances|
|-|:-|:-:|
| [[L-01](#l-01)] | Large assembly blocks should have extensive comments | 2|
| [[L-02](#l-02)] | Missing checks for `address(0)` when assigning values to address state variables | 19|
| [[L-03](#l-03)] | Array lengths not checked | 3|
| [[L-04](#l-04)] | Deleting mapping in struct will not delete the mapping | 2|
| [[L-05](#l-05)] | Empty receive functions can cause gas issues | 1|
| [[L-06](#l-06)] | `pure` function accesses storage | 6|
| [[L-07](#l-07)] | Two or more functions contain the exact same code | 14|
| [[L-08](#l-08)] | Must approve or increase allowance first | 2|
| [[L-09](#l-09)] | Emitting storage values instead of the memory one. | 9|
| [[L-10](#l-10)] | Missing contract-existence checks before low-level calls | 7|
| [[L-11](#l-11)] | Functions calling contracts/addresses with transfer hooks are missing reentrancy guards | 1|
| [[L-12](#l-12)] | Draft OpenZeppelin Dependencies | 1|
| [[L-13](#l-13)] | Zero-value `ERC20` token transfers can revert for certain tokens | 4|
| [[L-14](#l-14)] | Contracts are vulnerable to rebasing accounting-related issues | 5|
| [[L-15](#l-15)] | Code does not follow the best practice of check-effects-interaction | 51|
| [[L-16](#l-16)] | Consider bounding input array length | 8|
| [[L-17](#l-17)] | Use of `abi.encodePacked` with dynamic types inside `keccak256` | 3|
| [[L-18](#l-18)] | Large transfers may not work with some `ERC20` tokens | 5|


### NonCritical Risk Issues

| |Issue|Instances|
|-|:-|:-|
| [[N-01](#n-01)] | Floating pragma should be avoided | 1|
| [[N-02](#n-02)] | Empty function blocks | 4|
| [[N-03](#n-03)] | Keccak state variables should be immutable not constant | 3|
| [[N-04](#n-04)] | Functions which are either private or internal should have a preceding _ in their name | 38|
| [[N-05](#n-05)] | Private and internal state variables should have a preceding _ in their name unless they are constants | 11|
| [[N-06](#n-06)] | Function names should differ to make the code more readable | 2|
| [[N-07](#n-07)] | Emits without `msg.sender` parameter | 9|
| [[N-08](#n-08)] | A function which defines named returns in it's declaration doesn't need to use `return` | 1|
| [[N-09](#n-09)] | NatSpec `@return` argument is missing | 171|
| [[N-10](#n-10)] | NatSpec `@param` is missing | 265|
| [[N-11](#n-11)] | Use multiple `require()` and `if` statements instead of `&&` | 5|
| [[N-12](#n-12)] | Change `public` to `external` for functions that are not called internally | 10|
| [[N-13](#n-13)] | `Import` only specific files | 22|
| [[N-14](#n-14)] | `Constants` in comparisons should appear on the left side | 166|
| [[N-15](#n-15)] | Do not use underscore at the end of variable name | 1|
| [[N-16](#n-16)] | Event is missing `indexed` field | 30|
| [[N-17](#n-17)] | Numeric values having to do with time should use time units for readability | 4|
| [[N-18](#n-18)] | Consider using `delete` rather than assigning zero/false to clear values | 4|
| [[N-19](#n-19)] | Array is `push()`ed but not `pop()`ed | 2|
| [[N-20](#n-20)] | Unused contract variables | 18|
| [[N-21](#n-21)] | Assembly block creates dirty bits | 1|
| [[N-22](#n-22)] | `else`-block not required | 3|
| [[N-23](#n-23)] | Convert simple if-statements to ternary expressions | 15|
| [[N-24](#n-24)] | Remaining eth may not be refunded to users | 33|
| [[N-25](#n-25)] | External calls in an un-bounded `for`-loop may result in a DOS | 20|
| [[N-26](#n-26)] | `constructor` missing zero address check | 5|
| [[N-27](#n-27)] | Variable initialization with default value | 24|
| [[N-28](#n-28)] | Large multiples of ten should use scientific notation | 2|
| [[N-29](#n-29)] | Complex math should be split into multiple steps | 1|
| [[N-30](#n-30)] | Duplicated `require/if` statements should be refactored | 69|
| [[N-31](#n-31)] | Variable names don't follow the Solidity naming convention | 8|
| [[N-32](#n-32)] | Contract functions should use an `interface` | 18|
| [[N-33](#n-33)] | State variables should include comments | 7|
| [[N-34](#n-34)] | Missing NatSpec from contract declarations | 36|
| [[N-35](#n-35)] | Inconsistent usage of `require`/`error` | 6|
| [[N-36](#n-36)] | `require`/`revert` without any message | 4|
| [[N-37](#n-37)] | Events that mark critical parameter changes should contain both the old and the new value | 9|
| [[N-38](#n-38)] | Constant redefined elsewhere | 11|
| [[N-39](#n-39)] | Function ordering does not follow the Solidity style guide | 20|
| [[N-40](#n-40)] | Array indicies should be referenced via `enum`s rather than via numeric literals | 19|
| [[N-41](#n-41)] | Use of `override` is unnecessary | 25|
| [[N-42](#n-42)] | Unused function parameter | 9|
| [[N-43](#n-43)] | Unused `event` definition | 3|
| [[N-44](#n-44)] | Modifier declarations should have NatSpec descriptions | 9|
| [[N-45](#n-45)] | Event declarations should have NatSpec descriptions | 19|
| [[N-46](#n-46)] | Function declarations should have NatSpec descriptions | 132|
| [[N-47](#n-47)] | Function names should use lowerCamelCase | 4|
| [[N-48](#n-48)] | Overflows in unchecked blocks | 6|
| [[N-49](#n-49)] | Missing event and or timelock for critical parameter change | 12|
| [[N-50](#n-50)] | Setters should prevent re-setting of the same value | 19|
| [[N-51](#n-51)] | Interfaces should be defined in separate files from their usage | 3|
| [[N-52](#n-52)] | Consider disallowing transfers to `address(this)` | 2|
| [[N-53](#n-53)] | Named imports of parent contracts are missing | 2|
| [[N-54](#n-54)] | Events may be emitted out of order due to reentrancy | 12|
| [[N-55](#n-55)] | Function can return unassigned variable | 1|
| [[N-56](#n-56)] | Missing zero address check in initializer | 1|
| [[N-57](#n-57)] | Missing NatSpec `@author` from contract declaration | 16|
| [[N-58](#n-58)] | Missing NatSpec `@dev` from contract declaration | 49|
| [[N-59](#n-59)] | Missing NatSpec `@notice` from contract declaration | 42|
| [[N-60](#n-60)] | Missing NatSpec `@title` from contract declaration | 44|
| [[N-61](#n-61)] | Missing NatSpec `@dev` from error declaration | 2|
| [[N-62](#n-62)] | Missing NatSpec `@param` from error declaration | 2|
| [[N-63](#n-63)] | Missing NatSpec from event declaration | 19|
| [[N-64](#n-64)] | Missing NatSpec `@dev` from event declaration | 48|
| [[N-65](#n-65)] | Missing NatSpec `@notice` from event declaration | 20|
| [[N-66](#n-66)] | Missing NatSpec `@param` from event declaration | 50|
| [[N-67](#n-67)] | Missing NatSpec from modifiers definitions | 9|
| [[N-68](#n-68)] | Missing NatSpec `@dev` from modifier declaration | 21|
| [[N-69](#n-69)] | Missing NatSpec `@notice` from modifier declaration | 10|
| [[N-70](#n-70)] | Missing NatSpec `@param` from modifier declaration | 22|
| [[N-71](#n-71)] | Missing NatSpec from function definition | 128|
| [[N-72](#n-72)] | Missing NatSpec `@dev` from function declaration | 336|
| [[N-73](#n-73)] | Missing NatSpec `@notice` from function declaration | 340|
| [[N-74](#n-74)] | Missing NatSpec `@param` from function declaration | 365|
| [[N-75](#n-75)] | Incomplete NatSpec `@return` from function declaration | 379|
| [[N-76](#n-76)] | Simplify complex require statements | 33|
| [[N-77](#n-77)] | Events should be emitted before external calls | 22|
| [[N-78](#n-78)] | Use `@inheritdoc` for overridden functions | 25|
| [[N-79](#n-79)] | Missing NatSpec from variable declarations | 7|
| [[N-80](#n-80)] | Contract name does not follow the Solidity Style Guide | 6|
| [[N-81](#n-81)] | Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES | 5|
| [[N-82](#n-82)] | Use a single file for system wide constants | 73|
| [[N-83](#n-83)] | Contracts should have full test coverage | 1|
| [[N-84](#n-84)] | Large or complicated code bases should implement invariant tests | 1|
| [[N-85](#n-85)] | Codebase should implement formal verification testing | 1|
| [[N-86](#n-86)] | Use SafeCast to safely downcast variables | 45|
| [[N-87](#n-87)] | Consider adding a block/deny-list | 3|
| [[N-88](#n-88)] | Events should use parameters to convey information | 2|
| [[N-89](#n-89)] | Expressions for constant values should use `immutable` rather than `constant` | 27|

### Low Risk Issues

### [L-01]<a name="l-01"></a> Large assembly blocks should have extensive comments

Assembly blocks are take a lot more time to audit than normal Solidity code, and often have gotchas and side-effects that the Solidity versions of the same code do not. Consider adding more comments explaining what is being done in every step of the assembly code

*There are 2 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
 // @audit assembly block contains `10` Yul statements 
229	        assembly {
230	            // Copy function signature and arguments from calldata at zero position into memory at pointer position
231	            calldatacopy(0, 0, calldatasize())
232	            // Call method of the hyperchain diamond contract returns 0 on error
233	            let result := call(gas(), contractAddress, 0, 0, calldatasize(), 0, 0)
234	            // Get the size of the last return data
235	            let size := returndatasize()
236	            // Copy the size length of bytes from return data at zero position to pointer position
237	            returndatacopy(0, 0, size)
238	            // Depending on the result value
239	            switch result
240	            case 0 {
241	                // End execution and revert state changes
242	                revert(0, size)
243	            }
244	            default {
245	                // Return data with length of size at pointers position
246	                return(0, size)
247	            }
248	        }
```

*GitHub* : [229..248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L229-L248)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

```solidity
 // @audit assembly block contains `11` Yul statements 
35	        assembly {
36	            // The pointer to the free memory slot
37	            let ptr := mload(0x40)
38	            // Copy function signature and arguments from calldata at zero position into memory at pointer position
39	            calldatacopy(ptr, 0, calldatasize())
40	            // Delegatecall method of the implementation contract returns 0 on error
41	            let result := delegatecall(gas(), facetAddress, ptr, calldatasize(), 0, 0)
42	            // Get the size of the last return data
43	            let size := returndatasize()
44	            // Copy the size length of bytes from return data at zero position to pointer position
45	            returndatacopy(ptr, 0, size)
46	            // Depending on the result value
47	            switch result
48	            case 0 {
49	                // End execution and revert state changes
50	                revert(ptr, size)
51	            }
52	            default {
53	                // Return data with length of size at pointers position
54	                return(ptr, size)
55	            }
56	        }
```

*GitHub* : [35..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L35-L56)

### [L-02]<a name="l-02"></a> Missing checks for `address(0)` when assigning values to address state variables



*There are 19 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
106	    function initialize(
107	        address _owner,
108	        uint256 _eraFirstPostUpgradeBatch
109	    ) external reentrancyGuardInitializer initializer {
...
// @audit Address `ERA_ERC20_BRIDGE_ADDRESS` is not cheched for zero in current function
114	        l2BridgeAddress[ERA_CHAIN_ID] = ERA_ERC20_BRIDGE_ADDRESS;
...
144	    function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner {
...
// @audit Address `_l2BridgeAddress` is not cheched for zero in current function
145	        l2BridgeAddress[_chainId] = _l2BridgeAddress;
```

*GitHub* : [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L114), [145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L145)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
53	    function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
...
// @audit Address `_newPendingAdmin` is not cheched for zero in current function
57	        pendingAdmin = _newPendingAdmin;
...
62	    function acceptAdmin() external {
...
// @audit Address `currentPendingAdmin` is not cheched for zero in current function
67	        admin = currentPendingAdmin;
...
110	    function setSharedBridge(address _sharedBridge) external onlyOwner {
...
// @audit Address `` is not cheched for zero in current function
111	        sharedBridge = IL1SharedBridge(_sharedBridge);
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L57), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L67), [111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L111), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L136), [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L137)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [260](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L260)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L116), [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L126), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L135), [236](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L236), [284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L284)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L76)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol



---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L29), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L39)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L67), [101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L101)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L56)

### [L-03]<a name="l-03"></a> Array lengths not checked

If the length of the arrays are not required to be of the same length, user operations may not be fully executed due to a mismatch in the number of items iterated over, versus the number of items provided in the second array

*There are 3 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
500	    function _createBatchCommitment(
501	        CommitBatchInfo calldata _newBatchData,
502	        bytes32 _stateDiffHash,
503	        bytes32[] memory _blobCommitments,
504	        bytes32[] memory _blobHashes
505	    ) internal view returns (bytes32) {
...
537	    function _batchAuxiliaryOutput(
538	        CommitBatchInfo calldata _batch,
539	        bytes32 _stateDiffHash,
540	        bytes32[] memory _blobCommitments,
541	        bytes32[] memory _blobHashes
542	    ) internal pure returns (bytes memory) {
...
561	    function _encodeBlobAuxilaryOutput(
562	        bytes32[] memory _blobCommitments,
563	        bytes32[] memory _blobHashes
564	    ) internal pure returns (bytes32[] memory blobAuxOutputWords) {
```

*GitHub* : [500..505](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L500-L505), [537..542](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542), [561..564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L561-L564)

### [L-04]<a name="l-04"></a> Deleting mapping in struct will not delete the mapping



*There are 2 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
// @audit attempt to delete mapping in struct
249	        delete ds.selectorToFacet[_selector];
```

*GitHub* : [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L249)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

```solidity
// @audit attempt to delete mapping in struct
81	        delete _queue.data[head];
```

*GitHub* : [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L81)

### [L-05]<a name="l-05"></a> Empty receive functions can cause gas issues

In Solidity, functions that receive Ether without corresponding functionality to utilize or withdraw these funds can inadvertently lead to a permanent loss of value. This is because if someone sends Ether to the contract, they may be unable to retrieve it. To avoid this, functions receiving Ether should be accompanied by additional methods that process or allow the withdrawal of these funds. If the intent is to use the received Ether, it should trigger a separate function; if not, it should revert the transaction (for instance, via `require(msg.sender == address(weth))`). Access control checks can also prevent unintended Ether transfers, despite the slight gas cost they entail. If concerns over gas costs persist, at minimum, include a rescue function to recover unused Ether. Missteps in handling Ether in smart contracts can lead to irreversible financial losses, hence these precautions are crucial.

*There are 1 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
264	    receive() external payable {}
```

*GitHub* : [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L264)

### [L-06]<a name="l-06"></a> `pure` function accesses storage

While the compiler currently flags functions like these as being `pure`, this is a [bug](https://github.com/ethereum/solidity/issues/11573) which will be fixed in a future version, so it's best to not use `pure` visibility, in order to not break when this bug is fixed.

*There are 6 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
 // @audit Use of storage reference in `pure` functions
132	    function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {
...
 // @audit Use of storage reference in `pure` functions
291	    function _serializeL2Transaction(
292	        WritePriorityOpParams memory _priorityOpParams,
293	        bytes memory _calldata,
294	        bytes[] memory _factoryDeps
295	    ) internal pure returns (L2CanonicalTransaction memory transaction) {
```

*GitHub* : [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L132), [291..295](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L291-L295)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

```solidity
 // @audit Use of storage reference in `pure` functions
62	    function computeCreate2Address(
63	        address _sender,
64	        bytes32 _salt,
65	        bytes32 _bytecodeHash,
66	        bytes32 _constructorInputHash
67	    ) internal pure returns (address) {
```

*GitHub* : [62..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L62-L67)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
 // @audit Use of storage reference in `pure` functions
89	    function getDiamondStorage() internal pure returns (DiamondStorage storage diamondStorage) {
```

*GitHub* : [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L89)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
 // @audit Use of storage reference in `pure` functions
180	    function decodeString(bytes memory _input) external pure returns (string memory result) {
```

*GitHub* : [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L180)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol

```solidity
 // @audit Use of storage reference in `pure` functions
103	    function computeCreate2Address(
104	        address _sender,
105	        bytes32 _salt,
106	        bytes32 _bytecodeHash,
107	        bytes32 _constructorInputHash
108	    ) internal pure returns (address) {
```

*GitHub* : [103..108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L103-L108)

### [L-07]<a name="l-07"></a> Two or more functions contain the exact same code

In Solidity programming, duplicate code in multiple functions introduces potential security risks and maintainability issues. It magnifies the impact of any bugs or vulnerabilities, since developers must fix these in every location where the code is replicated. Overlooking any instance of replicated code could leave vulnerabilities intact. Furthermore, code duplication leads to contract bloating, diminishing the readability and manageability of the code. Future logic changes would need to be applied in every location where the code is replicated, increasing the complexity of updates. To resolve this, it is recommended to consolidate duplicate code into a single internal function, and replace the duplicate instances with calls to this new function. This approach streamlines the code, reducing the attack surface and making it easier to maintain and update.

*There are 14 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
162	    function freezeChain(uint256 _chainId) external onlyOwner {
...
167	    function unfreezeChain(uint256 _chainId) external onlyOwner {
```

*GitHub* : [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L162), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L167)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

```solidity
154	    function getL2SystemContractsUpgradeBatchNumber() external view returns (uint256) {
...
261	    function getL2SystemContractsUpgradeBlockNumber() external view returns (uint256) {
```

*GitHub* : [154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L154), [261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L261)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

```solidity
79	    function getTotalBatchesCommitted() external view returns (uint256) {
...
241	    function getTotalBlocksCommitted() external view returns (uint256) {
```

*GitHub* : [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L79), [241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L241)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

```solidity
89	    function getTotalBatchesExecuted() external view returns (uint256) {
...
251	    function getTotalBlocksExecuted() external view returns (uint256) {
```

*GitHub* : [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L89), [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L251)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

```solidity
84	    function getTotalBatchesVerified() external view returns (uint256) {
...
246	    function getTotalBlocksVerified() external view returns (uint256) {
```

*GitHub* : [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L84), [246](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L246)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L124), [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L256)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L265), [271](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L271)

### [L-08]<a name="l-08"></a> Must approve or increase allowance first

In the context of ERC20 tokens, a token holder needs to "approve" another account to transfer a certain amount of their tokens on their behalf. This is accomplished by calling the `approve()` function, which takes the address of the spender and the amount they're allowed to spend as parameters. 

This approval step is a crucial part of the ERC20 standard because it allows for secure delegated transfers. A common use case for this feature is in decentralized exchanges or DeFi protocols, where a user can approve a smart contract to transfer tokens on their behalf. 

After the approval step, the approved account (or contract) can then transfer tokens up to the approved amount from the token holder's account by calling the `transferFrom()` function. This function takes three parameters: the address of the token holder, the recipient's address, and the amount to transfer.

If an account tries to call `transferFrom()` before the token holder has called `approve()`, the transaction will fail because the ERC20 contract checks whether the `transferFrom()` caller has an adequate allowance. 

In summary, if a contract or user needs to move ERC20 tokens on behalf of another account, it's necessary to ensure that the token holder has first called `approve()` to set a sufficient allowance. This is a key aspect of ERC20 token security and functionality. 

*There are 2 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
 // @audit function call transfer from, but not approve
162	    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
...
164	        _token.safeTransferFrom(_from, address(sharedBridge), _amount);
```

*GitHub* : [164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L164)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
 // @audit function call transfer from, but not approve
175	    function _depositFunds(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
...
177	        _token.safeTransferFrom(_from, address(this), _amount);
```

*GitHub* : [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L177)

### [L-09]<a name="l-09"></a> Emitting storage values instead of the memory one.

Emitted values should not be read from storage again. Instead, the existing values from memory should be used.

*There are 9 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
71	        emit NewAdmin(previousAdmin, pendingAdmin);
```

*GitHub* : [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L71)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
252	        emit ChangeMinDelay(minDelay, _newDelay);
...
259	        emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```

*GitHub* : [252](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L252), [259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L259)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
130	        emit NewAdmin(previousAdmin, pendingAdmin);
...
229	        emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
```

*GitHub* : [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L130), [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L229)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
436	        emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);
...
496	        emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
```

*GitHub* : [436](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436), [496](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
103	        emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);
...
128	        emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);
```

*GitHub* : [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L103), [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L128)

### [L-10]<a name="l-10"></a> Missing contract-existence checks before low-level calls

Low-level calls return success if there is no code present at the specified address. In addition to the zero-address checks, add a check to verify that `<address>.code.length > 0`

*There are 7 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
// @audit contract existance not checked before this call
264	        (, bytes memory data1) = _token.staticcall(abi.encodeCall(IERC20Metadata.name, ()));
...
// @audit contract existance not checked before this call
265	        (, bytes memory data2) = _token.staticcall(abi.encodeCall(IERC20Metadata.symbol, ()));
...
// @audit contract existance not checked before this call
266	        (, bytes memory data3) = _token.staticcall(abi.encodeCall(IERC20Metadata.decimals, ()));
```

*GitHub* : [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L264), [265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L265), [266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L266)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
// @audit contract existance not checked before this call
228	            (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```

*GitHub* : [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L228)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
// @audit contract existance not checked before this call
612	        (bool success, bytes memory data) = POINT_EVALUATION_PRECOMPILE_ADDR.staticcall(precompileInput);
...
// @audit contract existance not checked before this call
680	        (bool success, bytes memory data) = s.blobVersionedHashRetriever.staticcall(abi.encode(_index));
```

*GitHub* : [612](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L612), [680](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L680)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
// @audit contract existance not checked before this call
285	            (bool success, bytes memory data) = _init.delegatecall(_calldata);
```

*GitHub* : [285](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L285)

### [L-11]<a name="l-11"></a> Functions calling contracts/addresses with transfer hooks are missing reentrancy guards

Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks will open the users of this protocol up to [read-only reentrancies](https://chainsecurity.com/curve-lp-oracle-manipulation-post-mortem/) with no way to protect against it, except by block-listing the whole protocol.`

*There are 1 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
65	    function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
...
// @audit Function `tranferTokenToSharedBridge` doesn't  have the `nonReentrant` modifier
69	        IERC20(_token).safeTransfer(address(sharedBridge), amount);
```

*GitHub* : [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L69)

### [L-12]<a name="l-12"></a> Draft OpenZeppelin Dependencies

OpenZeppelin contracts may be considered draft contracts if they have not received adequate security auditing or are liable to change with future development.

*There are 1 instance(s) of this issue:*


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
7	import {ERC20PermitUpgradeable} from "@openzeppelin/contracts-upgradeable/token/ERC20/extensions/draft-ERC20PermitUpgradeable.sol";
```

*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L7)

### [L-13]<a name="l-13"></a> Zero-value `ERC20` token transfers can revert for certain tokens

Some `ERC20` tokens revert for zero-value transfers (e.g. `LEND`). If used as a `order.baseAsset` and a small strike price, the fee token transfer will revert. Hence, assets and the strike can not be withdrawn and remain locked in the contract.
See [Weird ERC20 Tokens - Revert on Zero Value Transfers](https://github.com/d-xo/weird-erc20#revert-on-zero-value-transfers)

*There are 4 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
// @audit Contracts that implement `ERC20`: `ERC20`, `FeeOnTransferToken`, `IERC20`, `IERC20Metadata`, `RevertTransferERC20`, `TestnetERC20Token`, `SafeTransferLib`, `SafeERC20`
69	        IERC20(_token).safeTransfer(address(sharedBridge), amount);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `FeeOnTransferToken`, `IERC20`, `IERC20Metadata`, `RevertTransferERC20`, `TestnetERC20Token`, `SafeTransferLib`, `SafeERC20`
164	        _token.safeTransferFrom(_from, address(sharedBridge), _amount);
```

*GitHub* : [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L69), [164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L164)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
// @audit Contracts that implement `ERC20`: `ERC20`, `FeeOnTransferToken`, `IERC20`, `IERC20Metadata`, `RevertTransferERC20`, `TestnetERC20Token`, `SafeTransferLib`, `SafeERC20`
177	        _token.safeTransferFrom(_from, address(this), _amount);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `FeeOnTransferToken`, `IERC20`, `IERC20Metadata`, `RevertTransferERC20`, `TestnetERC20Token`, `SafeTransferLib`, `SafeERC20`
454	            IERC20(l1Token).safeTransfer(l1Receiver, amount);
```

*GitHub* : [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L177), [454](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L454)

### [L-14]<a name="l-14"></a> Contracts are vulnerable to rebasing accounting-related issues

Rebasing tokens are tokens that have each holder's `balanceof()` increase over time. Aave aTokens are an example of such tokens. If rebasing tokens are used, rewards accrue to the contract holding the tokens, and cannot be withdrawn by the original depositor. To address the issue, track 'shares' deposited on a pro-rata basis, and let shares be redeemed for their proportion of the current balance at the time of the withdrawal.

*There are 5 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
65	    function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
...
162	    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```

*GitHub* : [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65), [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L162)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
175	    function _depositFunds(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
...
305	    function _claimFailedDeposit(
306	        bool _checkedInLegacyBridge,
307	        uint256 _chainId,
308	        address _depositSender,
309	        address _l1Token,
310	        uint256 _amount,
311	        bytes32 _l2TxHash,
312	        uint256 _l2BatchNumber,
313	        uint256 _l2MessageIndex,
314	        uint16 _l2TxNumberInBatch,
315	        bytes32[] calldata _merkleProof
316	    ) internal nonReentrant {
...
411	    function _finalizeWithdrawal(
412	        uint256 _chainId,
413	        uint256 _l2BatchNumber,
414	        uint256 _l2MessageIndex,
415	        uint16 _l2TxNumberInBatch,
416	        bytes calldata _message,
417	        bytes32[] calldata _merkleProof
418	    ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
```

*GitHub* : [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175), [305..316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L305-L316), [411..418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L411-L418)

### [L-15]<a name="l-15"></a> Code does not follow the best practice of check-effects-interaction

Code should follow the best-practice of [check-effects-interaction](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs.

*There are 51 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
// @audit Some statements does not follow CEI
135	    function deposit(
136	        address _l2Receiver,
137	        address _l1Token,
138	        uint256 _amount,
139	        uint256 _l2TxGasLimit,
140	        uint256 _l2TxGasPerPubdataByte,
141	        address _refundRecipient
142	    ) public payable nonReentrant returns (bytes32 l2TxHash) {
...
// @audit Statement out of CEI order
156	        depositAmount[msg.sender][_l1Token][l2TxHash] = _amount;
...
// @audit Some statements does not follow CEI
162	    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
...
// @audit Statement out of CEI order
165	        uint256 balanceAfter = _token.balanceOf(address(sharedBridge));
...
// @audit Some statements does not follow CEI
210	    function finalizeWithdrawal(
211	        uint256 _l2BatchNumber,
212	        uint256 _l2MessageIndex,
213	        uint16 _l2TxNumberInBatch,
214	        bytes calldata _message,
215	        bytes32[] calldata _merkleProof
216	    ) external nonReentrant {
...
// @audit Statement out of CEI order
220	        (address l1Receiver, address l1Token, uint256 amount) = sharedBridge.finalizeWithdrawalLegacyErc20Bridge(
221	            _l2BatchNumber,
222	            _l2MessageIndex,
223	            _l2TxNumberInBatch,
224	            _message,
225	            _merkleProof
226	        );
```

*GitHub* : [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L156), [165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L165), [220..226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L220-L226)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
// @audit Some statements does not follow CEI
106	    function initialize(
107	        address _owner,
108	        uint256 _eraFirstPostUpgradeBatch
109	    ) external reentrancyGuardInitializer initializer {
...
// @audit Statement out of CEI order
114	        l2BridgeAddress[ERA_CHAIN_ID] = ERA_ERC20_BRIDGE_ADDRESS;
...
// @audit Some statements does not follow CEI
118	    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
...
// @audit Statement out of CEI order
135	            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
```

*GitHub* : [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L114), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L135), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L167), [178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L178), [221..227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L221-L227), [240](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L240), [602](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L602)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L67), [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L89), [99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L99), [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L105), [240..252](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L240-L252)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L181), [200](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L200), [221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L221)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L126)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L39), [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L64), [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L75), [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L93), [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L139), [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L149)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L86), [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L249), [300](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L300), [335](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L335), [362](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L362), [437](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L437), [488](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L488), [545](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L545), [582](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L582), [682](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L682)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L126), [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L174), [257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L257), [288](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L288)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L105), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L122), [216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L216), [257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L257)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L41)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L34)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L35)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L82)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L120)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L179)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L102), [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126)

### [L-16]<a name="l-16"></a> Consider bounding input array length

The functions below take in an unbounded array, and make function calls for entries in the array. While the function will revert if it eventually runs out of gas, it may be a nicer user experience to `require()` that the length of the array is below some reasonable maximum, so that the user doesn't have to use up a full transaction's gas only to see that the transaction reverts.

*There are 8 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
// @audit array parameter `_calls` is used as loop condition and length is not cheched in function
226	    function _execute(Call[] calldata _calls) internal {
...
// @audit loop uses unbounded parameter
227	        for (uint256 i = 0; i < _calls.length; ++i) {
```

*GitHub* : [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L227)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
// @audit array parameter `_newBatchesData` is used as loop condition and length is not cheched in function
112	        CommitBatchInfo[] calldata _newBatchesData
...
// @audit loop uses unbounded parameter
118	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```

*GitHub* : [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L118)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
// @audit array parameter `_newBatchesData` is used as loop condition and length is not cheched in function
131	        CommitBatchInfo[] calldata _newBatchesData
...
// @audit loop uses unbounded parameter
137	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```

*GitHub* : [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L137)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
// @audit array parameter `_newBatchesData` is used as loop condition and length is not cheched in function
184	    function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {
...
// @audit loop uses unbounded parameter
187	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```

*GitHub* : [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L187)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
// @audit array parameter `_newBatchesData` is used as loop condition and length is not cheched in function
207	        StoredBatchInfo[] calldata _newBatchesData
...
// @audit loop uses unbounded parameter
211	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```

*GitHub* : [211](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L211)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L259)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [291](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L291)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L228)

### [L-17]<a name="l-17"></a> Use of `abi.encodePacked` with dynamic types inside `keccak256`

`abi.encodePacked` should not be used with dynamic types when passing the result to a hash function such as `keccak256`. Use `abi.encode` instead, which will pad items to 32 bytes, to [prevent any hash collisions](https://docs.soliditylang.org/en/latest/abi-spec.html#non-standard-packed-mode).

*There are 3 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
460	                keccak256(
461	                    abi.encodePacked(
462	                        _prevBatchCommitment,
463	                        _currentBatchCommitment,
464	                        _verifierParams.recursionNodeLevelVkHash,
465	                        _verifierParams.recursionLeafLevelVkHash
466	                    )
467	                )
...
654	            blobCommitments[versionedHashIndex] = keccak256(
655	                abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
656	            );
```

*GitHub* : [460..467](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L460-L467), [654..656](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L654-L656)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
114	        bytes32 hashedLog = keccak256(
115	            abi.encodePacked(_log.l2ShardId, _log.isService, _log.txNumberInBatch, _log.sender, _log.key, _log.value)
116	        );
```

*GitHub* : [114..116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L114-L116)

### [L-18]<a name="l-18"></a> Large transfers may not work with some `ERC20` tokens

Some `IERC20` implementations (e.g `UNI`, `COMP`) may fail if the valued `transferred` is larger than `uint96`. [Source](https://github.com/d-xo/weird-erc20/blob/main/src/Uint96.sol).

*There are 5 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
// @audit Contracts that implement `ERC20`: `ERC20`, `FeeOnTransferToken`, `IERC20`, `IERC20Metadata`, `RevertTransferERC20`, `TestnetERC20Token`, `SafeTransferLib`, `SafeERC20`
69	        IERC20(_token).safeTransfer(address(sharedBridge), amount);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `FeeOnTransferToken`, `IERC20`, `IERC20Metadata`, `RevertTransferERC20`, `TestnetERC20Token`, `SafeTransferLib`, `SafeERC20`
164	        _token.safeTransferFrom(_from, address(sharedBridge), _amount);
```

*GitHub* : [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L69), [164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L164)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
// @audit Contracts that implement `ERC20`: `ERC20`, `FeeOnTransferToken`, `IERC20`, `IERC20Metadata`, `RevertTransferERC20`, `TestnetERC20Token`, `SafeTransferLib`, `SafeERC20`
177	        _token.safeTransferFrom(_from, address(this), _amount);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `FeeOnTransferToken`, `IERC20`, `IERC20Metadata`, `RevertTransferERC20`, `TestnetERC20Token`, `SafeTransferLib`, `SafeERC20`
364	            IERC20(_l1Token).safeTransfer(_depositSender, _amount);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `FeeOnTransferToken`, `IERC20`, `IERC20Metadata`, `RevertTransferERC20`, `TestnetERC20Token`, `SafeTransferLib`, `SafeERC20`
454	            IERC20(l1Token).safeTransfer(l1Receiver, amount);
```

*GitHub* : [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L177), [364](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L364), [454](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L454)

### NonCritical Risk Issues

### [N-01]<a name="n-01"></a> Floating pragma should be avoided



*There are 1 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol

```solidity
1	pragma solidity ^0.8.0;
```

*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L1)

### [N-02]<a name="n-02"></a> Empty function blocks

Empty code blocks (i.e., {}) in a Solidity contract can be harmful as they can lead to ambiguity, misinterpretation, and unintended behavior. When developers encounter empty code blocks, it may be unclear whether the absence of code is intentional or the result of an oversight. This uncertainty can cause confusion during development, testing, and debugging, increasing the likelihood of introducing errors or vulnerabilities. Moreover, empty code blocks may give a false impression of implemented functionality or security measures, creating a misleading sense of assurance. To ensure clarity and maintainability, it is essential to avoid empty code blocks and explicitly document the intended behavior or any intentional omissions.

*There are 4 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
62	    function initialize() external reentrancyGuardInitializer {}
```

*GitHub* : [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L62)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
40	    constructor() reentrancyGuardInitializer {}
```

*GitHub* : [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L40)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
264	    receive() external payable {}
```

*GitHub* : [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L264)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

```solidity
21	    constructor() reentrancyGuardInitializer {}
```

*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L21)

### [N-03]<a name="n-03"></a> Keccak state variables should be immutable not constant

Constant keccak variables should be replaced with immutable variables in Solidity contracts to optimize gas usage and enhance efficiency. While constant variables are evaluated and computed at runtime, immutable variables are assigned during contract deployment and stored directly in the contract bytecode. By using immutable for keccak variables, their hash values are computed only once during deployment, reducing the gas cost associated with repeated computations at runtime. This approach leads to more efficient execution, conserving resources for users, and allowing for smoother contract interactions, ultimately benefiting the overall performance and user experience.

*There are 3 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

```solidity
14	    bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");
```

*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L14)


---

	 - code/contracts/ethereum/contracts/common/Config.sol

```solidity
114	bytes32 constant TWO_BRIDGES_MAGIC_VALUE = bytes32(uint256(keccak256("TWO_BRIDGES_MAGIC_VALUE")) - 1);
```

*GitHub* : [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L114)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol

```solidity
87	    bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L87)

### [N-04]<a name="n-04"></a> Functions which are either private or internal should have a preceding _ in their name

Add a preceding underscore to the function name, take care to refactor where there functions are called

*There are 38 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

```solidity
23	    function hashL2Bytecode(bytes memory _bytecode) internal pure returns (bytes32 hashedBytecode) {
...
41	    function validateBytecodeHash(bytes32 _bytecodeHash) internal pure {
...
51	    function bytecodeLen(bytes32 _bytecodeHash) internal pure returns (uint256 codeLengthInWords) {
...
62	    function computeCreate2Address(
63	        address _sender,
64	        bytes32 _salt,
65	        bytes32 _bytecodeHash,
66	        bytes32 _constructorInputHash
67	    ) internal pure returns (address) {
```

*GitHub* : [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23), [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L41), [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L51), [62..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L62-L67)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol

```solidity
13	    function uncheckedInc(uint256 _number) internal pure returns (uint256) {
...
19	    function uncheckedAdd(uint256 _lhs, uint256 _rhs) internal pure returns (uint256) {
```

*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L13), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L19)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol

```solidity
21	    function readUint32(bytes memory _bytes, uint256 _start) internal pure returns (uint32 result, uint256 offset) {
...
28	    function readAddress(bytes memory _bytes, uint256 _start) internal pure returns (address result, uint256 offset) {
...
35	    function readUint256(bytes memory _bytes, uint256 _start) internal pure returns (uint256 result, uint256 offset) {
...
42	    function readBytes32(bytes memory _bytes, uint256 _start) internal pure returns (bytes32 result, uint256 offset) {
```

*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L21), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L28), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L35), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L42)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L89), [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L98)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


*GitHub* : [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L20), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L40)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [20..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L20-L24)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L37), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L42), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L47), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L52), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L57), [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L66), [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L74)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [21..26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L21-L26), [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L48), [71..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L71-L75), [111..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L111-L114), [130..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L130-L132)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L30), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L40)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L30), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L40)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L92), [103..108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L103-L108)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L29), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39), [78..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L78-L83), [97..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L97-L107), [123..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L123-L129)

### [N-05]<a name="n-05"></a> Private and internal state variables should have a preceding _ in their name unless they are constants

Add a preceding underscore to the state variable name, take care to refactor where there variables are read/wrote

*There are 11 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
47	    uint256 internal eraFirstPostUpgradeBatch;
...
63	    mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;
...
67	    mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L47), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L63), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L67)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
37	    address private pendingAdmin;
```

*GitHub* : [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L37)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
56	    address private pendingAdmin;
```

*GitHub* : [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L56)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
49	    mapping(uint256 => LibMap.Uint32Map) internal committedBatchTimestamp;
```

*GitHub* : [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L49)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

```solidity
14	    ZkSyncStateTransitionStorage internal s;
```

*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L14)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

```solidity
34	    bytes32 internal l2TokenProxyBytecodeHash;
...
39	    address private l1LegacyBridge;
```

*GitHub* : [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L34), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L39)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
28	    ERC20Getters private availableGetters;
```

*GitHub* : [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L28), [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L33)

### [N-06]<a name="n-06"></a> Function names should differ to make the code more readable

In Solidity, while function overriding allows for functions with the same name to coexist, it is advisable to avoid this practice to enhance code readability and maintainability. Having multiple functions with the same name, even with different parameters or in inherited contracts, can cause confusion and increase the likelihood of errors during development, testing, and debugging. Using distinct and descriptive function names not only clarifies the purpose and behavior of each function, but also helps prevent unintended function calls or incorrect overriding. By adopting a clear and consistent naming convention, developers can create more comprehensible and maintainable smart contracts.

*There are 2 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
100	    function deposit(
101	        address _l2Receiver,
102	        address _l1Token,
103	        uint256 _amount,
104	        uint256 _l2TxGasLimit,
105	        uint256 _l2TxGasPerPubdataByte
106	    ) external payable returns (bytes32 l2TxHash) {
...
135	    function deposit(
136	        address _l2Receiver,
137	        address _l1Token,
138	        uint256 _amount,
139	        uint256 _l2TxGasLimit,
140	        uint256 _l2TxGasPerPubdataByte,
141	        address _refundRecipient
142	    ) public payable nonReentrant returns (bytes32 l2TxHash) {
```

*GitHub* : [100..106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L100-L106), [135..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L135-L142)

### [N-07]<a name="n-07"></a> Emits without `msg.sender` parameter

If `msg.sender` play a part in the functionality of a function, any emits of this function should include msg.sender to ensure transparency with users

*There are 9 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
// @audit Current function use `msg.sender`, but do not emit it
70	        emit NewPendingAdmin(currentPendingAdmin, address(0));
...
// @audit Current function use `msg.sender`, but do not emit it
71	        emit NewAdmin(previousAdmin, pendingAdmin);
```

*GitHub* : [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L70), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L71)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
// @audit Current function use `msg.sender`, but do not emit it
129	        emit NewPendingAdmin(currentPendingAdmin, address(0));
...
// @audit Current function use `msg.sender`, but do not emit it
130	        emit NewAdmin(previousAdmin, pendingAdmin);
```

*GitHub* : [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L129), [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L130)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
// @audit Current function use `msg.sender`, but do not emit it
42	        emit NewPendingAdmin(pendingAdmin, address(0));
...
// @audit Current function use `msg.sender`, but do not emit it
43	        emit NewAdmin(previousAdmin, pendingAdmin);
```

*GitHub* : [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L42), [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L43)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

```solidity
// @audit Current function use `msg.sender`, but do not emit it
107	        emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);
```

*GitHub* : [107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L107)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
// @audit Current function use `msg.sender`, but do not emit it
103	        emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);
...
// @audit Current function use `msg.sender`, but do not emit it
128	        emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);
```

*GitHub* : [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L103), [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L128)

### [N-08]<a name="n-08"></a> A function which defines named returns in it's declaration doesn't need to use `return`

Once the return variable has been assigned (or has its default value), there is no need to explicitly return it at the end of the function, since it's returned automatically.
Remove the return statement once ensuring it is safe to do so

*There are 1 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
116	    function createNewChain(
117	        uint256 _chainId,
118	        address _stateTransitionManager,
119	        address _baseToken,
120	        uint256, //_salt
121	        address _admin,
122	        bytes calldata _initData
123	    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
```

*GitHub* : [116..123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L116-L123)

### [N-09]<a name="n-09"></a> NatSpec `@return` argument is missing



*There are 171 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
184	    function bridgehubDeposit(
185	        uint256 _chainId,
186	        address _prevMsgSender,
187	        uint256, // l2Value, needed for Weth deposits in the future
188	        bytes calldata _data
189	    ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
...
245	    function _getDepositL2Calldata(
246	        address _l1Sender,
247	        address _l2Receiver,
248	        address _l1Token,
249	        uint256 _amount
250	    ) internal view returns (bytes memory) {
...
256	    function _getERC20Getters(address _token) internal view returns (bytes memory) {
...
411	    function _finalizeWithdrawal(
412	        uint256 _chainId,
413	        uint256 _l2BatchNumber,
414	        uint256 _l2MessageIndex,
415	        uint16 _l2TxNumberInBatch,
416	        bytes calldata _message,
417	        bytes32[] calldata _merkleProof
418	    ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
...
460	    function _checkWithdrawal(
461	        uint256 _chainId,
462	        MessageParams memory _messageParams,
463	        bytes calldata _message,
464	        bytes32[] calldata _merkleProof
465	    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
...
489	    function _parseL2WithdrawalMessage(
490	        uint256 _chainId,
491	        bytes memory _l2ToL1message
492	    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
```

*GitHub* : [184..189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L184-L189), [245..250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L245-L250), [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L256), [411..418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L411-L418), [460..465](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L460-L465), [489..492](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L489-L492)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
77	    function getStateTransition(uint256 _chainId) public view returns (address) {
...
116	    function createNewChain(
117	        uint256 _chainId,
118	        address _stateTransitionManager,
119	        address _baseToken,
120	        uint256, //_salt
121	        address _admin,
122	        bytes calldata _initData
123	    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
...
154	    function proveL2MessageInclusion(
155	        uint256 _chainId,
156	        uint256 _batchNumber,
157	        uint256 _index,
158	        L2Message calldata _message,
159	        bytes32[] calldata _proof
160	    ) external view override returns (bool) {
...
166	    function proveL2LogInclusion(
167	        uint256 _chainId,
168	        uint256 _batchNumber,
169	        uint256 _index,
170	        L2Log memory _log,
171	        bytes32[] calldata _proof
172	    ) external view override returns (bool) {
```

*GitHub* : [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L77), [116..123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L116-L123), [154..160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L154-L160), [166..172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L166-L172), [178..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L178-L186), [200..205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L200-L205), [219..221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L219-L221), [264..266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L264-L266), [327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L327)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L86), [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L91), [97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L97), [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L102), [107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L107), [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L206)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L76)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L104)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [34..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L34-L38), [132..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L132-L135), [310](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L310), [453..457](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L453-L457), [500..505](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L500-L505), [515](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515), [525](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525), [537..542](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542), [561..564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L561-L564), [587](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L587), [592](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L592), [597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597), [625..628](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L625-L628), [679](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L679)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L34), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L39), [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L44), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L49), [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L54), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L59), [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L64), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L69), [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L74), [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L79), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L84), [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L89), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L94), [99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L99), [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L104), [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L109), [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L114), [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L119), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L124), [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L129), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L134), [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L139), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L144), [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L149), [154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L154), [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L159), [165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L165), [178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L178), [183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183), [190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L190), [195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L195), [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L204), [219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L219), [225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L225), [231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L231), [241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L241), [246](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L246), [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L251), [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L256), [261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L261)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [49..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L49-L51), [56..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L56-L61), [66..71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L66-L71), [76..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L76-L83), [106..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L106-L111), [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L132), [145..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L145-L149), [199..207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L199-L207), [230..232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L230-L232), [260..265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L260-L265), [291..295](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L291-L295), [318..322](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L318-L322), [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L355)


---

	 - code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol


*GitHub* : [15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L15)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L16)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L13), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L19)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol


*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L21), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L28), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L35), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L42)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L42)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [111..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L111-L114), [130..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L130-L132)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L26), [28..35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L28-L35), [37..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L37-L43), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L69), [71..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L71-L75)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [60..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L60-L64), [66..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L66-L74), [99..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L99-L105), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L116), [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L118), [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L120), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L122), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L124), [130..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L130-L135)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L19), [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L21), [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L23)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L71), [75..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L75-L81), [83..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L83-L89), [91..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L91-L99), [101..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L101-L103), [105..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L105-L107), [109..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L109-L114), [118..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L118-L125)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L43), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L45), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L47), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L49), [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L51), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L63)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L45), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L65), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L73)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [100..102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L100-L102)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L10)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L111), [140..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L140-L144), [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L159), [166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L166)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L161), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173), [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L180), [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L185)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L36), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L38), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L40)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L18), [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L20)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L55)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L29), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39), [78..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L78-L83), [97..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L97-L107), [123..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L123-L129)

### [N-10]<a name="n-10"></a> NatSpec `@param` is missing



*There are 265 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
55	    /// @dev Contract is expected to be used as proxy implementation.
56	    /// @dev Initialize the implementation to prevent Parity hack.
57	    constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
...
64	    /// @dev transfer token to shared bridge as part of upgrade
65	    function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
...
76	    /// @return The L2 token address that would be minted for deposit of the given L1 token on zkSync Era.
77	    function l2TokenAddress(address _l1Token) external view returns (address) {
...
160	    /// @dev Transfers tokens from the depositor address to the shared bridge address.
161	    /// @return The difference between the contract balance before and after the transferring of funds.
162	    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```

*GitHub* : [55..57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55-L57), [64..65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64-L65), [76..77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76-L77), [160..162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160-L162)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
90	    /// @dev Contract is expected to be used as proxy implementation.
91	    /// @dev Initialize the implementation to prevent Parity hack.
92	    constructor(
93	        address _l1WethAddress,
94	        IBridgehub _bridgehub,
95	        IL1ERC20Bridge _legacyBridge
96	    ) reentrancyGuardInitializer {
...
103	    /// @dev Initializes a contract bridge for later use. Expected to be used in the proxy
104	    /// @param _owner Address which can change L2 token implementation and upgrade the bridge
105	    /// implementation. The owner is the Governor and separate from the ProxyAdmin from now on, so that the Governor can call the bridge.
106	    function initialize(
107	        address _owner,
108	        uint256 _eraFirstPostUpgradeBatch
109	    ) external reentrancyGuardInitializer initializer {
...
117	    /// @dev tranfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process
118	    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
...
139	    function receiveEth(uint256 _chainId) external payable {
...
143	    /// @dev Initializes the l2Bridge address by governance for a specific chain.
144	    function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner {
...
148	    /// @notice Allows bridgehub to acquire mintValue for L1->L2 transactions.
149	    /// @dev If the corresponding L2 transaction fails, refunds are issued to a refund recipient on L2.
150	    function bridgehubDepositBaseToken(
151	        uint256 _chainId,
152	        address _prevMsgSender,
153	        address _l1Token,
154	        uint256 _amount
155	    ) external payable virtual onlyBridgehubOrEra(_chainId) {
```

*GitHub* : [90..96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90-L96), [103..109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L103-L109), [117..118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L117-L118), [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L139), [143..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L143-L144), [148..155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L148-L155), [173..175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L173-L175), [183..189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L183-L189), [232..238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L232-L238), [244..250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L244-L250), [255..256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L255-L256), [270..289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L270-L289), [304..316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L304-L316), [409..418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L409-L418), [459..465](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L459-L465), [489..492](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L489-L492), [532..564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L532-L564)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [42..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L42-L43), [52..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L52-L53), [76..77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L76-L77), [83..84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83-L84), [92..94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L92-L94), [102..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102-L103), [108..110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108-L110), [114..123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114-L123), [153..160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L153-L160), [165..172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L165-L172), [177..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L177-L186), [199..205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L199-L205), [215..221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L215-L221), [255..266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L255-L266), [327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L327)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [84..86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L84-L86), [90..91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L90-L91), [96..97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L96-L97), [101..102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L101-L102), [106..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L106-L107)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [58..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58-L60), [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L76), [80..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L80-L83), [111..112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L111-L112), [133..134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L133-L134), [138..139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138-L139), [143..148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L143-L148), [153..157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L153-L157), [161..162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L161-L162), [166..167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L166-L167), [171..172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L171-L172), [178..179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L178-L179), [232..235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L232-L235), [240..247](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L240-L247)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57), [74..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L74-L75), [79..80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L79-L80), [88..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L88-L89), [97..98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L97-L98), [103..104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L103-L104), [108..113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L108-L113), [126..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L126-L132), [145..148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L145-L148), [152..155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L152-L155), [159..166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L159-L166), [170..178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L170-L178), [182..184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L182-L184), [203..208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L203-L208), [225..227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L225-L227)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


*GitHub* : [23..26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L23-L26)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L13)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [24..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L24-L25), [46..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L46-L47), [52..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L52-L53), [59..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L59-L60), [68..69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L68-L69), [80..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L80-L81), [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L91), [101..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L101-L105), [124..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L124-L125)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [31..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L31-L38), [128..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L128-L135), [200..204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L200-L204), [208..213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L208-L213), [217..220](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L217-L220), [309..310](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L309-L310), [319..323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L319-L323), [338..342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L338-L342), [346..347](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L346-L347), [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351), [369..374](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L369-L374), [378..384](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L378-L384), [388..392](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L388-L392), [440](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L440), [452..457](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L452-L457), [471..472](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L471-L472), [476..477](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L476-L477), [481](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L481), [499..505](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L499-L505), [515](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515), [537..542](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542), [586..587](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L586-L587), [591..592](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L591-L592), [596..597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L596-L597), [601..609](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L601-L609), [621..628](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L621-L628), [676..679](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L676-L679)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [113..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L113-L114), [118..119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L118-L119), [123..124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L123-L124), [164..165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L164-L165), [182..183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L182-L183), [189..190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L189-L190), [218..219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L218-L219), [230..231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L230-L231), [255..256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L255-L256)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [48..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L48-L51), [55..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L55-L61), [65..71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L65-L71), [75..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L75-L83), [105..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L105-L111), [131..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L131-L132), [144..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L144-L149), [179..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L179-L186), [198..207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L198-L207), [230..232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L230-L232), [260..265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L260-L265), [291..295](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L291-L295), [317..322](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L317-L322), [354..355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L354-L355)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [178..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L178-L186)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L13), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L19)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol


*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L21), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L28), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L35), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L42)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [126..128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L126-L128), [149..151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L149-L151), [172..174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L172-L174), [189..191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L189-L191), [202..207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L202-L207), [228..230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L228-L230), [257..259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L257-L259), [278..280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L278-L280)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L41-L42)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [35..37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L35-L37), [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L41-L42), [46..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L46-L47), [51..52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L51-L52), [56..57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L56-L57), [65..66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L65-L66), [72..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L72-L74)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L26), [28..35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L28-L35), [37..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L37-L43), [45..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L45-L53), [55..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L55-L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L63), [71..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L71-L75), [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L77)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [60..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L60-L64), [66..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L66-L74), [76..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L76-L85), [87..97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L87-L97), [99..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L99-L105), [107..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L107-L114), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L122), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L124), [126..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L126-L135), [137..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L137-L142), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L144), [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L146)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [9..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L9-L15), [17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L17), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L19), [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L21)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol


*GitHub* : [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L9)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [60..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L60-L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L67), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L71), [73..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L73-L81), [83..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L83-L89), [91..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L91-L99), [101..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L101-L103), [105..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L105-L107), [109..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L109-L114), [118..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L118-L125), [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L127), [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L129), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L131), [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L133)


---

	 - code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol


*GitHub* : [26..27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L26-L27)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L43), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L45), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L47), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L49), [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L51), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L53), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L67)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L55), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L63), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L71), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L73), [75..82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L75-L82), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L84), [86..90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L86-L90), [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L92), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L94), [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L96)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L41-L42), [44..45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L44-L45), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L47)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol


*GitHub* : [144..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L144-L149), [162..168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L162-L168), [176..177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L176-L177), [185..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L185-L186)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol


*GitHub* : [66..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L66-L67), [69..70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L69-L70), [72..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L72-L75), [134..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L134-L135), [140..141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L140-L141), [143..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L143-L144), [146..147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L146-L147)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol


*GitHub* : [26..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L26-L30)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [100..102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L100-L102)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol


*GitHub* : [18..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L18-L25)


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L7)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L10)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [47..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L47-L56), [110..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L110-L111), [139..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L139-L144), [150..151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150-L151), [158..159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L158-L159), [163..166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L163-L166)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [179..180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L179-L180), [184..185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L184-L185)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [11..17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11-L17)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [11..18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L11-L18)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [26..32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L26-L32), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L34), [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L36), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L38)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L14), [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L16)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [36..52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L36-L52)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L16), [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L18)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L29), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39), [78..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L78-L83), [97..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L97-L107), [123..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L123-L129)

### [N-11]<a name="n-11"></a> Use multiple `require()` and `if` statements instead of `&&`

Using multiple `require()` and `if` improves code readability and makes it easier to debug.

*There are 5 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
77	        require(
78	            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
79	            "L1SharedBridge: not bridgehub or era chain"
80	        );
```

*GitHub* : [77..80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L77-L80)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
363	        if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {
364	            delete s.l2SystemContractsUpgradeTxHash;
365	            delete s.l2SystemContractsUpgradeBatchNumber;
366	        }
...
668	            require(
669	                (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
670	                    (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
671	                "bh"
672	            );
```

*GitHub* : [363..366](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L363-L366), [668..672](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L668-L672)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

```solidity
149	        if (
150	            _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) &&
151	            _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) &&
152	            _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)
153	        ) {
154	            return;
155	        }
```

*GitHub* : [149..155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L149-L155)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

```solidity
43	        require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash
```

*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43)

### [N-12]<a name="n-12"></a> Change `public` to `external` for functions that are not called internally

Contracts [are allowed](https://docs.soliditylang.org/en/latest/contracts.html#function-overriding) to override their parents' functions and change the visibility from `external` to `public`.

*There are 10 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
56	    function proveL2MessageInclusion(
57	        uint256 _batchNumber,
58	        uint256 _index,
59	        L2Message memory _message,
60	        bytes32[] calldata _proof
61	    ) public view returns (bool) {
...
76	    function proveL1ToL2TransactionStatus(
77	        bytes32 _l2TxHash,
78	        uint256 _l2BatchNumber,
79	        uint256 _l2MessageIndex,
80	        uint16 _l2TxNumberInBatch,
81	        bytes32[] calldata _merkleProof,
82	        TxStatus _status
83	    ) public view returns (bool) {
...
145	    function l2TransactionBaseCost(
146	        uint256 _gasPrice,
147	        uint256 _l2GasLimit,
148	        uint256 _l2GasPerPubdataByteLimit
149	    ) public view returns (uint256) {
```

*GitHub* : [56..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L56-L61), [76..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L76-L83), [145..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L145-L149)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

```solidity
69	    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public virtual returns (bytes32 txHash) {
```

*GitHub* : [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L69)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

```solidity
49	    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public virtual override returns (bytes32) {
```

*GitHub* : [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L49)


---

	 - code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

```solidity
15	    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```

*GitHub* : [15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L15)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

```solidity
16	    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L16)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
161	    function name() public view override returns (string memory) {
...
167	    function symbol() public view override returns (string memory) {
...
173	    function decimals() public view override returns (uint8) {
```

*GitHub* : [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L161), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173)

### [N-13]<a name="n-13"></a> `Import` only specific files

Using import declarations of the form `import {<identifier_name>} from "some/file.sol"` avoids polluting the symbol namespace making flattened files smaller, and speeds up compilation

*There are 22 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
9	import "./IBridgehub.sol";
...
10	import "../bridge/interfaces/IL1SharedBridge.sol";
...
11	import "../state-transition/IStateTransitionManager.sol";
...
12	import "../common/ReentrancyGuard.sol";
...
13	import "../state-transition/chain-interfaces/IZkSyncStateTransition.sol";
...
16	import "../vendor/AddressAliasHelper.sol";
```

*GitHub* : [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L9), [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L10), [11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L11), [12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L12), [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L13), [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L16)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

```solidity
14	import "../l2-deps/ISystemContext.sol";
```

*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L14)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

```solidity
7	import "../state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol";
...
8	import "../state-transition/chain-interfaces/IMailbox.sol";
...
9	import "../state-transition/chain-interfaces/IVerifier.sol";
```

*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L7), [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L8), [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L9), [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L10), [11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L11), [12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L12)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L7), [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L8), [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L9)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L7)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L8), [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L9), [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L10)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol


*GitHub* : [15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L15)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L7)

### [N-14]<a name="n-14"></a> `Constants` in comparisons should appear on the left side

Doing so will prevent [typo bugs](https://www.moserware.com/2008/01/constants-on-left-are-better-but-this.html)

*There are 166 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
143	        require(_amount != 0, "0T"); // empty deposit
...
188	        require(amount != 0, "2T"); // empty deposit
```

*GitHub* : [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L143), [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L188)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
110	        require(_owner != address(0), "ShB owner 0");
...
131	            require(amount > 0, "ShB: 0 amount to transfer");
...
160	            require(msg.value == 0, "ShB m.v > 0 b d.it");
...
190	        require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
...
204	            require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
...
202	            require(_depositAmount == 0, "ShB wrong withdraw amount");
...
210	        require(amount != 0, "6T"); // empty deposit amount
...
239	        require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");
```

*GitHub* : [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L110), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131), [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L160), [190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L190), [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L204), [202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202), [210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L210), [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L239), [329](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L329), [503](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L503), [519](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L519), [565](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L565), [580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L580)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L124), [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134), [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L227), [328](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L328), [331](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L331)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L44), [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L109), [242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L242)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L84), [108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L108), [248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L248)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L70)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L28), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L29), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L53)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol


*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L27), [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L27), [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L32)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L39), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L65), [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L70), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L52), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L53), [111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L111), [193](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L193), [196](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L196), [194](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L194), [233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L233), [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L239), [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L239), [286](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L286), [293](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L293), [325](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L325), [363](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L363), [428](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L428), [431](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L431), [442](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L442), [581](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L581), [582](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L582), [582](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L582), [593](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L593), [631](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631), [633](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L633), [639](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L639), [663](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L663), [669](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L669), [669](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L669), [670](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670), [670](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L171), [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L185)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L160), [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L174), [277](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L277), [279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L279)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L95), [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L112), [150](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L150), [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L151), [152](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L152), [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L188), [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L251), [253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L253)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L35), [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L37)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25), [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25), [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L27), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L28), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L29), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L29), [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L30), [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L32), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L34), [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43), [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L45), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L45), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L52)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


*GitHub* : [15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L15)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L109), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L134), [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L143), [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L157), [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L163), [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L177), [183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L183), [196](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L196), [215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L215), [235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L235), [252](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L252), [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L264), [281](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L281), [288](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L288), [299](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L299), [282](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L282)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


*GitHub* : [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L25), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L29), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L29), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L45), [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L50), [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L50)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L26), [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L27), [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L32), [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L32)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L62), [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L82)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L52), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L53), [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L54), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55), [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L56), [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L58), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L59), [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L60), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L61), [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L62)


---

	 - code/contracts/ethereum/contracts/common/Config.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L16), [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L114)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L60)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L57), [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L58), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L59), [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L60), [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L70), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L94), [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L98), [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L126), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L131)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L53), [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L139)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L72), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L73), [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L74), [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L76), [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L78)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L9), [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L9), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L61), [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L118), [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L119), [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L120), [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L130), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L131), [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L132), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L134), [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L137)

### [N-15]<a name="n-15"></a> Do not use underscore at the end of variable name

The use of underscore at the end of the variable name is uncommon and also suggests that the variable name was not completely changed.

Consider refactoring variableName_ to variableName.

*There are 1 instance(s) of this issue:*


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
33	    uint8 private decimals_;
```

*GitHub* : [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L33)

### [N-16]<a name="n-16"></a> Event is missing `indexed` field



*There are 30 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
31	    event NewExecutionDelay(uint256 _newExecutionDelay);
...
34	    event ValidatorAdded(uint256 _chainId, address _addedValidator);
...
37	    event ValidatorRemoved(uint256 _chainId, address _removedValidator);
```

*GitHub* : [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L31), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L34), [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L37)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

```solidity
60	    event NewVerifierParams(VerifierParams oldVerifierParams, VerifierParams newVerifierParams);
...
63	    event UpgradeComplete(uint256 indexed newProtocolVersion, bytes32 indexed l2UpgradeTxHash, ProposedUpgrade upgrade);
```

*GitHub* : [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L60), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L63)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
26	    event DiamondCut(FacetCut[] facetCuts, address initAddress, bytes initCalldata);
```

*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L26)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

```solidity
22	    event WithdrawalFinalized(address indexed to, address indexed l1Token, uint256 amount);
...
24	    event ClaimedFailedDeposit(address indexed to, address indexed l1Token, uint256 amount);
```

*GitHub* : [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L22), [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L24)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

```solidity
33	    event BridgehubDepositBaseTokenInitiated(
34	        uint256 indexed chainId,
35	        address indexed from,
36	        address l1Token,
37	        uint256 amount
38	    );
```

*GitHub* : [33..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L33-L38)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol

```solidity
135	    event NewChain(uint256 indexed chainId, address stateTransitionManager, address indexed chainGovernance);
```

*GitHub* : [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L135)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L70), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L73), [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L79), [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L82)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [32..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L32-L36)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L63), [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L66), [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L76), [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L79), [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L82), [85..90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L85-L90), [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L93)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol


*GitHub* : [213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L213)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [125..131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L125-L131), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L136)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol


*GitHub* : [19..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L19-L23)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L24)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L8), [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L10), [12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L12)

### [N-17]<a name="n-17"></a> Numeric values having to do with time should use time units for readability

There are [units](https://docs.soliditylang.org/en/latest/units-and-global-variables.html#time-units) for seconds, minutes, hours, days, and weeks, and since they're defined, they should be used

*There are 4 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

```solidity
70	    uint256[7] __DEPRECATED_diamondCutStorage;
```

*GitHub* : [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L70)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

```solidity
29	            uint256 bitOffset = (_index & 7) * 32;
...
50	            uint256 bitOffset = (_index & 7) * 32;
```

*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L29), [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L50)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

```solidity
45	uint256 constant L2_LOG_KEY_OFFSET = 24;
```

*GitHub* : [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L45)

### [N-18]<a name="n-18"></a> Consider using `delete` rather than assigning zero/false to clear values

The `delete` keyword more closely matches the semantics of what is being done, and draws more attention to the changing of state, which may lead to a more thorough audit of its associated logic

*There are 4 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
99	        stateTransitionManagerIsRegistered[_stateTransitionManager] = false;
...
278	                baseTokenMsgValue = 0;
```

*GitHub* : [99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L99), [278](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L278)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
93	        validators[_chainId][_validator] = false;
```

*GitHub* : [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L93)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
149	        diamondStorage.isFrozen = false;
```

*GitHub* : [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L149)

### [N-19]<a name="n-19"></a> Array is `push()`ed but not `pop()`ed

Array entries are added but are never removed. Consider whether this should be the case, or whether there should be a maximum, or whether old entries should be removed. Cases where there are specific potential problems will be flagged separately under a different issue.

*There are 2 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
198	            ds.facets.push(_facet);
...
225	        ds.facetToSelectors[_facet].selectors.push(_selector);
```

*GitHub* : [198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L198), [225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L225)

### [N-20]<a name="n-20"></a> Unused contract variables

Note that there may be cases where a variable appears to be used, but this is only because there are multiple definitions of the varible in different files. In such cases, the variable definition should be moved into a separate file. The instances below are the unused variables.

*There are 18 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
47	    mapping(address => uint256) private __DEPRECATED_lastWithdrawalLimitReset;
...
50	    mapping(address => uint256) private __DEPRECATED_withdrawnAmountInWindow;
...
53	    mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L47), [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L50), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L53)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
123	    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
```

*GitHub* : [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
228	            (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```

*GitHub* : [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L228)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
28	    string public constant override getName = "ValidatorTimelock";
...
40	    error AddressAlreadyValidator(uint256 _chainId);
...
43	    error ValidatorDoesNotExist(uint256 _chainId);
...
228	        address contractAddress = stateTransitionManager.stateTransition(_chainId);
```

*GitHub* : [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L28), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L40), [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L43), [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L228)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
22	    string public constant override getName = "AdminFacet";
```

*GitHub* : [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L22)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L27)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L37), [359](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L359)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L265), [271](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L271)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L31), [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L41)

### [N-21]<a name="n-21"></a> Assembly block creates dirty bits

Writing data to the free memory pointer without later updating the free memory pointer will cause there to be dirty bits at that memory location. Not updating the free memory pointer will make it [harder](https://docs.soliditylang.org/en/latest/ir-breaking-changes.html#cleanup) for the optimizer to reason about whether the memory needs to be cleaned before use, which will lead to worse optimizations. Update the free memory pointer and annotate the block (`assembly (\"memory-safe\") { ... }`) to avoid this issue.

*There are 1 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

```solidity
35	        assembly {
36	            // The pointer to the free memory slot
37	            let ptr := mload(0x40)
38	            // Copy function signature and arguments from calldata at zero position into memory at pointer position
39	            calldatacopy(ptr, 0, calldatasize())
40	            // Delegatecall method of the implementation contract returns 0 on error
41	            let result := delegatecall(gas(), facetAddress, ptr, calldatasize(), 0, 0)
42	            // Get the size of the last return data
43	            let size := returndatasize()
44	            // Copy the size length of bytes from return data at zero position to pointer position
45	            returndatacopy(ptr, 0, size)
46	            // Depending on the result value
47	            switch result
48	            case 0 {
49	                // End execution and revert state changes
50	                revert(ptr, size)
51	            }
52	            default {
53	                // Return data with length of size at pointers position
54	                return(ptr, size)
55	            }
56	        }
```

*GitHub* : [35..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L35-L56)

### [N-22]<a name="n-22"></a> `else`-block not required

One level of nesting can be removed by not having an `else` block when the `if`-block returns, and `if (foo) { return 1; } else { return 2; }` becomes `if (foo) { return 1; } return 2;`

*There are 3 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
109	        if (timestamp == 0) {
110	            return OperationState.Unset;
111	        } else if (timestamp == EXECUTED_PROPOSAL_TIMESTAMP) {
112	            return OperationState.Done;
113	        } else if (timestamp > block.timestamp) {
114	            return OperationState.Waiting;
115	        } else {
116	            return OperationState.Ready;
117	        }
...
111	        } else if (timestamp == EXECUTED_PROPOSAL_TIMESTAMP) {
112	            return OperationState.Done;
113	        } else if (timestamp > block.timestamp) {
114	            return OperationState.Waiting;
115	        } else {
116	            return OperationState.Ready;
117	        }
...
113	        } else if (timestamp > block.timestamp) {
114	            return OperationState.Waiting;
115	        } else {
116	            return OperationState.Ready;
117	        }
```

*GitHub* : [109..117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L109-L117), [111..117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L111-L117), [113..117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L113-L117)

### [N-23]<a name="n-23"></a> Convert simple if-statements to ternary expressions

The code can be made more compact while also increasing readability by converting the following `if`-statements to ternaries (e.g. `foo += (x > y) ? a : b`)

*There are 15 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
119	        if (_token == ETH_TOKEN_ADDRESS) {
120	            uint256 balanceBefore = address(this).balance;
121	            IMailbox(_target).transferEthToSharedBridge();
122	            uint256 balanceAfter = address(this).balance;
123	            require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");
124	            chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
125	                chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
126	                balanceAfter -
127	                balanceBefore;
128	        } else {
129	            uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
130	            uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
131	            require(amount > 0, "ShB: 0 amount to transfer");
132	            IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);
133	            uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
134	            require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
135	            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
136	        }
...
200	        if (_l1Token == ETH_TOKEN_ADDRESS) {
201	            amount = msg.value;
202	            require(_depositAmount == 0, "ShB wrong withdraw amount");
203	        } else {
204	            require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
205	            amount = _depositAmount;
206	
207	            uint256 withdrawAmount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount);
208	            require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic
209	        }
...
506	        if (bytes4(functionSignature) == IMailbox.finalizeEthWithdrawal.selector) {
507	            // this message is a base token withdrawal
508	            (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
509	            (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);
510	            l1Token = bridgehub.baseToken(_chainId);
511	        } else if (bytes4(functionSignature) == IL1ERC20Bridge.finalizeWithdrawal.selector) {
512	            // We use the IL1ERC20Bridge for backward compatibility with old withdrawals.
513	
514	            // this message is a token withdrawal
515	
516	            // Check that the message length is correct.
517	            // It should be equal to the length of the function signature + address + address + uint256 = 4 + 20 + 20 + 32 =
518	            // 76 (bytes).
519	            require(_l2ToL1message.length == 76, "ShB wrong msg len 2");
520	            (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
521	            (l1Token, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
522	            (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);
523	        } else {
524	            revert("ShB Incorrect message function selector");
525	        }
```

*GitHub* : [119..136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L119-L136), [200..209](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L200-L209), [506..525](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L506-L525)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
270	            if (token == ETH_TOKEN_ADDRESS) {
271	                require(
272	                    msg.value == _request.mintValue + _request.secondBridgeValue,
273	                    "Bridgehub: msg.value mismatch 2"
274	                );
275	                baseTokenMsgValue = _request.mintValue;
276	            } else {
277	                require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3");
278	                baseTokenMsgValue = 0;
279	            }
...
328	        if (_refundRecipient == address(0)) {
329	            // If the `_refundRecipient` is not provided, we use the `msg.sender` as the recipient.
330	            _recipient = msg.sender == tx.origin ? msg.sender : AddressAliasHelper.applyL1ToL2Alias(msg.sender);
331	        } else if (_refundRecipient.code.length > 0) {
332	            // If the `_refundRecipient` is a smart contract, we apply the L1 to L2 alias to prevent foot guns.
333	            _recipient = AddressAliasHelper.applyL1ToL2Alias(_refundRecipient);
334	        } else {
335	            _recipient = _refundRecipient;
336	        }
...
331	        } else if (_refundRecipient.code.length > 0) {
332	            // If the `_refundRecipient` is a smart contract, we apply the L1 to L2 alias to prevent foot guns.
333	            _recipient = AddressAliasHelper.applyL1ToL2Alias(_refundRecipient);
334	        } else {
335	            _recipient = _refundRecipient;
336	        }
```

*GitHub* : [270..279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L270-L279), [328..336](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L328-L336), [331..336](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L331-L336)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
54	        } else if (pubdataSource == uint8(PubdataSource.Blob)) {
55	            // We want only want to include the actual blob linear hashes when we send pubdata via blobs.
56	            // Otherwise we should be using bytes32(0)
57	            blobHashes[0] = logOutput.blob1Hash;
58	            blobHashes[1] = logOutput.blob2Hash;
59	            // In this scenario, pubdataCommitments is a list of: opening point (16 bytes) || claimed value (32 bytes) || commitment (48 bytes) || proof (48 bytes)) = 144 bytes
60	            blobCommitments = _verifyBlobInformation(_newBatch.pubdataCommitments[1:], blobHashes);
61	        } else if (pubdataSource == uint8(PubdataSource.Calldata)) {
62	            // In this scenario pubdataCommitments is actual pubdata consisting of l2 to l1 logs, l2 to l1 message, compressed smart contract bytecode, and compressed state diffs
63	            require(
64	                logOutput.pubdataHash ==
65	                    keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),
66	                "wp"
67	            );
68	            blobHashes[0] = logOutput.blob1Hash;
69	            blobCommitments[0] = bytes32(
70	                _newBatch.pubdataCommitments[_newBatch.pubdataCommitments.length - 32:_newBatch
71	                    .pubdataCommitments
72	                    .length]
73	            );
74	        }
...
155	            if (logKey == uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)) {
156	                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");
157	                logOutput.l2LogsTreeRoot = logValue;
158	            } else if (logKey == uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)) {
159	                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");
160	                logOutput.pubdataHash = logValue;
161	            } else if (logKey == uint256(SystemLogKey.STATE_DIFF_HASH_KEY)) {
162	                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");
163	                logOutput.stateDiffHash = logValue;
164	            } else if (logKey == uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)) {
165	                require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");
166	                logOutput.packedBatchAndL2BlockTimestamp = uint256(logValue);
167	            } else if (logKey == uint256(SystemLogKey.PREV_BATCH_HASH_KEY)) {
168	                require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");
169	                logOutput.previousBatchHash = logValue;
170	            } else if (logKey == uint256(SystemLogKey.CHAINED_PRIORITY_TXN_HASH_KEY)) {
171	                require(logSender == L2_BOOTLOADER_ADDRESS, "bl");
172	                logOutput.chainedPriorityTxsHash = logValue;
173	            } else if (logKey == uint256(SystemLogKey.NUMBER_OF_LAYER_1_TXS_KEY)) {
174	                require(logSender == L2_BOOTLOADER_ADDRESS, "bk");
175	                logOutput.numberOfLayer1Txs = uint256(logValue);
176	            } else if (logKey == uint256(SystemLogKey.BLOB_ONE_HASH_KEY)) {
177	                require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");
178	                logOutput.blob1Hash = logValue;
179	            } else if (logKey == uint256(SystemLogKey.BLOB_TWO_HASH_KEY)) {
180	                require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");
181	                logOutput.blob2Hash = logValue;
182	            } else if (logKey == uint256(SystemLogKey.EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY)) {
183	                require(logSender == L2_BOOTLOADER_ADDRESS, "bu");
184	                require(_expectedSystemContractUpgradeTxHash == logValue, "ut");
185	            } else {
186	                revert("ul");
187	            }
...
158	            } else if (logKey == uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)) {
159	                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");
160	                logOutput.pubdataHash = logValue;
161	            } else if (logKey == uint256(SystemLogKey.STATE_DIFF_HASH_KEY)) {
162	                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");
163	                logOutput.stateDiffHash = logValue;
164	            } else if (logKey == uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)) {
165	                require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");
166	                logOutput.packedBatchAndL2BlockTimestamp = uint256(logValue);
167	            } else if (logKey == uint256(SystemLogKey.PREV_BATCH_HASH_KEY)) {
168	                require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");
169	                logOutput.previousBatchHash = logValue;
170	            } else if (logKey == uint256(SystemLogKey.CHAINED_PRIORITY_TXN_HASH_KEY)) {
171	                require(logSender == L2_BOOTLOADER_ADDRESS, "bl");
172	                logOutput.chainedPriorityTxsHash = logValue;
173	            } else if (logKey == uint256(SystemLogKey.NUMBER_OF_LAYER_1_TXS_KEY)) {
174	                require(logSender == L2_BOOTLOADER_ADDRESS, "bk");
175	                logOutput.numberOfLayer1Txs = uint256(logValue);
176	            } else if (logKey == uint256(SystemLogKey.BLOB_ONE_HASH_KEY)) {
177	                require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");
178	                logOutput.blob1Hash = logValue;
179	            } else if (logKey == uint256(SystemLogKey.BLOB_TWO_HASH_KEY)) {
180	                require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");
181	                logOutput.blob2Hash = logValue;
182	            } else if (logKey == uint256(SystemLogKey.EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY)) {
183	                require(logSender == L2_BOOTLOADER_ADDRESS, "bu");
184	                require(_expectedSystemContractUpgradeTxHash == logValue, "ut");
185	            } else {
186	                revert("ul");
187	            }
...
161	            } else if (logKey == uint256(SystemLogKey.STATE_DIFF_HASH_KEY)) {
162	                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");
163	                logOutput.stateDiffHash = logValue;
164	            } else if (logKey == uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)) {
165	                require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");
166	                logOutput.packedBatchAndL2BlockTimestamp = uint256(logValue);
167	            } else if (logKey == uint256(SystemLogKey.PREV_BATCH_HASH_KEY)) {
168	                require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");
169	                logOutput.previousBatchHash = logValue;
170	            } else if (logKey == uint256(SystemLogKey.CHAINED_PRIORITY_TXN_HASH_KEY)) {
171	                require(logSender == L2_BOOTLOADER_ADDRESS, "bl");
172	                logOutput.chainedPriorityTxsHash = logValue;
173	            } else if (logKey == uint256(SystemLogKey.NUMBER_OF_LAYER_1_TXS_KEY)) {
174	                require(logSender == L2_BOOTLOADER_ADDRESS, "bk");
175	                logOutput.numberOfLayer1Txs = uint256(logValue);
176	            } else if (logKey == uint256(SystemLogKey.BLOB_ONE_HASH_KEY)) {
177	                require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");
178	                logOutput.blob1Hash = logValue;
179	            } else if (logKey == uint256(SystemLogKey.BLOB_TWO_HASH_KEY)) {
180	                require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");
181	                logOutput.blob2Hash = logValue;
182	            } else if (logKey == uint256(SystemLogKey.EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY)) {
183	                require(logSender == L2_BOOTLOADER_ADDRESS, "bu");
184	                require(_expectedSystemContractUpgradeTxHash == logValue, "ut");
185	            } else {
186	                revert("ul");
187	            }
```

*GitHub* : [54..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L54-L74), [155..187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L155-L187), [158..187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L158-L187), [161..187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L161-L187), [164..187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L164-L187), [167..187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L167-L187), [170..187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L170-L187), [173..187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L173-L187), [176..187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L176-L187)

### [N-24]<a name="n-24"></a> Remaining eth may not be refunded to users

 When a contract function accepts Ethereum and executes a `.call()` or similar function that also forwards Ethereum value, it's important to check for and refund any remaining balance. This is because some of the supplied value may not be used during the call execution due to gas constraints, a revert in the called contract, or simply because not all the value was needed.

If you do not account for this remaining balance, it can become "locked" in the contract. It's crucial to either return the remaining balance to the sender or handle it in a way that ensures it is not permanently stuck. Neglecting to do so can lead to loss of funds and degradation of the contract's reliability. Furthermore, it's good practice to ensure fairness and trust with your users by returning unused funds. 

*There are 33 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
100	    function deposit(
101	        address _l2Receiver,
102	        address _l1Token,
103	        uint256 _amount,
104	        uint256 _l2TxGasLimit,
105	        uint256 _l2TxGasPerPubdataByte
106	    ) external payable returns (bytes32 l2TxHash) {
...
135	    function deposit(
136	        address _l2Receiver,
137	        address _l1Token,
138	        uint256 _amount,
139	        uint256 _l2TxGasLimit,
140	        uint256 _l2TxGasPerPubdataByte,
141	        address _refundRecipient
142	    ) public payable nonReentrant returns (bytes32 l2TxHash) {
```

*GitHub* : [100..106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L100-L106), [135..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L135-L142)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
139	    function receiveEth(uint256 _chainId) external payable {
...
150	    function bridgehubDepositBaseToken(
151	        uint256 _chainId,
152	        address _prevMsgSender,
153	        address _l1Token,
154	        uint256 _amount
155	    ) external payable virtual onlyBridgehubOrEra(_chainId) {
...
184	    function bridgehubDeposit(
185	        uint256 _chainId,
186	        address _prevMsgSender,
187	        uint256, // l2Value, needed for Weth deposits in the future
188	        bytes calldata _data
189	    ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
...
556	    function depositLegacyErc20Bridge(
557	        address _prevMsgSender,
558	        address _l2Receiver,
559	        address _l1Token,
560	        uint256 _amount,
561	        uint256 _l2TxGasLimit,
562	        uint256 _l2TxGasPerPubdataByte,
563	        address _refundRecipient
564	    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
```

*GitHub* : [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L139), [150..155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L150-L155), [184..189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L184-L189), [556..564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L556-L564)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
219	    function requestL2TransactionDirect(
220	        L2TransactionRequestDirect calldata _request
221	    ) external payable override nonReentrant returns (bytes32 canonicalTxHash) {
...
264	    function requestL2TransactionTwoBridges(
265	        L2TransactionRequestTwoBridgesOuter calldata _request
266	    ) external payable override nonReentrant returns (bytes32 canonicalTxHash) {
```

*GitHub* : [219..221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L219-L221), [264..266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L264-L266)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
169	    function execute(Operation calldata _operation) external payable onlyOwnerOrSecurityCouncil {
...
188	    function executeInstant(Operation calldata _operation) external payable onlySecurityCouncil {
```

*GitHub* : [169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L169), [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L188)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [49..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L49-L51), [199..207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L199-L207)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [28..35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L28-L35), [37..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L37-L43)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [66..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L66-L74), [130..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L130-L135), [137..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L137-L142), [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L146)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [9..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L9-L15)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L7)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [101..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L101-L103), [105..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L105-L107)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L61)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [90..98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L90-L98), [100..102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L100-L102)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [81..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L81-L87)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [26..32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L26-L32)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [30..34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L30-L34), [45..52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L45-L52)


---

	 - code/contracts/zksync/contracts/ForceDeployUpgrader.sol


*GitHub* : [15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L15)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L49), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L67)

### [N-25]<a name="n-25"></a> External calls in an un-bounded `for`-loop may result in a DOS

Consider limiting the number of iterations in `for`-loops that make external calls

*There are 20 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
227	        for (uint256 i = 0; i < _calls.length; ++i) {
228	            (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
229	            if (!success) {
230	                // Propagate an error if the call fails.
231	                assembly {
232	                    revert(add(returnData, 0x20), mload(returnData))
233	                }
234	            }
235	        }
```

*GitHub* : [227..235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L227-L235)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
118	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
119	                committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);
120	            }
...
137	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
138	                committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);
139	            }
...
187	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
188	                uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
189	                    _newBatchesData[i].batchNumber
190	                );
191	
192	                // Note: if the `commitBatchTimestamp` is zero, that means either:
193	                // * The batch was committed, but not through this contract.
194	                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
195	                // We allow executing such batches.
196	
197	                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
198	            }
...
211	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
212	                uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
213	
214	                // Note: if the `commitBatchTimestamp` is zero, that means either:
215	                // * The batch was committed, but not through this contract.
216	                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
217	                // We allow executing such batches.
218	
219	                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
220	            }
```

*GitHub* : [118..120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L118-L120), [137..139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L137-L139), [187..198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L187-L198), [211..220](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L211-L220)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
144	        for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
145	            // Extract the values to be compared to/used such as the log sender, key, and value
146	            (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
147	            (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
148	            (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);
149	
150	            // Ensure that the log hasn't been processed already
151	            require(!_checkBit(processedLogs, uint8(logKey)), "kp");
152	            processedLogs = _setBit(processedLogs, uint8(logKey));
153	
154	            // Need to check that each log was sent by the correct address.
155	            if (logKey == uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)) {
156	                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");
157	                logOutput.l2LogsTreeRoot = logValue;
158	            } else if (logKey == uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)) {
159	                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");
160	                logOutput.pubdataHash = logValue;
161	            } else if (logKey == uint256(SystemLogKey.STATE_DIFF_HASH_KEY)) {
162	                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");
163	                logOutput.stateDiffHash = logValue;
164	            } else if (logKey == uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)) {
165	                require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");
166	                logOutput.packedBatchAndL2BlockTimestamp = uint256(logValue);
167	            } else if (logKey == uint256(SystemLogKey.PREV_BATCH_HASH_KEY)) {
168	                require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");
169	                logOutput.previousBatchHash = logValue;
170	            } else if (logKey == uint256(SystemLogKey.CHAINED_PRIORITY_TXN_HASH_KEY)) {
171	                require(logSender == L2_BOOTLOADER_ADDRESS, "bl");
172	                logOutput.chainedPriorityTxsHash = logValue;
173	            } else if (logKey == uint256(SystemLogKey.NUMBER_OF_LAYER_1_TXS_KEY)) {
174	                require(logSender == L2_BOOTLOADER_ADDRESS, "bk");
175	                logOutput.numberOfLayer1Txs = uint256(logValue);
176	            } else if (logKey == uint256(SystemLogKey.BLOB_ONE_HASH_KEY)) {
177	                require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");
178	                logOutput.blob1Hash = logValue;
179	            } else if (logKey == uint256(SystemLogKey.BLOB_TWO_HASH_KEY)) {
180	                require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");
181	                logOutput.blob2Hash = logValue;
182	            } else if (logKey == uint256(SystemLogKey.EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY)) {
183	                require(logSender == L2_BOOTLOADER_ADDRESS, "bu");
184	                require(_expectedSystemContractUpgradeTxHash == logValue, "ut");
185	            } else {
186	                revert("ul");
187	            }
188	        }
...
259	        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
260	            _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));
261	
262	            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
263	            emit BlockCommit(
264	                _lastCommittedBatchData.batchNumber,
265	                _lastCommittedBatchData.batchHash,
266	                _lastCommittedBatchData.commitment
267	            );
268	        }
...
291	        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
292	            // The upgrade transaction must only be included in the first batch.
293	            bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
294	            _lastCommittedBatchData = _commitOneBatch(
295	                _lastCommittedBatchData,
296	                _newBatchesData[i],
297	                expectedUpgradeTxHash
298	            );
299	
300	            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
301	            emit BlockCommit(
302	                _lastCommittedBatchData.batchNumber,
303	                _lastCommittedBatchData.batchHash,
304	                _lastCommittedBatchData.commitment
305	            );
306	        }
...
313	        for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {
314	            PriorityOperation memory priorityOp = s.priorityQueue.popFront();
315	            concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));
316	        }
...
353	        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
354	            _executeOneBatch(_batchesData[i], i);
355	            emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
356	        }
```

*GitHub* : [144..188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L144-L188), [259..268](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L259-L268), [291..306](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L291-L306), [313..316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313-L316), [353..356](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353-L356), [407..422](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L407-L422), [636..658](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636-L658), [667..673](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667-L673)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [358..365](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L358-L365)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [228..233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L228-L233)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [103..120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L103-L120), [140..146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L140-L146), [160..169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L160-L169), [180..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L180-L186)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [31..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L31-L36)

### [N-26]<a name="n-26"></a> `constructor` missing zero address check

It is important to ensure that the constructor does not allow zero address to be set.
    This is a common mistake that can lead to loss of funds or redeployment of the contract.

*There are 5 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
57	    constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L57)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
92	    constructor(
93	        address _l1WethAddress,
94	        IBridgehub _bridgehub,
95	        IL1ERC20Bridge _legacyBridge
96	    ) reentrancyGuardInitializer {
```

*GitHub* : [92..96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L92-L96)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
43	    constructor(address _admin, address _securityCouncil, uint256 _minDelay) {
```

*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L43)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
60	    constructor(address _bridgehub) reentrancyGuardInitializer {
```

*GitHub* : [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L60)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
57	    constructor(address _initialOwner, uint32 _executionDelay) {
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57)

### [N-27]<a name="n-27"></a> Variable initialization with default value

It's not necessary to initialize a variable with its default value, and it's actually worse in gas terms as it adds an overhead.

*There are 24 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
227	        for (uint256 i = 0; i < _calls.length; ++i) {
```

*GitHub* : [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L227)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
118	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
...
137	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
...
187	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
...
211	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```

*GitHub* : [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L118), [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L137), [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L187), [211](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L211)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
144	        for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
...
259	        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
...
291	        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
...
313	        for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {
...
353	        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
```

*GitHub* : [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L144), [259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L259), [291](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L291), [313](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313), [353](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353), [407](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L407), [580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580), [629](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L629), [636](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636), [667](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L210)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [358](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L358)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L228)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L103), [140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L140), [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L160), [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L180)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L94)


---

	 - code/contracts/ethereum/contracts/common/Config.sol


*GitHub* : [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L39)

### [N-28]<a name="n-28"></a> Large multiples of ten should use scientific notation

Use a scientific notation rather than decimal literals (e.g. `1e6` instead of `1000000`), for better code readability. The same for exponentiation  (e.g. `1e18` instead of `10**18`): although the compiler is capable of optimizing it, it is considered good coding practice to utilize idioms that don't rely on compiler optimization, whenever possible.

*There are 2 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/common/Config.sol

```solidity
35	uint256 constant MAX_ALLOWED_PROTOCOL_VERSION_DELTA = 100;
...
94	uint256 constant TX_SLOT_OVERHEAD_L2_GAS = 10000;
```

*GitHub* : [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L35), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L94)

### [N-29]<a name="n-29"></a> Complex math should be split into multiple steps

Consider splitting long arithmetic calculations into multiple steps to improve the code readability.

*There are 1 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
174	        uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata;
```

*GitHub* : [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L174)

### [N-30]<a name="n-30"></a> Duplicated `require/if` statements should be refactored

These statements should be refactored to a separate function, as there are multiple parts of the codebase that use the same logic, to improve the code readability and reduce code duplication.



*There are 69 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
68	        require(amount == _amount, "Incorrect amount");
...
145	        require(amount == _amount, "3T"); // The token has non-standard transfer logic
```

*GitHub* : [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L68), [145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L145)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
196	        require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");
...
200	        if (_l1Token == ETH_TOKEN_ADDRESS) {
...
204	            require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
...
213	        if (!hyperbridgingEnabled[_chainId]) {
...
257	        if (_token == ETH_TOKEN_ADDRESS) {
...
349	        if (!hyperbridgingEnabled[_chainId]) {
...
356	        if (_l1Token == ETH_TOKEN_ADDRESS) {
...
362	            require(callSuccess, "ShB: claimFailedDeposit failed");
```

*GitHub* : [196](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L196), [200](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L200), [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L204), [213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L213), [257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L257), [349](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L349), [356](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L356), [362](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L362), [397](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L397), [423](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L423), [439](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L439), [451](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L451), [566](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L566), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L71), [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L86), [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L119), [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L156), [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L160), [166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L166)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [270](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L270), [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L96), [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L128), [224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L224)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L157), [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L174), [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L179), [193](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L193), [198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L198)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L219), [197](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L197)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L164), [165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L165), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L167), [168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L168), [170](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L170), [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L171), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L173), [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L174), [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L176), [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L177), [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L179), [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L180), [182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L182), [183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L183), [404](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L404), [410](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L410), [616](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616), [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L54), [681](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L681), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L61), [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L155), [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L156), [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L158), [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L159), [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L161), [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L162)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41), [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L187), [208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L208)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L134), [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L157), [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L163), [183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L183)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L67), [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L75)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L58), [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L60)

### [N-31]<a name="n-31"></a> Variable names don't follow the Solidity naming convention

Use `mixedCase` for local and state variables that are not constants, and add a trailing underscore for internal variables. [Documentation](https://docs.soliditylang.org/en/latest/style-guide.html#local-and-state-variable-names)

*There are 8 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
47	    mapping(address => uint256) private __DEPRECATED_lastWithdrawalLimitReset;
...
50	    mapping(address => uint256) private __DEPRECATED_withdrawnAmountInWindow;
...
53	    mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L47), [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L50), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L53)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
192	        (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
...
192	        (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
...
192	        (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
```

*GitHub* : [192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L192), [192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L192), [192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L192)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

```solidity
71	        uint256 _status;
```

*GitHub* : [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L71)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
33	    uint8 private decimals_;
```

*GitHub* : [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L33)

### [N-32]<a name="n-32"></a> Contract functions should use an `interface`

All `external`/`public` functions should extend an `interface`. This is useful to make sure that the whole API is extracted.

*There are 18 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
62	    function initialize() external reentrancyGuardInitializer {}
```

*GitHub* : [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L62)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
106	    function initialize(
107	        address _owner,
108	        uint256 _eraFirstPostUpgradeBatch
109	    ) external reentrancyGuardInitializer initializer {
...
118	    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
...
144	    function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner {
```

*GitHub* : [106..109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L106-L109), [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L144)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
43	    function initialize(address _owner) external reentrancyGuardInitializer {
```

*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L43)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
172	    function revertBatches(uint256 _chainId, uint256 _newLastBatch) external onlyOwnerOrAdmin {
```

*GitHub* : [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L172)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
75	    function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {
...
80	    function addValidator(uint256 _chainId, address _newValidator) external onlyChainAdmin(_chainId) {
...
89	    function removeValidator(uint256 _chainId, address _validator) external onlyChainAdmin(_chainId) {
...
98	    function setExecutionDelay(uint32 _executionDelay) external onlyOwner {
```

*GitHub* : [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L75), [80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L80), [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L89), [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98), [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L104)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L69)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [51..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L51-L56)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L52), [113..118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L113-L118), [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L180), [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L185)


---

	 - code/contracts/zksync/contracts/ForceDeployUpgrader.sol


*GitHub* : [15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L15)

### [N-33]<a name="n-33"></a> State variables should include comments

Consider adding some comments on critical state variables to explain what they are supposed to do: this will help for future code reviews.

*There are 7 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

```solidity
14	    ZkSyncStateTransitionStorage internal s;
```

*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L14)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

```solidity
40	    uint256 private constant _NOT_ENTERED = 1;
...
41	    uint256 private constant _ENTERED = 2;
```

*GitHub* : [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L40), [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L41)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

```solidity
24	    uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L24)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

```solidity
39	    address private l1LegacyBridge;
```

*GitHub* : [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L39)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
28	    ERC20Getters private availableGetters;
```

*GitHub* : [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L28)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol

```solidity
24	    uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L24)

### [N-34]<a name="n-34"></a> Missing NatSpec from contract declarations

Some contracts miss a `@dev`/`@notice` NatSpec, which should be a [best practice](https://docs.soliditylang.org/en/latest/natspec-format.html) to add as a documentation.

*There are 36 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
18	contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
19	    /// @notice all the ether is held by the weth bridge
20	    IL1SharedBridge public sharedBridge;
```

*GitHub* : [18..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L18-L20)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
24	/// @title StateTransition contract
25	/// @author Matter Labs
26	/// @custom:security-contact security@matterlabs.dev
27	contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {
28	    /// @notice Address of the bridgehub
29	    address public immutable bridgehub;
```

*GitHub* : [24..29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L24-L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

```solidity
9	/// @title Diamond Proxy Contract (EIP-2535)
10	/// @author Matter Labs
11	/// @custom:security-contact security@matterlabs.dev
12	contract DiamondProxy {
13	    constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
```

*GitHub* : [9..13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L9-L13)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
17	/// @title Admin Contract controls access rights for contract management.
18	/// @author Matter Labs
19	/// @custom:security-contact security@matterlabs.dev
20	contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {
21	    /// @inheritdoc IZkSyncStateTransitionBase
22	    string public constant override getName = "AdminFacet";
```

*GitHub* : [17..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L17-L22)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
21	/// @title zkSync hyperchain Executor contract capable of processing events emitted in the zkSync hyperchain protocol.
22	/// @author Matter Labs
23	/// @custom:security-contact security@matterlabs.dev
24	contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {
25	    using UncheckedMath for uint256;
```

*GitHub* : [21..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L21-L25)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

```solidity
19	/// @title Getters Contract implements functions for getting contract state from outside the blockchain.
20	/// @author Matter Labs
21	/// @custom:security-contact security@matterlabs.dev
22	contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {
23	    using UncheckedMath for uint256;
```

*GitHub* : [19..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L19-L23)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
29	/// @title zkSync Mailbox contract providing interfaces for L1 <-> L2 interaction.
30	/// @author Matter Labs
31	/// @custom:security-contact security@matterlabs.dev
32	contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {
33	    using UncheckedMath for uint256;
```

*GitHub* : [29..33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L29-L33)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

```solidity
10	/// @title Base contract containing functions accessible to the other facets.
11	/// @author Matter Labs
12	/// @custom:security-contact security@matterlabs.dev
13	contract ZkSyncStateTransitionBase is ReentrancyGuard {
14	    ZkSyncStateTransitionStorage internal s;
```

*GitHub* : [10..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L10-L14)


---

	 - code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

```solidity
10	/// @author Matter Labs
11	/// @custom:security-contact security@matterlabs.dev
12	contract DefaultUpgrade is BaseZkSyncUpgrade {
13	    /// @notice The main function that will be called by the upgrade proxy.
14	    /// @param _proposedUpgrade The upgrade to be executed.
15	    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```

*GitHub* : [10..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L10-L15)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

```solidity
11	/// @author Matter Labs
12	/// @custom:security-contact security@matterlabs.dev
13	contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {
14	    /// @notice The main function that will be called by the upgrade proxy.
15	    /// @param _proposedUpgrade The upgrade to be executed.
16	    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```

*GitHub* : [11..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L11-L16)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [9..12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L9-L12)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [12..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L12-L21)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [11..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L11-L15)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [7..9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L7-L9)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol


*GitHub* : [6..7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L6-L7)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [44..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L44-L47)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [7..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L7-L16)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [28..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L28-L30)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [12..19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L12-L19)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [63..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L63-L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol


*GitHub* : [72..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L72-L85)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol


*GitHub* : [12..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L12-L21)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [10..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L10-L20)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol


*GitHub* : [14..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L14-L21)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol


*GitHub* : [17..19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L17-L19)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol


*GitHub* : [6..11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L6-L11)


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol


*GitHub* : [6..7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L6-L7)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [9..10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L9-L10)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L23-L24)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [7..11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L7-L11)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [7..11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L7-L11)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [7..9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L7-L9)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [7..8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L7-L8)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [16..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L16-L30)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L23-L24)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [28..29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L28-L29)

### [N-35]<a name="n-35"></a> Inconsistent usage of `require`/`error`

Some parts of the codebase use `require` statements, while others use custom errors. Consider refactoring the code to use the same approach: the following findings represent the minority of `require` vs error, and they show the first occurance in each file, for brevity.

*There are 6 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
82	            revert AddressAlreadyValidator(_chainId);
...
91	            revert ValidatorDoesNotExist(_chainId);
...
64	        require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");
...
70	        require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
...
197	                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
...
219	                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
```

*GitHub* : [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L82), [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L91), [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L64), [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L70), [197](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L197), [219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L219)

### [N-36]<a name="n-36"></a> `require`/`revert` without any message

If a transaction reverts, it can be confusing to debug if there aren't any messages. Add a descriptive message to all require/revert statements.

*There are 4 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
53	            require(_newBatch.pubdataCommitments.length == 1);
```

*GitHub* : [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L53)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
163	        if (availableGetters.ignoreName) revert();
...
169	        if (availableGetters.ignoreSymbol) revert();
...
175	        if (availableGetters.ignoreDecimals) revert();
```

*GitHub* : [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L163), [169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L169), [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L175)

### [N-37]<a name="n-37"></a> Events that mark critical parameter changes should contain both the old and the new value

This should especially be done if the new value is not required to be different from the old value

*There are 9 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

```solidity
33	    event BridgehubDepositBaseTokenInitiated(
34	        uint256 indexed chainId,
35	        address indexed from,
36	        address l1Token,
37	        uint256 amount
38	    );
```

*GitHub* : [33..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L33-L38)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol

```solidity
79	    event ChangeSecurityCouncil(address _securityCouncilBefore, address _securityCouncilAfter);
...
82	    event ChangeMinDelay(uint256 _delayBefore, uint256 _delayAfter);
```

*GitHub* : [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L79), [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L82)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

```solidity
32	    event SetChainIdUpgrade(
33	        address indexed _stateTransitionChain,
34	        L2CanonicalTransaction _l2Transaction,
35	        uint256 indexed _protocolVersion
36	    );
```

*GitHub* : [32..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L32-L36)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol

```solidity
63	    event IsPorterAvailableStatusUpdate(bool isPorterAvailable);
...
66	    event ValidatorStatusUpdate(address indexed validatorAddress, bool isActive);
...
82	    event ValidiumModeStatusUpdate(PubdataPricingMode validiumMode);
```

*GitHub* : [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L63), [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L66), [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L82)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol

```solidity
19	    event ProposeTransparentUpgrade(
20	        Diamond.DiamondCutData diamondCut,
21	        uint256 indexed proposalId,
22	        bytes32 proposalSalt
23	    );
```

*GitHub* : [19..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L19-L23)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol

```solidity
24	    event BaseTokenReceived(uint256 amount);
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L24)

### [N-38]<a name="n-38"></a> Constant redefined elsewhere

Consider defining in only one contract so that values cannot become out of sync when only one location is updated. A [cheap way](https://medium.com/coinmonks/gas-cost-of-solidity-library-functions-dbe0cedd4678) to store constants in a single location is to create an `internal constant` in a `library`. If the variable is a local cache of another contract's value, consider making the cache variable internal or private, which will require external users to query the contract with the source of truth, so that callers don't get out of sync.

*There are 11 instance(s) of this issue:*


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol

```solidity
// @audit Variable redefined in: file `cache/solpp-generated-contracts/common/libraries/L2ContractHelper.sol`: `CREATE2_PREFIX`, file `cache-zk/solpp-generated-contracts/L2ContractHelper.sol`: `CREATE2_PREFIX`
87	    bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L87)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

```solidity
// @audit Variable redefined in: file `cache/solpp-generated-contracts/common/libraries/L2ContractHelper.sol`: `CREATE2_PREFIX`, file `cache-zk/solpp-generated-contracts/L2ContractHelper.sol`: `CREATE2_PREFIX`
14	    bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");
```

*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L14)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
// @audit Variable redefined in: file `cache/solpp-generated-contracts/bridge/L1SharedBridge.sol`: `bridgehub`, file `cache/solpp-generated-contracts/state-transition/StateTransitionManager.sol`: `bridgehub`
39	    IBridgehub public immutable override bridgehub;
```

*GitHub* : [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L39)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
// @audit Variable redefined in: file `cache/solpp-generated-contracts/bridge/L1SharedBridge.sol`: `bridgehub`, file `cache/solpp-generated-contracts/state-transition/StateTransitionManager.sol`: `bridgehub`
29	    address public immutable bridgehub;
```

*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L29)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
// @audit Variable redefined in: file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Admin.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Executor.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Getters.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Mailbox.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/ValidatorTimelock.sol`: `getName`
28	    string public constant override getName = "ValidatorTimelock";
```

*GitHub* : [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L28)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
// @audit Variable redefined in: file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Admin.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Executor.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Getters.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Mailbox.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/ValidatorTimelock.sol`: `getName`
22	    string public constant override getName = "AdminFacet";
```

*GitHub* : [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L22)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
// @audit Variable redefined in: file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Admin.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Executor.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Getters.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Mailbox.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/ValidatorTimelock.sol`: `getName`
29	    string public constant override getName = "ExecutorFacet";
```

*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

```solidity
// @audit Variable redefined in: file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Admin.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Executor.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Getters.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Mailbox.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/ValidatorTimelock.sol`: `getName`
27	    string public constant override getName = "GettersFacet";
```

*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L27)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
// @audit Variable redefined in: file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Admin.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Executor.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Getters.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/chain-deps/facets/Mailbox.sol`: `getName`, file `cache/solpp-generated-contracts/state-transition/ValidatorTimelock.sol`: `getName`
37	    string public constant override getName = "MailboxFacet";
```

*GitHub* : [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L37)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol

```solidity
// @audit Variable redefined in: file `cache/solpp-generated-contracts/vendor/AddressAliasHelper.sol`: `offset`, file `cache-zk/solpp-generated-contracts/vendor/AddressAliasHelper.sol`: `offset`
24	    uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L24)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L24)

### [N-39]<a name="n-39"></a> Function ordering does not follow the Solidity style guide

According to the [Solidity style guide](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#order-of-functions), functions should be laid out in the following order :`constructor()`, `receive()`, `fallback()`, `external`, `public`, `internal`, `private`, but the cases below do not follow this pattern

*There are 20 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
// @audit function `_depositFundsToSharedBridge` is `internal` followed by function `claimFailedDeposit` which is `external`
162	    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```

*GitHub* : [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L162)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
// @audit function `_depositFunds` is `internal` followed by function `bridgehubDeposit` which is `external`
175	    function _depositFunds(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
...
// @audit function `_getERC20Getters` is `internal` followed by function `claimFailedDeposit` which is `external`
256	    function _getERC20Getters(address _token) internal view returns (bytes memory) {
...
// @audit function `_isEraLegacyWithdrawal` is `internal` followed by function `finalizeWithdrawal` which is `external`
376	    function _isEraLegacyWithdrawal(uint256 _chainId, uint256 _l2BatchNumber) internal view returns (bool) {
...
// @audit function `_parseL2WithdrawalMessage` is `internal` followed by function `depositLegacyErc20Bridge` which is `external`
489	    function _parseL2WithdrawalMessage(
490	        uint256 _chainId,
491	        bytes memory _l2ToL1message
492	    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
```

*GitHub* : [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175), [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L256), [376](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L376), [489..492](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L489-L492)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
// @audit function `getStateTransition` is `public` followed by function `addStateTransitionManager` which is `external`
77	    function getStateTransition(uint256 _chainId) public view returns (address) {
```

*GitHub* : [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L77)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
// @audit function `getOperationState` is `public` followed by function `scheduleTransparent` which is `external`
107	    function getOperationState(bytes32 _id) public view returns (OperationState) {
...
// @audit function `_checkPredecessorDone` is `internal` followed by function `updateDelay` which is `external`
241	    function _checkPredecessorDone(bytes32 _predecessorId) internal view {
```

*GitHub* : [107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L107), [241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L241)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
// @audit function `_setChainIdUpgrade` is `internal` followed by function `registerAlreadyDeployedStateTransition` which is `external`
179	    function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
```

*GitHub* : [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L179)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
// @audit function `_processL2Logs` is `internal` followed by function `commitBatches` which is `external`
132	    function _processL2Logs(
133	        CommitBatchInfo calldata _newBatch,
134	        bytes32 _expectedSystemContractUpgradeTxHash
135	    ) internal pure returns (LogProcessingOutput memory logOutput) {
```

*GitHub* : [132..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L132-L135), [323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L323), [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351), [453..457](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L453-L457)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [56..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L56-L61), [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L132), [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L111), [140..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L140-L144)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173)

### [N-40]<a name="n-40"></a> Array indicies should be referenced via `enum`s rather than via numeric literals



*There are 19 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

```solidity
43	        s.storedBatchHashes[0] = _initializeData.storedBatchZero;
```

*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L43)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
41	        uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));
...
65	                    keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),
...
68	            blobHashes[0] = logOutput.blob1Hash;
...
69	            blobCommitments[0] = bytes32(
...
57	            blobHashes[0] = logOutput.blob1Hash;
...
58	            blobHashes[1] = logOutput.blob2Hash;
...
60	            blobCommitments = _verifyBlobInformation(_newBatch.pubdataCommitments[1:], blobHashes);
...
289	        s.l2SystemContractsUpgradeBatchNumber = _newBatchesData[0].batchNumber;
```

*GitHub* : [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L41), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L65), [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L68), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L69), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L57), [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L58), [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L60), [289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

```solidity
172	            bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];
```

*GitHub* : [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L172)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L42), [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L52), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L52)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L216)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L56), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L57), [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L58), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L59)

### [N-41]<a name="n-41"></a> Use of `override` is unnecessary

Starting with Solidity version [0.8.8](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding), using the `override` keyword when the function solely overrides an interface function, and the function doesn't exist in multiple base contracts, is unnecessary.

*There are 25 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
184	    function bridgehubDeposit(
185	        uint256 _chainId,
186	        address _prevMsgSender,
187	        uint256, // l2Value, needed for Weth deposits in the future
188	        bytes calldata _data
189	    ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
...
234	    function bridgehubConfirmL2Transaction(
235	        uint256 _chainId,
236	        bytes32 _txDataHash,
237	        bytes32 _txHash
238	    ) external override onlyBridgehub {
...
279	    function claimFailedDeposit(
280	        uint256 _chainId,
281	        address _depositSender,
282	        address _l1Token,
283	        uint256 _amount,
284	        bytes32 _l2TxHash,
285	        uint256 _l2BatchNumber,
286	        uint256 _l2MessageIndex,
287	        uint16 _l2TxNumberInBatch,
288	        bytes32[] calldata _merkleProof
289	    ) external override {
...
387	    function finalizeWithdrawal(
388	        uint256 _chainId,
389	        uint256 _l2BatchNumber,
390	        uint256 _l2MessageIndex,
391	        uint16 _l2TxNumberInBatch,
392	        bytes calldata _message,
393	        bytes32[] calldata _merkleProof
394	    ) external override {
...
556	    function depositLegacyErc20Bridge(
557	        address _prevMsgSender,
558	        address _l2Receiver,
559	        address _l1Token,
560	        uint256 _amount,
561	        uint256 _l2TxGasLimit,
562	        uint256 _l2TxGasPerPubdataByte,
563	        address _refundRecipient
564	    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
...
617	    function finalizeWithdrawalLegacyErc20Bridge(
618	        uint256 _l2BatchNumber,
619	        uint256 _l2MessageIndex,
620	        uint16 _l2TxNumberInBatch,
621	        bytes calldata _message,
622	        bytes32[] calldata _merkleProof
623	    ) external override onlyLegacyBridge returns (address l1Receiver, address l1Token, uint256 amount) {
...
646	    function claimFailedDepositLegacyErc20Bridge(
647	        address _depositSender,
648	        address _l1Token,
649	        uint256 _amount,
650	        bytes32 _l2TxHash,
651	        uint256 _l2BatchNumber,
652	        uint256 _l2MessageIndex,
653	        uint16 _l2TxNumberInBatch,
654	        bytes32[] calldata _merkleProof
655	    ) external override onlyLegacyBridge {
```

*GitHub* : [184..189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L184-L189), [234..238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L234-L238), [279..289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L279-L289), [387..394](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L387-L394), [556..564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L556-L564), [617..623](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L617-L623), [646..655](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L646-L655)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
154	    function proveL2MessageInclusion(
155	        uint256 _chainId,
156	        uint256 _batchNumber,
157	        uint256 _index,
158	        L2Message calldata _message,
159	        bytes32[] calldata _proof
160	    ) external view override returns (bool) {
...
166	    function proveL2LogInclusion(
167	        uint256 _chainId,
168	        uint256 _batchNumber,
169	        uint256 _index,
170	        L2Log memory _log,
171	        bytes32[] calldata _proof
172	    ) external view override returns (bool) {
...
178	    function proveL1ToL2TransactionStatus(
179	        uint256 _chainId,
180	        bytes32 _l2TxHash,
181	        uint256 _l2BatchNumber,
182	        uint256 _l2MessageIndex,
183	        uint16 _l2TxNumberInBatch,
184	        bytes32[] calldata _merkleProof,
185	        TxStatus _status
186	    ) external view override returns (bool) {
```

*GitHub* : [154..160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L154-L160), [166..172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L166-L172), [178..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L178-L186), [219..221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L219-L221), [264..266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L264-L266)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L76)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L49)


---

	 - code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol


*GitHub* : [15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L15)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L16)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [81..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L81-L87), [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L125), [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L151)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L147), [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L156), [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L161), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173)

### [N-42]<a name="n-42"></a> Unused function parameter

Comment out the variable name to suppress compiler warnings

*There are 9 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

```solidity
265	    function _upgradeL1Contract(bytes calldata _customCallDataForUpgrade) internal virtual {}
...
271	    function _postUpgrade(bytes calldata _customCallDataForUpgrade) internal virtual {}
```

*GitHub* : [265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L265), [271](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L271)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol

```solidity
21	    function readUint32(bytes memory _bytes, uint256 _start) internal pure returns (uint32 result, uint256 offset) {
...
28	    function readAddress(bytes memory _bytes, uint256 _start) internal pure returns (address result, uint256 offset) {
...
35	    function readUint256(bytes memory _bytes, uint256 _start) internal pure returns (uint256 result, uint256 offset) {
...
42	    function readBytes32(bytes memory _bytes, uint256 _start) internal pure returns (bytes32 result, uint256 offset) {
```

*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L21), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L28), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L35), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L42)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

```solidity
42	    function _efficientHash(bytes32 _lhs, bytes32 _rhs) private pure returns (bytes32 result) {
```

*GitHub* : [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L42)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
113	    function reinitializeToken(
114	        ERC20Getters calldata _availableGetters,
115	        string memory _newName,
116	        string memory _newSymbol,
117	        uint8 _version
118	    ) external onlyNextVersion(_version) reinitializer(_version) {
```

*GitHub* : [113..118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L113-L118)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol

```solidity
39	    function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {
```

*GitHub* : [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39)

### [N-43]<a name="n-43"></a> Unused `event` definition

Note that there may be cases where an event superficially appears to be used, but this is only because there are multiple definitions of the event in different files. In such cases, the event definition should be moved into a separate file. The instances below are the unused definitions

*There are 3 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

```solidity
136	    event EthWithdrawalFinalized(address indexed to, uint256 amount);
```

*GitHub* : [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L136)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol

```solidity
19	    event ProposeTransparentUpgrade(
20	        Diamond.DiamondCutData diamondCut,
21	        uint256 indexed proposalId,
22	        bytes32 proposalSalt
23	    );
```

*GitHub* : [19..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L19-L23)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol

```solidity
24	    event BaseTokenReceived(uint256 amount);
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L24)

### [N-44]<a name="n-44"></a> Modifier declarations should have NatSpec descriptions



*There are 9 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
47	    modifier onlyOwnerOrAdmin() {
48	        require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");
49	        _;
50	    }
```

*GitHub* : [47..50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L47-L50)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

```solidity
28	    modifier onlyStateTransitionManager() {
29	        require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");
30	        _;
31	    }
...
33	    modifier onlyBridgehub() {
34	        require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");
35	        _;
36	    }
...
38	    modifier onlyAdminOrStateTransitionManager() {
39	        require(
40	            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
41	            "StateTransition Chain: Only by admin or state transition manager"
42	        );
43	        _;
44	    }
...
46	    modifier onlyValidatorOrStateTransitionManager() {
47	        require(
48	            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
49	            "StateTransition Chain: Only by validator or state transition manager"
50	        );
51	        _;
52	    }
...
54	    modifier onlyBaseTokenBridge() {
55	        require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
56	        _;
57	    }
```

*GitHub* : [28..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L28-L31), [33..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L33-L36), [38..44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L38-L44), [46..52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L46-L52), [54..57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L54-L57)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

```solidity
43	    modifier reentrancyGuardInitializer() {
44	        _initializeReentrancyGuard();
45	        _;
46	    }
```

*GitHub* : [43..46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L43-L46)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
131	    modifier onlyBridge() {
132	        require(msg.sender == l2Bridge, "xnt"); // Only L2 bridge can call this method
133	        _;
134	    }
...
136	    modifier onlyNextVersion(uint8 _version) {
137	        // The version should be incremented by 1. Otherwise, the governor risks disabling
138	        // future reinitialization of the token by providing too large a version.
139	        require(_version == _getInitializedVersion() + 1, "v");
140	        _;
141	    }
```

*GitHub* : [131..134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L131-L134), [136..141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L136-L141)

### [N-45]<a name="n-45"></a> Event declarations should have NatSpec descriptions



*There are 19 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
26	    event DiamondCut(FacetCut[] facetCuts, address initAddress, bytes initCalldata);
```

*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L26)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

```solidity
14	    event DepositInitiated(
15	        bytes32 indexed l2DepositTxHash,
16	        address indexed from,
17	        address indexed to,
18	        address l1Token,
19	        uint256 amount
20	    );
...
22	    event WithdrawalFinalized(address indexed to, address indexed l1Token, uint256 amount);
...
24	    event ClaimedFailedDeposit(address indexed to, address indexed l1Token, uint256 amount);
```

*GitHub* : [14..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L14-L20), [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L22), [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L24)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

```solidity
15	    event LegacyDepositInitiated(
16	        uint256 indexed chainId,
17	        bytes32 indexed l2DepositTxHash,
18	        address indexed from,
19	        address to,
20	        address l1Token,
21	        uint256 amount
22	    );
...
24	    event BridgehubDepositInitiated(
25	        uint256 indexed chainId,
26	        bytes32 indexed txDataHash,
27	        address indexed from,
28	        address to,
29	        address l1Token,
30	        uint256 amount
31	    );
...
33	    event BridgehubDepositBaseTokenInitiated(
34	        uint256 indexed chainId,
35	        address indexed from,
36	        address l1Token,
37	        uint256 amount
38	    );
...
40	    event BridgehubDepositFinalized(
41	        uint256 indexed chainId,
42	        bytes32 indexed txDataHash,
43	        bytes32 indexed l2DepositTxHash
44	    );
...
46	    event WithdrawalFinalizedSharedBridge(
47	        uint256 indexed chainId,
48	        address indexed to,
49	        address indexed l1Token,
50	        uint256 amount
51	    );
...
53	    event ClaimedFailedDepositSharedBridge(
54	        uint256 indexed chainId,
55	        address indexed to,
56	        address indexed l1Token,
57	        uint256 amount
58	    );
```

*GitHub* : [15..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L15-L22), [24..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L24-L31), [33..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L33-L38), [40..44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L40-L44), [46..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L46-L51), [53..58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L53-L58)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L135)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L30), [32..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L32-L36)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol


*GitHub* : [19..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L19-L23)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [9..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L9-L14), [16..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L16-L21)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L8), [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L10), [12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L12)

### [N-46]<a name="n-46"></a> Function declarations should have NatSpec descriptions



*There are 132 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
139	    function receiveEth(uint256 _chainId) external payable {
...
489	    function _parseL2WithdrawalMessage(
490	        uint256 _chainId,
491	        bytes memory _l2ToL1message
492	    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
```

*GitHub* : [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L139), [489..492](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L489-L492)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
327	    function _actualRefundRecipient(address _refundRecipient) internal view returns (address _recipient) {
```

*GitHub* : [327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L327)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
76	    function getChainAdmin(uint256 _chainId) external view override returns (address) {
...
232	    function registerAlreadyDeployedStateTransition(
233	        uint256 _chainId,
234	        address _stateTransitionContract
235	    ) external onlyOwner {
```

*GitHub* : [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L76), [232..235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L232-L235)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
57	    constructor(address _initialOwner, uint32 _executionDelay) {
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

```solidity
13	    constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
```

*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L13)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
91	    function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {
...
102	    function upgradeChainFromVersion(
103	        uint256 _oldProtocolVersion,
104	        Diamond.DiamondCutData calldata _diamondCut
105	    ) external onlyAdminOrStateTransitionManager {
```

*GitHub* : [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L91), [102..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L102-L105)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
217	    function _commitBatches(
218	        StoredBatchInfo memory _lastCommittedBatchData,
219	        CommitBatchInfo[] calldata _newBatchesData
220	    ) internal {
```

*GitHub* : [217..220](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L217-L220), [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351), [388..392](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L388-L392), [440](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L440), [481](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L481), [515](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515), [525](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525), [537..542](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [230..232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L230-L232), [260..265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L260-L265), [291..295](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L291-L295)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L13), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L19)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol


*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L21), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L28), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L35), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L42)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L26), [28..35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L28-L35), [37..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L37-L43), [45..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L45-L53), [55..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L55-L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L69), [71..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L71-L75), [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L77)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [60..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L60-L64), [66..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L66-L74), [76..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L76-L85), [87..97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L87-L97), [99..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L99-L105), [107..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L107-L114), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L116), [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L118), [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L120), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L122), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L124), [130..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L130-L135), [137..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L137-L142), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L144), [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L146)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [9..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L9-L15), [17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L17), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L19), [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L21), [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L23)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L7), [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L9)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L71), [75..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L75-L81), [83..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L83-L89), [91..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L91-L99), [101..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L101-L103), [105..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L105-L107), [109..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L109-L114), [118..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L118-L125), [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L127), [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L129), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L131), [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L133)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L43), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L45), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L47), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L49), [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L51), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L53), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L67)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L45), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L71), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L73), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L84), [86..90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L86-L90), [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L92), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L94), [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L96)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L47)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [100..102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L100-L102)


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L7)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L10)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L48)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L161), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [11..17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11-L17)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [11..18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L11-L18)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [26..32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L26-L32), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L34), [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L36), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L38), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L40)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L14), [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L16), [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L18), [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L20)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L16), [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L18)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L29), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39), [78..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L78-L83), [97..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L97-L107), [123..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L123-L129)

### [N-47]<a name="n-47"></a> Function names should use lowerCamelCase

According to the Solidity [style guide](https://docs.soliditylang.org/en/latest/style-guide.html#function-names) function names should be in `mixedCase` (lowerCamelCase)

*There are 4 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
256	    function _getERC20Getters(address _token) internal view returns (bytes memory) {
```

*GitHub* : [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L256)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
132	    function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {
```

*GitHub* : [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L132)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol

```solidity
97	    function getFarCallABI(
98	        uint32 dataOffset,
99	        uint32 memoryPage,
100	        uint32 dataStart,
101	        uint32 dataLength,
102	        uint32 gasPassed,
103	        uint8 shardId,
104	        CalldataForwardingMode forwardingMode,
105	        bool isConstructorCall,
106	        bool isSystemCall
107	    ) internal pure returns (uint256 farCallAbi) {
...
123	    function getFarCallABIWithEmptyFatPointer(
124	        uint32 gasPassed,
125	        uint8 shardId,
126	        CalldataForwardingMode forwardingMode,
127	        bool isConstructorCall,
128	        bool isSystemCall
129	    ) internal pure returns (uint256 farCallAbiWithEmptyFatPtr) {
```

*GitHub* : [97..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L97-L107), [123..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L123-L129)

### [N-48]<a name="n-48"></a> Overflows in unchecked blocks

While integers with a large number of bits are unlikely to overflow on human time scales, it is not strictly correct to use an `unchecked` block around them, because _eventually_ they will overflow, and `unchecked` blocks are meant for cases where it's mathematically impossible for an operation to trigger an overflow (e.g. a prior `require()` statement prevents the overflow case)

*There are 6 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
114	        unchecked {
115	            // This contract is only a temporary solution, that hopefully will be disabled until 2106 year, so...
116	            // It is safe to cast.
117	            uint32 timestamp = uint32(block.timestamp);
118	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
119	                committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);
120	            }
121	        }
...
133	        unchecked {
134	            // This contract is only a temporary solution, that hopefully will be disabled until 2106 year, so...
135	            // It is safe to cast.
136	            uint32 timestamp = uint32(block.timestamp);
137	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
138	                committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);
139	            }
140	        }
...
186	        unchecked {
187	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
188	                uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
189	                    _newBatchesData[i].batchNumber
190	                );
191	
192	                // Note: if the `commitBatchTimestamp` is zero, that means either:
193	                // * The batch was committed, but not through this contract.
194	                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
195	                // We allow executing such batches.
196	
197	                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
198	            }
199	        }
...
210	        unchecked {
211	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
212	                uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
213	
214	                // Note: if the `commitBatchTimestamp` is zero, that means either:
215	                // * The batch was committed, but not through this contract.
216	                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
217	                // We allow executing such batches.
218	
219	                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
220	            }
221	        }
```

*GitHub* : [114..121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L114-L121), [133..140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L133-L140), [186..199](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L186-L199), [210..221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L210-L221)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

```solidity
21	        unchecked {
22	            // Each storage slot can store 256 bits of data.
23	            // As uint32 is 32 bits long, 8 uint32s can be packed into one storage slot.
24	            // Hence, `_index / 8` is done to find the storage slot that contains the required uint32.
25	            uint256 mapValue = _map.map[_index / 8];
26	
27	            // First three bits of the original `_index` denotes the position of the uint32 in that slot.
28	            // So, '(_index & 7) * 32' is done to find the bit position of the uint32 in that storage slot.
29	            uint256 bitOffset = (_index & 7) * 32;
30	
31	            // Shift the bits to the right and retrieve the uint32 value.
32	            result = uint32(mapValue >> bitOffset);
33	        }
...
41	        unchecked {
42	            // Each storage slot can store 256 bits of data.
43	            // As uint32 is 32 bits long, 8 uint32s can be packed into one storage slot.
44	            // Hence, `_index / 8` is done to find the storage slot that contains the required uint32.
45	            uint256 mapIndex = _index / 8;
46	            uint256 mapValue = _map.map[mapIndex];
47	
48	            // First three bits of the original `_index` denotes the position of the uint32 in that slot.
49	            // So, '(_index & 7) * 32' is done to find the bit position of the uint32 in that storage slot.
50	            uint256 bitOffset = (_index & 7) * 32;
51	
52	            // XORing a value A with B, and then with A again, gives the original value B.
53	            // We will use this property to update the uint32 value in the slot.
54	
55	            // Shift the bits to the right and retrieve the uint32 value.
56	            uint32 oldValue = uint32(mapValue >> bitOffset);
57	
58	            // Calculate the XOR of the new value and the existing value.
59	            uint256 newValueXorOldValue = uint256(oldValue ^ _value);
60	
61	            // Finally, we XOR the slot with the XOR of the new value and the existing value,
62	            // shifted to its proper position. The XOR operation will effectively replace the old value with the new value.
63	            _map.map[mapIndex] = (newValueXorOldValue << bitOffset) ^ mapValue;
64	        }
```

*GitHub* : [21..33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L21-L33), [41..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L41-L64)

### [N-49]<a name="n-49"></a> Missing event and or timelock for critical parameter change

Events help non-contract tools to track changes, and timelocks prevent users from being surprised by changes

*There are 12 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
150	    function bridgehubDepositBaseToken(
151	        uint256 _chainId,
152	        address _prevMsgSender,
153	        address _l1Token,
154	        uint256 _amount
155	    ) external payable virtual onlyBridgehubOrEra(_chainId) {
```

*GitHub* : [150..155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L150-L155)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
53	    function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
...
110	    function setSharedBridge(address _sharedBridge) external onlyOwner {
```

*GitHub* : [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L53), [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L110)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
251	    function updateDelay(uint256 _newDelay) external onlySelf {
...
258	    function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
```

*GitHub* : [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L251), [258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L258)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
112	    function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
...
134	    function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {
...
139	    function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {
...
144	    function setNewVersionUpgrade(
145	        Diamond.DiamondCutData calldata _cutData,
146	        uint256 _oldProtocolVersion,
147	        uint256 _newProtocolVersion
148	    ) external onlyOwner {
...
154	    function setUpgradeDiamondCut(
155	        Diamond.DiamondCutData calldata _cutData,
156	        uint256 _oldProtocolVersion
157	    ) external onlyOwner {
```

*GitHub* : [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L112), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L134), [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L139), [144..148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L144-L148), [154..157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L154-L157)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L75), [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98)

### [N-50]<a name="n-50"></a> Setters should prevent re-setting of the same value

This especially problematic when the setter also emits the same value, which may be confusing to offline parsers

*There are 19 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
135	    function deposit(
136	        address _l2Receiver,
137	        address _l1Token,
138	        uint256 _amount,
139	        uint256 _l2TxGasLimit,
140	        uint256 _l2TxGasPerPubdataByte,
141	        address _refundRecipient
142	    ) public payable nonReentrant returns (bytes32 l2TxHash) {
```

*GitHub* : [135..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L135-L142)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
106	    function initialize(
107	        address _owner,
108	        uint256 _eraFirstPostUpgradeBatch
109	    ) external reentrancyGuardInitializer initializer {
...
144	    function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner {
...
234	    function bridgehubConfirmL2Transaction(
235	        uint256 _chainId,
236	        bytes32 _txDataHash,
237	        bytes32 _txHash
238	    ) external override onlyBridgehub {
```

*GitHub* : [106..109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L106-L109), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L144), [234..238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L234-L238)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
53	    function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
...
110	    function setSharedBridge(address _sharedBridge) external onlyOwner {
...
116	    function createNewChain(
117	        uint256 _chainId,
118	        address _stateTransitionManager,
119	        address _baseToken,
120	        uint256, //_salt
121	        address _admin,
122	        bytes calldata _initData
123	    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
```

*GitHub* : [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L53), [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L110), [116..123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L116-L123)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
251	    function updateDelay(uint256 _newDelay) external onlySelf {
...
258	    function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
```

*GitHub* : [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L251), [258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L258)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
112	    function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
```

*GitHub* : [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L112), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L134), [144..148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L144-L148), [232..235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L232-L235)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L75), [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [51..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L51-L56), [81..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L81-L87)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L52), [113..118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L113-L118)

### [N-51]<a name="n-51"></a> Interfaces should be defined in separate files from their usage

The interfaces below should be defined in separate files, so that it's easier for future projects to import them, and to avoid duplication later on if they need to be used elsewhere in the project

*There are 3 instance(s) of this issue:*


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol

```solidity
20	interface IL2Messenger {
21	    /// @notice Sends an arbitrary length message to L1.
22	    /// @param _message The variable length message to be sent to L1.
23	    /// @return Returns the keccak256 hashed value of the message.
24	    function sendToL1(bytes memory _message) external returns (bytes32);
...
32	interface IContractDeployer {
33	    /// @notice A struct that describes a forced deployment on an address.
34	    /// @param bytecodeHash The bytecode hash to put on an address.
35	    /// @param newAddress The address on which to deploy the bytecodehash to.
36	    /// @param callConstructor Whether to run the constructor on the force deployment.
37	    /// @param value The `msg.value` with which to initialize a contract.
38	    /// @param input The constructor calldata.
39	    struct ForceDeployment {
...
63	interface IBaseToken {
64	    /// @notice Allows the withdrawal of ETH to a given L1 receiver along with an additional message.
65	    /// @param _l1Receiver The address on L1 to receive the withdrawn ETH.
66	    /// @param _additionalData Additional message or data to be sent alongside the withdrawal.
67	    function withdrawWithMessage(address _l1Receiver, bytes memory _additionalData) external payable;
```

*GitHub* : [20..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L20-L24), [32..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L32-L39), [63..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L63-L67)

### [N-52]<a name="n-52"></a> Consider disallowing transfers to `address(this)`



*There are 2 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
305	    function _claimFailedDeposit(
306	        bool _checkedInLegacyBridge,
307	        uint256 _chainId,
308	        address _depositSender,
309	        address _l1Token,
310	        uint256 _amount,
311	        bytes32 _l2TxHash,
312	        uint256 _l2BatchNumber,
313	        uint256 _l2MessageIndex,
314	        uint16 _l2TxNumberInBatch,
315	        bytes32[] calldata _merkleProof
316	    ) internal nonReentrant {
...
411	    function _finalizeWithdrawal(
412	        uint256 _chainId,
413	        uint256 _l2BatchNumber,
414	        uint256 _l2MessageIndex,
415	        uint16 _l2TxNumberInBatch,
416	        bytes calldata _message,
417	        bytes32[] calldata _merkleProof
418	    ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
```

*GitHub* : [305..316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L305-L316), [411..418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L411-L418)

### [N-53]<a name="n-53"></a> Named imports of parent contracts are missing



*There are 2 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
18	contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
19	    /// @notice all the ether is held by the weth bridge
20	    IL1SharedBridge public sharedBridge;
```

*GitHub* : [18..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L18-L20)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

```solidity
13	contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {
14	    /// @notice The main function that will be called by the upgrade proxy.
15	    /// @param _proposedUpgrade The upgrade to be executed.
16	    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```

*GitHub* : [13..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L13-L16)

### [N-54]<a name="n-54"></a> Events may be emitted out of order due to reentrancy

Ensure that events follow the best practice of check-effects-interaction, and are emitted before external calls

*There are 12 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
178	    function claimFailedDeposit(
179	        address _depositSender,
180	        address _l1Token,
181	        bytes32 _l2TxHash,
182	        uint256 _l2BatchNumber,
183	        uint256 _l2MessageIndex,
184	        uint16 _l2TxNumberInBatch,
185	        bytes32[] calldata _merkleProof
186	    ) external nonReentrant {
```

*GitHub* : [178..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L178-L186)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
305	    function _claimFailedDeposit(
306	        bool _checkedInLegacyBridge,
307	        uint256 _chainId,
308	        address _depositSender,
309	        address _l1Token,
310	        uint256 _amount,
311	        bytes32 _l2TxHash,
312	        uint256 _l2BatchNumber,
313	        uint256 _l2MessageIndex,
314	        uint16 _l2TxNumberInBatch,
315	        bytes32[] calldata _merkleProof
316	    ) internal nonReentrant {
...
411	    function _finalizeWithdrawal(
412	        uint256 _chainId,
413	        uint256 _l2BatchNumber,
414	        uint256 _l2MessageIndex,
415	        uint16 _l2TxNumberInBatch,
416	        bytes calldata _message,
417	        bytes32[] calldata _merkleProof
418	    ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
```

*GitHub* : [305..316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L305-L316), [411..418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L411-L418)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
116	    function createNewChain(
117	        uint256 _chainId,
118	        address _stateTransitionManager,
119	        address _baseToken,
120	        uint256, //_salt
121	        address _admin,
122	        bytes calldata _initData
123	    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
```

*GitHub* : [116..123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L116-L123)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
179	    function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
```

*GitHub* : [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L179)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
102	    function upgradeChainFromVersion(
103	        uint256 _oldProtocolVersion,
104	        Diamond.DiamondCutData calldata _diamondCut
105	    ) external onlyAdminOrStateTransitionManager {
...
125	    function executeUpgrade(Diamond.DiamondCutData calldata _diamondCut) external onlyStateTransitionManager {
```

*GitHub* : [102..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L102-L105), [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L125)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
318	    function _writePriorityOp(
319	        WritePriorityOpParams memory _priorityOpParams,
320	        bytes memory _calldata,
321	        bytes[] memory _factoryDeps
322	    ) internal returns (bytes32 canonicalTxHash) {
```

*GitHub* : [318..322](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L318-L322)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

```solidity
94	    function _setL2DefaultAccountBytecodeHash(bytes32 _l2DefaultAccountBytecodeHash) private {
...
111	    function _setL2BootloaderBytecodeHash(bytes32 _l2BootloaderBytecodeHash) private {
```

*GitHub* : [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L94), [111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L111)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [81..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L81-L87), [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L125)

### [N-55]<a name="n-55"></a> Function can return unassigned variable

Make sure that functions with a return value always return a valid and assigned value. Even if the default value is as expected, it should be assigned with the default value for code clarity and to reduce confusion.

*There are 1 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

```solidity
//@audit Variable `l2ProtocolUpgradeTxHash` defined here, but never assigned
214	        bytes32 l2ProtocolUpgradeTxHash = keccak256(encodedTransaction);
...
//@audit Variable returned here uninitialized
218	        return l2ProtocolUpgradeTxHash;
```

*GitHub* : [218](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L218)

### [N-56]<a name="n-56"></a> Missing zero address check in initializer



*There are 1 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
43	    function initialize(address _owner) external reentrancyGuardInitializer {
```

*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L43)

### [N-57]<a name="n-57"></a> Missing NatSpec `@author` from contract declaration

Some contract definitions have an incomplete NatSpec: add a `@author` notation to improve the code documentation.

*There are 16 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
18	contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
19	    /// @notice all the ether is held by the weth bridge
20	    IL1SharedBridge public sharedBridge;
```

*GitHub* : [18..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L18-L20)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol

```solidity
6	interface IWETH9 {
7	    function deposit() external payable;
```

*GitHub* : [6..7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L6-L7)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol

```solidity
44	interface IBridgehub {
45	    /// @notice pendingAdmin is changed
46	    /// @dev Also emitted when new admin is accepted and in this case, `newPendingAdmin` would be zero address
47	    event NewPendingAdmin(address indexed oldPendingAdmin, address indexed newPendingAdmin);
```

*GitHub* : [44..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L44-L47)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

```solidity
28	interface IStateTransitionManager {
29	    // when a new Chain is added
30	    event StateTransitionNewChain(uint256 indexed _chainId, address indexed _stateTransitionContract);
```

*GitHub* : [28..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L28-L30)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol

```solidity
63	interface IDiamondInit {
64	    function initialize(InitializeData calldata _initData) external returns (bytes32);
```

*GitHub* : [63..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L63-L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol

```solidity
17	interface IZkSyncStateTransition is IAdmin, IExecutor, IGetters, IMailbox {
18	    // KL todo: need this in the server for now
19	    event ProposeTransparentUpgrade(
```

*GitHub* : [17..19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L17-L19)


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol

```solidity
6	interface ISystemContext {
7	    function setChainId(uint256 _newChainId) external;
```

*GitHub* : [6..7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L6-L7)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol

```solidity
9	interface IDefaultUpgrade {
10	    function upgrade(ProposedUpgrade calldata _upgrade) external returns (bytes32);
```

*GitHub* : [9..10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L9-L10)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

```solidity
7	/**
8	 * @custom:security-contact security@matterlabs.dev
9	 * @dev Contract module that helps prevent reentrant calls to a function.
10	 *
11	 * Inheriting from `ReentrancyGuard` will make the {nonReentrant} modifier
12	 * available, which can be applied to functions to make sure there are no nested
13	 * (reentrant) calls to them.
14	 *
15	 * Note that because there is a single `nonReentrant` guard, functions marked as
16	 * `nonReentrant` may not call one another. This can be worked around by making
17	 * those functions `private`, and then adding `external` `nonReentrant` entry
18	 * points to them.
19	 *
20	 * TIP: If you would like to learn more about reentrancy and alternative ways
21	 * to protect against it, check out our blog post
22	 * https://blog.openzeppelin.com/reentrancy-after-istanbul/[Reentrancy After Istanbul].
23	 *
24	 * _Since v2.5.0:_ this module is now much more gas efficient, given net gas
25	 * metering changes introduced in the Istanbul hardfork.
26	 */
27	abstract contract ReentrancyGuard {
28	    /// @dev Address of lock flag variable.
29	    /// @dev Flag is placed at random memory location to not interfere with Storage contract.
30	    // keccak256("ReentrancyGuard") - 1;
31	    uint256 private constant LOCK_FLAG_ADDRESS = 0x8e94fed44239eb2314ab7a406345e6c5a8f0ccedf3b600de3d004e672c33abf4;
```

*GitHub* : [7..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L7-L31)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

```solidity
23	library AddressAliasHelper {
24	    uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
```

*GitHub* : [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L23-L24)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [7..8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L7-L8)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [16..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L16-L30)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L23-L24)


---

	 - code/contracts/zksync/contracts/ForceDeployUpgrader.sol


*GitHub* : [9..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L9-L15)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [28..29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L28-L29), [36..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L36-L39)

### [N-58]<a name="n-58"></a> Missing NatSpec `@dev` from contract declaration

Some contract definitions have an incomplete NatSpec: add a `@dev` notation to improve the code documentation.

*There are 49 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
18	contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
19	    /// @notice all the ether is held by the weth bridge
20	    IL1SharedBridge public sharedBridge;
```

*GitHub* : [18..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L18-L20)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
24	/// @title StateTransition contract
25	/// @author Matter Labs
26	/// @custom:security-contact security@matterlabs.dev
27	contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {
28	    /// @notice Address of the bridgehub
29	    address public immutable bridgehub;
```

*GitHub* : [24..29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L24-L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

```solidity
9	/// @title Diamond Proxy Contract (EIP-2535)
10	/// @author Matter Labs
11	/// @custom:security-contact security@matterlabs.dev
12	contract DiamondProxy {
13	    constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
```

*GitHub* : [9..13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L9-L13)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
17	/// @title Admin Contract controls access rights for contract management.
18	/// @author Matter Labs
19	/// @custom:security-contact security@matterlabs.dev
20	contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {
21	    /// @inheritdoc IZkSyncStateTransitionBase
22	    string public constant override getName = "AdminFacet";
```

*GitHub* : [17..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L17-L22)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
21	/// @title zkSync hyperchain Executor contract capable of processing events emitted in the zkSync hyperchain protocol.
22	/// @author Matter Labs
23	/// @custom:security-contact security@matterlabs.dev
24	contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {
25	    using UncheckedMath for uint256;
```

*GitHub* : [21..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L21-L25)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

```solidity
19	/// @title Getters Contract implements functions for getting contract state from outside the blockchain.
20	/// @author Matter Labs
21	/// @custom:security-contact security@matterlabs.dev
22	contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {
23	    using UncheckedMath for uint256;
```

*GitHub* : [19..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L19-L23)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
29	/// @title zkSync Mailbox contract providing interfaces for L1 <-> L2 interaction.
30	/// @author Matter Labs
31	/// @custom:security-contact security@matterlabs.dev
32	contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {
33	    using UncheckedMath for uint256;
```

*GitHub* : [29..33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L29-L33)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

```solidity
10	/// @title Base contract containing functions accessible to the other facets.
11	/// @author Matter Labs
12	/// @custom:security-contact security@matterlabs.dev
13	contract ZkSyncStateTransitionBase is ReentrancyGuard {
14	    ZkSyncStateTransitionStorage internal s;
```

*GitHub* : [10..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L10-L14)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

```solidity
43	/// @author Matter Labs
44	/// @custom:security-contact security@matterlabs.dev
45	/// @notice Interface to which all the upgrade implementations should adhere
46	abstract contract BaseZkSyncUpgrade is ZkSyncStateTransitionBase {
47	    /// @notice Changes the protocol version
48	    event NewProtocolVersion(uint256 indexed previousProtocolVersion, uint256 indexed newProtocolVersion);
```

*GitHub* : [43..48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L43-L48)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

```solidity
16	/// @author Matter Labs
17	/// @custom:security-contact security@matterlabs.dev
18	/// @notice Interface to which all the upgrade implementations should adhere
19	abstract contract BaseZkSyncUpgradeGenesis is BaseZkSyncUpgrade {
20	    /// @notice Changes the protocol version
21	    /// @param _newProtocolVersion The new protocol version
22	    function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
```

*GitHub* : [16..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L16-L22)


---

	 - code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol


*GitHub* : [10..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L10-L15)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol


*GitHub* : [11..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L11-L16)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [7..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L7-L14)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


*GitHub* : [7..13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L7-L13)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [10..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L10-L14)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [9..12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L9-L12)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [12..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L12-L21)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [9..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L9-L14)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [11..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L11-L15)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [7..9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L7-L9)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol


*GitHub* : [6..7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L6-L7)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [44..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L44-L47)


---

	 - code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol


*GitHub* : [7..18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L7-L18)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [7..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L7-L16)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [28..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L28-L30)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [12..19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L12-L19)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [63..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L63-L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol


*GitHub* : [72..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L72-L85)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol


*GitHub* : [12..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L12-L21)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [10..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L10-L20)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol


*GitHub* : [14..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L14-L21)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol


*GitHub* : [17..19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L17-L19)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol


*GitHub* : [6..11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L6-L11)


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol


*GitHub* : [6..7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L6-L7)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [9..10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L9-L10)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L23-L24)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [21..27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L21-L27)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [13..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L13-L22)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [7..11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L7-L11)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [7..11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L7-L11)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [7..9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L7-L9)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [7..8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L7-L8)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [16..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L16-L30)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L23-L24)


---

	 - code/contracts/zksync/contracts/ForceDeployUpgrader.sol


*GitHub* : [9..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L9-L15)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [27..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L27-L39), [58..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L58-L67), [80..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L80-L87)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [28..29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L28-L29)

### [N-59]<a name="n-59"></a> Missing NatSpec `@notice` from contract declaration

Some contract definitions have an incomplete NatSpec: add a `@notice` notation to describe the contract to improve the code documentation.

*There are 42 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
28	/// @author Matter Labs
29	/// @custom:security-contact security@matterlabs.dev
30	/// @dev Bridges assets between L1 and hyperchains, supporting both ETH and ERC20 tokens.
31	/// @dev Designed for use with a proxy for upgradability.
32	contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {
33	    using SafeERC20 for IERC20;
```

*GitHub* : [28..33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L28-L33)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
18	contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
19	    /// @notice all the ether is held by the weth bridge
20	    IL1SharedBridge public sharedBridge;
```

*GitHub* : [18..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L18-L20)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
24	/// @title StateTransition contract
25	/// @author Matter Labs
26	/// @custom:security-contact security@matterlabs.dev
27	contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {
28	    /// @notice Address of the bridgehub
29	    address public immutable bridgehub;
```

*GitHub* : [24..29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L24-L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

```solidity
16	/// @author Matter Labs
17	/// @dev The contract is used only once to initialize the diamond proxy.
18	/// @dev The deployment process takes care of this contract's initialization.
19	contract DiamondInit is ZkSyncStateTransitionBase, IDiamondInit {
20	    /// @dev Initialize the implementation to prevent any possibility of a Parity hack.
21	    constructor() reentrancyGuardInitializer {}
```

*GitHub* : [16..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L16-L21)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

```solidity
9	/// @title Diamond Proxy Contract (EIP-2535)
10	/// @author Matter Labs
11	/// @custom:security-contact security@matterlabs.dev
12	contract DiamondProxy {
13	    constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
```

*GitHub* : [9..13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L9-L13)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
17	/// @title Admin Contract controls access rights for contract management.
18	/// @author Matter Labs
19	/// @custom:security-contact security@matterlabs.dev
20	contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {
21	    /// @inheritdoc IZkSyncStateTransitionBase
22	    string public constant override getName = "AdminFacet";
```

*GitHub* : [17..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L17-L22)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
21	/// @title zkSync hyperchain Executor contract capable of processing events emitted in the zkSync hyperchain protocol.
22	/// @author Matter Labs
23	/// @custom:security-contact security@matterlabs.dev
24	contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {
25	    using UncheckedMath for uint256;
```

*GitHub* : [21..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L21-L25)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

```solidity
19	/// @title Getters Contract implements functions for getting contract state from outside the blockchain.
20	/// @author Matter Labs
21	/// @custom:security-contact security@matterlabs.dev
22	contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {
23	    using UncheckedMath for uint256;
```

*GitHub* : [19..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L19-L23)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
29	/// @title zkSync Mailbox contract providing interfaces for L1 <-> L2 interaction.
30	/// @author Matter Labs
31	/// @custom:security-contact security@matterlabs.dev
32	contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {
33	    using UncheckedMath for uint256;
```

*GitHub* : [29..33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L29-L33)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

```solidity
10	/// @title Base contract containing functions accessible to the other facets.
11	/// @author Matter Labs
12	/// @custom:security-contact security@matterlabs.dev
13	contract ZkSyncStateTransitionBase is ReentrancyGuard {
14	    ZkSyncStateTransitionStorage internal s;
```

*GitHub* : [10..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L10-L14)


---

	 - code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol


*GitHub* : [10..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L10-L15)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol


*GitHub* : [11..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L11-L16)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol


*GitHub* : [7..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L7-L21)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [9..12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L9-L12)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [18..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L18-L23)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [12..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L12-L21)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [11..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L11-L15)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [7..9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L7-L9)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol


*GitHub* : [6..7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L6-L7)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [44..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L44-L47)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [7..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L7-L16)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [28..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L28-L30)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [12..19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L12-L19)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [63..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L63-L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol


*GitHub* : [72..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L72-L85)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol


*GitHub* : [12..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L12-L21)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol


*GitHub* : [9..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L9-L16)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [10..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L10-L20)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol


*GitHub* : [14..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L14-L21)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol


*GitHub* : [17..19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L17-L19)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol


*GitHub* : [6..11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L6-L11)


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol


*GitHub* : [6..7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L6-L7)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [9..10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L9-L10)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [7..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L7-L31)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L23-L24)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [7..11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L7-L11)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [7..11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L7-L11)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [7..9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L7-L9)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [7..8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L7-L8)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [16..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L16-L30)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L23-L24)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [28..29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L28-L29)

### [N-60]<a name="n-60"></a> Missing NatSpec `@title` from contract declaration

Some contract definitions have an incomplete NatSpec: add a `@title` notation to describe the contract to improve the code documentation.

*There are 44 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
16	/// @author Matter Labs
17	/// @custom:security-contact security@matterlabs.dev
18	/// @notice Smart contract that allows depositing ERC20 tokens from Ethereum to hyperchains
19	/// @dev It is a legacy bridge from zkSync Era, that was deprecated in favour of shared bridge.
20	/// It is needed for backward compatibility with already integrated projects.
21	contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {
22	    using SafeERC20 for IERC20;
```

*GitHub* : [16..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L16-L22)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
28	/// @author Matter Labs
29	/// @custom:security-contact security@matterlabs.dev
30	/// @dev Bridges assets between L1 and hyperchains, supporting both ETH and ERC20 tokens.
31	/// @dev Designed for use with a proxy for upgradability.
32	contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {
33	    using SafeERC20 for IERC20;
```

*GitHub* : [28..33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L28-L33)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
18	contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
19	    /// @notice all the ether is held by the weth bridge
20	    IL1SharedBridge public sharedBridge;
```

*GitHub* : [18..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L18-L20)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
10	/// @author Matter Labs
11	/// @custom:security-contact security@matterlabs.dev
12	/// @dev Contract design is inspired by OpenZeppelin TimelockController and in-house Diamond Proxy upgrade mechanism.
13	/// @notice This contract manages operations (calls with preconditions) for governance tasks.
14	/// The contract allows for operations to be scheduled, executed, and canceled with
15	/// appropriate permissions and delays. It is used for managing and coordinating upgrades
16	/// and changes in all zkSync hyperchain governed contracts.
17	///
18	/// Operations can be proposed as either fully transparent upgrades with on-chain data,
19	/// or "shadow" upgrades where upgrade data is not published on-chain before execution. Proposed operations
20	/// are subject to a delay before they can be executed, but they can be executed instantly
21	/// with the security council’s permission.
22	contract Governance is IGovernance, Ownable2Step {
23	    /// @notice A constant representing the timestamp for completed operations.
24	    uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1);
```

*GitHub* : [10..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L10-L24)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
13	/// @author Matter Labs
14	/// @custom:security-contact security@matterlabs.dev
15	/// @notice Intermediate smart contract between the validator EOA account and the hyperchains state transition diamond smart contract.
16	/// @dev The primary purpose of this contract is to provide a trustless means of delaying batch execution without
17	/// modifying the main hyperchain diamond contract. As such, even if this contract is compromised, it will not impact the main
18	/// contract.
19	/// @dev zkSync actively monitors the chain activity and reacts to any suspicious activity by freezing the chain.
20	/// This allows time for investigation and mitigation before resuming normal operations.
21	/// @dev The contract overloads all of the 4 methods, that are used in state transition. When the batch is committed,
22	/// the timestamp is stored for it. Later, when the owner calls the batch execution, the contract checks that batch
23	/// was committed not earlier than X time ago.
24	contract ValidatorTimelock is IExecutor, Ownable2Step {
25	    using LibMap for LibMap.Uint32Map;
```

*GitHub* : [13..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L13-L25)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

```solidity
16	/// @author Matter Labs
17	/// @dev The contract is used only once to initialize the diamond proxy.
18	/// @dev The deployment process takes care of this contract's initialization.
19	contract DiamondInit is ZkSyncStateTransitionBase, IDiamondInit {
20	    /// @dev Initialize the implementation to prevent any possibility of a Parity hack.
21	    constructor() reentrancyGuardInitializer {}
```

*GitHub* : [16..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L16-L21)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

```solidity
43	/// @author Matter Labs
44	/// @custom:security-contact security@matterlabs.dev
45	/// @notice Interface to which all the upgrade implementations should adhere
46	abstract contract BaseZkSyncUpgrade is ZkSyncStateTransitionBase {
47	    /// @notice Changes the protocol version
48	    event NewProtocolVersion(uint256 indexed previousProtocolVersion, uint256 indexed newProtocolVersion);
```

*GitHub* : [43..48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L43-L48)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

```solidity
16	/// @author Matter Labs
17	/// @custom:security-contact security@matterlabs.dev
18	/// @notice Interface to which all the upgrade implementations should adhere
19	abstract contract BaseZkSyncUpgradeGenesis is BaseZkSyncUpgrade {
20	    /// @notice Changes the protocol version
21	    /// @param _newProtocolVersion The new protocol version
22	    function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
```

*GitHub* : [16..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L16-L22)


---

	 - code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

```solidity
10	/// @author Matter Labs
11	/// @custom:security-contact security@matterlabs.dev
12	contract DefaultUpgrade is BaseZkSyncUpgrade {
13	    /// @notice The main function that will be called by the upgrade proxy.
14	    /// @param _proposedUpgrade The upgrade to be executed.
15	    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```

*GitHub* : [10..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L10-L15)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

```solidity
11	/// @author Matter Labs
12	/// @custom:security-contact security@matterlabs.dev
13	contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {
14	    /// @notice The main function that will be called by the upgrade proxy.
15	    /// @param _proposedUpgrade The upgrade to be executed.
16	    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```

*GitHub* : [11..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L11-L16)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [7..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L7-L14)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


*GitHub* : [7..13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L7-L13)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol


*GitHub* : [7..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L7-L21)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [10..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L10-L14)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


*GitHub* : [6..12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L6-L12)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [9..12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L9-L12)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [18..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L18-L23)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [7..9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L7-L9)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol


*GitHub* : [6..7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L6-L7)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [44..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L44-L47)


---

	 - code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol


*GitHub* : [7..18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L7-L18)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [28..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L28-L30)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [63..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L63-L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol


*GitHub* : [9..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L9-L16)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol


*GitHub* : [17..19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L17-L19)


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol


*GitHub* : [6..7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L6-L7)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [9..10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L9-L10)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [7..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L7-L31)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L23-L24)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [21..27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L21-L27)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [13..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L13-L22)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [7..11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L7-L11)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [7..9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L7-L9)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [7..8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L7-L8)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [16..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L16-L30)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol


*GitHub* : [7..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L7-L16)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L23-L24)


---

	 - code/contracts/zksync/contracts/ForceDeployUpgrader.sol


*GitHub* : [9..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L9-L15)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [7..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L7-L24), [27..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L27-L39), [58..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L58-L67), [80..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L80-L87)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [28..29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L28-L29), [36..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L36-L39)

### [N-61]<a name="n-61"></a> Missing NatSpec `@dev` from error declaration

Some errors have an incomplete NatSpec: add a `@dev` notation to describe the error to improve the code documentation.

*There are 2 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
39	    /// @notice Error for when an address is already a validator.
40	    error AddressAlreadyValidator(uint256 _chainId);
...
42	    /// @notice Error for when an address is not a validator.
43	    error ValidatorDoesNotExist(uint256 _chainId);
```

*GitHub* : [39..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L39-L40), [42..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L42-L43)

### [N-62]<a name="n-62"></a> Missing NatSpec `@param` from error declaration

Some errors have an incomplete NatSpec: add a `@param` notation to describe the error parameters to improve the code documentation.

*There are 2 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
39	    /// @notice Error for when an address is already a validator.
40	    error AddressAlreadyValidator(uint256 _chainId);
...
42	    /// @notice Error for when an address is not a validator.
43	    error ValidatorDoesNotExist(uint256 _chainId);
```

*GitHub* : [39..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L39-L40), [42..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L42-L43)

### [N-63]<a name="n-63"></a> Missing NatSpec from event declaration

Consider adding some comments on event declarations to explain what they are supposed to do: this will help for future code reviews.

*There are 19 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
26	    event DiamondCut(FacetCut[] facetCuts, address initAddress, bytes initCalldata);
```

*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L26)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

```solidity
14	    event DepositInitiated(
15	        bytes32 indexed l2DepositTxHash,
16	        address indexed from,
17	        address indexed to,
18	        address l1Token,
19	        uint256 amount
20	    );
...
22	    event WithdrawalFinalized(address indexed to, address indexed l1Token, uint256 amount);
...
24	    event ClaimedFailedDeposit(address indexed to, address indexed l1Token, uint256 amount);
```

*GitHub* : [14..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L14-L20), [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L22), [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L24)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

```solidity
15	    event LegacyDepositInitiated(
16	        uint256 indexed chainId,
17	        bytes32 indexed l2DepositTxHash,
18	        address indexed from,
19	        address to,
20	        address l1Token,
21	        uint256 amount
22	    );
...
24	    event BridgehubDepositInitiated(
25	        uint256 indexed chainId,
26	        bytes32 indexed txDataHash,
27	        address indexed from,
28	        address to,
29	        address l1Token,
30	        uint256 amount
31	    );
...
33	    event BridgehubDepositBaseTokenInitiated(
34	        uint256 indexed chainId,
35	        address indexed from,
36	        address l1Token,
37	        uint256 amount
38	    );
...
40	    event BridgehubDepositFinalized(
41	        uint256 indexed chainId,
42	        bytes32 indexed txDataHash,
43	        bytes32 indexed l2DepositTxHash
44	    );
...
46	    event WithdrawalFinalizedSharedBridge(
47	        uint256 indexed chainId,
48	        address indexed to,
49	        address indexed l1Token,
50	        uint256 amount
51	    );
...
53	    event ClaimedFailedDepositSharedBridge(
54	        uint256 indexed chainId,
55	        address indexed to,
56	        address indexed l1Token,
57	        uint256 amount
58	    );
```

*GitHub* : [15..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L15-L22), [24..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L24-L31), [33..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L33-L38), [40..44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L40-L44), [46..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L46-L51), [53..58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L53-L58)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L135)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L30), [32..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L32-L36)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol


*GitHub* : [19..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L19-L23)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [9..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L9-L14), [16..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L16-L21)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L8), [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L10), [12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L12)

### [N-64]<a name="n-64"></a> Missing NatSpec `@dev` from event declaration

Some events have an incomplete NatSpec: add a `@dev` notation to describe the event to improve the code documentation.

*There are 48 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
30	    /// @notice The delay between committing and executing batches is changed.
31	    event NewExecutionDelay(uint256 _newExecutionDelay);
...
33	    /// @notice A new validator has been added.
34	    event ValidatorAdded(uint256 _chainId, address _addedValidator);
...
36	    /// @notice A validator has been removed.
37	    event ValidatorRemoved(uint256 _chainId, address _removedValidator);
```

*GitHub* : [30..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L30-L31), [33..34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L33-L34), [36..37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L36-L37)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

```solidity
47	    /// @notice Changes the protocol version
48	    event NewProtocolVersion(uint256 indexed previousProtocolVersion, uint256 indexed newProtocolVersion);
...
50	    /// @notice Сhanges to the bytecode that is used in L2 as a bootloader (start program)
51	    event NewL2BootloaderBytecodeHash(bytes32 indexed previousBytecodeHash, bytes32 indexed newBytecodeHash);
...
53	    /// @notice Сhanges to the bytecode that is used in L2 as a default account
54	    event NewL2DefaultAccountBytecodeHash(bytes32 indexed previousBytecodeHash, bytes32 indexed newBytecodeHash);
...
56	    /// @notice Verifier address changed
57	    event NewVerifier(address indexed oldVerifier, address indexed newVerifier);
...
59	    /// @notice Verifier parameters changed
60	    event NewVerifierParams(VerifierParams oldVerifierParams, VerifierParams newVerifierParams);
...
62	    /// @notice Notifies about complete upgrade
63	    event UpgradeComplete(uint256 indexed newProtocolVersion, bytes32 indexed l2UpgradeTxHash, ProposedUpgrade upgrade);
```

*GitHub* : [47..48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L47-L48), [50..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L50-L51), [53..54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L53-L54), [56..57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L56-L57), [59..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L59-L60), [62..63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L62-L63)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
26	    event DiamondCut(FacetCut[] facetCuts, address initAddress, bytes initCalldata);
```

*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L26)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [14..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L14-L20), [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L22), [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L24)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [15..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L15-L22), [24..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L24-L31), [33..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L33-L38), [40..44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L40-L44), [46..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L46-L51), [53..58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L53-L58)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [49..50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L49-L50), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L135)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [69..70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L69-L70), [72..73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L72-L73), [75..76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L75-L76), [78..79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L78-L79), [81..82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L81-L82), [84..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L84-L85)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L30), [32..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L32-L36), [42..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L42-L43)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [62..63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L62-L63), [65..66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L65-L66), [72..73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L72-L73), [75..76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L75-L76), [78..79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L78-L79), [81..82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L81-L82), [84..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L84-L85), [92..93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L92-L93), [95..96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L95-L96), [98..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L98-L99)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [118..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L118-L125), [133..136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L133-L136)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol


*GitHub* : [19..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L19-L23)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [9..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L9-L14), [16..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L16-L21)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L8), [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L10), [12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L12)

### [N-65]<a name="n-65"></a> Missing NatSpec `@notice` from event declaration

Some events have an incomplete NatSpec: add a `@notice` notation to describe the event to improve the code documentation.

*There are 20 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
26	    event DiamondCut(FacetCut[] facetCuts, address initAddress, bytes initCalldata);
```

*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L26)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

```solidity
14	    event DepositInitiated(
15	        bytes32 indexed l2DepositTxHash,
16	        address indexed from,
17	        address indexed to,
18	        address l1Token,
19	        uint256 amount
20	    );
...
22	    event WithdrawalFinalized(address indexed to, address indexed l1Token, uint256 amount);
...
24	    event ClaimedFailedDeposit(address indexed to, address indexed l1Token, uint256 amount);
```

*GitHub* : [14..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L14-L20), [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L22), [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L24)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

```solidity
15	    event LegacyDepositInitiated(
16	        uint256 indexed chainId,
17	        bytes32 indexed l2DepositTxHash,
18	        address indexed from,
19	        address to,
20	        address l1Token,
21	        uint256 amount
22	    );
...
24	    event BridgehubDepositInitiated(
25	        uint256 indexed chainId,
26	        bytes32 indexed txDataHash,
27	        address indexed from,
28	        address to,
29	        address l1Token,
30	        uint256 amount
31	    );
...
33	    event BridgehubDepositBaseTokenInitiated(
34	        uint256 indexed chainId,
35	        address indexed from,
36	        address l1Token,
37	        uint256 amount
38	    );
...
40	    event BridgehubDepositFinalized(
41	        uint256 indexed chainId,
42	        bytes32 indexed txDataHash,
43	        bytes32 indexed l2DepositTxHash
44	    );
...
46	    event WithdrawalFinalizedSharedBridge(
47	        uint256 indexed chainId,
48	        address indexed to,
49	        address indexed l1Token,
50	        uint256 amount
51	    );
...
53	    event ClaimedFailedDepositSharedBridge(
54	        uint256 indexed chainId,
55	        address indexed to,
56	        address indexed l1Token,
57	        uint256 amount
58	    );
```

*GitHub* : [15..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L15-L22), [24..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L24-L31), [33..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L33-L38), [40..44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L40-L44), [46..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L46-L51), [53..58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L53-L58)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L135)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L30), [32..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L32-L36)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol


*GitHub* : [19..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L19-L23)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [9..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L9-L14), [16..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L16-L21), [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L23-L24)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L8), [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L10), [12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L12)

### [N-66]<a name="n-66"></a> Missing NatSpec `@param` from event declaration

Some events have an incomplete NatSpec: add a `@param` notation to describe the event to improve the code documentation.

*There are 50 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
30	    /// @notice The delay between committing and executing batches is changed.
31	    event NewExecutionDelay(uint256 _newExecutionDelay);
...
33	    /// @notice A new validator has been added.
34	    event ValidatorAdded(uint256 _chainId, address _addedValidator);
...
36	    /// @notice A validator has been removed.
37	    event ValidatorRemoved(uint256 _chainId, address _removedValidator);
```

*GitHub* : [30..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L30-L31), [33..34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L33-L34), [36..37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L36-L37)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

```solidity
47	    /// @notice Changes the protocol version
48	    event NewProtocolVersion(uint256 indexed previousProtocolVersion, uint256 indexed newProtocolVersion);
...
50	    /// @notice Сhanges to the bytecode that is used in L2 as a bootloader (start program)
51	    event NewL2BootloaderBytecodeHash(bytes32 indexed previousBytecodeHash, bytes32 indexed newBytecodeHash);
...
53	    /// @notice Сhanges to the bytecode that is used in L2 as a default account
54	    event NewL2DefaultAccountBytecodeHash(bytes32 indexed previousBytecodeHash, bytes32 indexed newBytecodeHash);
...
56	    /// @notice Verifier address changed
57	    event NewVerifier(address indexed oldVerifier, address indexed newVerifier);
...
59	    /// @notice Verifier parameters changed
60	    event NewVerifierParams(VerifierParams oldVerifierParams, VerifierParams newVerifierParams);
...
62	    /// @notice Notifies about complete upgrade
63	    event UpgradeComplete(uint256 indexed newProtocolVersion, bytes32 indexed l2UpgradeTxHash, ProposedUpgrade upgrade);
```

*GitHub* : [47..48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L47-L48), [50..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L50-L51), [53..54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L53-L54), [56..57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L56-L57), [59..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L59-L60), [62..63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L62-L63)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
26	    event DiamondCut(FacetCut[] facetCuts, address initAddress, bytes initCalldata);
```

*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L26)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [14..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L14-L20), [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L22), [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L24)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [15..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L15-L22), [24..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L24-L31), [33..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L33-L38), [40..44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L40-L44), [46..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L46-L51), [53..58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L53-L58)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [45..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L45-L47), [49..50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L49-L50), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L135)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [69..70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L69-L70), [72..73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L72-L73), [75..76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L75-L76), [78..79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L78-L79), [81..82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L81-L82), [84..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L84-L85)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L30), [32..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L32-L36), [38..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L38-L40), [42..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L42-L43)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [62..63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L62-L63), [65..66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L65-L66), [68..70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L68-L70), [72..73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L72-L73), [75..76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L75-L76), [78..79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L78-L79), [81..82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L81-L82), [84..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L84-L85), [92..93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L92-L93), [95..96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L95-L96), [98..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L98-L99)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol


*GitHub* : [19..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L19-L23)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [9..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L9-L14), [16..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L16-L21), [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L23-L24)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L8), [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L10), [12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L12)

### [N-67]<a name="n-67"></a> Missing NatSpec from modifiers definitions

Consider adding some comments on modifier declarations to explain what they are supposed to do: this will help for future code reviews.

*There are 9 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
47	    modifier onlyOwnerOrAdmin() {
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L47)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

```solidity
28	    modifier onlyStateTransitionManager() {
...
33	    modifier onlyBridgehub() {
...
38	    modifier onlyAdminOrStateTransitionManager() {
...
46	    modifier onlyValidatorOrStateTransitionManager() {
...
54	    modifier onlyBaseTokenBridge() {
```

*GitHub* : [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L28), [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L33), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L38), [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L46), [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L54)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

```solidity
43	    modifier reentrancyGuardInitializer() {
```

*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L43)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
131	    modifier onlyBridge() {
...
136	    modifier onlyNextVersion(uint8 _version) {
```

*GitHub* : [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L131), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L136)

### [N-68]<a name="n-68"></a> Missing NatSpec `@dev` from modifier declaration

Some modifiers have an incomplete NatSpec: add a `@dev` notation to describe the modifier to improve the code documentation.

*There are 21 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
69	    /// @notice Checks that the message sender is the bridgehub.
70	    modifier onlyBridgehub() {
...
75	    /// @notice Checks that the message sender is the bridgehub or zkSync Era Diamond Proxy.
76	    modifier onlyBridgehubOrEra(uint256 _chainId) {
...
84	    /// @notice Checks that the message sender is the legacy bridge.
85	    modifier onlyLegacyBridge() {
```

*GitHub* : [69..70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69-L70), [75..76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75-L76), [84..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L84-L85)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
47	    modifier onlyOwnerOrAdmin() {
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L47)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
59	    /// @notice Checks that the message sender is contract itself.
60	    modifier onlySelf() {
...
65	    /// @notice Checks that the message sender is an active security council.
66	    modifier onlySecurityCouncil() {
...
71	    /// @notice Checks that the message sender is an active owner or an active security council.
72	    modifier onlyOwnerOrSecurityCouncil() {
```

*GitHub* : [59..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59-L60), [65..66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L65-L66), [71..72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L71-L72)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
64	    /// @notice only the bridgehub can call
65	    modifier onlyBridgehub() {
...
70	    /// @notice the admin can call, for non-critical updates
71	    modifier onlyOwnerOrAdmin() {
```

*GitHub* : [64..65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64-L65), [70..71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L70-L71)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
62	    /// @notice Checks if the caller is the admin of the chain.
63	    modifier onlyChainAdmin(uint256 _chainId) {
```

*GitHub* : [62..63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62-L63), [68..69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68-L69)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol


*GitHub* : [16..17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16-L17), [22..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22-L23), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L28), [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L33), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L38), [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L46), [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L54)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L43)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L131), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L136)

### [N-69]<a name="n-69"></a> Missing NatSpec `@notice` from modifier declaration

Some modifiers have an incomplete NatSpec: add a `@notice` notation to describe the modifier to improve the code documentation.

*There are 10 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
47	    modifier onlyOwnerOrAdmin() {
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L47)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

```solidity
28	    modifier onlyStateTransitionManager() {
...
33	    modifier onlyBridgehub() {
...
38	    modifier onlyAdminOrStateTransitionManager() {
...
46	    modifier onlyValidatorOrStateTransitionManager() {
...
54	    modifier onlyBaseTokenBridge() {
```

*GitHub* : [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L28), [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L33), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L38), [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L46), [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L54)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

```solidity
43	    modifier reentrancyGuardInitializer() {
...
63	    /**
64	     * @dev Prevents a contract from calling itself, directly or indirectly.
65	     * Calling a `nonReentrant` function from another `nonReentrant`
66	     * function is not supported. It is possible to prevent this from happening
67	     * by making the `nonReentrant` function external, and make it call a
68	     * `private` function that does the actual work.
69	     */
70	    modifier nonReentrant() {
```

*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L43), [63..70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L63-L70)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
131	    modifier onlyBridge() {
...
136	    modifier onlyNextVersion(uint8 _version) {
```

*GitHub* : [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L131), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L136)

### [N-70]<a name="n-70"></a> Missing NatSpec `@param` from modifier declaration

Some modifiers have an incomplete NatSpec: add a `@param` notation to describe the modifier parameters to improve the code documentation.

*There are 22 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
69	    /// @notice Checks that the message sender is the bridgehub.
70	    modifier onlyBridgehub() {
...
75	    /// @notice Checks that the message sender is the bridgehub or zkSync Era Diamond Proxy.
76	    modifier onlyBridgehubOrEra(uint256 _chainId) {
...
84	    /// @notice Checks that the message sender is the legacy bridge.
85	    modifier onlyLegacyBridge() {
```

*GitHub* : [69..70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69-L70), [75..76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75-L76), [84..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L84-L85)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
47	    modifier onlyOwnerOrAdmin() {
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L47)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
59	    /// @notice Checks that the message sender is contract itself.
60	    modifier onlySelf() {
...
65	    /// @notice Checks that the message sender is an active security council.
66	    modifier onlySecurityCouncil() {
...
71	    /// @notice Checks that the message sender is an active owner or an active security council.
72	    modifier onlyOwnerOrSecurityCouncil() {
```

*GitHub* : [59..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59-L60), [65..66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L65-L66), [71..72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L71-L72)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
64	    /// @notice only the bridgehub can call
65	    modifier onlyBridgehub() {
...
70	    /// @notice the admin can call, for non-critical updates
71	    modifier onlyOwnerOrAdmin() {
```

*GitHub* : [64..65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64-L65), [70..71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L70-L71)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
62	    /// @notice Checks if the caller is the admin of the chain.
63	    modifier onlyChainAdmin(uint256 _chainId) {
```

*GitHub* : [62..63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62-L63), [68..69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68-L69)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol


*GitHub* : [16..17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16-L17), [22..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22-L23), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L28), [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L33), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L38), [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L46), [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L54)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L43), [63..70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L63-L70)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L131), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L136)

### [N-71]<a name="n-71"></a> Missing NatSpec from function definition

Some functions miss a NatSpec, which should be a [best practice](https://docs.soliditylang.org/en/latest/natspec-format.html) to add as a documentation.

Even if Natspec for internal and private function is not parsed (but this may change in the future, according to the official docs), it still helps while reviewing the codebase.

*There are 128 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
139	    function receiveEth(uint256 _chainId) external payable {
...
489	    function _parseL2WithdrawalMessage(
490	        uint256 _chainId,
491	        bytes memory _l2ToL1message
492	    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
```

*GitHub* : [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L139), [489..492](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L489-L492)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
327	    function _actualRefundRecipient(address _refundRecipient) internal view returns (address _recipient) {
```

*GitHub* : [327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L327)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
76	    function getChainAdmin(uint256 _chainId) external view override returns (address) {
...
232	    function registerAlreadyDeployedStateTransition(
233	        uint256 _chainId,
234	        address _stateTransitionContract
235	    ) external onlyOwner {
```

*GitHub* : [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L76), [232..235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L232-L235)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
57	    constructor(address _initialOwner, uint32 _executionDelay) {
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

```solidity
13	    constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
```

*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L13)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
91	    function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {
```

*GitHub* : [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L91)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
217	    function _commitBatches(
218	        StoredBatchInfo memory _lastCommittedBatchData,
219	        CommitBatchInfo[] calldata _newBatchesData
220	    ) internal {
...
351	    function _executeBatches(StoredBatchInfo[] calldata _batchesData) internal {
```

*GitHub* : [217..220](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L217-L220), [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351), [388..392](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L388-L392), [440](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L440), [481](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L481), [515](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515), [525](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525), [537..542](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [230..232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L230-L232), [260..265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L260-L265), [291..295](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L291-L295)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L13), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L19)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol


*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L21), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L28), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L35), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L42)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L26), [28..35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L28-L35), [37..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L37-L43), [45..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L45-L53), [55..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L55-L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L69), [71..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L71-L75), [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L77)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [60..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L60-L64), [66..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L66-L74), [76..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L76-L85), [87..97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L87-L97), [99..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L99-L105), [107..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L107-L114), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L116), [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L118), [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L120), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L122), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L124), [137..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L137-L142), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L144), [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L146)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [9..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L9-L15), [17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L17), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L19), [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L21), [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L23)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L7), [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L9)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L71), [83..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L83-L89), [91..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L91-L99), [101..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L101-L103), [105..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L105-L107), [109..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L109-L114), [118..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L118-L125), [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L127), [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L129), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L131), [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L133)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L43), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L45), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L47), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L49), [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L51), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L53), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L67)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L45), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L71), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L73), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L84), [86..90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L86-L90), [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L92), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L94), [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L96)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L47)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [100..102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L100-L102)


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L7)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L10)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L48)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L161), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [11..17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11-L17)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [11..18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L11-L18)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [26..32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L26-L32), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L34), [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L36), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L38), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L40)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L14), [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L16), [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L18), [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L20)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L16), [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L18)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L29), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39), [78..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L78-L83), [97..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L97-L107), [123..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L123-L129)

### [N-72]<a name="n-72"></a> Missing NatSpec `@dev` from function declaration

Some functions have an incomplete NatSpec: add a `@dev` notation to describe the function to improve the code documentation.

*There are 336 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
76	    /// @return The L2 token address that would be minted for deposit of the given L1 token on zkSync Era.
77	    function l2TokenAddress(address _l1Token) external view returns (address) {
...
204	    /// @notice Finalize the withdrawal and release funds
205	    /// @param _l2BatchNumber The L2 batch number where the withdrawal was processed
206	    /// @param _l2MessageIndex The position in the L2 logs Merkle tree of the l2Log that was sent with the message
207	    /// @param _l2TxNumberInBatch The L2 transaction number in the batch, in which the log was sent
208	    /// @param _message The L2 withdraw data, stored in an L2 -> L1 message
209	    /// @param _merkleProof The Merkle proof of the inclusion L2 -> L1 message about withdrawal initialization
210	    function finalizeWithdrawal(
211	        uint256 _l2BatchNumber,
212	        uint256 _l2MessageIndex,
213	        uint16 _l2TxNumberInBatch,
214	        bytes calldata _message,
215	        bytes32[] calldata _merkleProof
216	    ) external nonReentrant {
```

*GitHub* : [76..77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76-L77), [204..216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L204-L216)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
139	    function receiveEth(uint256 _chainId) external payable {
...
183	    /// @notice Initiates a deposit transaction within Bridgehub, used by `requestL2TransactionTwoBridges`.
184	    function bridgehubDeposit(
185	        uint256 _chainId,
186	        address _prevMsgSender,
187	        uint256, // l2Value, needed for Weth deposits in the future
188	        bytes calldata _data
189	    ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
...
232	    /// @notice Confirms the acceptance of a transaction by the Mailbox, as part of the L2 transaction process within Bridgehub.
233	    /// This function is utilized by `requestL2TransactionTwoBridges` to validate the execution of a transaction.
234	    function bridgehubConfirmL2Transaction(
235	        uint256 _chainId,
236	        bytes32 _txDataHash,
237	        bytes32 _txHash
238	    ) external override onlyBridgehub {
...
380	    /// @notice Finalize the withdrawal and release funds
381	    /// @param _chainId The chain ID of the transaction to check
382	    /// @param _l2BatchNumber The L2 batch number where the withdrawal was processed
383	    /// @param _l2MessageIndex The position in the L2 logs Merkle tree of the l2Log that was sent with the message
384	    /// @param _l2TxNumberInBatch The L2 transaction number in the batch, in which the log was sent
385	    /// @param _message The L2 withdraw data, stored in an L2 -> L1 message
386	    /// @param _merkleProof The Merkle proof of the inclusion L2 -> L1 message about withdrawal initialization
387	    function finalizeWithdrawal(
388	        uint256 _chainId,
389	        uint256 _l2BatchNumber,
390	        uint256 _l2MessageIndex,
391	        uint16 _l2TxNumberInBatch,
392	        bytes calldata _message,
393	        bytes32[] calldata _merkleProof
394	    ) external override {
...
489	    function _parseL2WithdrawalMessage(
490	        uint256 _chainId,
491	        bytes memory _l2ToL1message
492	    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
...
607	    /// @notice Finalizes the withdrawal for transactions initiated via the legacy ERC20 bridge.
608	    /// @param _l2BatchNumber The L2 batch number where the withdrawal was processed
609	    /// @param _l2MessageIndex The position in the L2 logs Merkle tree of the l2Log that was sent with the message
610	    /// @param _l2TxNumberInBatch The L2 transaction number in the batch, in which the log was sent
611	    /// @param _message The L2 withdraw data, stored in an L2 -> L1 message
612	    /// @param _merkleProof The Merkle proof of the inclusion L2 -> L1 message about withdrawal initialization
613	    ///
614	    /// @return l1Receiver The address on L1 that will receive the withdrawn funds
615	    /// @return l1Token The address of the L1 token being withdrawn
616	    /// @return amount The amount of the token being withdrawns
617	    function finalizeWithdrawalLegacyErc20Bridge(
618	        uint256 _l2BatchNumber,
619	        uint256 _l2MessageIndex,
620	        uint16 _l2TxNumberInBatch,
621	        bytes calldata _message,
622	        bytes32[] calldata _merkleProof
623	    ) external override onlyLegacyBridge returns (address l1Receiver, address l1Token, uint256 amount) {
...
634	    /// @notice Withdraw funds from the initiated deposit, that failed when finalizing on zkSync Era chain.
635	    /// This function is specifically designed for maintaining backward-compatibility with legacy `claimFailedDeposit`
636	    /// method in `L1ERC20Bridge`.
637	    ///
638	    /// @param _depositSender The address of the deposit initiator
639	    /// @param _l1Token The address of the deposited L1 ERC20 token
640	    /// @param _amount The amount of the deposit that failed.
641	    /// @param _l2TxHash The L2 transaction hash of the failed deposit finalization
642	    /// @param _l2BatchNumber The L2 batch number where the deposit finalization was processed
643	    /// @param _l2MessageIndex The position in the L2 logs Merkle tree of the l2Log that was sent with the message
644	    /// @param _l2TxNumberInBatch The L2 transaction number in a batch, in which the log was sent
645	    /// @param _merkleProof The Merkle proof of the processing L1 -> L2 transaction with deposit finalization
646	    function claimFailedDepositLegacyErc20Bridge(
647	        address _depositSender,
648	        address _l1Token,
649	        uint256 _amount,
650	        bytes32 _l2TxHash,
651	        uint256 _l2BatchNumber,
652	        uint256 _l2MessageIndex,
653	        uint16 _l2TxNumberInBatch,
654	        bytes32[] calldata _merkleProof
655	    ) external override onlyLegacyBridge {
```

*GitHub* : [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L139), [183..189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L183-L189), [232..238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L232-L238), [380..394](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L380-L394), [489..492](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L489-L492), [607..623](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L607-L623), [634..655](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L634-L655)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
39	    /// @notice to avoid parity hack
40	    constructor() reentrancyGuardInitializer {}
```

*GitHub* : [39..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L39-L40), [42..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L42-L43), [52..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L52-L53), [61..62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L61-L62), [76..77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L76-L77), [83..84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83-L84), [92..94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L92-L94), [102..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102-L103), [108..110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108-L110), [114..123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114-L123), [153..160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L153-L160), [165..172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L165-L172), [177..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L177-L186), [199..205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L199-L205), [215..221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L215-L221), [255..266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L255-L266), [327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L327)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [39..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L39-L43)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L76), [111..112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L111-L112), [120..121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L120-L121), [232..235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L232-L235), [240..247](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L240-L247)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


*GitHub* : [23..26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L23-L26)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L13)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [24..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L24-L25), [33..34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L33-L34), [46..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L46-L47), [52..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L52-L53), [59..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L59-L60), [68..69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L68-L69), [80..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L80-L81), [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L91), [101..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L101-L105), [124..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L124-L125), [134..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L134-L135), [144..145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L144-L145)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [101..109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L101-L109), [200..204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L200-L204), [208..213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L208-L213), [217..220](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L217-L220), [338..342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L338-L342), [346..347](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L346-L347), [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351), [369..374](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L369-L374), [378..384](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L378-L384), [388..392](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L388-L392), [440](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L440), [471..472](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L471-L472), [476..477](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L476-L477), [481](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L481), [515](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515), [525](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525), [537..542](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542), [586..587](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L586-L587), [591..592](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L591-L592), [596..597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L596-L597), [601..609](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L601-L609)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [33..34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L33-L34), [38..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L38-L39), [43..44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L43-L44), [48..49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L48-L49), [53..54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L53-L54), [58..59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L58-L59), [63..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L63-L64), [68..69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L68-L69), [73..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L73-L74), [78..79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L78-L79), [83..84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L83-L84), [88..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L88-L89), [93..94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L93-L94), [98..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L98-L99), [103..104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L103-L104), [108..109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L108-L109), [113..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L113-L114), [118..119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L118-L119), [123..124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L123-L124), [128..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L128-L129), [133..134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L133-L134), [138..139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L138-L139), [143..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L143-L144), [148..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L148-L149), [153..154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L153-L154), [158..159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L158-L159), [164..165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L164-L165), [177..178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L177-L178), [182..183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L182-L183), [189..190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L189-L190), [194..195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L194-L195), [203..204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L203-L204), [218..219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L218-L219), [224..225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L224-L225), [230..231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L230-L231), [240..241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L240-L241), [245..246](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L245-L246), [250..251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L250-L251), [255..256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L255-L256), [260..261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L260-L261)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [39..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39-L40), [48..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L48-L51), [55..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L55-L61), [65..71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L65-L71), [75..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L75-L83), [144..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L144-L149), [154..158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L154-L158), [179..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L179-L186), [198..207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L198-L207), [230..232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L230-L232), [260..265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L260-L265), [291..295](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L291-L295), [317..322](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L317-L322), [354..355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L354-L355)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [92..94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L92-L94), [109..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L109-L111), [126..128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L126-L128), [142..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L142-L144), [162..165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L162-L165), [170..173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L170-L173), [221..224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L221-L224), [236..238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L236-L238), [261..265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L261-L265), [267..271](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L267-L271)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [20..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20-L22)


---

	 - code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol


*GitHub* : [13..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L13-L15)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol


*GitHub* : [14..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L14-L16)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [16..23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L16-L23), [48..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L48-L51), [55..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L55-L67)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L13), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L19)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol


*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L21), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L28), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L35), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L42)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [88..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L88-L89)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [35..37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L35-L37), [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L41-L42), [46..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L46-L47), [51..52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L51-L52), [56..57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L56-L57), [65..66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L65-L66), [72..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L72-L74)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [106..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L106-L114)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L26), [28..35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L28-L35), [37..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L37-L43), [45..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L45-L53), [55..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L55-L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L69), [71..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L71-L75), [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L77)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [60..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L60-L64), [66..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L66-L74), [76..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L76-L85), [87..97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L87-L97), [99..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L99-L105), [107..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L107-L114), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L116), [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L118), [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L120), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L122), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L124), [126..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L126-L135), [137..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L137-L142), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L144), [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L146)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [9..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L9-L15), [17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L17), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L19), [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L21), [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L23)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L7), [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L9)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [52..55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L52-L55), [57..58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L57-L58), [60..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L60-L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L71), [73..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L73-L81), [83..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L83-L89), [91..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L91-L99), [101..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L101-L103), [105..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L105-L107), [109..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L109-L114), [118..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L118-L125), [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L127), [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L129), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L131), [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L133)


---

	 - code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol


*GitHub* : [26..27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L26-L27), [29..33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L29-L33)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L43), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L45), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L47), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L49), [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L51), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L53), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L67)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L45), [47..50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L47-L50), [52..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L52-L53), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L71), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L73), [75..82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L75-L82), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L84), [86..90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L86-L90), [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L92), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L94), [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L96)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [16..19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L16-L19), [21..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L21-L22), [24..27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L24-L27), [29..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L29-L31), [33..35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L33-L35), [37..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L37-L39), [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L41-L42), [44..45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L44-L45), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L47)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol


*GitHub* : [133..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L133-L142), [144..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L144-L149), [162..168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L162-L168), [170..174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L170-L174), [176..177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L176-L177), [179..183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L179-L183), [185..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L185-L186)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol


*GitHub* : [20..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L20-L21), [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L23-L24), [26..27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L26-L27), [29..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L29-L30), [32..33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L32-L33), [35..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L35-L36), [38..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L38-L39), [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L41-L42), [44..45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L44-L45), [47..48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L47-L48), [50..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L50-L51), [60..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L60-L61), [63..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L63-L64), [66..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L66-L67), [69..70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L69-L70), [77..78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L77-L78), [80..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L80-L81), [83..84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L83-L84), [86..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L86-L87), [89..90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L89-L90), [92..93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L92-L93), [102..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L102-L103), [105..108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L105-L108), [110..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L110-L111), [113..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L113-L114), [116..117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L116-L117), [131..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L131-L132), [134..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L134-L135), [137..138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L137-L138), [140..141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L140-L141), [143..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L143-L144), [146..147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L146-L147)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [14..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L14-L25), [27..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L27-L38), [40..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L40-L56), [58..70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L58-L70), [100..102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L100-L102), [104..113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L104-L113), [115..116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L115-L116)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol


*GitHub* : [27..29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L27-L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol


*GitHub* : [10..11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L10-L11)


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L7)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L10)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L48)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [26..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L26-L30), [36..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L36-L40)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [47..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L47-L56), [75..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L75-L87), [120..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L120-L125), [150..151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150-L151)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L161), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [11..17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11-L17)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [11..18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L11-L18)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [26..32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L26-L32), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L34), [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L36), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L38), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L40)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L14), [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L16), [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L18), [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L20)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L16), [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L18)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [26..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L26-L30), [36..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L36-L40)


---

	 - code/contracts/zksync/contracts/ForceDeployUpgrader.sol


*GitHub* : [13..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L13-L15)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [21..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L21-L24), [47..49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L47-L49), [51..55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L51-L55), [64..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L64-L67), [89..92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L89-L92), [96..108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L96-L108)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L29), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39), [78..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L78-L83), [97..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L97-L107), [123..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L123-L129)

### [N-73]<a name="n-73"></a> Missing NatSpec `@notice` from function declaration

Some functions have an incomplete NatSpec: add a `@notice` notation to describe the function to improve the code documentation.

*There are 340 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
55	    /// @dev Contract is expected to be used as proxy implementation.
56	    /// @dev Initialize the implementation to prevent Parity hack.
57	    constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
...
61	    /// @dev Initializes the reentrancy guard. Expected to be used in the proxy.
62	    function initialize() external reentrancyGuardInitializer {}
...
64	    /// @dev transfer token to shared bridge as part of upgrade
65	    function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
...
76	    /// @return The L2 token address that would be minted for deposit of the given L1 token on zkSync Era.
77	    function l2TokenAddress(address _l1Token) external view returns (address) {
...
160	    /// @dev Transfers tokens from the depositor address to the shared bridge address.
161	    /// @return The difference between the contract balance before and after the transferring of funds.
162	    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
...
170	    /// @dev Withdraw funds from the initiated deposit, that failed when finalizing on L2.
171	    /// @param _depositSender The address of the deposit initiator
172	    /// @param _l1Token The address of the deposited L1 ERC20 token
173	    /// @param _l2TxHash The L2 transaction hash of the failed deposit finalization
174	    /// @param _l2BatchNumber The L2 batch number where the deposit finalization was processed
175	    /// @param _l2MessageIndex The position in the L2 logs Merkle tree of the l2Log that was sent with the message
176	    /// @param _l2TxNumberInBatch The L2 transaction number in a batch, in which the log was sent
177	    /// @param _merkleProof The Merkle proof of the processing L1 -> L2 transaction with deposit finalization
178	    function claimFailedDeposit(
179	        address _depositSender,
180	        address _l1Token,
181	        bytes32 _l2TxHash,
182	        uint256 _l2BatchNumber,
183	        uint256 _l2MessageIndex,
184	        uint16 _l2TxNumberInBatch,
185	        bytes32[] calldata _merkleProof
186	    ) external nonReentrant {
```

*GitHub* : [55..57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55-L57), [61..62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L61-L62), [64..65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64-L65), [76..77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76-L77), [160..162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160-L162), [170..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L170-L186)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
90	    /// @dev Contract is expected to be used as proxy implementation.
91	    /// @dev Initialize the implementation to prevent Parity hack.
92	    constructor(
93	        address _l1WethAddress,
94	        IBridgehub _bridgehub,
95	        IL1ERC20Bridge _legacyBridge
96	    ) reentrancyGuardInitializer {
...
103	    /// @dev Initializes a contract bridge for later use. Expected to be used in the proxy
104	    /// @param _owner Address which can change L2 token implementation and upgrade the bridge
105	    /// implementation. The owner is the Governor and separate from the ProxyAdmin from now on, so that the Governor can call the bridge.
106	    function initialize(
107	        address _owner,
108	        uint256 _eraFirstPostUpgradeBatch
109	    ) external reentrancyGuardInitializer initializer {
...
117	    /// @dev tranfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process
118	    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
...
139	    function receiveEth(uint256 _chainId) external payable {
```

*GitHub* : [90..96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90-L96), [103..109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L103-L109), [117..118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L117-L118), [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L139), [143..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L143-L144), [173..175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L173-L175), [244..250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L244-L250), [255..256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L255-L256), [270..289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L270-L289), [304..316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L304-L316), [372..376](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L372-L376), [409..418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L409-L418), [459..465](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L459-L465), [489..492](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L489-L492)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [52..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L52-L53), [61..62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L61-L62), [327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L327)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [84..86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L84-L86), [90..91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L90-L91), [96..97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L96-L97), [101..102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L101-L102), [106..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L106-L107), [153..156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L153-L156), [204..206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L204-L206), [214..217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L214-L217), [224..226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L224-L226), [249..251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L249-L251), [256..258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L256-L258), [263..264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L263-L264)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [58..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58-L60), [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L76), [80..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L80-L83), [111..112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L111-L112), [120..121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L120-L121), [133..134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L133-L134), [138..139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138-L139), [143..148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L143-L148), [153..157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L153-L157), [161..162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L161-L162), [166..167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L166-L167), [171..172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L171-L172), [178..179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L178-L179), [232..235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L232-L235)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57), [74..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L74-L75), [79..80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L79-L80), [88..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L88-L89), [97..98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L97-L98), [103..104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L103-L104), [108..113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L108-L113), [126..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L126-L132), [145..148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L145-L148), [152..155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L152-L155), [159..166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L159-L166), [170..178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L170-L178), [182..184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L182-L184), [203..208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L203-L208), [225..227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L225-L227)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


*GitHub* : [20..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L20-L21)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L13), [20..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L20-L22)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [24..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L24-L25), [33..34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L33-L34), [46..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L46-L47), [52..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L52-L53), [59..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L59-L60), [68..69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L68-L69), [80..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L80-L81), [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L91), [101..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L101-L105), [124..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L124-L125), [134..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L134-L135), [144..145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L144-L145)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [128..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L128-L135), [200..204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L200-L204), [208..213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L208-L213), [217..220](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L217-L220), [252..258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L252-L258), [271..279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L271-L279), [309..310](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L309-L310), [319..323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L319-L323), [338..342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L338-L342), [346..347](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L346-L347), [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351), [369..374](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L369-L374), [378..384](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L378-L384), [388..392](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L388-L392), [440](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L440), [452..457](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L452-L457), [471..472](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L471-L472), [476..477](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L476-L477), [481](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L481), [499..505](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L499-L505), [515](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515), [525](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525), [537..542](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542), [557..564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L557-L564), [621..628](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L621-L628), [676..679](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L676-L679)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [33..34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L33-L34), [38..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L38-L39), [43..44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L43-L44), [48..49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L48-L49), [53..54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L53-L54), [58..59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L58-L59), [63..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L63-L64), [68..69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L68-L69), [73..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L73-L74), [78..79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L78-L79), [83..84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L83-L84), [88..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L88-L89), [93..94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L93-L94), [98..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L98-L99), [103..104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L103-L104), [108..109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L108-L109), [113..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L113-L114), [118..119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L118-L119), [123..124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L123-L124), [128..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L128-L129), [133..134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L133-L134), [138..139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L138-L139), [143..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L143-L144), [148..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L148-L149), [153..154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L153-L154), [158..159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L158-L159), [164..165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L164-L165), [177..178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L177-L178), [182..183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L182-L183), [189..190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L189-L190), [194..195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L194-L195), [203..204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L203-L204), [218..219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L218-L219), [224..225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L224-L225), [230..231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L230-L231), [240..241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L240-L241), [245..246](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L245-L246), [250..251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L250-L251), [255..256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L255-L256), [260..261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L260-L261)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [39..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39-L40), [55..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L55-L61), [65..71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L65-L71), [75..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L75-L83), [105..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L105-L111), [131..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L131-L132), [144..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L144-L149), [179..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L179-L186), [198..207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L198-L207), [230..232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L230-L232), [260..265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L260-L265), [291..295](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L291-L295)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L13), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L19)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol


*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L21), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L28), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L35), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L42)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [88..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L88-L89), [96..98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L96-L98), [126..128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L126-L128), [149..151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L149-L151), [172..174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L172-L174), [189..191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L189-L191), [202..207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L202-L207), [228..230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L228-L230), [257..259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L257-L259), [278..280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L278-L280)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


*GitHub* : [16..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L16-L20), [36..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L36-L40)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [14..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L14-L24), [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L41-L42)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L41-L42), [46..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L46-L47), [51..52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L51-L52), [65..66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L65-L66)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [16..26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L16-L26), [46..48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L46-L48), [65..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L65-L75)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L26), [28..35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L28-L35), [37..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L37-L43), [45..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L45-L53), [55..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L55-L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L69), [71..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L71-L75), [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L77)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [60..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L60-L64), [66..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L66-L74), [76..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L76-L85), [87..97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L87-L97), [99..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L99-L105), [107..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L107-L114), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L116), [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L118), [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L120), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L122), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L124), [126..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L126-L135), [137..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L137-L142), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L144), [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L146)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [9..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L9-L15), [17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L17), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L19), [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L21), [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L23)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L7), [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L9)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [60..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L60-L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L71), [73..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L73-L81), [83..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L83-L89), [91..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L91-L99), [101..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L101-L103), [105..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L105-L107), [109..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L109-L114), [118..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L118-L125), [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L127), [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L129), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L131), [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L133)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L43), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L45), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L47), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L49), [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L51), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L53), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L67)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L45), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L71), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L73), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L84), [86..90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L86-L90), [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L92), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L94), [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L96)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L47)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol


*GitHub* : [20..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L20-L21), [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L23-L24), [26..27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L26-L27), [29..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L29-L30), [32..33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L32-L33), [35..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L35-L36), [38..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L38-L39), [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L41-L42), [44..45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L44-L45), [47..48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L47-L48), [50..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L50-L51), [60..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L60-L61), [63..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L63-L64), [66..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L66-L67), [69..70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L69-L70), [77..78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L77-L78), [80..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L80-L81), [83..84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L83-L84), [86..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L86-L87), [89..90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L89-L90), [92..93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L92-L93), [95..100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L95-L100), [102..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L102-L103), [105..108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L105-L108), [110..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L110-L111), [113..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L113-L114), [116..117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L116-L117), [131..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L131-L132), [134..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L134-L135), [137..138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L137-L138), [140..141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L140-L141), [143..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L143-L144), [146..147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L146-L147)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol


*GitHub* : [14..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L14-L16), [18..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L18-L20), [22..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L22-L24), [32..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L32-L38)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [100..102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L100-L102)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol


*GitHub* : [18..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L18-L25)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol


*GitHub* : [10..11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L10-L11)


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L7)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L10)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L48)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [41..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L41-L43), [110..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L110-L111), [139..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L139-L144), [150..151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150-L151), [158..159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L158-L159), [163..166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L163-L166)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L41-L42), [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L161), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173), [179..180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L179-L180), [184..185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L184-L185)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [11..17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11-L17)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [11..18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L11-L18)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [26..32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L26-L32), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L34), [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L36), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L38), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L40)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L14), [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L16), [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L18), [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L20)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [17..34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L17-L34), [36..52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L36-L52)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L16), [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L18)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L29), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39), [78..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L78-L83), [97..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L97-L107), [123..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L123-L129)

### [N-74]<a name="n-74"></a> Missing NatSpec `@param` from function declaration

Some functions have an incomplete NatSpec: add a `@param` notation to describe the function parameters to improve the code documentation.

*There are 365 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
55	    /// @dev Contract is expected to be used as proxy implementation.
56	    /// @dev Initialize the implementation to prevent Parity hack.
57	    constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
...
61	    /// @dev Initializes the reentrancy guard. Expected to be used in the proxy.
62	    function initialize() external reentrancyGuardInitializer {}
...
64	    /// @dev transfer token to shared bridge as part of upgrade
65	    function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
...
76	    /// @return The L2 token address that would be minted for deposit of the given L1 token on zkSync Era.
77	    function l2TokenAddress(address _l1Token) external view returns (address) {
...
160	    /// @dev Transfers tokens from the depositor address to the shared bridge address.
161	    /// @return The difference between the contract balance before and after the transferring of funds.
162	    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```

*GitHub* : [55..57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55-L57), [61..62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L61-L62), [64..65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64-L65), [76..77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76-L77), [160..162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160-L162)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
90	    /// @dev Contract is expected to be used as proxy implementation.
91	    /// @dev Initialize the implementation to prevent Parity hack.
92	    constructor(
93	        address _l1WethAddress,
94	        IBridgehub _bridgehub,
95	        IL1ERC20Bridge _legacyBridge
96	    ) reentrancyGuardInitializer {
...
117	    /// @dev tranfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process
118	    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
...
139	    function receiveEth(uint256 _chainId) external payable {
...
143	    /// @dev Initializes the l2Bridge address by governance for a specific chain.
144	    function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner {
...
148	    /// @notice Allows bridgehub to acquire mintValue for L1->L2 transactions.
149	    /// @dev If the corresponding L2 transaction fails, refunds are issued to a refund recipient on L2.
150	    function bridgehubDepositBaseToken(
151	        uint256 _chainId,
152	        address _prevMsgSender,
153	        address _l1Token,
154	        uint256 _amount
155	    ) external payable virtual onlyBridgehubOrEra(_chainId) {
```

*GitHub* : [90..96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90-L96), [117..118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L117-L118), [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L139), [143..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L143-L144), [148..155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L148-L155), [173..175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L173-L175), [183..189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L183-L189), [232..238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L232-L238), [244..250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L244-L250), [255..256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L255-L256), [304..316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L304-L316), [409..418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L409-L418), [459..465](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L459-L465), [489..492](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L489-L492)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [39..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L39-L40), [42..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L42-L43), [52..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L52-L53), [61..62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L61-L62), [76..77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L76-L77), [83..84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83-L84), [92..94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L92-L94), [102..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102-L103), [108..110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108-L110), [114..123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114-L123), [153..160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L153-L160), [165..172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L165-L172), [177..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L177-L186), [199..205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L199-L205), [215..221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L215-L221), [255..266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L255-L266), [327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L327)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [84..86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L84-L86), [90..91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L90-L91), [96..97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L96-L97), [101..102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L101-L102), [106..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L106-L107), [263..264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L263-L264)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [58..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58-L60), [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L76), [80..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L80-L83), [111..112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L111-L112), [120..121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L120-L121), [133..134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L133-L134), [138..139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138-L139), [143..148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L143-L148), [153..157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L153-L157), [161..162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L161-L162), [166..167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L166-L167), [171..172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L171-L172), [178..179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L178-L179), [232..235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L232-L235), [240..247](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L240-L247)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57), [74..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L74-L75), [79..80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L79-L80), [88..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L88-L89), [97..98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L97-L98), [103..104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L103-L104), [108..113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L108-L113), [126..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L126-L132), [145..148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L145-L148), [152..155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L152-L155), [159..166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L159-L166), [170..178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L170-L178), [182..184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L182-L184), [203..208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L203-L208), [225..227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L225-L227)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


*GitHub* : [20..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L20-L21), [23..26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L23-L26)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L13), [20..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L20-L22)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [24..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L24-L25), [33..34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L33-L34), [46..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L46-L47), [52..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L52-L53), [59..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L59-L60), [68..69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L68-L69), [80..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L80-L81), [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L91), [101..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L101-L105), [124..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L124-L125), [134..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L134-L135), [144..145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L144-L145)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [31..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L31-L38), [128..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L128-L135), [200..204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L200-L204), [208..213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L208-L213), [217..220](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L217-L220), [309..310](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L309-L310), [319..323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L319-L323), [338..342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L338-L342), [346..347](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L346-L347), [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351), [369..374](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L369-L374), [378..384](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L378-L384), [388..392](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L388-L392), [440](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L440), [452..457](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L452-L457), [471..472](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L471-L472), [476..477](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L476-L477), [481](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L481), [499..505](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L499-L505), [515](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515), [525](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525), [537..542](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542), [586..587](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L586-L587), [591..592](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L591-L592), [596..597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L596-L597), [601..609](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L601-L609), [621..628](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L621-L628), [676..679](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L676-L679)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [33..34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L33-L34), [38..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L38-L39), [43..44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L43-L44), [48..49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L48-L49), [53..54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L53-L54), [58..59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L58-L59), [63..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L63-L64), [68..69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L68-L69), [73..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L73-L74), [78..79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L78-L79), [83..84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L83-L84), [88..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L88-L89), [93..94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L93-L94), [98..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L98-L99), [103..104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L103-L104), [108..109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L108-L109), [113..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L113-L114), [118..119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L118-L119), [123..124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L123-L124), [128..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L128-L129), [133..134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L133-L134), [138..139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L138-L139), [143..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L143-L144), [148..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L148-L149), [153..154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L153-L154), [158..159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L158-L159), [164..165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L164-L165), [177..178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L177-L178), [182..183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L182-L183), [189..190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L189-L190), [194..195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L194-L195), [203..204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L203-L204), [218..219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L218-L219), [224..225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L224-L225), [230..231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L230-L231), [240..241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L240-L241), [245..246](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L245-L246), [250..251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L250-L251), [255..256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L255-L256), [260..261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L260-L261)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [39..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39-L40), [48..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L48-L51), [55..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L55-L61), [65..71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L65-L71), [75..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L75-L83), [105..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L105-L111), [131..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L131-L132), [144..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L144-L149), [179..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L179-L186), [198..207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L198-L207), [230..232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L230-L232), [260..265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L260-L265), [291..295](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L291-L295), [317..322](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L317-L322), [354..355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L354-L355)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L13), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L19)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol


*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L21), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L28), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L35), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L42)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [88..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L88-L89), [126..128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L126-L128), [149..151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L149-L151), [172..174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L172-L174), [189..191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L189-L191), [202..207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L202-L207), [228..230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L228-L230), [257..259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L257-L259), [278..280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L278-L280)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L41-L42)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [35..37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L35-L37), [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L41-L42), [46..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L46-L47), [51..52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L51-L52), [56..57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L56-L57), [65..66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L65-L66), [72..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L72-L74)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L26), [28..35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L28-L35), [37..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L37-L43), [45..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L45-L53), [55..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L55-L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L69), [71..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L71-L75), [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L77)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [60..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L60-L64), [66..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L66-L74), [76..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L76-L85), [87..97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L87-L97), [99..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L99-L105), [107..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L107-L114), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L116), [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L118), [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L120), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L122), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L124), [126..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L126-L135), [137..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L137-L142), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L144), [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L146)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [9..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L9-L15), [17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L17), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L19), [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L21), [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L23)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L7), [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L9)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [57..58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L57-L58), [60..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L60-L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L71), [73..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L73-L81), [83..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L83-L89), [91..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L91-L99), [101..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L101-L103), [105..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L105-L107), [109..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L109-L114), [118..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L118-L125), [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L127), [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L129), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L131), [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L133)


---

	 - code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol


*GitHub* : [26..27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L26-L27)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L43), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L45), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L47), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L49), [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L51), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L53), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L67)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L45), [52..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L52-L53), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L71), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L73), [75..82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L75-L82), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L84), [86..90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L86-L90), [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L92), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L94), [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L96)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [21..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L21-L22), [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L41-L42), [44..45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L44-L45), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L47), [54..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L54-L56), [58..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L58-L60)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol


*GitHub* : [144..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L144-L149), [162..168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L162-L168), [176..177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L176-L177), [185..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L185-L186)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol


*GitHub* : [20..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L20-L21), [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L23-L24), [26..27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L26-L27), [29..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L29-L30), [32..33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L32-L33), [35..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L35-L36), [38..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L38-L39), [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L41-L42), [44..45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L44-L45), [47..48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L47-L48), [50..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L50-L51), [53..58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L53-L58), [60..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L60-L61), [63..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L63-L64), [66..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L66-L67), [69..70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L69-L70), [72..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L72-L75), [77..78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L77-L78), [80..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L80-L81), [83..84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L83-L84), [86..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L86-L87), [89..90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L89-L90), [92..93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L92-L93), [95..100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L95-L100), [102..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L102-L103), [110..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L110-L111), [113..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L113-L114), [116..117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L116-L117), [131..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L131-L132), [134..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L134-L135), [137..138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L137-L138), [140..141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L140-L141), [143..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L143-L144), [146..147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L146-L147)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol


*GitHub* : [14..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L14-L16), [18..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L18-L20), [22..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L22-L24), [26..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L26-L30), [32..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L32-L38)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [100..102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L100-L102), [115..116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L115-L116)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol


*GitHub* : [18..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L18-L25), [27..29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L27-L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol


*GitHub* : [10..11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L10-L11)


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L7)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L10)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L48)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [41..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L41-L43), [110..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L110-L111), [139..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L139-L144), [150..151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150-L151), [158..159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L158-L159), [163..166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L163-L166)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L41-L42), [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L161), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173), [179..180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L179-L180), [184..185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L184-L185)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [11..17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11-L17)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [11..18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L11-L18)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [26..32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L26-L32), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L34), [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L36), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L38), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L40)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L14), [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L16), [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L18), [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L20)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L16), [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L18)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L29), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39), [78..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L78-L83), [97..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L97-L107), [123..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L123-L129)

### [N-75]<a name="n-75"></a> Incomplete NatSpec `@return` from function declaration

Some functions have an incomplete NatSpec: add a `@return` notation to describe the function return value to improve the code documentation.

*There are 379 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
55	    /// @dev Contract is expected to be used as proxy implementation.
56	    /// @dev Initialize the implementation to prevent Parity hack.
57	    constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
...
61	    /// @dev Initializes the reentrancy guard. Expected to be used in the proxy.
62	    function initialize() external reentrancyGuardInitializer {}
...
64	    /// @dev transfer token to shared bridge as part of upgrade
65	    function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
...
170	    /// @dev Withdraw funds from the initiated deposit, that failed when finalizing on L2.
171	    /// @param _depositSender The address of the deposit initiator
172	    /// @param _l1Token The address of the deposited L1 ERC20 token
173	    /// @param _l2TxHash The L2 transaction hash of the failed deposit finalization
174	    /// @param _l2BatchNumber The L2 batch number where the deposit finalization was processed
175	    /// @param _l2MessageIndex The position in the L2 logs Merkle tree of the l2Log that was sent with the message
176	    /// @param _l2TxNumberInBatch The L2 transaction number in a batch, in which the log was sent
177	    /// @param _merkleProof The Merkle proof of the processing L1 -> L2 transaction with deposit finalization
178	    function claimFailedDeposit(
179	        address _depositSender,
180	        address _l1Token,
181	        bytes32 _l2TxHash,
182	        uint256 _l2BatchNumber,
183	        uint256 _l2MessageIndex,
184	        uint16 _l2TxNumberInBatch,
185	        bytes32[] calldata _merkleProof
186	    ) external nonReentrant {
...
204	    /// @notice Finalize the withdrawal and release funds
205	    /// @param _l2BatchNumber The L2 batch number where the withdrawal was processed
206	    /// @param _l2MessageIndex The position in the L2 logs Merkle tree of the l2Log that was sent with the message
207	    /// @param _l2TxNumberInBatch The L2 transaction number in the batch, in which the log was sent
208	    /// @param _message The L2 withdraw data, stored in an L2 -> L1 message
209	    /// @param _merkleProof The Merkle proof of the inclusion L2 -> L1 message about withdrawal initialization
210	    function finalizeWithdrawal(
211	        uint256 _l2BatchNumber,
212	        uint256 _l2MessageIndex,
213	        uint16 _l2TxNumberInBatch,
214	        bytes calldata _message,
215	        bytes32[] calldata _merkleProof
216	    ) external nonReentrant {
```

*GitHub* : [55..57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55-L57), [61..62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L61-L62), [64..65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64-L65), [170..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L170-L186), [204..216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L204-L216)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
90	    /// @dev Contract is expected to be used as proxy implementation.
91	    /// @dev Initialize the implementation to prevent Parity hack.
92	    constructor(
93	        address _l1WethAddress,
94	        IBridgehub _bridgehub,
95	        IL1ERC20Bridge _legacyBridge
96	    ) reentrancyGuardInitializer {
...
103	    /// @dev Initializes a contract bridge for later use. Expected to be used in the proxy
104	    /// @param _owner Address which can change L2 token implementation and upgrade the bridge
105	    /// implementation. The owner is the Governor and separate from the ProxyAdmin from now on, so that the Governor can call the bridge.
106	    function initialize(
107	        address _owner,
108	        uint256 _eraFirstPostUpgradeBatch
109	    ) external reentrancyGuardInitializer initializer {
...
117	    /// @dev tranfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process
118	    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
...
139	    function receiveEth(uint256 _chainId) external payable {
...
143	    /// @dev Initializes the l2Bridge address by governance for a specific chain.
144	    function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner {
```

*GitHub* : [90..96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90-L96), [103..109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L103-L109), [117..118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L117-L118), [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L139), [143..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L143-L144), [148..155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L148-L155), [183..189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L183-L189), [232..238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L232-L238), [244..250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L244-L250), [255..256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L255-L256), [270..289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L270-L289), [304..316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L304-L316), [380..394](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L380-L394), [409..418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L409-L418), [459..465](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L459-L465), [489..492](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L489-L492), [634..655](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L634-L655)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [39..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L39-L40), [42..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L42-L43), [52..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L52-L53), [61..62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L61-L62), [76..77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L76-L77), [83..84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83-L84), [92..94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L92-L94), [102..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102-L103), [108..110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108-L110), [114..123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114-L123), [153..160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L153-L160), [165..172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L165-L172), [177..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L177-L186), [199..205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L199-L205), [215..221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L215-L221), [255..266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L255-L266), [327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L327)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [39..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L39-L43), [84..86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L84-L86), [90..91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L90-L91), [96..97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L96-L97), [101..102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L101-L102), [106..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L106-L107), [124..131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L124-L131), [137..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L137-L144), [153..156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L153-L156), [166..169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L166-L169), [185..188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L185-L188), [204..206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L204-L206), [214..217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L214-L217), [224..226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L224-L226), [238..241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L238-L241), [249..251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L249-L251), [256..258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L256-L258), [263..264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L263-L264)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [58..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58-L60), [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L76), [80..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L80-L83), [111..112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L111-L112), [120..121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L120-L121), [133..134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L133-L134), [138..139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138-L139), [143..148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L143-L148), [153..157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L153-L157), [161..162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L161-L162), [166..167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L166-L167), [171..172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L171-L172), [178..179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L178-L179), [232..235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L232-L235), [240..247](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L240-L247)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57), [74..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L74-L75), [79..80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L79-L80), [88..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L88-L89), [97..98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L97-L98), [103..104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L103-L104), [108..113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L108-L113), [126..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L126-L132), [145..148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L145-L148), [152..155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L152-L155), [159..166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L159-L166), [170..178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L170-L178), [182..184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L182-L184), [203..208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L203-L208), [225..227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L225-L227)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


*GitHub* : [20..21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L20-L21)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L13), [20..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L20-L22)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [24..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L24-L25), [33..34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L33-L34), [46..47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L46-L47), [52..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L52-L53), [59..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L59-L60), [68..69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L68-L69), [80..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L80-L81), [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L91), [101..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L101-L105), [124..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L124-L125), [134..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L134-L135), [144..145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L144-L145)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [31..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L31-L38), [101..109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L101-L109), [128..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L128-L135), [200..204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L200-L204), [208..213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L208-L213), [217..220](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L217-L220), [252..258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L252-L258), [271..279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L271-L279), [309..310](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L309-L310), [319..323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L319-L323), [338..342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L338-L342), [346..347](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L346-L347), [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351), [369..374](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L369-L374), [378..384](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L378-L384), [388..392](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L388-L392), [440](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L440), [452..457](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L452-L457), [471..472](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L471-L472), [476..477](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L476-L477), [481](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L481), [499..505](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L499-L505), [515](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515), [525](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525), [537..542](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542), [557..564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L557-L564), [586..587](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L586-L587), [591..592](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L591-L592), [596..597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L596-L597), [601..609](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L601-L609), [621..628](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L621-L628), [676..679](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L676-L679)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [33..34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L33-L34), [38..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L38-L39), [43..44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L43-L44), [48..49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L48-L49), [53..54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L53-L54), [58..59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L58-L59), [63..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L63-L64), [68..69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L68-L69), [73..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L73-L74), [78..79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L78-L79), [83..84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L83-L84), [88..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L88-L89), [93..94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L93-L94), [98..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L98-L99), [103..104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L103-L104), [108..109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L108-L109), [113..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L113-L114), [118..119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L118-L119), [123..124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L123-L124), [128..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L128-L129), [133..134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L133-L134), [138..139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L138-L139), [143..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L143-L144), [148..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L148-L149), [153..154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L153-L154), [158..159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L158-L159), [164..165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L164-L165), [177..178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L177-L178), [182..183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L182-L183), [189..190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L189-L190), [194..195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L194-L195), [203..204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L203-L204), [218..219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L218-L219), [224..225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L224-L225), [230..231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L230-L231), [240..241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L240-L241), [245..246](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L245-L246), [250..251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L250-L251), [255..256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L255-L256), [260..261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L260-L261)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [39..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39-L40), [48..51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L48-L51), [55..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L55-L61), [65..71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L65-L71), [75..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L75-L83), [105..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L105-L111), [131..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L131-L132), [144..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L144-L149), [179..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L179-L186), [198..207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L198-L207), [230..232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L230-L232), [260..265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L260-L265), [291..295](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L291-L295), [317..322](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L317-L322), [354..355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L354-L355)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [92..94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L92-L94), [109..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L109-L111), [126..128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L126-L128), [142..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L142-L144), [162..165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L162-L165), [170..173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L170-L173), [221..224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L221-L224), [236..238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L236-L238), [261..265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L261-L265), [267..271](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L267-L271)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [20..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20-L22)


---

	 - code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol


*GitHub* : [13..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L13-L15)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol


*GitHub* : [14..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L14-L16)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [37..41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L37-L41)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L13), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L19)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol


*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L21), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L28), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L35), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L42)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [96..98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L96-L98), [126..128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L126-L128), [149..151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L149-L151), [172..174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L172-L174), [189..191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L189-L191), [202..207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L202-L207), [228..230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L228-L230), [257..259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L257-L259), [278..280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L278-L280)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


*GitHub* : [36..40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L36-L40)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L41-L42)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [56..57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L56-L57)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [16..26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L16-L26), [46..48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L46-L48), [106..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L106-L114), [124..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L124-L132)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L26), [28..35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L28-L35), [37..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L37-L43), [45..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L45-L53), [55..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L55-L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L69), [71..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L71-L75), [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L77)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [60..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L60-L64), [66..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L66-L74), [76..85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L76-L85), [87..97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L87-L97), [99..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L99-L105), [107..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L107-L114), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L116), [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L118), [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L120), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L122), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L124), [126..135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L126-L135), [137..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L137-L142), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L144), [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L146)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [9..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L9-L15), [17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L17), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L19), [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L21), [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L23)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L7), [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L9)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [52..55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L52-L55), [57..58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L57-L58), [60..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L60-L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L71), [73..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L73-L81), [83..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L83-L89), [91..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L91-L99), [101..103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L101-L103), [105..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L105-L107), [109..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L109-L114), [118..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L118-L125), [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L127), [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L129), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L131), [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L133)


---

	 - code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol


*GitHub* : [26..27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L26-L27), [29..33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L29-L33)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L43), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L45), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L47), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L49), [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L51), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L53), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L67)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L45), [47..50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L47-L50), [52..53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L52-L53), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L71), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L73), [75..82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L75-L82), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L84), [86..90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L86-L90), [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L92), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L94), [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L96)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [16..19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L16-L19), [21..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L21-L22), [24..27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L24-L27), [29..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L29-L31), [33..35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L33-L35), [37..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L37-L39), [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L41-L42), [44..45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L44-L45), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L47), [49..52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L49-L52), [54..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L54-L56), [58..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L58-L60)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol


*GitHub* : [133..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L133-L142), [144..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L144-L149), [151..160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L151-L160), [162..168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L162-L168), [170..174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L170-L174), [176..177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L176-L177), [179..183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L179-L183), [185..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L185-L186)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [58..70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L58-L70), [100..102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L100-L102), [115..116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L115-L116)


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol


*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L7)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L10)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L48)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [41..43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L41-L43), [47..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L47-L56), [75..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L75-L87), [110..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L110-L111), [120..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L120-L125), [139..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L139-L144), [158..159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L158-L159), [163..166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L163-L166)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [41..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L41-L42), [47..52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L47-L52), [106..118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L106-L118), [143..147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L143-L147), [152..156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L152-L156), [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L161), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173), [179..180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L179-L180), [184..185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L184-L185)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [11..17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11-L17)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [11..18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L11-L18)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [26..32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L26-L32), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L34), [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L36), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L38), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L40)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L14), [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L16), [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L18), [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L20)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [36..52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L36-L52)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L16), [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L18)


---

	 - code/contracts/zksync/contracts/ForceDeployUpgrader.sol


*GitHub* : [13..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L13-L15)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [47..49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L47-L49), [51..55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L51-L55), [64..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L64-L67)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L29), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39), [78..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L78-L83), [97..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L97-L107), [123..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L123-L129)

### [N-76]<a name="n-76"></a> Simplify complex require statements

Simplifying complex `require` statements with local variables and `if`(or `revert`) statements can improve readability, make debugging easier, and promote modularity and reusability in the code.

*There are 33 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
77	        require(
78	            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
79	            "L1SharedBridge: not bridgehub or era chain"
80	        );
...
134	            require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
```

*GitHub* : [77..80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L77-L80), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L134)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
48	        require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");
...
271	                require(
272	                    msg.value == _request.mintValue + _request.secondBridgeValue,
273	                    "Bridgehub: msg.value mismatch 2"
274	                );
```

*GitHub* : [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L48), [271..274](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L271-L274)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
73	        require(
74	            msg.sender == owner() || msg.sender == securityCouncil,
75	            "Only the owner and security council are allowed to call this function"
76	        );
...
242	        require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");
```

*GitHub* : [73..76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L73-L76), [242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L242)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
72	        require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");
```

*GitHub* : [72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L72)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
197	                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
...
219	                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
```

*GitHub* : [197](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L197), [219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L219)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

```solidity
27	        require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
```

*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L27)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L39), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L42), [63..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L63-L67), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L124), [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L125), [325](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L325), [632](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L632), [633](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L633), [668..672](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L668-L672)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [274](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L274)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol


*GitHub* : [39..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L39-L42), [47..50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L47-L50)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [244..247](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L244-L247)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [29..32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L29-L32)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L28), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L29), [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L45)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L28)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L32)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [89..93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L89-L93)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L139)

### [N-77]<a name="n-77"></a> Events should be emitted before external calls

Ensure that events follow the best practice of check-effects-interaction, and are emitted before external calls

*There are 22 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
// @audit functions: `claimFailedDepositLegacyErc20Bridge` called before this event
201	        emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);
...
// @audit functions: `finalizeWithdrawalLegacyErc20Bridge` called before this event
227	        emit WithdrawalFinalized(l1Receiver, l1Token, amount);
```

*GitHub* : [201](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L201), [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L227)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
// @audit functions: `decode`, `baseToken`, `encode` called before this event
229	        emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);
...
// @audit functions: `proveL1ToL2TransactionStatus`, `encode`, `safeTransfer` called before this event
369	        emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);
...
// @audit functions: `isEthWithdrawalFinalized`, `safeTransfer` called before this event
456	        emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);
...
// @audit functions: `applyL1ToL2Alias`, `encode` called before this event
604	        emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
```

*GitHub* : [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L229), [369](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L369), [456](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L456), [604](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L604)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
// @audit functions: `createNewChain` called before this event
147	        emit NewChain(_chainId, _stateTransitionManager, _admin);
```

*GitHub* : [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L147)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
// @audit functions: `encodeCall`, `encodeCall`, `executeUpgrade` called before this event
229	        emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
...
// @audit functions: `decode`, `concat` called before this event
289	        emit StateTransitionNewChain(_chainId, stateTransitionAddress);
```

*GitHub* : [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L229), [289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L289)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
// @audit functions: `encode`, `upgradeCutHash`, `diamondCut` called before this event
117	        emit ExecuteUpgrade(_diamondCut);
```

*GitHub* : [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L117), [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L127), [141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L141), [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L151)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [436](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [345..351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L345-L351)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L106), [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L123)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L123)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L107), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L136)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L103), [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L128)

### [N-78]<a name="n-78"></a> Use `@inheritdoc` for overridden functions

It is recommended to use `@inheritdoc` for overridden functions.

*There are 25 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
183	    /// @notice Initiates a deposit transaction within Bridgehub, used by `requestL2TransactionTwoBridges`.
184	    function bridgehubDeposit(
185	        uint256 _chainId,
186	        address _prevMsgSender,
187	        uint256, // l2Value, needed for Weth deposits in the future
188	        bytes calldata _data
189	    ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
...
232	    /// @notice Confirms the acceptance of a transaction by the Mailbox, as part of the L2 transaction process within Bridgehub.
233	    /// This function is utilized by `requestL2TransactionTwoBridges` to validate the execution of a transaction.
234	    function bridgehubConfirmL2Transaction(
235	        uint256 _chainId,
236	        bytes32 _txDataHash,
237	        bytes32 _txHash
238	    ) external override onlyBridgehub {
...
270	    /// @dev Withdraw funds from the initiated deposit, that failed when finalizing on L2
271	    /// @param _depositSender The address of the deposit initiator
272	    /// @param _l1Token The address of the deposited L1 ERC20 token
273	    /// @param _amount The amount of the deposit that failed.
274	    /// @param _l2TxHash The L2 transaction hash of the failed deposit finalization
275	    /// @param _l2BatchNumber The L2 batch number where the deposit finalization was processed
276	    /// @param _l2MessageIndex The position in the L2 logs Merkle tree of the l2Log that was sent with the message
277	    /// @param _l2TxNumberInBatch The L2 transaction number in a batch, in which the log was sent
278	    /// @param _merkleProof The Merkle proof of the processing L1 -> L2 transaction with deposit finalization
279	    function claimFailedDeposit(
280	        uint256 _chainId,
281	        address _depositSender,
282	        address _l1Token,
283	        uint256 _amount,
284	        bytes32 _l2TxHash,
285	        uint256 _l2BatchNumber,
286	        uint256 _l2MessageIndex,
287	        uint16 _l2TxNumberInBatch,
288	        bytes32[] calldata _merkleProof
289	    ) external override {
...
380	    /// @notice Finalize the withdrawal and release funds
381	    /// @param _chainId The chain ID of the transaction to check
382	    /// @param _l2BatchNumber The L2 batch number where the withdrawal was processed
383	    /// @param _l2MessageIndex The position in the L2 logs Merkle tree of the l2Log that was sent with the message
384	    /// @param _l2TxNumberInBatch The L2 transaction number in the batch, in which the log was sent
385	    /// @param _message The L2 withdraw data, stored in an L2 -> L1 message
386	    /// @param _merkleProof The Merkle proof of the inclusion L2 -> L1 message about withdrawal initialization
387	    function finalizeWithdrawal(
388	        uint256 _chainId,
389	        uint256 _l2BatchNumber,
390	        uint256 _l2MessageIndex,
391	        uint16 _l2TxNumberInBatch,
392	        bytes calldata _message,
393	        bytes32[] calldata _merkleProof
394	    ) external override {
...
532	    /// @notice Initiates a deposit by locking funds on the contract and sending the request
533	    /// of processing an L2 transaction where tokens would be minted.
534	    /// @dev If the token is bridged for the first time, the L2 token contract will be deployed. Note however, that the
535	    /// newly-deployed token does not support any custom logic, i.e. rebase tokens' functionality is not supported.
536	    /// @param _l2Receiver The account address that should receive funds on L2
537	    /// @param _l1Token The L1 token address which is deposited
538	    /// @param _amount The total amount of tokens to be bridged
539	    /// @param _l2TxGasLimit The L2 gas limit to be used in the corresponding L2 transaction
540	    /// @param _l2TxGasPerPubdataByte The gasPerPubdataByteLimit to be used in the corresponding L2 transaction
541	    /// @param _refundRecipient The address on L2 that will receive the refund for the transaction.
542	    /// @dev If the L2 deposit finalization transaction fails, the `_refundRecipient` will receive the `_l2Value`.
543	    /// Please note, the contract may change the refund recipient's address to eliminate sending funds to addresses
544	    /// out of control.
545	    /// - If `_refundRecipient` is a contract on L1, the refund will be sent to the aliased `_refundRecipient`.
546	    /// - If `_refundRecipient` is set to `address(0)` and the sender has NO deployed bytecode on L1, the refund will
547	    /// be sent to the `msg.sender` address.
548	    /// - If `_refundRecipient` is set to `address(0)` and the sender has deployed bytecode on L1, the refund will be
549	    /// sent to the aliased `msg.sender` address.
550	    /// @dev The address aliasing of L1 contracts as refund recipient on L2 is necessary to guarantee that the funds
551	    /// are controllable through the Mailbox, since the Mailbox applies address aliasing to the from address for the
552	    /// L2 tx if the L1 msg.sender is a contract. Without address aliasing for L1 contracts as refund recipients they
553	    /// would not be able to make proper L2 tx requests through the Mailbox to use or withdraw the funds from L2, and
554	    /// the funds would be lost.
555	    /// @return l2TxHash The L2 transaction hash of deposit finalization.
556	    function depositLegacyErc20Bridge(
557	        address _prevMsgSender,
558	        address _l2Receiver,
559	        address _l1Token,
560	        uint256 _amount,
561	        uint256 _l2TxGasLimit,
562	        uint256 _l2TxGasPerPubdataByte,
563	        address _refundRecipient
564	    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
...
607	    /// @notice Finalizes the withdrawal for transactions initiated via the legacy ERC20 bridge.
608	    /// @param _l2BatchNumber The L2 batch number where the withdrawal was processed
609	    /// @param _l2MessageIndex The position in the L2 logs Merkle tree of the l2Log that was sent with the message
610	    /// @param _l2TxNumberInBatch The L2 transaction number in the batch, in which the log was sent
611	    /// @param _message The L2 withdraw data, stored in an L2 -> L1 message
612	    /// @param _merkleProof The Merkle proof of the inclusion L2 -> L1 message about withdrawal initialization
613	    ///
614	    /// @return l1Receiver The address on L1 that will receive the withdrawn funds
615	    /// @return l1Token The address of the L1 token being withdrawn
616	    /// @return amount The amount of the token being withdrawns
617	    function finalizeWithdrawalLegacyErc20Bridge(
618	        uint256 _l2BatchNumber,
619	        uint256 _l2MessageIndex,
620	        uint16 _l2TxNumberInBatch,
621	        bytes calldata _message,
622	        bytes32[] calldata _merkleProof
623	    ) external override onlyLegacyBridge returns (address l1Receiver, address l1Token, uint256 amount) {
...
634	    /// @notice Withdraw funds from the initiated deposit, that failed when finalizing on zkSync Era chain.
635	    /// This function is specifically designed for maintaining backward-compatibility with legacy `claimFailedDeposit`
636	    /// method in `L1ERC20Bridge`.
637	    ///
638	    /// @param _depositSender The address of the deposit initiator
639	    /// @param _l1Token The address of the deposited L1 ERC20 token
640	    /// @param _amount The amount of the deposit that failed.
641	    /// @param _l2TxHash The L2 transaction hash of the failed deposit finalization
642	    /// @param _l2BatchNumber The L2 batch number where the deposit finalization was processed
643	    /// @param _l2MessageIndex The position in the L2 logs Merkle tree of the l2Log that was sent with the message
644	    /// @param _l2TxNumberInBatch The L2 transaction number in a batch, in which the log was sent
645	    /// @param _merkleProof The Merkle proof of the processing L1 -> L2 transaction with deposit finalization
646	    function claimFailedDepositLegacyErc20Bridge(
647	        address _depositSender,
648	        address _l1Token,
649	        uint256 _amount,
650	        bytes32 _l2TxHash,
651	        uint256 _l2BatchNumber,
652	        uint256 _l2MessageIndex,
653	        uint16 _l2TxNumberInBatch,
654	        bytes32[] calldata _merkleProof
655	    ) external override onlyLegacyBridge {
```

*GitHub* : [183..189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L183-L189), [232..238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L232-L238), [270..289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L270-L289), [380..394](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L380-L394), [532..564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L532-L564), [607..623](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L607-L623), [634..655](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L634-L655)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
153	    /// @notice forwards function call to Mailbox based on ChainId
154	    function proveL2MessageInclusion(
155	        uint256 _chainId,
156	        uint256 _batchNumber,
157	        uint256 _index,
158	        L2Message calldata _message,
159	        bytes32[] calldata _proof
160	    ) external view override returns (bool) {
...
165	    /// @notice forwards function call to Mailbox based on ChainId
166	    function proveL2LogInclusion(
167	        uint256 _chainId,
168	        uint256 _batchNumber,
169	        uint256 _index,
170	        L2Log memory _log,
171	        bytes32[] calldata _proof
172	    ) external view override returns (bool) {
...
177	    /// @notice forwards function call to Mailbox based on ChainId
178	    function proveL1ToL2TransactionStatus(
179	        uint256 _chainId,
180	        bytes32 _l2TxHash,
181	        uint256 _l2BatchNumber,
182	        uint256 _l2MessageIndex,
183	        uint16 _l2TxNumberInBatch,
184	        bytes32[] calldata _merkleProof,
185	        TxStatus _status
186	    ) external view override returns (bool) {
```

*GitHub* : [153..160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L153-L160), [165..172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L165-L172), [177..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L177-L186), [215..221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L215-L221), [255..266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L255-L266)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L76)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [20..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20-L22), [45..49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L45-L49)


---

	 - code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol


*GitHub* : [13..15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L13-L15)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol


*GitHub* : [14..16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L14-L16)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [75..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L75-L87), [120..125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L120-L125), [150..151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150-L151)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [143..147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L143-L147), [152..156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L152-L156), [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L161), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173)

### [N-79]<a name="n-79"></a> Missing NatSpec from variable declarations

Some variables miss a NatSpec, which should be a [best practice](https://docs.soliditylang.org/en/latest/natspec-format.html) to add as a documentation.

Even if Natspec for internal and private variables is not parsed (but this may change in the future, according to the official docs), it still helps while reviewing the codebase.

*There are 7 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

```solidity
14	    ZkSyncStateTransitionStorage internal s;
```

*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L14)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

```solidity
40	    uint256 private constant _NOT_ENTERED = 1;
...
41	    uint256 private constant _ENTERED = 2;
```

*GitHub* : [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L40), [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L41)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

```solidity
24	    uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L24)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

```solidity
39	    address private l1LegacyBridge;
```

*GitHub* : [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L39)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
28	    ERC20Getters private availableGetters;
```

*GitHub* : [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L28)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol

```solidity
24	    uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L24)

### [N-80]<a name="n-80"></a> Contract name does not follow the Solidity Style Guide

According to the [Solidity Style Guide](https://docs.soliditylang.org/en/latest/style-guide.html#contract-and-library-names), contracts and libraries should be named using the CapWords style.

*There are 6 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
21	contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {
22	    using SafeERC20 for IERC20;
```

*GitHub* : [21..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L21-L22)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
32	contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {
33	    using SafeERC20 for IERC20;
```

*GitHub* : [32..33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L32-L33)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

```solidity
12	library L2ContractHelper {
13	    /// @dev The prefix used to create CREATE2 addresses.
14	    bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");
```

*GitHub* : [12..14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L12-L14)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

```solidity
25	contract L2SharedBridge is IL2SharedBridge, Initializable {
26	    /// @dev The address of the L1 bridge counterpart.
27	    address public override l1Bridge;
```

*GitHub* : [25..27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L25-L27)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
17	contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {
18	    /// @dev Describes whether there is a specific getter in the token.
19	    /// @notice Used to explicitly separate which getters the token has and which it does not.
20	    /// @notice Different tokens in L1 can implement or not implement getter function as `name`/`symbol`/`decimals`,
21	    /// @notice Our goal is to store all the getters that L1 token implements, and for others, we keep it as an unimplemented method.
22	    struct ERC20Getters {
```

*GitHub* : [17..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L17-L22)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol

```solidity
85	library L2ContractHelper {
86	    /// @dev The prefix used to create CREATE2 addresses.
87	    bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");
```

*GitHub* : [85..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L85-L87)

### [N-81]<a name="n-81"></a> Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES

For `immutable` variable names, each word should use all capital letters, with underscores separating each word (UPPER_CASE_WITH_UNDERSCORES)

*There are 5 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
25	    IL1SharedBridge public immutable override sharedBridge;
```

*GitHub* : [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L25)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
36	    address public immutable override l1WethAddress;
...
39	    IBridgehub public immutable override bridgehub;
...
42	    IL1ERC20Bridge public immutable override legacyBridge;
```

*GitHub* : [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L36), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L39), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L42)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
29	    address public immutable bridgehub;
```

*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L29)

### [N-82]<a name="n-82"></a> Use a single file for system wide constants

Consider grouping all the system constants under a single file.

*There are 73 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
24	    uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1);
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L24)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
28	    string public constant override getName = "ValidatorTimelock";
```

*GitHub* : [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L28)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
22	    string public constant override getName = "AdminFacet";
```

*GitHub* : [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L22)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
29	    string public constant override getName = "ExecutorFacet";
```

*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

```solidity
27	    string public constant override getName = "GettersFacet";
```

*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L27)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
37	    string public constant override getName = "MailboxFacet";
```

*GitHub* : [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L37)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

```solidity
14	    bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");
```

*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L14)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
19	    bytes32 internal constant DIAMOND_INIT_SUCCESS_RETURN_VALUE =
20	        0x33774e659306e47509050e97cb651e731180a42d458212294d30751925c551a2; // keccak256("diamond.zksync.init") - 1
...
23	    bytes32 private constant DIAMOND_STORAGE_POSITION =
24	        0xc8fcad8db84d3cc18b4c41d551ea0ee66dd599cde068d998e57d5e09332c131b; // keccak256("diamond.standard.diamond.storage") - 1;
```

*GitHub* : [19..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L19-L20), [23..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L23-L24)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

```solidity
42	uint256 constant L2_LOG_ADDRESS_OFFSET = 4;
```

*GitHub* : [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L42), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L45), [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L48), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L52), [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L56), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L59), [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L62), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L65), [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L70)


---

	 - code/contracts/ethereum/contracts/common/Config.sol


*GitHub* : [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L8), [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L13), [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L16), [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L21), [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L24), [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L27), [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L30), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L35), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L39), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L42), [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L46), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L49), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L52), [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L56), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L59), [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L62), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L65), [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L68), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L71), [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L74), [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L77), [80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L80), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L84), [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L87), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L94), [101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L101), [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L103), [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L106), [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L109), [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L112), [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L114), [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L117)


---

	 - code/contracts/ethereum/contracts/common/L2ContractAddresses.sol


*GitHub* : [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L8), [11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L11), [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L14), [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L23), [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L26), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L29), [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L32), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L35)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L31), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L40), [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L41)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L24)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L14)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L24)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L70), [72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L72), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L73), [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L74), [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L76), [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L78), [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L87)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L9), [12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L12)

### [N-83]<a name="n-83"></a> Contracts should have full test coverage

A 100% test coverage is not foolproof, but it helps immensely in reducing the amount of bugs that may occur.

*There are 1 instance(s) of this issue:*

*GitHub* : [project\2024-03-zksync](https://github.com/code-423n4/2024-03-zksync/blob/main/#L0)

### [N-84]<a name="n-84"></a> Large or complicated code bases should implement invariant tests

This includes: large code bases, or code with lots of inline-assembly, complicated math, or complicated interactions between multiple contracts.

Invariant fuzzers such as Echidna require the test writer to come up with invariants which should not be violated under any circumstances, and the fuzzer tests various inputs and function calls to ensure that the invariants always hold.

Even code with 100% code coverage can still have bugs due to the order of the operations a user performs, and invariant fuzzers may help significantly.

*There are 1 instance(s) of this issue:*

*GitHub* : [project\2024-03-zksync](https://github.com/code-423n4/2024-03-zksync/blob/main/#L0)

### [N-85]<a name="n-85"></a> Codebase should implement formal verification testing

Formal verification is the act of proving or disproving the correctness of intended algorithms underlying a system with respect to a certain formal specification/property/invariant, using formal methods of mathematics.

Some tools that are currently available to perform these tests on smart contracts are [SMTChecker](https://docs.soliditylang.org/en/latest/smtchecker.html) and [Certora Prover](https://www.certora.com/).

*There are 1 instance(s) of this issue:*

*GitHub* : [project\2024-03-zksync](https://github.com/code-423n4/2024-03-zksync/blob/main/#L0)

### [N-86]<a name="n-86"></a> Use SafeCast to safely downcast variables

Downcasting int/uints in Solidity can be unsafe due to the potential for data loss and unintended behavior. When downcasting a larger integer type to a smaller one (e.g., `uint256` to `uint128`), the value may exceed the range of the target type, leading to truncation and loss of significant digits. This data loss can result in unexpected state changes, incorrect calculations, or other contract vulnerabilities, ultimately compromising the contracts functionality and reliability. To prevent these risks, developers should carefully consider the range of values their variables may hold and ensure that proper checks are in place to prevent out-of-range values before performing downcasting. Also consider using OZ SafeCast functionality.

*There are 45 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
79	        bytes32 salt = bytes32(uint256(uint160(_l1Token)));
```

*GitHub* : [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L79)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
260	            bytes memory decimals = abi.encode(uint8(18));
```

*GitHub* : [260](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L260)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
186	            from: uint256(uint160(L2_FORCE_DEPLOYER_ADDR)),
...
187	            to: uint256(uint160(L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR)),
...
266	            bytes32(uint256(uint160(bridgehub))),
...
267	            bytes32(uint256(uint160(address(this)))),
...
269	            bytes32(uint256(uint160(_admin))),
...
270	            bytes32(uint256(uint160(validatorTimelock))),
...
271	            bytes32(uint256(uint160(_baseToken))),
...
272	            bytes32(uint256(uint160(_sharedBridge))),
```

*GitHub* : [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L186), [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L187), [266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L266), [267](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L267), [269](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L269), [270](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L270), [271](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L271), [272](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L272)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L117), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L136)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L41), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L42), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L42), [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L54), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L61), [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L151), [152](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L152), [520](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L520), [644](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L644)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L139), [285](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L285), [298](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L298), [299](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L299), [308](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L308), [340](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L340)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L42), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L52), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L52), [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L68), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L73)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


*GitHub* : [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L32), [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L56)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L24), [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L32), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L42)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L160), [168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L168)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L24), [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L32), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L42)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L109), [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L114)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L32)

### [N-87]<a name="n-87"></a> Consider adding a block/deny-list

Doing so will significantly increase centralization, but will help to prevent hackers from using stolen tokens

*There are 3 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
21	contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {
22	    using SafeERC20 for IERC20;
```

*GitHub* : [21..22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L21-L22)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
32	contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {
33	    using SafeERC20 for IERC20;
```

*GitHub* : [32..33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L32-L33)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
22	contract Governance is IGovernance, Ownable2Step {
23	    /// @notice A constant representing the timestamp for completed operations.
24	    uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1);
```

*GitHub* : [22..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L22-L24)

### [N-88]<a name="n-88"></a> Events should use parameters to convey information

For example, rather than using `event Paused()` and `event Unpaused()`, use `event PauseState(address indexed whoChangedIt, bool wasPaused, bool isNowPaused)`

*There are 2 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol

```solidity
96	    event Freeze();
...
99	    event Unfreeze();
```

*GitHub* : [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L96), [99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L99)

### [N-89]<a name="n-89"></a> Expressions for constant values should use `immutable` rather than `constant`

While it does not save gas for some simple binary expressions because the compiler knows that developers often make this mistake, it's still best to use the right tool for the task at hand. There is a difference between `constant` variables and `immutable` variables, and they should each be used in their appropriate contexts. `constants` should be used for literal values written into the code, and `immutable` variables should be used for expressions, or values calculated in, or passed into the constructor.

*There are 27 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
24	    uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1);
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L24)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

```solidity
14	    bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");
```

*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L14)


---

	 - code/contracts/ethereum/contracts/common/Config.sol

```solidity
16	uint256 constant MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES = 4 + L2_TO_L1_LOG_SERIALIZE_SIZE * 512;
...
24	bytes32 constant DEFAULT_L2_LOGS_TREE_ROOT_HASH = bytes32(0);
...
87	address constant POINT_EVALUATION_PRECOMPILE_ADDR = address(0x0A);
...
103	address constant ETH_TOKEN_ADDRESS = address(1);
...
109	address constant ERA_ERC20_BRIDGE_ADDRESS = address(1233);
...
114	bytes32 constant TWO_BRIDGES_MAGIC_VALUE = bytes32(uint256(keccak256("TWO_BRIDGES_MAGIC_VALUE")) - 1);
...
117	address constant BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS = address(uint160(type(uint16).max));
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L16), [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L24), [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L87), [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L103), [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L109), [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L114), [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L117)


---

	 - code/contracts/ethereum/contracts/common/L2ContractAddresses.sol

```solidity
8	address constant L2_BOOTLOADER_ADDRESS = address(0x8001);
```

*GitHub* : [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L8), [11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L11), [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L14), [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L23), [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L26), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L29), [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L32), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L35)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L24)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L14)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L24)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L72), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L73), [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L74), [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L76), [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L78), [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L87)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L9)