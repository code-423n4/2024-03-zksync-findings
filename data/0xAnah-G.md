# ZKSYNC GAS OPTIMIZATIONS


## INTRODUCTION
Highlighted below are optimizations exclusively targeting state-mutating functions and view/pure functions invoked by state-mutating functions. In the discussion that follows, only runtime gas is emphasized, given its inevitable dominance over deployment gas costs throughout the protocol's lifetime. 

Please be aware that some code snippets may be shortened to conserve space, and certain code snippets may include @audit tags in comments to facilitate issue explanations."




## [G-01] Unnecessary copy of storage struct to memory

Having to copy a complete storage struct into memory only to end up using one of its attributes is unnecessary and gas inneficient. The functions should be refactored such that only the required attribute is read from storage and cached into stack variable.

### Instances

1. #### Refactor `_addAggregator()` function to avoid coping the storage struct `ds.selectorToFacet[selector]` into memory struct variable `oldFacet`.
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L140

Having to copy the storage struct `ds.selectorToFacet[selector]` into memory struct variable `oldFacet` just to read one attribute `facetAddress` is unnecessary as it involves having to copy the struct from storage to memory rather we can just read the attribute directly from the storage variable and cache the value into a stack variable. The fact that this is done inside a loop even makes the function more gas consuming. The function should be refactored as shown in the diff below:

```solidity
file: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

126:    function _addFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {
127:        DiamondStorage storage ds = getDiamondStorage();
128:
129:        // Facet with no code cannot be added.
130:        // This check also verifies that the facet does not have zero address, since it is the
131:        // address with which 0x00000000 selector is associated.
132:        require(_facet.code.length > 0, "G");
133:
134:        // Add facet to the list of facets if the facet address is new one
135:        _saveFacetIfNew(_facet);
136:
137:        uint256 selectorsLength = _selectors.length;
138:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
139:            bytes4 selector = _selectors[i];
140:            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
141:            require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists
142:
143:            _addOneFunction(_facet, selector, _isFacetFreezable);
144:        }
145:    }
```

```diff
diff --git a/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol b/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
index 329f7f7..d9432ef 100644
--- a/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
+++ b/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
@@ -137,8 +137,8 @@ library Diamond {
         uint256 selectorsLength = _selectors.length;
         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
             bytes4 selector = _selectors[i];
-            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
-            require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists
+            address _facetAddress = ds.selectorToFacet[selector].facetAddress;
+            require(_facetAddress == address(0), "J"); // facet for this selector already exists

             _addOneFunction(_facet, selector, _isFacetFreezable);
         }
```


2. #### Refactor `_replaceFunctions()` function to avoid coping the storage struct `ds.selectorToFacet[selector]` into memory struct variable `oldFacet`.
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L160

Having to copy the storage struct `ds.selectorToFacet[selector]` into memory struct variable `oldFacet` just to read one attribute `facetAddress` is unnecessary as it involves having to copy the struct from storage to memory rather we can just read the attribute directly from the storage variable and cache the value into a stack variable. The fact that this is done inside a loop even makes the function more gas consuming. The function should be refactored as shown in the diff below:

```solidity
file: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

149:    function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {
150:        DiamondStorage storage ds = getDiamondStorage();
151:
152:        // Facet with no code cannot be added.
153:        // This check also verifies that the facet does not have zero address, since it is the
154:        // address with which 0x00000000 selector is associated.
155:        require(_facet.code.length > 0, "K");
156:
157:        uint256 selectorsLength = _selectors.length;
158:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
159:            bytes4 selector = _selectors[i];
160:            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
161:            require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address
162:
163:            _removeOneFunction(oldFacet.facetAddress, selector);
164:            // Add facet to the list of facets if the facet address is a new one
165:            _saveFacetIfNew(_facet);
166:            _addOneFunction(_facet, selector, _isFacetFreezable);
167:        }
168:    }
```

```diff
diff --git a/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol b/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
index 329f7f7..5055873 100644
--- a/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
+++ b/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
@@ -157,10 +157,10 @@ library Diamond {
         uint256 selectorsLength = _selectors.length;
         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
             bytes4 selector = _selectors[i];
-            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
-            require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address
+            address _facetAddress = ds.selectorToFacet[selector].facetAddress;
+            require(_facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

-            _removeOneFunction(oldFacet.facetAddress, selector);
+            _removeOneFunction(_facetAddress, selector);
             // Add facet to the list of facets if the facet address is a new one
             _saveFacetIfNew(_facet);
             _addOneFunction(_facet, selector, _isFacetFreezable);
```


