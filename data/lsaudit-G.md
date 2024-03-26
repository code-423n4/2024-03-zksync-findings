To improve the report readability and its transparency - the report is divided into two sections. The first section contains issues evaluated during the manual process of code-review. It focuses on two types of findings:
* Full optimizations - e.g., "Function `X()` can be optimized" - which describes multiple of optimizations related to a single feature. Each issue requires some code refactoring.
* Issue related optimization - e.g., repacking of structs, changing orders of `require` statements, etc. Each of these issue required a manual review, which allowed us to confirm that the optimization would indeed save some gas. The manual process allowed us to provide a short explanation, why the proposed solution will save gas.

The second section - is related to automated findings. These findings - will - most likely - be ignored and their proposed fixes not implemented, because they significantly affect the code readability and provide just a minimal gas savings. These findings describe issues like: using assembly for simple operations, marking constructors as payable, etc. Nonetheless, we've decide to contain them in the report for the completeness. 
Since during the automated process - we have been using own tooling, we've decide to simplify some of its detectors and re-write them as a simple `grep` commands. To improve the report quality and readability, we've decide to not list the exact instances found during the automated process - but instead, we've provided a simple `grep` instruction, which allows to identified those issue by the reader.
Finding marked as `[AUTOMATED-FINDING-N]` describes how to use `grep` to identify most of the instances related to each finding. Please notice, that those `grep` instructions won't identify every affected instance - but in most cases - they will report enough results to understand the crux of the issue.
In the automated findings, we've piped our `grep` detectors by `| wc -l`, just to demonstrate how many instances are affected. To list exact lines affected, please remove it from the command.

# [1] Function `_revertBatches()` can be optimized

**File:** `Executor.sol`

This issue contains multiple of optimizations which requires code refactoring. Thus it was reported as separated finding.

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L481)
```solidity
481:     function _revertBatches(uint256 _newLastBatch) internal {
482:         require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch
483:         require(_newLastBatch >= s.totalBatchesExecuted, "v2"); // Already executed batches cannot be reverted
484: 
485:         if (_newLastBatch < s.totalBatchesVerified) {
486:             s.totalBatchesVerified = _newLastBatch;
487:         }
488:         s.totalBatchesCommitted = _newLastBatch;
489: 
490:         // Reset the batch number of the executed system contracts upgrade transaction if the batch
491:         // where the system contracts upgrade was committed is among the reverted batches.
492:         if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) {
493:             delete s.l2SystemContractsUpgradeBatchNumber;
494:         }
495: 
496:         emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
```

At line 488, we assign `_newLastBatch` to state variable `s.totalBatchesCommitted`. Since this value is not being changed, we can re-use `_newLastBatch` at line 496, to avoid additional reading of a state variable: `emit BlocksRevert(_newLastBatch, s.totalBatchesVerified, s.totalBatchesExecuted);`.

Moreover, `s.totalBatchesExecuted` is used twice and can be cached.

At line 485, when the condition if fulfilled, we will be reading `s.totalBatchesVerified` three times (line 485, 486, 487). We can re-factor the code to avoid additional reading of `s.totalBatchesVerified`. This is what needs to be done:
1. move `s.totalBatchesCommitted = _newLastBatch` higher 
2. move `if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch)` higher
3. rewrite `if (_newLastBatch < s.totalBatchesVerified)` to `if`-`else` condition, when `if` block will be executed, we will avoid additional reading.
Please notice that in that case, we will read `s.totalBatchesVerified` only twice (explained in the comment section)


```
   function _revertBatches(uint256 _newLastBatch) internal {
        require(s.totalBatchesCommitted > _newLastBatch, "v1"); 
        uint256 cachedtotalBatchesExecuted = s.totalBatchesExecuted;
        require(_newLastBatch >= cachedtotalBatchesExecuted, "v2"); 

        s.totalBatchesCommitted = _newLastBatch;  // line 488 can be moved higher

        if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) { // line 497 can be moved higher
            delete s.l2SystemContractsUpgradeBatchNumber;
        }

        if (_newLastBatch < s.totalBatchesVerified) { // first read of `s.totalBatchesVerified`
            s.totalBatchesVerified = _newLastBatch;  // when if returns true, 2nd read of `s.totalBatchesVerified`
            emit BlocksRevert(_newLastBatch, _newLastBatch, cachedtotalBatchesExecuted);  // we can use _newLastBatch now
        } else  {
            emit BlocksRevert(_newLastBatch, s.totalBatchesVerified, cachedtotalBatchesExecuted); // when if returns false, 2nd read of `s.totalBatchesVerified`
        }
 
    }
```


# [2] Function `setNewBatch()` from `SystemContext.sol` can be optimized

**File:** `SystemContext.sol`
This issue requires code-refactoring of some code, thus it was reported separately.

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L452)
```solidity
452:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
453: 
454:         _ensureBatchConsistentWithL2Block(_newTimestamp);
455: 
456:         batchHashes[previousBatchNumber] = _prevBatchHash;
457: 
458:         // Setting new block number and timestamp
459:         BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp});
```

There's unnecessary addition, which can be removed from above function. Let's take a look at lines 452 and 459: `previousBatchNumber + 1`.
Since line 452 requires, that `previousBatchNumber + 1 == _expectedNewNumber` (otherwise, function will revert), we can be sure, that `_expectedNewNumber == previousBatchNumber + 1`. This implies, that at line 459, instead of using addition again, we can simply use `_expectedNewNumber` instead:

```
459:         BlockInfo memory newBlockInfo = BlockInfo({number: _expectedNewNumber, timestamp: _newTimestamp});
```

This will save us from spending additional gas on unnecessary operation.



# [3] Function `initialize()` in `L2SharedBridge.sol` can be optimized

**File:** `L2SharedBridge.sol`

This issue requires code-refactoring of some code, thus it was reported separately.

[File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L60)
```solidity
60:         l1Bridge = _l1Bridge;
61:         l2TokenProxyBytecodeHash = _l2TokenProxyBytecodeHash;
62: 
63:         if (block.chainid != ERA_CHAIN_ID) {
64:             address l2StandardToken = address(new L2StandardERC20{salt: bytes32(0)}());
65:             l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(l2StandardToken);
66:             l2TokenBeacon.transferOwnership(_aliasedOwner);
67:         } else {
68:             require(_l1LegecyBridge != address(0), "bf2");
69:             // l2StandardToken and l2TokenBeacon are already deployed on ERA, and stored in the proxy
70:         }
```

When `block.chainid` is `ERA_CHAIN_ID` and `_l1LegecyBridge` is `address(0)` - we can revert earlier, without wasting gas on reading state variables: `l1Bridge` and `l2TokenProxyBytecodeHash`.
Moreover, we can use `==` operator, instead of `!=`.

```
        if (block.chainid == ERA_CHAIN_ID) {
        require(_l1LegecyBridge != address(0), "bf2");
        } else {
            address l2StandardToken = address(new L2StandardERC20{salt: bytes32(0)}());
            l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(l2StandardToken);
            l2TokenBeacon.transferOwnership(_aliasedOwner);
        }
        l1Bridge = _l1Bridge;
        l2TokenProxyBytecodeHash = _l2TokenProxyBytecodeHash;

```



# [4] Refactor `Diamond.sol` by inlining `_saveFacetIfNew()` function

**File:** `Diamond.sol`

This issue is reported as separate finding, since it requires multiple of changes in the code base.
Our recommendation is to inline `_saveFacetIfNew()` to avoid additional SSTORE performed by `DiamondStorage storage ds = getDiamondStorage()`.

[File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L189)
```solidity
189:     function _saveFacetIfNew(address _facet) private {
190:         DiamondStorage storage ds = getDiamondStorage();
191: 
192:         uint256 selectorsLength = ds.facetToSelectors[_facet].selectors.length;
193:         // If there are no selectors associated with facet then save facet as new one
194:         if (selectorsLength == 0) {
195:             ds.facetToSelectors[_facet].facetPosition = ds.facets.length.toUint16();
196:             ds.facets.push(_facet);
197:         }
198:     }
```