3. #### Refactor `_replaceFunctions()` function to avoid coping the storage struct `ds.selectorToFacet[selector]` into memory struct variable `oldFacet`.
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L180

Having to copy the storage struct `ds.selectorToFacet[selector]` into memory struct variable `oldFacet` just to read one attribute `facetAddress` is unnecessary as it involves having to copy the struct from storage to memory rather we can just read the attribute directly from the storage variable and cache the value into a stack variable. The fact that this is done inside a loop even makes the function more gas consuming. The function should be refactored as shown in the diff below:

```solidity
file: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

172:    function _removeFunctions(address _facet, bytes4[] memory _selectors) private {
173:        DiamondStorage storage ds = getDiamondStorage();
174:
175:        require(_facet == address(0), "a1"); // facet address must be zero
176:
177:        uint256 selectorsLength = _selectors.length;
178:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
179:            bytes4 selector = _selectors[i];
180:            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
181:            require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet
182:
183:            _removeOneFunction(oldFacet.facetAddress, selector);
184:        }
185:    }
```

```diff
diff --git a/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol b/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
index 329f7f7..680e9a5 100644
--- a/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
+++ b/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
@@ -177,10 +177,10 @@ library Diamond {
         uint256 selectorsLength = _selectors.length;
         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
             bytes4 selector = _selectors[i];
-            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
-            require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet
+            address _facetAddress = ds.selectorToFacet[selector].facetAddress;
+            require(_facetAddress != address(0), "a2"); // Can't delete a non-existent facet

-            _removeOneFunction(oldFacet.facetAddress, selector);
+            _removeOneFunction(_facetAddress, selector);
         }
     }
```

## [G-02] Cache state variables outside of loop to avoid reading/writing storage on every iteration
Reading from storage should always try to be avoided within loops. In the following instances, we are able to cache state variables outside of the loop to save a Gwarmaccess (100 gas) per loop iteration.

### Instances
1. #### The loop in `ValidatorTimelock.commitBatches()` could be refactored to make the function cheaper
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L117

The loop in `ValidatorTimelock.commitBatches()` reads the `committedBatchTimestamp[ERA_CHAIN_ID]` mapping variable for every of its iteration which is highly gas inefficient rather the mapping variable should be cached in a local storage `LibMap.Uint32Map` variable then the variable be used in the loop. In implementing this saves the EVM from having to re-calculate the mapping key for every iteration of the loop thereby saving an estimated `40` gas units for each of the loop iteration. The diff below shows how the code should be refactored:

```solidity
file: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

108:    function commitBatches(
109:        StoredBatchInfo calldata,
110:        CommitBatchInfo[] calldata _newBatchesData
111:    ) external onlyValidator(ERA_CHAIN_ID) {
112:        unchecked {
113:            // This contract is only a temporary solution, that hopefully will be disabled until 2106 year, so...
114:            // It is safe to cast.
115:            uint32 timestamp = uint32(block.timestamp);
116:            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
117:                committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);   //@audit read committedBatchTimestamp[ERA_CHAIN_ID] outside of loop
118:            }
119:        }
120:
121:        _propagateToZkSyncStateTransition(ERA_CHAIN_ID);
122:    }
```

```diff
diff --git a/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol b/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
index 944e7cb..763d22c 100644
--- a/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
+++ b/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
@@ -113,8 +113,9 @@ contract ValidatorTimelock is IExecutor, Ownable2Step {
             // This contract is only a temporary solution, that hopefully will be disabled until 2106 year, so...
             // It is safe to cast.
             uint32 timestamp = uint32(block.timestamp);
+            LibMap.Uint32Map storage _map = committedBatchTimestamp[ERA_CHAIN_ID];
             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
-                committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);
+                _map.set(_newBatchesData[i].batchNumber, timestamp);
             }
         }
```
```
Estimated gas saved: 40 gas units per loop iteration
```


2. #### The loop in `ValidatorTimelock.commitBatchesSharedBridge()` could be refactored to make the function cheaper
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L136

The loop in `ValidatorTimelock.commitBatchesSharedBridge()` reads the `committedBatchTimestamp[_chainId]` mapping variable for every of its iteration which is highly gas inefficient rather the mapping variable should be cached in a local storage `LibMap.Uint32Map` variable then the variable be used in the loop. In implementing this saves the EVM from having to re-calculate the mapping key for every iteration of the loop thereby saving an estimated `40` gas units for each of the loop iteration. The diff below shows how the code should be refactored:

```solidity
file: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

126:    function commitBatchesSharedBridge(
127:        uint256 _chainId,
128:        StoredBatchInfo calldata,
129:        CommitBatchInfo[] calldata _newBatchesData
130:    ) external onlyValidator(_chainId) {
131:        unchecked {
132:            // This contract is only a temporary solution, that hopefully will be disabled until 2106 year, so...
133:            // It is safe to cast.
134:            uint32 timestamp = uint32(block.timestamp);
135:            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
136:                committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);
137:            }
138:        }
139:
140:        _propagateToZkSyncStateTransition(_chainId);
141:    }
```

```diff
diff --git a/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol b/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
index 944e7cb..79dbc9c 100644
--- a/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
+++ b/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
@@ -132,8 +132,9 @@ contract ValidatorTimelock is IExecutor, Ownable2Step {
             // This contract is only a temporary solution, that hopefully will be disabled until 2106 year, so...
             // It is safe to cast.
             uint32 timestamp = uint32(block.timestamp);
+            LibMap.Uint32Map storage _map = committedBatchTimestamp[_chainId];
             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
-                committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);
+                _map.set(_newBatchesData[i].batchNumber, timestamp);
             }
         }
```
```
Estimated gas saved: 40 gas units per loop iteration
```


3. #### The loop in `ValidatorTimelock.executeBatches()` could be refactored to make the function cheaper
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L186

The loop in `ValidatorTimelock.executeBatches()` reads the `committedBatchTimestamp[ERA_CHAIN_ID]` mapping variable for every of its iteration which is highly gas inefficient rather the mapping variable should be cached in a local storage `LibMap.Uint32Map` variable then the variable be used in the loop. In implementing this saves the EVM from having to re-calculate the mapping key for every iteration of the loop thereby saving an estimated `40` gas units for each of the loop iteration. The diff below shows how the code should be refactored:

```solidity
file: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

182:    function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {
183:        uint256 delay = executionDelay; // uint32
184:        unchecked {
185:            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
186:                uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
187:                    _newBatchesData[i].batchNumber
188:                );
189:
190:                // Note: if the `commitBatchTimestamp` is zero, that means either:
191:                // * The batch was committed, but not through this contract.
192:                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
193:                // We allow executing such batches.
194:
195:                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
196:            }
197:        }
198:        _propagateToZkSyncStateTransition(ERA_CHAIN_ID);
199:    }
```

```diff
diff --git a/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol b/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
index 944e7cb..7998c4f 100644
--- a/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
+++ b/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
@@ -182,8 +182,9 @@ contract ValidatorTimelock is IExecutor, Ownable2Step {
     function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {
         uint256 delay = executionDelay; // uint32
         unchecked {
+            LibMap.Uint32Map storage _map = committedBatchTimestamp[ERA_CHAIN_ID];
             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
-                uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
+                uint256 commitBatchTimestamp = _map.get(
                     _newBatchesData[i].batchNumber
                 );
```
```
Estimated gas saved: 40 gas units per loop iteration
```


4. #### The loop in `ValidatorTimelock.executeBatchesSharedBridge()` could be refactored to make the function cheaper
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L210

The loop in `ValidatorTimelock.executeBatches()` reads the `committedBatchTimestamp[_chainId]` mapping variable for every of its iteration which is highly gas inefficient rather the mapping variable should be cached in a local storage `LibMap.Uint32Map` variable then the variable be used in the loop. In implementing this saves the EVM from having to re-calculate the mapping key for every iteration of the loop thereby saving an estimated `40` gas units for each of the loop iteration. The diff below shows how the code should be refactored:

```solidity
file: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

203:    function executeBatchesSharedBridge(
204:        uint256 _chainId,
205:        StoredBatchInfo[] calldata _newBatchesData
206:    ) external onlyValidator(_chainId) {
207:        uint256 delay = executionDelay; // uint32
208:        unchecked {
209:            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
210:                uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
211:
212:                // Note: if the `commitBatchTimestamp` is zero, that means either:
213:                // * The batch was committed, but not through this contract.
214:                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
215:                // We allow executing such batches.
216:
217:                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
218:            }
219:        }
220:        _propagateToZkSyncStateTransition(_chainId);
221:    }
```