Function `_saveFacetIfNew()` executes `DiamondStorage storage ds = getDiamondStorage();` (line 189).
We can spot, that function `_saveFacetIfNew()` is called inside `_addFunctions()` and `_replaceFunctions()`. Those functions - at the beginning of their implementation perform the same operation: `DiamondStorage storage ds = getDiamondStorage();`.
This basically means, that `DiamondStorage storage ds = getDiamondStorage();` is redundant in the `_saveFacetIfNew()`. We can inline `_saveFacetIfNew()` in `_addFunctions()` and `_replaceFunctions()` to avoid repeating `DiamondStorage storage ds = getDiamondStorage();`.



# [5] Alter some struct's fields datatype to improve packing

**Files:** `Messaging.sol`, `BaseZkSyncUpgrade.sol`, `IExecutor.sol`

[File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L28)
```solidity
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

`newProtocolVersion` is being increases every time upgrade is made. `upgradeTimestamp` contains the timestamp of the upgrade. Both these fields can be `uint128` (instead of `uint256`) to fit into one slot.


[File: code/contracts/ethereum/contracts/common/Messaging.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L098)
```solidity
098: struct L2CanonicalTransaction {
099:     uint256 txType;
100:     uint256 from;
101:     uint256 to;
102:     uint256 gasLimit;
103:     uint256 gasPerPubdataByteLimit;
104:     uint256 maxFeePerGas;
105:     uint256 maxPriorityFeePerGas;
106:     uint256 paymaster;
107:     uint256 nonce;
108:     uint256 value;
```

Both `nonce` and `txType` fields can be `uint128 ` to fit into single slot.
Both `gasLimit` and `gasPerPubdataByteLimit` can be `uint128` to fit into single slot.


[File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L83)
```solidity
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

`timestamp` field can be `uint64`. Then, it can be moved after `batchNumber` to fit a single slot (`uint64` + `uint64`).


# [6] State variables may be packed into fewer storage slots

**File:** `Governance.sol`

[File: code/contracts/ethereum/contracts/governance/Governance.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L26)
```solidity
26:     address public securityCouncil;
27: 
28:     /// @notice A mapping to store timestamps when each operation will be ready for execution.
29:     /// @dev - 0 means the operation is not created.
30:     /// @dev - 1 (EXECUTED_PROPOSAL_TIMESTAMP) means the operation is already executed.
31:     /// @dev - any other value means timestamp in seconds when the operation will be ready for execution.
32:     mapping(bytes32 operationId => uint256 executionTimestamp) public timestamps;
33: 
34:     /// @notice The minimum delay in seconds for operations to be ready for execution.
35:     uint256 public minDelay;
```

Consider changing `minDelay` type from `uint256` to `uint64`. Then, it could be packed in a single storage slot with `address public securityCouncil`.



# [7] In `NonceHolder.sol`, ID mappings can be combined into a single `mapping` of an ID to a `struct`

**File:** `NonceHolder.sol`

[File: code/system-contracts/contracts/NonceHolder.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L36)
```solidity
36:     mapping(uint256 account => uint256 packedMinAndDeploymentNonce) internal rawNonces;
37: 
38:     /// Mapping of values under nonces for accounts.
39:     /// The main key of the mapping is the 256-bit address of the account, while the
40:     /// inner mapping is a mapping from a nonce to the value stored there.
41:     mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;
```


# [8] Repack struct by putting data types that fit together into one slot next to each other

This issue, in comparison to `# [5] Alter some struct's fields datatype to improve packing`  is related to changing the order of fields in the struct (while `[5]` suggests changing the datatype of fields) - thus it's being reported separately.

**File:** `IExecutor.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L83)
```solidity
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

`batchNumber` and `indexRepeatedStorageChanges` will fit into one slot.


# [9]  Avoid reading state variable twice

**Files:** `SystemContext.sol`, `L2StandardERC20.sol`

Reading state variables costs a lot of gas. It's better to always cache the state variable into local variable and read the local variable instead.

[File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L093)
```solidity
093:         try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {
094:             // Set decoded value for decimals.
095:             decimals_ = decimalsUint8;
096:         } catch {
097:             getters.ignoreDecimals = true;
098:         }
099: 
100:         availableGetters = getters;
101:         emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);
```

Variable `decimals_` is a state variable, thus reading it costs more gas than local variable.
Please notice, that we're reading this variable twice - firstly, at line 95, then at line 101.


Reading state variables multiple of times costs a lot of gas. Much more effective solution would be to just read it once and cache the result into local variable.

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L117)
```solidity
117:     function getCurrentPubdataSpent() public view returns (uint256) {
118:         uint256 pubdataPublished = SystemContractHelper.getZkSyncMeta().pubdataPublished;
119:         return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;
120:     }
```

To avoid reading `basePubdataSpent` twice, above code can be rewritten to:

```
    function getCurrentPubdataSpent() public view returns (uint256) {
        uint256 cachedBasePubdataSpent = basePubdataSpent;
        uint256 pubdataPublished = SystemContractHelper.getZkSyncMeta().pubdataPublished;
        return pubdataPublished > cachedBasePubdataSpent ? pubdataPublished - cachedBasePubdataSpent : 0;
    }
```

# [10] Refactor functions with events which emit both new and old values

**Files:** `StateTransitionManager.sol`, `Admin.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L23)
```solidity
23:     function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {
24:         // Save previous value into the stack to put it into the event later
25:         address oldPendingAdmin = s.pendingAdmin;
26:         // Change pending admin
27:         s.pendingAdmin = _newPendingAdmin;
28:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
29:     }
```

To avoid creating additional variable `oldPendingAdmin` which stores `s.pendingAdmin` before the update - we can move emitting event one line above:

```
   function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {
        emit NewPendingAdmin(s.pendingAdmin, _newPendingAdmin);
        s.pendingAdmin = _newPendingAdmin;  
    }
```

The same issue was observed in other instances:

[File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L110)
```solidity
110:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
111:         // Save previous value into the stack to put it into the event later
112:         address oldPendingAdmin = pendingAdmin;
113:         // Change pending admin
114:         pendingAdmin = _newPendingAdmin;
115:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
116:     }
```

Should be changed as above.

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L58)
```solidity
58:     function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager { 
59:         require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");
60: 
61:         uint256 oldPriorityTxMaxGasLimit = s.priorityTxMaxGasLimit;
62:         s.priorityTxMaxGasLimit = _newPriorityTxMaxGasLimit;
63:         emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);
64:     }
```

can be changed to:

```
    function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager { 
        require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");
        emit NewPriorityTxMaxGasLimit(s.priorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);
        s.priorityTxMaxGasLimit = _newPriorityTxMaxGasLimit;
        
    }
```



# [11] Do not calculate the length of array multiple of times

**Files:** `L2ContractHelper.sol`, `Compressor.sol`, `BaseZkSyncUpgrade.sol`, `PubdataChunkPublisher.sol`, `Executor.sol`, `DiamondProxy.sol`

While calculating the length of an array costs a lot of gas - it's recommended to calculate it once and then, cache the result inside the local variable.
Please notice that this is NOT the same issue as bot-report mentions. The bot-report contains instances of calculating array's length in the loop iterator, e.g.: `for (uint i=0; i < array.length; i++)`, while this issue reports that the length of the array is calculated within the loop (line 42).


[File: code/system-contracts/contracts/PubdataChunkPublisher.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)
```solidity
36:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
37:             uint256 start = BLOB_SIZE_BYTES * i;
38: 
39:             // We break if the pubdata isn't enough to cover 2 blobs. On L1 it is expected that the hash
40:             // will be bytes32(0) if a blob isn't going to be used.
41:             if (start >= _pubdata.length) {
42:                 break;
43:             }
```

In function `chunkAndPublishPubdata()`, the length of array is calculated on every loop iteration.

[File: code/system-contracts/contracts/Compressor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L52)
```solidity
52:                 encodedData.length * 4 == _bytecode.length,
53:                 "Encoded data length should be 4 times shorter than the original bytecode"
54:             );
55: 
56:             require(
57:                 dictionary.length / 8 <= encodedData.length / 2,
58:                 "Dictionary should have at most the same number of entries as the encoded data"
59:             );
60: 
61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
62:                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
63:                 require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");
```

`encodedData.length` is calculated 3 times (lines 52, 57, 61). Calculate it once and cache its value to local variable.
`dictionary.length` is calculated 2 times (line 57, 63). Calculate it once and cache its value to local variable.

[File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23)
```solidity
23:         require(_bytecode.length % 32 == 0, "pq");
24: 
25:         uint256 bytecodeLenInWords = _bytecode.length / 32;
```

`_bytecode.length` is calculated twice, it would be more efficient to calculate it once and cache the result before line 23.


[File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L223)
```solidity
223:         require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");
224:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");
225: 
226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```

`_factoryDeps.length` is calculated 3 times (lines 223, 224, 226). Calculate it once and cache the result into local variable before line 223.


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25)
```solidity
25:         require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
```

`msg.data.length` is calculated twice. Calculate it once and cache the result into local variable.


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631)
```solidity
631:         require(_pubdataCommitments.length > 0, "pl");
632:         require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");
633:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");
634:         blobCommitments = new bytes32[](MAX_NUMBER_OF_BLOBS);
635: 
636:         for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {
```

`_pubdataCommitments.length` is calculated 4 times (lines 631, 632, 633m 636). Calculate it once and cache the result into local variable.



# [12] Proof verification in `Executor.sol` is performed twice 

**File:** `Executor.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L429)
```solidity
429:         if (_proof.serializedProof.length > 0) {
430:             _verifyProof(proofPublicInput, _proof);
431:         }
432:         // #else
433:         _verifyProof(proofPublicInput, _proof);
434:         // #endif
```