```diff
diff --git a/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol b/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
index 944e7cb..1fa65be 100644
--- a/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
+++ b/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
@@ -205,9 +205,10 @@ contract ValidatorTimelock is IExecutor, Ownable2Step {
         StoredBatchInfo[] calldata _newBatchesData
     ) external onlyValidator(_chainId) {
         uint256 delay = executionDelay; // uint32
+        LibMap.Uint32Map storage _map = committedBatchTimestamp[_chainId];
         unchecked {
             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
-                uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
+                uint256 commitBatchTimestamp = _map.get(_newBatchesData[i].batchNumber);

                 // Note: if the `commitBatchTimestamp` is zero, that means either:
                 // * The batch was committed, but not through this contract.
```
```
Estimated gas saved: 40 gas units per loop iteration
```


## [G-03] Avoid using state variable in emit
In scenarios where you have a memory, calldata variable or parameter with the same value as the state variable you should use the memory, calldata variable or parameter in the emit statement rather than state variable.

### Instances
1. #### Use `address(0)` in place of `pendingAdmin` in the `NewAdmin()` event
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69

Rather than having to read the `pendingAdmin` state variable in the `emit NewAdmin(previousAdmin, pendingAdmin)` statement we could use `address(0)` since on [line 66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L66) the previous value `pendingAdmin` was deleted (so its current value at that point would be the default address value which is zero address). In refactoring the function this way we would avoid having to read from state 
thereby saving 1 `SLOAD` Gwarmaccess `100` gas units. The diff below shows how the code should be refactored:

```solidity
file: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

60:    function acceptAdmin() external {
61:        address currentPendingAdmin = pendingAdmin;
62:        require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights
63:
64:        address previousAdmin = admin;
65:        admin = currentPendingAdmin;
66:        delete pendingAdmin;
67:
68:        emit NewPendingAdmin(currentPendingAdmin, address(0));
69:        emit NewAdmin(previousAdmin, pendingAdmin);  //@audit use address(0) inplace of pendingAdmin
90:    }
```

```diff
diff --git a/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol b/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol
index 201b42f..0927914 100644
--- a/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol
+++ b/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol
@@ -66,7 +66,7 @@ contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
         delete pendingAdmin;

         emit NewPendingAdmin(currentPendingAdmin, address(0));
-        emit NewAdmin(previousAdmin, pendingAdmin);
+        emit NewAdmin(previousAdmin, address(0));
     }

     ///// Getters
```

```
Estimated gas saved: 100 gas units
```

2. #### Use `address(0)` in place of `pendingAdmin` in the `NewAdmin()` event
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L128

Rather than having to read the `pendingAdmin` state variable in the `emit NewAdmin(previousAdmin, pendingAdmin)` statement we could use `address(0)` since on [line 125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L125) the previous value `pendingAdmin` was deleted (so its current value at that point would be the default address value which is zero address). In refactoring the function this way we would avoid having to read from state thereby saving 1 `SLOAD` Gwarmaccess `100` gas units. The diff below shows how the code should be refactored:

```solidity
file: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

119:    function acceptAdmin() external {
120:        address currentPendingAdmin = pendingAdmin;
121:        require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights
122:
123:        address previousAdmin = admin;
124:        admin = currentPendingAdmin;
125:        delete pendingAdmin;
126:
127:        emit NewPendingAdmin(currentPendingAdmin, address(0));
128:        emit NewAdmin(previousAdmin, pendingAdmin);  //@audit use address(0) inplace of pendingAdmin
129:    }
```

```diff
diff --git a/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol b/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
index 0c27439..64dd6b8 100644
--- a/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
+++ b/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
@@ -125,7 +125,7 @@ contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Own
         delete pendingAdmin;

         emit NewPendingAdmin(currentPendingAdmin, address(0));
-        emit NewAdmin(previousAdmin, pendingAdmin);
+        emit NewAdmin(previousAdmin, address(0));
     }
```
```
Estimated gas saved: 100 gas units
```




## [G-04]  Move lesser gas costing require checks to the top
Require() or revert() statements that check input arguments or cost lesser gas should be at the top of the function.
Checks that involve constants should come before checks that involve state variables, function calls, and calculations. By doing these checks first, the function is able to revert before wasting alot of gas in a function that may ultimately revert in the unhappy case.

### Instances
1. #### Move the `require(_amount > 0, "y1")` check to the top of the function.
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L303-#L368