When `_proof.serializedProof.length > 0` function will call `_verifyProof(proofPublicInput, _proof)` twice - at line 430 and at line 433.


# [13] Divide loop in `_commitBatchesWithSystemContractsUpgrade()` to avoid redundant `if`

**File:** `Executor.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289)
```solidity
289:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
290:             // The upgrade transaction must only be included in the first batch.
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
292:             _lastCommittedBatchData = _commitOneBatch(
293:                 _lastCommittedBatchData,
294:                 _newBatchesData[i],
295:                 expectedUpgradeTxHash
296:             );
```

In function `_commitBatchesWithSystemContractsUpgrade()` - on every loop iteration - we check if `i == 0` (line 291). This condition is obviously `true` only during the first loop iteration. It's recommended to divide the loop into two parts:  
```
for (uint256 i = 0; i < 1; i = i.uncheckedInc())
```

```
for (uint256 i = 1; i < _newBatchesData.length; i = i.uncheckedInc())
```

Moreover, this would allow us to declare `expectedUpgradeTxHash` outside the loop - thus we won't spend additional gas on declaring this variable during every loop iteration.

That way, in the second loop we will be able to remove `i == 0` condition.


# [14] Pre-compute and cache `domainSeparator` in `TransactionHelper.sol`

**File:** `TransactionHelper.sol`

[File: code/system-contracts/contracts/libraries/TransactionHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L138)
```solidity
138:         bytes32 domainSeparator = keccak256(
139:             abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
140:         );
```

It's a common pattern to pre-compute and cache domain separator and then, compare it with pre-computed, cached value, instead of calculating it every time.



# [15] Create one, specific event, instead of emitting two events in a row

**Files:** `StateTransitionManager.sol`, `Bridgehub.sol`, `Admin.sol`

Instead of spending gas on emitting two events at once, it's better to create one, single event and emit it once.

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40)
```solidity
40:         emit NewPendingAdmin(pendingAdmin, address(0));
41:         emit NewAdmin(previousAdmin, pendingAdmin);
```

[File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L127)
```solidity
127:         emit NewPendingAdmin(currentPendingAdmin, address(0));
128:         emit NewAdmin(previousAdmin, pendingAdmin);
```

[File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68)
```solidity
68:         emit NewPendingAdmin(currentPendingAdmin, address(0));
69:         emit NewAdmin(previousAdmin, pendingAdmin);
```

# [16] Redundant casting in `getSize()`

**File:** `PriorityQueue.sol`

[File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L45)
```solidity
45:     function getSize(Queue storage _queue) internal view returns (uint256) {
46:         return uint256(_queue.tail - _queue.head);
47:     }
```

Since both `_queue.tail` and `_queue.head` are `uint256`, there's no need to cast `_queue.tail - _queue.head` to `uint256`. 



# [17] Utilize post-incrementing to optimize `pushBack()` function

**File:** `PriorityQueue.sol`

This issue is reported as separate finding, because proposed optimizations require code refactoring.

[File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L55)
```solidity
55:     function pushBack(Queue storage _queue, PriorityOperation memory _operation) internal {
56:         // Save value into the stack to avoid double reading from the storage
57:         uint256 tail = _queue.tail;
58: 
59:         _queue.data[tail] = _operation;
60:         _queue.tail = tail + 1;
61:     }
```

We can get rid of variable `tail` by using `_queue.tail++` directly in `_queue.data`:

```
function pushBack(Queue storage _queue, PriorityOperation memory _operation) internal {
    _queue.data[_queue.tail++] = _operation;
}
```


# [18] Redundant casting of addresses in `isSystemContract()`

**File:** `SystemContractHelper.sol`

[File: code/system-contracts/contracts/libraries/SystemContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L338)
```solidity
338:     function isSystemContract(address _address) internal pure returns (bool) {
339:         return uint160(_address) <= uint160(MAX_SYSTEM_CONTRACT_ADDRESS);
340:     }
```

Solidity allows to compare two addresses without casting them to integer first. This means, that above code can be changed to:

```
return _address <= MAX_SYSTEM_CONTRACT_ADDRESS;
```


# [19] Checking balance after the transfer cannot underflow, thus can be unchecked

**File:** `L1ERC20Bridge.sol`

This issue has been reported as separate finding, as it uses different invariant for underflow detection. While another finding uses the invariant that subtraction won't underflow, because `require` guarantees that subtrahend is lower than minuend, this one utilizes the fact that after the transfer, the balance cannot be lower then the balance before the transfer, thus line 165 won't underflow and can be unchecked.

[File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L161)
```solidity
161:         uint256 balanceBefore = _token.balanceOf(address(sharedBridge));
162:         _token.safeTransferFrom(_from, address(sharedBridge), _amount);
163:         uint256 balanceAfter = _token.balanceOf(address(sharedBridge));
164: 
165:         return balanceAfter - balanceBefore;
```

Balance after the transfer cannot be lower then before the transfer, thus `balanceAfter - balanceBefore` won't underflow and can be unchecked.


# [20] Removing code related to testing - to decrease the contract size and the deployment costs

**File:** `SystemContext.sol`

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L469)
```solidity
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
```

Both NatSpec and the code-base suggests that above code is just for testing and should not be on the production.
While it's not possible to use this code in a non-testing environment (`onlyCallFromBootloader` modifier won't let to call this code directly), it's recommend to remove this function.
Getting rid of redundant functions will decrease the contract size, thus less gas will be spent during the deployment process.

# [21] Do not assign `offset` in the last call of `UnsafeBytes.readUint256()` in `_parseL2WithdrawalMessage()`

**File:** `L1SharedBridge.sol`

A simple test in Remix IDE has been created, to compare gas usage of assigning more than one value from function call:

```
  function getUints() public pure returns (uint, uint) {return (1, 2);}
   function funcA() public view {
    uint a; uint b; 
    (a, b) = getUints();
    uint g = gasleft();
    (a, b) = getUints();
    console.log(g - gasleft());
   }
    function funcB() public view {
    uint a; uint b; 
    (a, b) = getUints();
    uint g = gasleft();
    (a, ) = getUints();
    console.log(g - gasleft());
   }