In the `_claimFailedDeposit()` function as shown below the require statement `require(_amount > 0, "y1")` is less gas costing compared to `require(proofValid, "yn")` require statement as the latter requires an external call to determine the value of `proofValid` while the former is an argument to the function  therefore we should move `require(_amount > 0, "y1")` to the top of the function so that in scenarios where the `require(_amount > 0, "y1")` statement fails the EVM would not have to perform the gas consuming operations of `require(proofValid, "yn")`. The diff below shows how the code should be refactored:

```solidity
file: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

303:   function _claimFailedDeposit(
304:        bool _checkedInLegacyBridge,
305:        uint256 _chainId,
306:        address _depositSender,
307:        address _l1Token,
308:        uint256 _amount,
309:        bytes32 _l2TxHash,
310:        uint256 _l2BatchNumber,
311:        uint256 _l2MessageIndex,
312:        uint16 _l2TxNumberInBatch,
313:        bytes32[] calldata _merkleProof
314:    ) internal nonReentrant {
315:        {
316:            bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
317:                _chainId,
318:                _l2TxHash,
319:                _l2BatchNumber,
320:                _l2MessageIndex,
321:                _l2TxNumberInBatch,
322:                _merkleProof,
323:                TxStatus.Failure
324:            );
325:            require(proofValid, "yn");
326:        }
327:        require(_amount > 0, "y1");     //@audit move check to function top
.
.
.
368:    }
```

```diff
diff --git a/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol b/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
index 791e1dc..8e2b875 100644
--- a/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
+++ b/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
@@ -312,6 +312,7 @@ contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Owna
         uint16 _l2TxNumberInBatch,
         bytes32[] calldata _merkleProof
     ) internal nonReentrant {
+        require(_amount > 0, "y1");
         {
             bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
                 _chainId,
@@ -324,7 +325,7 @@ contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Owna
             );
             require(proofValid, "yn");
         }
-        require(_amount > 0, "y1");
```
```
Estimated gas saved: 100 gas units
```

2. #### Move the `require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2")` check to the top of the function.
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L554-#L603

In the `depositLegacyErc20Bridge()` function as shown below the require statement `require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2")` is less gas costing compared to `require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep")` require statement as the latter reads a mapping while the former is an argument to the function  therefore we should move `require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2")` to the top of the function so that in scenarios where the `require(_amount > 0, "y1")` statement fails the EVM would not have to perform the gas consuming operations of `require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep")`. The diff below shows how the code should be refactored:

```solidity
file: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

554:    function depositLegacyErc20Bridge(
555:        address _prevMsgSender,
556:        address _l2Receiver,
557:        address _l1Token,
558:        uint256 _amount,
559:        uint256 _l2TxGasLimit,
560:        uint256 _l2TxGasPerPubdataByte,
561:        address _refundRecipient
562:    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
563:        require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
564:        require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");    //@audit move to function top
.
.
.
603:    }
```

```diff
diff --git a/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol b/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
index 791e1dc..239bf00 100644
--- a/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
+++ b/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
@@ -560,8 +560,9 @@ contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Owna
         uint256 _l2TxGasPerPubdataByte,
         address _refundRecipient
     ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
-        require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
+        require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
+

         // Note that funds have been transferred to this contract in the legacy ERC20 bridge.
         if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {
```
```
Estimated gas saved: 2140 gas units
```

3. #### Move the `require(msg.data.length >= 4 || msg.data.length == 0, "Ut")` check to the top of the function.
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25

In the `fallback()` function as shown below the checks for `msg.data.length` should be done before reading diamond storage from state this is because in scenarios where the `msg.data.length` checks fails the function can revert without having to perform a state read which is an expensive operation. The diff below shows how the code should be refactored:

```solidity
file: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

20:    fallback() external payable {
21:        Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
22:        // Check whether the data contains a "full" selector or it is empty.
23:        // Required because Diamond proxy finds a facet by function signature,
24:        // which is not defined for data length in range [1, 3].
25:        require(msg.data.length >= 4 || msg.data.length == 0, "Ut"); //@audit move check to function top
26:        // Get facet from function selector
27:        Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];
28:        address facetAddress = facet.facetAddress;
.
.
.
55:    }
```