```

`funcB()` costs 74 gas, while `funcA()` costs 82 gas. This implies, that we shouldn't assign every parameter from function call if it's not needed.

[File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L520)
```solidity
520:             (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);
```

In the last call of `UnsafeBytes.readUint256(_l2ToL1message, offset)` (line 520), we won't need `offset` anymore, thus we can remove `offset` and change this line to: `(amount, ) = UnsafeBytes.readUint256(_l2ToL1message, offset)`.




# [22] Operations capped by `totalSupply` in `L2BaseToken` can be unchecked

**File:** `L2BaseToken.sol`

[File: code/system-contracts/contracts/L2BaseToken.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L64)
```solidity
64:     function mint(address _account, uint256 _amount) external override onlyCallFromBootloader {
65:         totalSupply += _amount;
66:         balance[_account] += _amount;
67:         emit Mint(_account, _amount);
68:     }
```

User's balance is capped by `totalSupply`. When `totalSupply += _amount` won't revert (due to overflow) - we can be sure, that `balance[_account] += _amount` won't overflow either, thus line 66 can be unchecked.
Important - please notice, that only line 66: `balance[_account] += _amount` can be unchecked.




# [23] Use `delete` to clear data, instead of assigning data to `0`

**File:** `L1Messenger.sol`

[File: code/system-contracts/contracts/L1Messenger.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L328)
```solidity
328:         /// Clear logs state
329:         chainedLogsHash = bytes32(0);
330:         numberOfLogsToProcess = 0;
331:         chainedMessagesHash = bytes32(0);
332:         chainedL1BytecodesRevealDataHash = bytes32(0);
```


# [24] Redundant `require` in `BaseZkSyncUpgradeGenesis`

**File:** `BaseZkSyncUpgradeGenesis.sol`

[File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22)
```solidity
22:         require(
23:             // Genesis Upgrade difference: Note this is the only thing change > to >=
24:             _newProtocolVersion >= previousProtocolVersion,
25:             "New protocol version is not greater than the current one"
26:         );
27:         require(
28:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
29:             "Too big protocol version difference"
30:         );
```

To not revert, two conditions must occur: `_newProtocolVersion >= previousProtocolVersion` and `_newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA`.
However, please notice, that the first `require` (lines 23-26) is redundant and can be removed. When `_newProtocolVersion < previousProtocolVersion`, function will already revert due to underflow in the second `require` at line 28.
This basically means, that it's enough to leave just only the second `require`: (when the first condition won't be fulfilled, function will revert due to underflow in the 2nd `require`).





# [25] Use de Morgan's laws to reduce number of negations 

**File:** `DiamondProxy.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L31)
```solidity
31:         require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen
```

According to de Morgan's laws: `!A || !B <=> !(A & B)`, which means we can reduce one negation and rewrite above line to:

```
require(!(diamondStorage.isFrozen && facet.isFreezable), "q1"); // Facet is frozen
```


# [26] Do not repeat `if` checks in `_constructContract()`

**File:** `ContractDeployer.sol`

Function `_constructContract()` performs the same conditional `if` check twice. This is a waste of gas:

[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L332)
```solidity
332:             if (value > 0) {
333:                 BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo(address(this), _newAddress, value);
334:             }
335:             // 2. Set the constructed code hash on the account
336:             _storeConstructingByteCodeHashOnAddress(_newAddress, _bytecodeHash);
337: 
338:             // 3. Call the constructor on behalf of the account
339:             if (value > 0) {
340:                 // Safe to cast value, because `msg.value` <= `uint128.max` due to `MessageValueSimulator` invariant
341:                 SystemContractHelper.setValueForNextFarCall(uint128(value));
342:             }
```

Firstly, there's a check (line 332) if `value` is bigger then 0. Then, at line 339, the same check is being made again.

# [27] Do not import the whole library, when only a few functions from that library are being used

**File:** `Mailbox.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L5)
```solidity
5: import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
```

`Mailbox.sol` imports the whole `Math.sol` library, while it only uses `Math.max()` function.



# [28] Calculate simple operations at once

**File:** `TransactionValidator.sol`

[File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L77)
```solidity
77:             costForComputation = L1_TX_INTRINSIC_L2_GAS;
78: 
79:             // Taking into account the hashing costs that depend on the length of the transaction
80:             // Note that L1_TX_DELTA_544_ENCODING_BYTES is the delta in the price for every 544 bytes of
81:             // the transaction's encoding. It is taken as LCM between 136 and 32 (the length for each keccak256 round
82:             // and the size of each new encoding word).
83:             costForComputation += Math.ceilDiv(_encodingLength * L1_TX_DELTA_544_ENCODING_BYTES, 544);
84: 
85:             // Taking into the account the additional costs of providing new factory dependencies
86:             costForComputation += _numberOfFactoryDependencies * L1_TX_DELTA_FACTORY_DEPS_L2_GAS;
87: 
88:             // There is a minimal amount of computational L2 gas that the transaction should cover
89:             costForComputation = Math.max(costForComputation, L1_TX_MIN_L2_GAS_BASE);
```

Above code performs redundant addition at lines 83, 86. Every time it adds the value to `costForComputation`, instead of doing it only once:

```
            costForComputation = Math.max(L1_TX_INTRINSIC_L2_GAS + Math.ceilDiv(_encodingLength * L1_TX_DELTA_544_ENCODING_BYTES, 544) + _numberOfFactoryDependencies * L1_TX_DELTA_FACTORY_DEPS_L2_GAS, L1_TX_MIN_L2_GAS_BASE);
```


# [29] Use calldata instead of memory, when struct is not being changed

**File:** `TransactionValidator.sol`

[File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L46)
```solidity
46:     function validateUpgradeTransaction(L2CanonicalTransaction memory _transaction) internal pure {
```

Function `validateUpgradeTransaction()` verifies fields of `_transaction`, but does not alter it. This implies, that instead of `memory`, `calldata` should be used.

# [30] Some operations which won't underflow may be unchecked

**Files:** `GasBoundCaller.sol`, `SystemContext.sol`, `MsgValueSimulator.sol`

[File: code/system-contracts/contracts/GasBoundCaller.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L49)
```solidity
49:         uint256 pubdataAllowance = _maxTotalGas > expectedForCompute ? _maxTotalGas - expectedForCompute : 0;
```

Since `_maxTotalGas > expectedForCompute`, we know that `_maxTotalGas - expectedForCompute` won't underflow, thus it can be unchecked.

[File: code/system-contracts/contracts/GasBoundCaller.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L63)
```solidity
63:         uint256 pubdataSpent = pubdataPublishedAfter > pubdataPublishedBefore
64:             ? pubdataPublishedAfter - pubdataPublishedBefore
65:             : 0;
```

Since `pubdataPublishedAfter > pubdataPublishedBefore`, we know that `pubdataPublishedAfter - pubdataPublishedBefore` won't underflow, thus it can be unchecked.


[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L119)
```solidity
119:         return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;
```

Since `pubdataPublished > basePubdataSpent`, we know that `pubdataPublished - basePubdataSpent` won't underflow, thus it can be unchecked.


[File: code/system-contracts/contracts/MsgValueSimulator.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L53)
```solidity
53:         uint256 userGas = gasInContext > MSG_VALUE_SIMULATOR_STIPEND_GAS
54:             ? gasInContext - MSG_VALUE_SIMULATOR_STIPEND_GAS
55:             : 0;
```

Since `gasInContext > MSG_VALUE_SIMULATOR_STIPEND_GAS`, we know that `gasInContext - MSG_VALUE_SIMULATOR_STIPEND_GAS` won't underflow, thus it can be unchecked.


# [31]  Use `require` which costs less gas first

**Files:** `Executor.sol`, `BaseZkSyncUpgrade.sol`, `L2SharedBridge.sol`, `Admin.sol`

Because failed `require` revert the whole operation - it's more profitable to use `require` which spends less gas first.

[File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L87)
```solidity
87:         require(
88:             AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
89:                 AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
90:             "mq"
91:         );
92:         require(msg.value == 0, "Value should be 0 for ERC20 bridge");
```

Reading `msg.value` costs less gas than reading `l1Bridge` and `l1LegacyBridge`, thus order of `require` can be changed.


[File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L223)
```solidity
223:         require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");
224:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");
```

Comparing `_factoryDeps.length` to constant `MAX_NEW_FACTORY_DEPS` costs less gas than comparing it to length of another array: `_expectedHashes.length`. Above code should be changed to:

```
require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");
require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L105)
```solidity
105:         require(
106:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107:             "StateTransition: cutHash mismatch"
108:         );
109: 
110:         require(
111:             s.protocolVersion == _oldProtocolVersion,
112:             "StateTransition: protocolVersion mismatch in STC when upgrading"
113:         );
```

`s.protocolVersion == _oldProtocolVersion` uses less gas than `cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion)`. The second `require` is just reading, while the first one - calling external function `upgradeCutHash()`. Thus the order of `require` should be changed.


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L226)
```solidity
226:         require(
227:             IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
228:             "Executor facet: wrong protocol version"
229:         );
230:         // With the new changes for EIP-4844, namely the restriction on number of blobs per block, we only allow for a single batch to be committed at a time.
231:         require(_newBatchesData.length == 1, "e4");
```

`_newBatchesData.length == 1` uses less gas than calling `protocolVersion()` in the first `require`: `IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion` (especially, that we expect `_newBatchesData.length` to be equal to 1). This implies, that the order of `require` statements should be changed.

# [32] Execute `require` before other operations 

**Files:** `GasBoundCaller.sol`, `Executor.sol`

Because `require` reverts the whole operation, it's better to perform `require` statements before any other operation. When `require` reverts, function won't use additional gas for other operations.

[File: code/system-contracts/contracts/GasBoundCaller.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L40)
```solidity
40:         uint256 expectedForCompute = gasleft() + CALL_ENTRY_OVERHEAD;
[...]
46:         require(_maxTotalGas >= gasleft(), "Gas limit is too low");
```

We can move `require` from line 46 above line 40. When `_maxTotalGas` won't be greater or equal `gasleft()` - function will revert immediately, thus we won't waste additional gas on `expectedForCompute` assignment.


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L356)
```solidity
356:         uint256 newTotalBatchesExecuted = s.totalBatchesExecuted + nBatches;
357:         s.totalBatchesExecuted = newTotalBatchesExecuted;
358:         require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.
```

We can move `require` from line 358, before line 357. When condition `newTotalBatchesExecuted <= s.totalBatchesVerified` won't be fulfilled, function will revert without wasting gas on executing line 357. The fixed code should look like this:

```
        uint256 newTotalBatchesExecuted = s.totalBatchesExecuted + nBatches;
        require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.
        s.totalBatchesExecuted = newTotalBatchesExecuted;
```


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L629)
```solidity
629:         uint256 versionedHashIndex = 0;
630: 
631:         require(_pubdataCommitments.length > 0, "pl");
632:         require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");
633:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");
```

Move `require` statements from lines 631, 632, 633 above line 629. If any of these `require` revert, function won't waste additional gas on `versionedHashIndex` initialization.
 

# [33] Use short-circuiting in OR operations

**File:** `NonceHolder.sol`

Solidity uses short-circuiting while performing OR operations. This means, that in the expression `A() OR B()` - when `A()` evaluates to `true` - expression `B()` won't be executed (because `true OR whatever` evaluates to `true`).
This behavior suggests, that it's better to use less-gas-costly operation first (if it will be evaluated to `true`, Solidity won't waste gas on executing the 2nd operation). 

[File: code/system-contracts/contracts/NonceHolder.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L156)
```solidity
156:         return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);
```

Function `getMinNonce()` reads state variable and performs multiple of other operations. This means, that it uses more gas than just reading `nonceValues[addressAsKey][_nonce]` state variable and comparing it to `0`. Above code should be rewritten to:

```
 return (nonceValues[addressAsKey][_nonce] > 0 || _nonce < getMinNonce(_address));
```

# [34] Do not declare variables inside loop

**Files:** `Compressor.sol`, `Mailbox.sol`, `ImmutableSimulator.sol`, `ValidatorTimelock.sol`, `Executor.sol`

Move variable declaration outside the loop. While the variable is declared inside the loop - every loop iteration will spend gas on that variable declaration.

[File: code/system-contracts/contracts/ImmutableSimulator.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L38)
```solidity
38:             for (uint256 i = 0; i < immutablesLength; ++i) {
39:                 uint256 index = _immutables[i].index;
40:                 bytes32 value = _immutables[i].value;
```

should be changed to:

```
    uint256 index;
    bytes32 value;
    for (uint256 i = 0; i < immutablesLength; ++i) {
        index = _immutables[i].index;
        value = _immutables[i].value;
```


[File: code/system-contracts/contracts/Compressor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L61)
```solidity
61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
62:                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
```

should be changed to:

```
            uint256 indexOfEncodedChunk;
            for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
                indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
```


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289)
```solidity
289:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
290:             // The upgrade transaction must only be included in the first batch.
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
```

Should be changed to:

```
        bytes32 expectedUpgradeTxHash;
        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
            // The upgrade transaction must only be included in the first batch.
            expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356)
```solidity
356:         for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {
357:             bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);
```

Should be changed to:

```
        bytes32 hashedBytecode;
        for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {
            hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);
```

[File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185)
```solidity
185:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
186:                 uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
```

Should be changed to :

```
            uint256 commitBatchTimestamp;
            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
```


[File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)
```solidity
209:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
210:                 uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
```

Should be changed to:

```
            uint256 commitBatchTimestamp;
            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
```

# [35] Avoid declaring unused variables

**File:** `Constants.sol`

[File: code/system-contracts/contracts/Constants.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L93)
```solidity
93: /// @dev The maximal msg.value that context can have
94: uint256 constant MAX_MSG_VALUE = 2 ** 128 - 1;
```

Constant `MAX_MSG_VALUE` is not used anymore, thus it should be removed from `Constnats.sol`

# [36] Use bitwise operators instead of multiplication/division by value of 2 to the power of N

**Files:** `L2ContractHelper.sol`, `Compressor.sol`, `Executor.sol`, `Merkle.sol`

[File: code/system-contracts/contracts/Compressor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L52)
```solidity
52:                 encodedData.length * 4 == _bytecode.length,
[...]
57:                 dictionary.length / 8 <= encodedData.length / 2,
[...]
62:                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
[...]
66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);
```

[File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L33)
```solidity
33:             _index /= 2;
```


[File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25)
```solidity
25:         uint256 bytecodeLenInWords = _bytecode.length / 32;
26:         require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L581)
```solidity
581:             blobAuxOutputWords[i * 2] = _blobHashes[i];
582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
```



# [37] Code related to local testing should be removed