```diff
diff --git a/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol b/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol
index 8d16c56..a5bcc9b 100644
--- a/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol
+++ b/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol
@@ -18,11 +18,13 @@ contract DiamondProxy {
     /// @dev 1. Find the facet for the function that is called.
     /// @dev 2. Delegate the execution to the found facet via `delegatecall`.
     fallback() external payable {
-        Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
         // Check whether the data contains a "full" selector or it is empty.
         // Required because Diamond proxy finds a facet by function signature,
         // which is not defined for data length in range [1, 3].
         require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
+
+        Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
+
         // Get facet from function selector
         Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];
         address facetAddress = facet.facetAddress;
```
```
Estimated gas saved: 2100 gas units
```

4. #### Move the `require(_newBatchesData.length == 1, "e4")` check to the top of the function.
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L215-#L248

In the `_commitBatches()` function as shown below the require statement `require(_newBatchesData.length == 1, "e4")` is less gas costing compared to `require(IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,"Executor facet: wrong protocol version")` require statement as the performs an external call while the former is an argument to the function  therefore we should move `require(_newBatchesData.length == 1, "e4")` to the top of the function so that in scenarios where the `require(_newBatchesData.length == 1, "e4")` statement fails the EVM would not have to perform the gas consuming operations of `require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep")`. The diff below shows how the code should be refactored:

```solidity
file: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

215:    function _commitBatches(
216:        StoredBatchInfo memory _lastCommittedBatchData,
217:        CommitBatchInfo[] calldata _newBatchesData
218:    ) internal {
219:        // check that we have the right protocol version
220:        // three comments:
221:        // 1. A chain has to keep their protocol version up to date, as processing a block requires the latest or previous protocol version
222:        // to solve this we will need to add the feature to create batches with only the protocol upgrade tx, without any other txs.
223:        // 2. A chain might become out of sync if it launches while we are in the middle of a protocol upgrade. This would mean they cannot process their genesis upgrade
224:        // as thier protocolversion would be outdated, and they also cannot process the protocol upgrade tx as they have a pending upgrade.
225:        // 3. The protocol upgrade is increased in the BaseZkSyncUpgrade, in the executor only the systemContractsUpgradeTxHash is checked
226:        require(
227:            IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
228:            "Executor facet: wrong protocol version"
229:        );
230:        // With the new changes for EIP-4844, namely the restriction on number of blobs per block, we only allow for a single batch to be committed at a time.
231:        require(_newBatchesData.length == 1, "e4");
232:        // Check that we commit batches after last committed batch
233:        require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data
.
.
.
248:    }
```

```diff
diff --git a/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol b/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
index 36df6dd..9607b44 100644
--- a/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
+++ b/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
@@ -216,6 +216,9 @@ contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {
         StoredBatchInfo memory _lastCommittedBatchData,
         CommitBatchInfo[] calldata _newBatchesData
     ) internal {
+        // With the new changes for EIP-4844, namely the restriction on number of blobs per block, we only allow for a single batch to be committed at a time.
+
+        require(_newBatchesData.length == 1, "e4");
         // check that we have the right protocol version
         // three comments:
         // 1. A chain has to keep their protocol version up to date, as processing a block requires the latest or previous protocol version
@@ -227,8 +230,7 @@ contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {
             IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
             "Executor facet: wrong protocol version"
         );
-        // With the new changes for EIP-4844, namely the restriction on number of blobs per block, we only allow for a single batch to be committed at a time.
-        require(_newBatchesData.length == 1, "e4");
+
         // Check that we commit batches after last committed batch
         require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data
```

```
Estimated gas saved: 100 gas units
```


5. #### Move the `require(msg.value == 0, "Value should be 0 for ERC20 bridge")` check to the top of the function.
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L79-#L106

In the `finalizeDeposit()` function as shown below the require statement `require(msg.value == 0, "Value should be 0 for ERC20 bridge")` is less gas costing compared to `require(AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge || AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,"mq");` require statement as the performs an external call while the former is an argument to the function  therefore we should move `require(msg.value == 0, "Value should be 0 for ERC20 bridge")` to the top of the function so that in scenarios where the `require(msg.value == 0, "Value should be 0 for ERC20 bridge")` statement fails the EVM would not have to perform the gas consuming operations of `require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep")`. The diff below shows how the code should be refactored:

```solidity
file: contracts/zksync/contracts/bridge/L2SharedBridge.sol

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
.
.
.
106:    }
```

```diff
diff --git a/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol b/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol
index 0360a0c..f45949b 100644
--- a/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol
+++ b/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol
@@ -83,14 +83,14 @@ contract L2SharedBridge is IL2SharedBridge, Initializable {
         uint256 _amount,
         bytes calldata _data
     ) external payable override {
+        require(msg.value == 0, "Value should be 0 for ERC20 bridge");
         // Only the L1 bridge counterpart can initiate and finalize the deposit.
         require(
             AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
                 AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
             "mq"
         );
-        require(msg.value == 0, "Value should be 0 for ERC20 bridge");
-
+
         address expectedL2Token = l2TokenAddress(_l1Token);
         address currentL1Token = l1TokenAddress[expectedL2Token];
         if (currentL1Token == address(0)) {
```




## [G-05] Avoid Reading and writing to state if the amount is zero

### Instances
1. #### Refactor `L2BaseToken.mint()` to avoid reading or writing to state if `_amount` is 0.
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L65-#L66

In the `L2BaseToken.mint()` function as shown below checks should be implemented to avoid  reading and writing to state if the `_amount` argument is zero this is because in scenarios where `_amount` is 0 the statements  `totalSupply += _amount` and `balance[_account] += _amount` would not in any way change the value of `totalSupply` and `balance[_account]` respectively since they are being incremented by 0.  This then means that in scenarios where `_amount` is 0 the statements `totalSupply += _amount` and `balance[_account] += _amount` is re-assigning the same value to state i.e there is no state change.

```solidity
file: system-contracts/contracts/L2BaseToken.sol

64:    function mint(address _account, uint256 _amount) external override onlyCallFromBootloader {
65:        totalSupply += _amount;
66:        balance[_account] += _amount;
67:        emit Mint(_account, _amount);
68:    }
```

```diff
diff --git a/code/system-contracts/contracts/L2BaseToken.sol b/code/system-contracts/contracts/L2BaseToken.sol
index 573548a..9774a7c 100644
--- a/code/system-contracts/contracts/L2BaseToken.sol
+++ b/code/system-contracts/contracts/L2BaseToken.sol
@@ -62,9 +62,12 @@ contract L2BaseToken is IBaseToken, ISystemContract {
     /// @param _account The address which to mint the funds to.
     /// @param _amount The amount of ETH in wei to be minted.
     function mint(address _account, uint256 _amount) external override onlyCallFromBootloader {
-        totalSupply += _amount;
-        balance[_account] += _amount;
-        emit Mint(_account, _amount);
+        if (_amount > 0) {
+            totalSupply += _amount;
+            balance[_account] += _amount;
+            emit Mint(_account, _amount);
+        }
+
     }
```
```
Estimated gas saved: 10000 gas units
```

2. #### Refactor `L2BaseToken.transferFromTo()` to avoid reading or writing to state if `_amount` is 0.
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L46

In the `L2BaseToken.transferFromTo()` function as shown below checks should be implemented to avoid reading and writing to state if the `_amount` argument is zero this is because in scenarios where `_amount` is 0 the statement `balance[_to] += _amount` would not in any way change the value of `balance[_to]` since it is being incremented by 0.  This then means that in scenarios where `_amount` is 0 the statement `balance[_to] += _amount` is re-assigning the same value to state i.e there is no state change.

```solidity
file: system-contracts/contracts/L2BaseToken.sol

32:    function transferFromTo(address _from, address _to, uint256 _amount) external override {
33:        require(
34:            msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
35:                msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
36:                msg.sender == BOOTLOADER_FORMAL_ADDRESS,
37:            "Only system contracts with special access can call this method"
38:        );
39:
40:        uint256 fromBalance = balance[_from];
41:        require(fromBalance >= _amount, "Transfer amount exceeds balance");
42:        unchecked {
43:            balance[_from] = fromBalance - _amount;
44:            // Overflow not possible: the sum of all balances is capped by totalSupply, and the sum is preserved by
45:            // decrementing then incrementing.
46:            balance[_to] += _amount;     //@audit implement chek for _amount 0
47:        }
48:
49:        emit Transfer(_from, _to, _amount);
50:    }
```