**Files:** `StateTransitionManager.sol`, `DiamondInit.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L49)
```solidity
49:         // While this does not provide a protection in the production, it is needed for local testing
50:         // Length of the L2Log encoding should not be equal to the length of other L2Logs' tree nodes preimages
51:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32); 
```

[File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L104)
```solidity
104:         // While this does not provide a protection in the production, it is needed for local testing
105:         // Length of the L2Log encoding should not be equal to the length of other L2Logs' tree nodes preimages
106:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32); 
```

Above `assert()` is just a waste of gas in the production environment. Moreover it increases the size of the contract, thus increases the deployment cost. Our recommendation is to get rid of code related to local testing only.




# [38] Dot notation for struct assignment costs less gas

**File:** `Diamond.sol`

Using named arguments for struct means that the compiler needs to organize the fields in memory before doing the assignment, which wastes gas. Set each field directly in storage (use dot-notation), or use the unnamed version of the constructor.

[File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L218)
```solidity
218:         ds.selectorToFacet[_selector] = SelectorToFacet({
219:             facetAddress: _facet,
220:             selectorPosition: selectorPosition,
221:             isFreezable: _isSelectorFreezable
222:         });
```

should be optimized to:

```
ds.selectorToFacet[_selector].facetAddress = _facet;
ds.selectorToFacet[_selector].selectorPosition = selectorPosition;
ds.selectorToFacet[_selector].isFreezable = _isSelectorFreezable;
```

# [39] Use AND operators instead of modulo (%) to check if number is odd/even

**Files:** `L2ContractHelper.sol`, `Utils.sol`, `Merkle.sol`, `KnownCodesStorage.sol`

[File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43)
```solidity
43:         require(bytecodeLen(_bytecodeHash) % 2 == 1, "uy"); // Code length in words must be odd
```

[File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L27)
```solidity
27:         require(bytecodeLenInWords % 2 == 1, "ps"); // bytecode length in words must be odd
```

[File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L30)
```solidity
30:             currentHash = (_index % 2 == 0)
```

[File: code/system-contracts/contracts/KnownCodesStorage.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L78)
```solidity
78:         require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd");
```

[File: code/system-contracts/contracts/libraries/Utils.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L88)
```solidity
88:         require(lengthInWords % 2 == 1, "pr"); // bytecode length in words must be odd
```



# [40] else-block is not required in `getOperationState()`

**File:** `Governance.sol`

[File: code/contracts/ethereum/contracts/governance/Governance.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L105)
```solidity
105:     function getOperationState(bytes32 _id) public view returns (OperationState) {
106:         uint256 timestamp = timestamps[_id];
107:         if (timestamp == 0) {
108:             return OperationState.Unset;
109:         } else if (timestamp == EXECUTED_PROPOSAL_TIMESTAMP) {
110:             return OperationState.Done;
111:         } else if (timestamp > block.timestamp) {
112:             return OperationState.Waiting;
113:         } else {
114:             return OperationState.Ready;
115:         }
116:     }
```

The `else` instruction at line 113 can be removed. When previous conditions won't be fulfilled, function will still return `OperationState.Ready`. Getting rid of redundant `else` instruction saves additional gas.


# [41] Inline `modifier`s that are only used once, to save gas

**Files:** `ContractDeployer.sol`, `KnownCodesStorage.sol`

[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L213)
```solidity
213:     function forceDeployOnAddress(ForceDeployment calldata _deployment, address _sender) external payable onlySelf {
```

[File: code/system-contracts/contracts/KnownCodesStorage.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L39)
```solidity
39:     function markBytecodeAsPublished(bytes32 _bytecodeHash) external onlyCompressor {
```

Modifiers `onlySelf` and `onlyCompressor` where used only once, thus they can be inlined.


# [42] Use `""` instead of `new bytes(0)`

**Files:** `StateTransitionManager.sol`, `Mailbox.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L308)
```solidity
308:             signature: new bytes(0),
309:             factoryDeps: _hashFactoryDeps(_factoryDeps),
310:             paymasterInput: new bytes(0),
311:             reservedDynamic: new bytes(0)
```

[File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L196)
```solidity
196:             signature: new bytes(0),
197:             factoryDeps: uintEmptyArray,
198:             paymasterInput: new bytes(0),
199:             reservedDynamic: new bytes(0)
```


# [43] `public` functions which are not called by the contract should be declared as `external`

**File:** `Mailbox.sol`

When `public` function is never called internally and is only expected to be invoked externally, it is more gas-efficient to explicitly declare it as `external`.

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L74)
```solidity
74:     function proveL1ToL2TransactionStatus(
75:         bytes32 _l2TxHash,
76:         uint256 _l2BatchNumber,
77:         uint256 _l2MessageIndex,
78:         uint16 _l2TxNumberInBatch,
79:         bytes32[] calldata _merkleProof,
80:         TxStatus _status
81:     ) public view returns (bool) {
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L143)
```solidity
143:     function l2TransactionBaseCost(
144:         uint256 _gasPrice,
145:         uint256 _l2GasLimit,
146:         uint256 _l2GasPerPubdataByteLimit
147:     ) public view returns (uint256) {
```



# [44] Do not emit events with empty data

**File:** `Admin.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L139)
```solidity
139:         emit Freeze();
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L149)
```solidity
149:         emit Unfreeze();
```


# [45]  Do not declare local variables used only once

**Files:** `L2ContractHelper.sol`, `Compressor.sol`, `L2SharedBridge.sol`, `Mailbox.sol`, `L1ERC20Bridge.sol`, `NonceHolder.sol`, `DefaultAccount.sol`, `EfficientCall.sol`, `AccountCodeStorage.sol`, `L1SharedBridge.sol`, `Diamond.sol`, `L2StandardERC20.sol`, `SystemContractHelper.sol`, `KnownCodesStorage.sol`, `Admin.sol`, `ContractDeployer.sol`

[File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L119)
```solidity
119:         address beaconAddress = _getBeacon();
120:         require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");
```

Variable `beaconAddress` is used only once, thus this variable is redundant. Above code can be rewritten to:

```
require(msg.sender == UpgradeableBeacon(_getBeacon()).owner(), "tt");
```


[File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L64)
```solidity
64:             address l2StandardToken = address(new L2StandardERC20{salt: bytes32(0)}());
65:             l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(l2StandardToken);
```

Variable `l2StandardToken` is used only once, thus it is redundant. Above code can be changed to:

```
l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(address(new L2StandardERC20{salt: bytes32(0)}()));
```

[File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L110)
```solidity
110:         bytes32 salt = _getCreate2Salt(_l1Token);
111: 
112:         BeaconProxy l2Token = _deployBeaconProxy(salt);
```

Variable `salt` is used only once, thus it is redundant. Above code can be changed to:

```
BeaconProxy l2Token = _deployBeaconProxy(_getCreate2Salt(_l1Token));
```

[File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150)
```solidity
150:         bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""));
151:         bytes32 salt = _getCreate2Salt(_l1Token);
152:         return
153:             L2ContractHelper.computeCreate2Address(address(this), salt, l2TokenProxyBytecodeHash, constructorInputHash);
```

Variables `constructorInputHash` and `salt` are used only once, thus they are redundant. Above code can be changed to:

```
return
    L2ContractHelper.computeCreate2Address(address(this), _getCreate2Salt(_l1Token), l2TokenProxyBytecodeHash, keccak256(abi.encode(address(l2TokenBeacon), "")));