```diff
diff --git a/code/system-contracts/contracts/L2BaseToken.sol b/code/system-contracts/contracts/L2BaseToken.sol
index 573548a..9da2cca 100644
--- a/code/system-contracts/contracts/L2BaseToken.sol
+++ b/code/system-contracts/contracts/L2BaseToken.sol
@@ -37,16 +37,19 @@ contract L2BaseToken is IBaseToken, ISystemContract {
             "Only system contracts with special access can call this method"
         );

-        uint256 fromBalance = balance[_from];
-        require(fromBalance >= _amount, "Transfer amount exceeds balance");
-        unchecked {
-            balance[_from] = fromBalance - _amount;
-            // Overflow not possible: the sum of all balances is capped by totalSupply, and the sum is preserved by
-            // decrementing then incrementing.
-            balance[_to] += _amount;
+        if (_amount > 0) {
+            uint256 fromBalance = balance[_from];
+            require(fromBalance >= _amount, "Transfer amount exceeds balance");
+            unchecked {
+                balance[_from] = fromBalance - _amount;
+                // Overflow not possible: the sum of all balances is capped by totalSupply, and the sum is preserved by
+                // decrementing then incrementing.
+                balance[_to] += _amount;
+            }
+
+            emit Transfer(_from, _to, _amount);
         }

-        emit Transfer(_from, _to, _amount);
     }
```

```
Estimated gas saved: 5000 gas units
```


## [G-06] The `ContractDeployer._storeAccountInfo()` function is unnecessary
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L58-#L60

Having to declare an internal function `ContractDeployer._storeAccountInfo()` to set the `accountInfo[_address]` mapping is unnecessary as we can simply inline this operation rather than calling a function which would incur 2 `JUMP` instruction and cost of the stack setup for the function call totalling around `40` gas units. Removing this function would also help reduce deployment cost.

```solidity
file: system-contracts/contracts/ContractDeployer.sol

58:    function _storeAccountInfo(address _address, AccountInfo memory _newInfo) internal {
59:        accountInfo[_address] = _newInfo;
60:    }
```



## [G-07] Events should be emitted outside of loops
Emitting an event has an overhead of **375 gas**, which will be incurred on every iteration of the loop. It is cheaper to `emit` only [once](https://github.com/ethereum/EIPs/blob/adad5968fd6de29902174e0cb51c8fc3dceb9ab5/EIPS/eip-1155.md?plain=1#L68) after the loop has finished.

### 3 Instances
- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261-#L265

```solidity
file: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

253:    function _commitBatchesWithoutSystemContractsUpgrade(
254:        StoredBatchInfo memory _lastCommittedBatchData,
255:        CommitBatchInfo[] calldata _newBatchesData
256:    ) internal {
257:        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
258:            _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));
259:
260:            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
261:            emit BlockCommit(
262:                _lastCommittedBatchData.batchNumber,
263:                _lastCommittedBatchData.batchHash,
264:                _lastCommittedBatchData.commitment
265:            );
266:        }
267:    }
```

- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L299-#L303
```solidity
file: ontracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

273:    function _commitBatchesWithSystemContractsUpgrade(
274:        StoredBatchInfo memory _lastCommittedBatchData,
275:        CommitBatchInfo[] calldata _newBatchesData,
276:        bytes32 _systemContractUpgradeTxHash
277:    ) internal {
.
.
.
289:        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
290:            // The upgrade transaction must only be included in the first batch.
291:            bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
292:            _lastCommittedBatchData = _commitOneBatch(
293:                _lastCommittedBatchData,
294:                _newBatchesData[i],
295:                expectedUpgradeTxHash
296:            );
297:
298:            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
299:            emit BlockCommit(
300:                _lastCommittedBatchData.batchNumber,
301:                _lastCommittedBatchData.batchHash,
302:                _lastCommittedBatchData.commitment
303:            );
304:        }
305:    }
```

- https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353
```solidity
file: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

349:    function _executeBatches(StoredBatchInfo[] calldata _batchesData) internal {
350:        uint256 nBatches = _batchesData.length;
351:        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
352:            _executeOneBatch(_batchesData[i], i);
353:            emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
354:        }
.
.
.
365:    }
```


## CONCLUSION
As you embark on incorporating the recommended optimizations, we want to emphasize the utmost importance of proceeding with vigilance and dedicating thorough efforts to comprehensive testing. It is of paramount significance to ensure that the proposed alterations do not inadvertently introduce fresh vulnerabilities, while also successfully achieving the anticipated enhancements in performance.

We strongly advise conducting a meticulous and exhaustive evaluation of the modifications made to the codebase. This rigorous scrutiny and exhaustive assessment will play a pivotal role in affirming both the security and efficacy of the refactored code. Your careful attention to detail, coupled with the implementation of a robust testing framework, will provide the necessary assurance that the refined code aligns with your security objectives and effectively fulfills the intended performance optimizations.