```


[File: code/system-contracts/contracts/libraries/EfficientCall.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L261)
```solidity
261:         uint32 shrinkTo = uint32(msg.data.length - (_data.length + dataOffset));
262:         SystemContractHelper.ptrShrinkIntoActive(shrinkTo);
263: 
264:         uint32 gas = Utils.safeCastToU32(_gas);
265:         uint256 farCallAbi = SystemContractsCaller.getFarCallABIWithEmptyFatPointer(
266:             gas,
```

`shrinkTo` and `gas` are used only once, thus there's no need to declare them at all:

```
        SystemContractHelper.ptrShrinkIntoActive(uint32(msg.data.length - (_data.length + dataOffset)));

        uint256 farCallAbi = SystemContractsCaller.getFarCallABIWithEmptyFatPointer(
            Utils.safeCastToU32(_gas),
```

[File: code/system-contracts/contracts/libraries/SystemContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L217)
```solidity
217:         uint256 shifted = (meta << (256 - size - offset));
218:         // Then we shift everything back
219:         result = (shifted >> (256 - size));
```

`shifted` is used only once, thus there's no need to declare this variable at all:

```
result = ((meta << (256 - size - offset)) >> (256 - size));
```

[File: code/system-contracts/contracts/NonceHolder.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L92)
```solidity
92:         uint256 addressAsKey = uint256(uint160(msg.sender));
93: 
94:         nonceValues[addressAsKey][_key] = _value;
```

`addressAsKey` is used only once, thus there's no need to declare this variable at all:

```
 nonceValues[uint256(uint160(msg.sender))][_key] = _value;
```


[File: code/system-contracts/contracts/NonceHolder.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L103)
```solidity
103:         uint256 addressAsKey = uint256(uint160(msg.sender));
104:         return nonceValues[addressAsKey][_key];
```

`addressAsKey` is used only once, thus there's no need to declare this variable at all:

```
 return nonceValues[uint256(uint160(msg.sender))][_key];
```

[File: code/system-contracts/contracts/KnownCodesStorage.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L75)
```solidity
75:         uint8 version = uint8(_bytecodeHash[0]);
76:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
```

`version` is used only once, thus there's no need to declare this variable at all:

```
require(uint8(_bytecodeHash[0]) == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
```


[File: code/system-contracts/contracts/DefaultAccount.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L099)
```solidity
099:         uint256 totalRequiredBalance = _transaction.totalRequiredBalance();
100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");
```

`totalRequiredBalance` is used only once, thus there's no need to declare this variable at all:

```
require(_transaction.totalRequiredBalance() <= address(this).balance, "Not enough balance for fee + value");
```


[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L121)
```solidity
121:         bytes32 hash = keccak256(
122:             bytes.concat(CREATE_PREFIX, bytes32(uint256(uint160(_sender))), bytes32(_senderNonce))
123:         );
124: 
125:         newAddress = address(uint160(uint256(hash)));
```

`hash` is used only once, thus there's no need to declare this variable at all:

```
newAddress = address(uint160(uint256(keccak256(bytes.concat(CREATE_PREFIX, bytes32(uint256(uint160(_sender))), bytes32(_senderNonce))))));
```


[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L302)
```solidity
302:         uint256 knownCodeMarker = KNOWN_CODE_STORAGE_CONTRACT.getMarker(_bytecodeHash);
303:         require(knownCodeMarker > 0, "The code hash is not known");
```

`knownCodeMarker` is used only once, thus there's no need to declare this variable at all:

```
require(KNOWN_CODE_STORAGE_CONTRACT.getMarker(_bytecodeHash) > 0, "The code hash is not known");
```


[File: code/system-contracts/contracts/Compressor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L65)
```solidity
65:                 uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);
66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);
67: 
68:                 require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");
```

`encodedChunk` and `realChunk` are used only once, thus there's no need to declare those variables at all:

```
require(dictionary.readUint64(indexOfEncodedChunk) == _bytecode.readUint64(encodedDataPointer * 4), "Encoded chunk does not match the original bytecode");
```


[File: code/system-contracts/contracts/AccountCodeStorage.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L60)
```solidity
60:         bytes32 constructedBytecodeHash = Utils.constructedBytecodeHash(codeHash);
61: 
62:         _storeCodeHash(_address, constructedBytecodeHash);
```

`constructedBytecodeHash` is used only once, thus there's no need to declare this variable at all:

```
_storeCodeHash(_address, Utils.constructedBytecodeHash(codeHash));
```


[File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L192)
```solidity
192:         uint256 selectorsLength = ds.facetToSelectors[_facet].selectors.length;
193:         // If there are no selectors associated with facet then save facet as new one
194:         if (selectorsLength == 0) {
```

`selectorsLength` is used only once, thus there's no need to declare this variable at all:

```
if (ds.facetToSelectors[_facet].selectors.length == 0) {
```


[File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L40)
```solidity
40:         uint8 version = uint8(_bytecodeHash[0]);
41:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash
```

`version` is used once, thus there's no need to declare this variable at all:

```
require(uint8(_bytecodeHash[0]) == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash
```


[File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L66)
```solidity
66:         bytes32 senderBytes = bytes32(uint256(uint160(_sender)));
67:         bytes32 data = keccak256(
68:             bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
69:         );
70: 
71:         return address(uint160(uint256(data)));
```

`senderBytes` and `data` are used once, thus there's no need to declare those variables:

```
return address(uint160(uint256( keccak256(
            bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, _constructorInputHash)
        ))));
```


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104)
```solidity
104:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
105:         require(
106:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107:             "StateTransition: cutHash mismatch"
108:         );
109: 
```

`cutHashInput` is used only once, thus there's no need to declare this variable at all:

```
        require(
            keccak256(abi.encode(_diamondCut)) == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
            "StateTransition: cutHash mismatch"
        );
```


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41)
```solidity
41:         uint256 amount = address(this).balance;
42:         address sharedBridgeAddress = s.baseTokenBridge;
43:         IL1SharedBridge(sharedBridgeAddress).receiveEth{value: amount}(ERA_CHAIN_ID);
```

`amount` and `sharedBridgeAddress` are used only once, thus there's no need to declare those variables at all:

```
IL1SharedBridge(s.baseTokenBridge).receiveEth{value: address(this).balance}(ERA_CHAIN_ID);
```


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L123)
```solidity
123:         bytes32 calculatedRootHash = Merkle.calculateRoot(_proof, _index, hashedLog);
124:         bytes32 actualRootHash = s.l2LogsRootHashes[_batchNumber];
125: 
126:         return actualRootHash == calculatedRootHash;
```

`calculatedRootHash` and `actualRootHash` are used only once, thus there's no need to declare those variables at all:

```
return Merkle.calculateRoot(_proof, _index, hashedLog) == s.l2LogsRootHashes[_batchNumber];
```


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L148)
```solidity
148:         uint256 l2GasPrice = _deriveL2GasPrice(_gasPrice, _l2GasPerPubdataByteLimit);
149:         return l2GasPrice * _l2GasLimit;
```

`l2GasPrice` is used only once, thus there's no need to declare this variable at all:

```
return _deriveL2GasPrice(_gasPrice, _l2GasPerPubdataByteLimit) * _l2GasLimit;;
```


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L271)
```solidity
271:         uint256 baseCost = _params.l2GasPrice * _params.l2GasLimit;
272:         require(_mintValue >= baseCost + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost
```

`baseCost` is used only once, thus there's no need to declare this variable at all:

```
require(_mintValue >= _params.l2GasPrice * _params.l2GasLimit + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost
```

[File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L160)
```solidity
160:             uint256 amount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _amount); // note if _prevMsgSender is this contract, this will return 0. This does not happen.
161:             require(amount == _amount, "3T"); // The token has non-standard transfer logic
```

`amount` is used only once, thus there's no need to declare this variable at all:

```
require(_depositFunds(_prevMsgSender, IERC20(_l1Token), _amount) == _amount, "3T"); // The token has non-standard transfer logic
```


[File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L205)
```solidity
205:             uint256 withdrawAmount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount);
206:             require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic
```

`withdrawAmount` is used only once, thus there's no need to declare this variable at all:

```
 require(_depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount) == _depositAmount, "5T"); // The token has non-standard transfer logic
```


[File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L340)
```solidity
340:                 bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
341:                 bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));
342:                 require(dataHash == txDataHash, "ShB: d.it not hap");
```

`dataHash` and `txDataHash` are used only once, thus there's no need to declare those variables at all:

```
require(depositHappened[_chainId][_l2TxHash] == keccak256(abi.encode(_depositSender, _l1Token, _amount)), "ShB: d.it not hap");
```

[File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76)
```solidity
76:         bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
77:         bytes32 salt = bytes32(uint256(uint160(_l1Token)));
78: 
79:         return L2ContractHelper.computeCreate2Address(l2Bridge, salt, l2TokenProxyBytecodeHash, constructorInputHash);
```

`constructorInputHash` and `salt` are used only once, thus there's no need to declare those variables at all:

```
return L2ContractHelper.computeCreate2Address(l2Bridge,  bytes32(uint256(uint160(_l1Token))), l2TokenProxyBytecodeHash, keccak256(abi.encode(l2TokenBeacon, "")));
```

# [46] Use `msg.value` directly, instead of assigning it to variable

**File:** `ContractDeployer.sol`

[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L329)
```solidity
329:         uint256 value = msg.value;
```

# [47] Storage values shouldn't be updated when value is not being changed

**Files:** `SystemContext.sol`, `Bridgehub.sol`, `ValidatorTimelock.sol`, `Governance.sol`, `StateTransitionManager.sol`, `Admin.sol`, `ContractDeployer.sol`

It's recommended to add additional `require` statement, which will verify if the value is really changed, before we will store it in the storage variables
E.g., let's consider a function `setChainId()` from `SystemContext.sol`. When `chainId` is `1` and we will call `setChainId(1)`, function will re-store the same value (Gsreset (900 gas)).


[File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L51)
```solidity
51:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
```

[File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108)
```solidity
108:     function setSharedBridge(address _sharedBridge) external onlyOwner {
```

[File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L132)
```solidity
132:     function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {
[...]
137:     function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {
[...]
142:     function setNewVersionUpgrade(
[...]
152:     function setUpgradeDiamondCut(
```


[File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L110)
```solidity
110:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
```

[File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L73)
```solidity
73:     function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {
```


[File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96)
```solidity
96:     function setExecutionDelay(uint32 _executionDelay) external onlyOwner { 
```


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79)
```solidity
79:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {
[...]
89:     function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {
```


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L45)
```solidity
45:     function setValidator(address _validator, bool _active) external onlyStateTransitionManager {
[...]
51:     function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {
[...]
58:     function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager { 
```


[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L84)
```solidity
84:     function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {
```


[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L099)
```solidity
099:     function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {
[...]
105:     function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {
[...]
112:     function setPubdataInfo(uint256 _gasPerPubdataByte, uint256 _basePubdataSpent) external onlyCallFromBootloader {
```


[File: code/contracts/ethereum/contracts/governance/Governance.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L249)
```solidity
249:     function updateDelay(uint256 _newDelay) external onlySelf {
[...]
256:     function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
```


[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L65)
```solidity
65:     function updateAccountVersion(AccountAbstractionVersion _version) external onlySystemCall {
```


[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L67)
```solidity
67:     function changeFeeParams(FeeParams calldata _newFeeParams) external onlyAdminOrStateTransitionManager {
```

# [AUTOMATED-FINDING-1] Using `bool`s for storage incurs overhead

Booleans are more expensive than uint256 or any type that takes up a full word because each write operation emits an extra SLOAD to first read the slot's contents, replace the bits taken up by the boolean, and then write back. This is the compiler's defense against contract upgrades and pointer aliasing, and it cannot be disabled.

Above code detects every instance of  mappings which utilizes boolean instead of uint
```
% grep "=>" -ri . | grep mapping | grep bool | wc -l                    
       9
```


# [AUTOMATED-FINDING-2] Mark constructor as payable

Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided. A constructor can safely be marked as payable, since only the deployer would be able to pass funds, and the project itself would not pass any funds.

```
% grep "constructor(" -ri . |  grep -v "//" | grep "{" | grep -v "payable" | grep -v "/test"  | wc -l
      16
```


# [AUTOMATED-FINDING-3] Functions guaranteed to revert when called by normal users can be marked `payable`

If a function modifier such as onlyOwner is used, the function will revert if a normal user tries to pay the function. Marking the function as payable will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided. 

```
% grep "function" -ri . |  grep -v "//" | grep "{" | grep "only" | grep -v "payable" | grep -v "/test" | grep only | wc -l
      64
```


# [AUTOMATED-FINDING-4] Index all 3 parameters in events

```
% grep "event " -ri . |  grep -v "//" | grep -v "/test" | grep ";" | grep -v indexed | grep -v "()" | wc -l
      19
```

Above detector identifies events which are not properly indexed.


# [AUTOMATED-FINDING-5] Nesting if-statements is cheaper than using &&

Nesting if-statements avoids the stack operations of setting up and using an extra jumpdest, and saves 6 gas. This basically means that: `if (A && B)` can be represented as `if (A) { if (B) }`.

```
% grep "if (" -r . | grep "&&" | grep -v "/test" | grep ".sol" | wc -l
       9
```


# [AUTOMATED-FINDING-6] Assembly: Use scratch space for calculating small keccak256 hashes

If the arguments to the encode call can fit into the scratch space (two words or fewer), then it's more efficient to use assembly to generate the hash (80 gas)

Below code detects only the instances where there's a single argument in `keccak256`.
```
% grep "keccak256(" -r . | grep ")" | grep -v "/test" | grep ".sol" | grep -v ":=" | grep -v "," | grep -v "//" | grep -v "constant" | wc -l
      17
```


# [AUTOMATED-FINDING-7] Assembly: Use scratch space when building emitted events with two data arguments

To efficiently emit events, it's possible to utilize assembly by making use of scratch space and the free memory pointer. This approach has the advantage of potentially avoiding the costs associated with memory expansion.

Below code detects only the instances where there's a single (or no) argument in the event.

```
% grep "emit " -r . | grep ")" | grep -v "/test" | grep ".sol" | grep -v "," | grep -v "//" | wc -l
      12
```


# [AUTOMATED-FINDING-8] `abi.encode()` is less efficient than `abi.encodePacked()`

```
% grep "abi.encode" -r . | grep -v "//" | grep -v "/test" | wc -l
      63
```


# [AUTOMATED-FINDING-9] `""` has the same value as `new bytes(0)` but costs less gas

```
% grep "new bytes(0)" -ri . | wc -l
      17
```

# [AUTOMATED-FINDING-10] Function names can be optimized to save gas

Function that are public/external and public state variable names can be optimized to save gas.

Method IDs that have two leading zero bytes can save 128 gas each during deployment, and renaming functions to have lower method IDs will save 22 gas per call, per sorted position shifted.

You can use the [Function Name Optimizer Tool](https://emn178.github.io/solidity-optimize-name/) to find new function names.


# [AUTOMATED-FINDING-11] Integer increments by one can be unchecked

```
% grep  "+= 1;" -r . | wc -l
       9
```


# [AUTOMATED-FINDING-12] Low-level call can be optimized with assembly

returnData is copied to memory even if the variable is not utilized: the proper way to handle this is through a low level assembly call and save 159 gas.

```
% grep "call{" -ri . | wc -l
      11
```


# [AUTOMATED-FINDING-13] Operator >=/<= costs less gas than operator >/<

The compiler uses opcodes GT and ISZERO for solidity code that uses >, but only requires LT for >=, which saves 3 gas. If < is being used, the condition can be inverted.

```
% grep -E "if \(|require\(" -r . | grep ">" | grep -v ">=" | grep ".sol" | wc -l
      42
```

```
% grep -E "if \(|require\(" -r . | grep "<" | grep -v "<=" | grep ".sol" | wc -l
      15
```


# [AUTOMATED-FINDING-14] Reduce deployment gas costs by fine-tuning IPFS file hashes

Solc currently by default appends the IPFS hash (in CID v0) of the canonical metadata file and the compiler version to the end of the bytecode. This value is variable-length CBOR-encoded i.e. it can be optimized in order to reduce deployment gas costs.



# [AUTOMATED-FINDING-15] Simple checks for zero can be done using assembly to save gas

Using assembly for simple zero checks on unsigned integers can save gas due to lower-level, optimized operations.

Below code returns only the simple `if` conditions without additional `&&` and `||` operators, such as: `if (A == 0)`

```
% grep "if (" -r . | grep -v "//" | grep -v "&&" | grep -v "||"  | grep " == 0)" | grep .sol | wc -l
      14
```

# [AUTOMATED-FINDING-16] Use assembly to validate msg.sender

We can use assembly to efficiently validate msg.sender with the least amount of opcodes necessary.

Below code returns only the simple `if` conditions without additional `&&` and `||` operators, such as: `if (msg.sender == 0)`

```
% grep -E "require|if \(" -r . | grep -v "//" | grep -v "&&" | grep -v "||"  | grep ")" | grep .sol | grep "msg.sender" | wc -l
      29
```


# [AUTOMATED-FINDING-17] Use assembly in place of abi.decode to save gas

Instead of using abi.decode, we can use assembly to decode our desired calldata values directly. This will allow us to avoid decoding calldata values that we will not use.

```
% grep "abi.decode" -r . | grep -v "//" | wc -l
      13
```


# [AUTOMATED-FINDING-18] Counting down in `for`-loop is more gas efficient

Counting down is more gas efficient than counting up because neither we are making zero variable to non-zero variable and also we will get gas refund in the last transaction when making non-zero to zero variable

```
% grep "for (" -r . | grep " = 0" | grep "++" | grep -v "/test" | grep ".sol" | wc -l
      18
```

# [AUTOMATED-FINDING-19] `do`-`while` is cheaper than `for`-loops when the initial check can be skipped

Using do-while loops instead of for loops can be more gas-efficient. Even if you add an if condition to account for the case where the loop doesn't execute at all, a do-while loop can still be cheaper in terms of gas.

```
% grep "for (" -r . | grep " = 0" | grep "++" | grep -v "/test" | grep ".sol" | wc -l
      18
```

# [AUTOMATED-FINDING-20]  Use direct `unchecked` block, instead of importing it from the library
Library `UncheckedMath.sol` implements a simple `uncheckedInc()` function which is responsible for performing unchecked incrementation. This function is used in multiple of loops in the code-base.
However, it's cheaper to use `unchecked` block directly, like that:

```
for (uint256 i = 0; i < length;) {
      ...
      unchecked {
            ++i;
      }
}
```

instead using imported function:

```
for (uint256 i = 0; i < length; i = i.uncheckedInc()) {
      ...
}
```

Below code detects the instances where `i.uncheckedInc()` is used inside the loops:

```
% grep "uncheckedInc()" -r . | grep "for (" | wc
      12     154    1772
```