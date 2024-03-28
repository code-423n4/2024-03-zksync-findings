**ZKSYNC GAS OPTIMIZATION REPORT**
INTRODUCTION
Highlighted below are optimizations exclusively targeting state-mutating functions and view/pure functions invoked by state-mutating functions. In the discussion that follows, only runtime gas is emphasized, given its inevitable dominance over deployment gas costs throughout the protocol's lifetime.

Please be aware that some code snippets may be shortened to conserve space, and certain code snippets may include @audit tags in comments to facilitate issue explanations."

## Gas Optimizations
1. [Re-arrange state variable order to save storage slots (Saves ~2000 Gas)](#g-01-re-arrange-state-variable-order-to-save-storage-slots-saves-2000-gas)
2. [Reorder struct variables and pack them together to save storage slots+(Gas Saved ~ 2000 Gas)](#g-02-reorder-struct-variables-and-pack-them-together-to-save-storage-slotsgas-saved--2000-gas)
3. [The result of a function call should be cached rather than re-calling the function](#g-03-the-result-of-a-function-call-should-be-cached-rather-than-re-calling-the-function)
4. [Mark variable as a constants](#g-04-mark-variable-as-a-constants)
5. [Avoiding unnecessary state variable emissions can save gas in Solidity](#g-05-avoiding-unnecessary-state-variable-emissions-can-save-gas-in-solidity)
6. [cache variable in local varibale reduce gas costs by minimizing redundant accesses to the array](#g-06-cache-variable-in-local-varibale-reduce-gas-costs-by-minimizing-redundant-accesses-to-the-array)
7. [No need to cache when used only once through out function](#g-07-no-need-to-cache-when-used-only-once-through-out-function)
8. [Caching the length of an array in a local variable can save gas](#g-08-caching-the-length-of-an-array-in-a-local-variable-can-save-gas)
9. [Use bytes32 instead of string for constant values can save gas in Solidity contracts](#g-09-use-bytes32-instead-of-string-for-constant-values-can-save-gas-in-solidity-contracts)
10. [State variables should be cached in stack variables rather than re-reading them from storage](#g-10-state-variables-should-be-cached-in-stack-variables-rather-than-re-reading-them-from-storage)
11. [ Use assembly for low level call](#g-11-use-assembly-for-low-level-call)
12. [Use storage instaed of memory when function visibility is external](#g-12-use-storage-instaed-of-memory-when-function-visibility-is-external)
13. [For Operations that will not overflow, you could use unchecked](#g-13-for-operations-that-will-not-overflow-you-could-use-unchecked)
14. [Do not cache global variable in local variable](#g-14-do-not-cache-global-variable-in-local-variable)
15. [No explicit increment operation is needed for numberOfLogsToProcess as it's done during assignment](#g-15-no-explicit-increment-operation-is-needed-for-numberoflogstoprocess-as-its-done-during-assignment)
16. [Check previous then update state variable](#g-16-check-previous-then-update-state-variable)
17. [](#gas-35-use--0-instead-of--0-for-unsigned-integer-comparison)
18. [Use preincrement instaed of state variable for increment](#g-18-use-preincrement-instaed-of-state-variable-for-increment)
19. [`abi.encode` is more efficient than `abi.encodePacked`](#gas-19-abiencode-is-more-efficient-than-abiencodepacked)
20. [With assembly, .call (bool success) transfer can be done gas-optimized](#gas-20-with-assembly-call-bool-success-transfer-can-be-done-gas-optimized)
21. [ Use assembly to emit events](#gas-21-use-assembly-to-emit-events)
22. [ Use assembly for small keccak256 hashes, in order to save gas](#gas-22-use-assembly-for-small-keccak256-hashes-in-order-to-save-gas)
23. [ Use uint256(1)/uint256(2) instead for true and false boolean states](#gas-23-use-uint2561uint2562-instead-for-true-and-false-boolean-states)
24. [<array>.length should not be looked up in every loop of a for-loop](#gas-24-length-should-not-be-looked-up-in-every-loop-of-a-for-loop)
25. [For Operations that will not overflow, you could use unchecked](#gas-26-dont-compare-boolean-expressions-to-boolean-literals)
26. [Don't compare boolean expressions to boolean literals](#gas-26-dont-compare-boolean-expressions-to-boolean-literals)
27. [ Multiplication/division by two should use bit shifting](#gas-27-multiplicationdivision-by-two-should-use-bit-shifting)
28. [>=/ <= costs less gas than >/<](#gas-28---costs-less-gas-than)
29. [Use hardcode address instead of address(this) ](#gas-29-use-hardcode-address-instead-of-addressthis)
30. [Don't initialize variables with default value](#gas-30-dont-initialize-variables-with-default-value)
31. [ Long revert strings](#gas-31-long-revert-strings)
32. [Constructors can be marked payable](#gas-32-constructors-can-be-marked-payable)
33. [Use shift Right/Left instead of division/multiplication if possible](#gas-33-use-shift-rightleft-instead-of-divisionmultiplication-if-possible)
34. [ Using this to access functions results in an external call, wasting gas](#gas-34-using-this-to-access-functions-results-in-an-external-call-wasting-gas)



## Note: Sorted by gas savings, I have placed the findings with the greatest impact at the top of this report

## [G-01] Re-arrange state variable order to save storage slots (Saves ~2000 Gas)

### Details
In first instances  `txNumberInBlock` we can re-arrange `origin` state variable
### Proof of Code
- [SystemContext.sol#L89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L89)
```solidity
File: system-contracts/contracts/SystemContext.sol
89:  uint16 public txNumberInBlock; //@audit pack state avriable

    /// @notice The current gas per pubdata byte
    uint256 public gasPerPubdataByte;
```
### Optimized code:

```diff
diff --git a/code/system-contracts/contracts/SystemContext.sol b/code/system-contracts/contracts/SystemContext.sol
index 3d0a972..8c33352 100644
--- a/code/system-contracts/contracts/SystemContext.sol
+++ b/code/system-contracts/contracts/SystemContext.sol
@@ -29,6 +29,9 @@ contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContr
     /// @dev It is updated before each transaction by the bootloader
     address public origin;
 
+    /// @notice Number of current transaction in block.
+    uint16 public txNumberInBlock;
+
     /// @notice The `tx.gasPrice` in the current transaction.
     /// @dev It is updated before each transaction by the bootloader
     uint256 public gasPrice;
@@ -85,9 +88,6 @@ contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContr
         chainId = _newChainId;
     }
 
-    /// @notice Number of current transaction in block.
-    uint16 public txNumberInBlock;
-
     /// @notice The current gas per pubdata byte
     uint256 public gasPerPubdataByte;
```
## [G-02] Reorder struct variables and pack them together to save storage slots+(Gas Saved ~ 2000 Gas)

### Details
In contract  `zkPorterIsAvailable` we can re-arrange `blocSyncTh__DEPRECATED_pendingGovernorreshold` struct variable save 1 slot

### Details

### Proof of Code
- [ZkSyncStateTransitionStorage.sol#L103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L103)
```solidity
File: state-transition/chain-deps/ZkSyncStateTransitionStorage.sol
101:/// @dev Indicates that the porter may be touched on L2 transactions.
    /// @dev Used as an input to zkp-circuit.
    bool zkPorterIsAvailable; //@audit
```
### Optimized code:

```diff
diff --git a/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol b/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol
index 4beec8f..8a6be96 100644
--- a/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol
+++ b/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol
@@ -71,6 +71,9 @@ struct ZkSyncStateTransitionStorage {
     /// @notice Address that the governor proposed as one that will replace it
     address __DEPRECATED_pendingGovernor;
     /// @notice List of permitted validators
+    /// @dev Indicates that the porter may be touched on L2 transactions.
+    /// @dev Used as an input to zkp-circuit.
+    bool zkPorterIsAvailable;
     mapping(address validatorAddress => bool isValidator) validators;
     /// @dev Verifier contract. Used to verify aggregated proof for batches
     IVerifier verifier;
@@ -98,9 +101,6 @@ struct ZkSyncStateTransitionStorage {
     /// @notice Bytecode hash of default account (bytecode for EOA).
```
## [G-03] The result of a function call should be cached rather than re-calling the function

### Details
The function calls in solidity are expensive. If the same result of the same function calls are to be used several times, the result should be cached to reduce the gas consumption of repeated calls.

### Proof of Code
- [GasBoundCaller.sol#L40C7-L46C68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L40C7-L46C68)
```solidity
File: system-contracts/contracts/GasBoundCaller.sol
35: function gasBoundCall(address _to, uint256 _maxTotalGas, bytes calldata _data) external payable {
        // At the start of the execution we deduce how much gas be spent on things that will be
        // paid for later on by the transaction.
        // The `expectedForCompute` variable is an upper bound of how much this contract can spend on compute and
        // MUST be higher or equal to the `gas` passed into the call.
        uint256 expectedForCompute = gasleft() + CALL_ENTRY_OVERHEAD; //@audit cache gasleft()

        // We expect that the `_maxTotalGas` at least includes the `gas` required for the call.
        // This require is more of a safety protection for the users that call this function with incorrect parameters.
        //
        // Ultimately, the entire `gas` sent to this call can be spent on compute regardless of the `_maxTotalGas` parameter.
        require(_maxTotalGas >= gasleft(), "Gas limit is too low");

        // This is the amount of gas that can be spent *exclusively* on pubdata in addition to the `gas` provided to this function.
        uint256 pubdataAllowance = _maxTotalGas > expectedForCompute ? _maxTotalGas - expectedForCompute : 0;

        uint256 pubdataPublishedBefore = REAL_SYSTEM_CONTEXT_CONTRACT.getCurrentPubdataSpent();
```
### Optimized code:

```diff
diff --git a/code/system-contracts/contracts/GasBoundCaller.sol b/code/system-contracts/contracts/GasBoundCaller.sol
index 5a177aa..0858e5f 100644
--- a/code/system-contracts/contracts/GasBoundCaller.sol
+++ b/code/system-contracts/contracts/GasBoundCaller.sol
@@ -37,13 +37,14 @@ contract GasBoundCaller {
         // paid for later on by the transaction.
         // The `expectedForCompute` variable is an upper bound of how much this contract can spend on compute and
         // MUST be higher or equal to the `gas` passed into the call.
-        uint256 expectedForCompute = gasleft() + CALL_ENTRY_OVERHEAD;
+        uint256 _gasleft = gasleft();
+        uint256 expectedForCompute = _gasleft + CALL_ENTRY_OVERHEAD;
 
         // We expect that the `_maxTotalGas` at least includes the `gas` required for the call.
         // This require is more of a safety protection for the users that call this function with incorrect parameters.
         //
         // Ultimately, the entire `gas` sent to this call can be spent on compute regardless of the `_maxTotalGas` parameter.
-        require(_maxTotalGas >= gasleft(), "Gas limit is too low");
+        require(_maxTotalGas >= _gasleft, "Gas limit is too low");
 
         // This is the amount of gas that can be spent *exclusively* on pubdata in addition to the `gas` provided to this function.
         uint256 pubdataAllowance = _maxTotalGas > expectedForCompute ? _maxTotalGas - expectedForCompute : 0;
```
### Instances - 2 
- [ValidatorTimelock.sol#L182C3-L196C14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L182C3-L196C14)
```solidity
File: state-transition/ValidatorTimelock.sol
182:  function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {
        uint256 delay = executionDelay; // uint32
        unchecked {
            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
                    _newBatchesData[i].batchNumber
                );

                // Note: if the `commitBatchTimestamp` is zero, that means either:
                // * The batch was committed, but not through this contract.
                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
                // We allow executing such batches.

                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed //@audit cache uint32 timestamp = uint32(block.timestamp);
            }
        }
        _propagateToZkSyncStateTransition(ERA_CHAIN_ID);
    }
```
### Optimized code:

```diff
diff --git a/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol b/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
index 944e7cb..06d4cd6 100644
--- a/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
+++ b/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
@@ -181,6 +181,7 @@ contract ValidatorTimelock is IExecutor, Ownable2Step {
     /// make a call to the hyperchain diamond contract with the same calldata.
     function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {
         uint256 delay = executionDelay; // uint32
+        uint32 timestamp = uint32(block.timestamp);
         unchecked {
             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                 uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
@@ -192,7 +193,7 @@ contract ValidatorTimelock is IExecutor, Ownable2Step {
                 // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
                 // We allow executing such batches.
 
-                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
+                require(timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
             }
         }
         _propagateToZkSyncStateTransition(ERA_CHAIN_ID);
``` 
### Instances - 3

### Proof of Code
- [ValidatorTimelock.sol#L203C3-L222C1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L203C3-L222C1)
```solidity
File: state-transition/ValidatorTimelock.sol
204:  function executeBatchesSharedBridge(
        uint256 _chainId,
        StoredBatchInfo[] calldata _newBatchesData
    ) external onlyValidator(_chainId) {
        uint256 delay = executionDelay; // uint32
        unchecked {
            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);

                // Note: if the `commitBatchTimestamp` is zero, that means either:
                // * The batch was committed, but not through this contract.
                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
                // We allow executing such batches.

                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed //@audit uint32 timestamp = uint32(block.timestamp);
            }
        }
        _propagateToZkSyncStateTransition(_chainId);
    }
```
### Optimized code:

```diff
diff --git a/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol b/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
index 944e7cb..06d4cd6 100644
--- a/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
+++ b/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
@@ -205,6 +206,7 @@ contract ValidatorTimelock is IExecutor, Ownable2Step {
         StoredBatchInfo[] calldata _newBatchesData
     ) external onlyValidator(_chainId) {
         uint256 delay = executionDelay; // uint32
+        uint32 timestamp = uint32(block.timestamp);
         unchecked {
             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                 uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
@@ -214,7 +216,7 @@ contract ValidatorTimelock is IExecutor, Ownable2Step {
                 // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
                 // We allow executing such batches.
 
-                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
+                require(timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
             }
         }
         _propagateToZkSyncStateTransition(_chainId);
```
## [G-04] Mark variable as a constants

### Details
Mark as constant because When you declare a variable as constant, Solidity replaces all occurrences of that variable with its value at compile time.
### Proof of Code
- [SystemContext.sol#L44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L44)
```solidity
File: code/system-contracts/contracts/SystemContext.sol
43: /// @notice Formal `block.difficulty` parameter.
44:    uint256 public difficulty = 2.5e15; //@audit mark constant
```
## [G-05] Avoiding unnecessary state variable emissions can save gas in Solidity

### Details
When we emit an event in Solidity, it consumes gas. Emitting an event involves writing log data to the Ethereum blockchain, which requires computation and storage resources.
### Proof of Code
- [Bridgehub.sol#L60C1-L70C6](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L60C1-L70C6)
```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol
60: function acceptAdmin() external {
        address currentPendingAdmin = pendingAdmin;
        require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

        address previousAdmin = admin;
        admin = currentPendingAdmin;
        delete pendingAdmin;

        emit NewPendingAdmin(currentPendingAdmin, address(0));
        emit NewAdmin(previousAdmin, pendingAdmin); //@audit do not emit state variable
    }
```
### Optimized code:

```diff
60: function acceptAdmin() external {
        address currentPendingAdmin = pendingAdmin;
        require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

        address previousAdmin = admin;
        admin = currentPendingAdmin;
        delete pendingAdmin;

        emit NewPendingAdmin(currentPendingAdmin, address(0));
-        emit NewAdmin(previousAdmin, pendingAdmin); 
+        emit NewAdmin(previousAdmin,currentPendingAdmin); 
    }
```
### Instances - 2

### Proof of Code
- [StateTransitionManager.sol#L119C5-L130C1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L119C5-L130C1)
```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
119: function acceptAdmin() external {
        address currentPendingAdmin = pendingAdmin;
        require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

        address previousAdmin = admin;
        admin = currentPendingAdmin;
        delete pendingAdmin;

        emit NewPendingAdmin(currentPendingAdmin, address(0));
        emit NewAdmin(previousAdmin, pendingAdmin); //@audit do not emit state variable
    }
```
### Optimized code:

```diff
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
119: function acceptAdmin() external {
        address currentPendingAdmin = pendingAdmin;
        require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

        address previousAdmin = admin;
        admin = currentPendingAdmin;
        delete pendingAdmin;

-        emit NewPendingAdmin(currentPendingAdmin, address(0));
+        emit NewAdmin(previousAdmin, currentPendingAdmin);
    }
```

## [G-06] cache variable in local varibale reduce gas costs by minimizing redundant accesses to the array

### Instances - 1
cache `_deployments[i]` in local varibale instead avoid fetch repeatly
### Proof of Code
- [ContractDeployer.sol#L238C2-L258C18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L238C2-L258C18)
```solidity
File: code/system-contracts/contracts/ContractDeployer.sol
238:     function forceDeployOnAddresses(ForceDeployment[] calldata _deployments) external payable {
        require(
            msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
            "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
        );

        uint256 deploymentsLength = _deployments.length;
        // We need to ensure that the `value` provided by the call is enough to provide `value`
        // for all of the deployments
        uint256 sumOfValues = 0;
        for (uint256 i = 0; i < deploymentsLength; ++i) {
            sumOfValues += _deployments[i].value; //@audit cache value
        }
        require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");

        for (uint256 i = 0; i < deploymentsLength; ++i) {
            this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender); //@audit cache deployment[i]
        }
    }
```
### Optimized code:

```diff
diff --git a/code/system-contracts/contracts/ContractDeployer.sol b/code/system-contracts/contracts/ContractDeployer.sol
index 5d85f40..04dbfb9 100644
--- a/code/system-contracts/contracts/ContractDeployer.sol
+++ b/code/system-contracts/contracts/ContractDeployer.sol
@@ -72,7 +72,7 @@ contract ContractDeployer is IContractDeployer, ISystemContract {
     /// it only allows changes from sequential to arbitrary ordering.
     /// @param _nonceOrdering The new nonce ordering to use.
     function updateNonceOrdering(AccountNonceOrdering _nonceOrdering) external onlySystemCall {
-        AccountInfo memory currentInfo = accountInfo[msg.sender];
+        AccountInfo memory currentInfo = accountInfo[msg.sender];
 
         require(
             _nonceOrdering == AccountNonceOrdering.Arbitrary &&
@@ -246,12 +246,14 @@ contract ContractDeployer is IContractDeployer, ISystemContract {
         // for all of the deployments
         uint256 sumOfValues = 0;
         for (uint256 i = 0; i < deploymentsLength; ++i) {
-            sumOfValues += _deployments[i].value;
+            uint256 deployments= _deployments[i];
+            sumOfValues += deployments.value;
         }
         require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");
 
         for (uint256 i = 0; i < deploymentsLength; ++i) {
-            this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
+            uint256 deployments= _deployments[i];
+            this.forceDeployOnAddress{value: deployments.value}(deployments, msg.sender);
         }
     }
```
## [G-07] No need to cache when used only once through out function

### Details
Caching a variable in memory is useful when you need to access it multiple times within a function.If varibale use once then directly accessing the variable or value is more efficient and concise.

In the setL2Block function, the currentBatchInfo.timestamp variable is used only once, and caching it in memory might not offer significant benefits unless it's reused multiple times within the same function or if its computation is costly.
### Proof of Code
- [SystemContext.sol#L341C4-L366C30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L341C4-L366C30)
```solidity
File: system-contracts/contracts/SystemContext.sol
341: function setL2Block(
        uint128 _l2BlockNumber,
        uint128 _l2BlockTimestamp,
        bytes32 _expectedPrevL2BlockHash,
        bool _isFirstInBatch,
        uint128 _maxVirtualBlocksToCreate
    ) external onlyCallFromBootloader {
        // We check that the timestamp of the L2 block is consistent with the timestamp of the batch.
        if (_isFirstInBatch) {
            uint128 currentBatchTimestamp = currentBatchInfo.timestamp; //@audit do not cache
            require(
                _l2BlockTimestamp >= currentBatchTimestamp,
                "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
            );
            require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");
        }
```
### Optimized code:

```diff
diff --git a/code/system-contracts/contracts/SystemContext.sol b/code/system-contracts/contracts/SystemContext.sol
index 3d0a972..579b364 100644
--- a/code/system-contracts/contracts/SystemContext.sol
+++ b/code/system-contracts/contracts/SystemContext.sol
@@ -347,9 +347,8 @@ contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContr
     ) external onlyCallFromBootloader {
         // We check that the timestamp of the L2 block is consistent with the timestamp of the batch.
         if (_isFirstInBatch) {
-            uint128 currentBatchTimestamp = currentBatchInfo.timestamp;
             require(
-                _l2BlockTimestamp >= currentBatchTimestamp,
+                _l2BlockTimestamp >= currentBatchInfo.timestamp,
                 "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
             );
             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");
```
## [G-08] Caching the length of an array in a local variable can save gas 

### Details
In Solidity, accessing the length of an array inside a loop condition or during iteration can result in an SLOAD operation, which consumes gas. By caching the length of the array in a local variable, you avoid this repeated SLOAD operation, potentially saving gas.
### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L501

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
501:  // So the data is expected to be at least 56 bytes long.
        require(_l2ToL1message.length >= 56, "ShB wrong msg len"); // wrong messsage length  //@audit cache length 

        (uint32 functionSignature, uint256 offset) = UnsafeBytes.readUint32(_l2ToL1message, 0);
        if (bytes4(functionSignature) == IMailbox.finalizeEthWithdrawal.selector) {
            // this message is a base token withdrawal
            (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
            (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);
            l1Token = bridgehub.baseToken(_chainId);
        } else if (bytes4(functionSignature) == IL1ERC20Bridge.finalizeWithdrawal.selector) {
            // We use the IL1ERC20Bridge for backward compatibility with old withdrawals.

            // this message is a token withdrawal

            // Check that the message length is correct.
            // It should be equal to the length of the function signature + address + address + uint256 = 4 + 20 + 20 + 32 =
            // 76 (bytes).
            require(_l2ToL1message.length == 76, "ShB wrong msg len 2");

```
### Instances - 2

### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L51C10-L59C15

```solidity
File: code/system-contracts/contracts/Compressor.sol
44: function publishCompressedBytecode(
        bytes calldata _bytecode,
        bytes calldata _rawCompressedData
    ) external payable onlyCallFromBootloader returns (bytes32 bytecodeHash) {
        unchecked {
            (bytes calldata dictionary, bytes calldata encodedData) = _decodeRawBytecode(_rawCompressedData);

            require(
                encodedData.length * 4 == _bytecode.length,
                "Encoded data length should be 4 times shorter than the original bytecode"
            );

            require(
                dictionary.length / 8 <= encodedData.length / 2,//@audit cache length
                "Dictionary should have at most the same number of entries as the encoded data"
            );

            for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
                uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
                require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

                uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);
                uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

                require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");
            }
        }

        bytecodeHash = Utils.hashL2Bytecode(_bytecode);
        L1_MESSENGER_CONTRACT.sendToL1(_rawCompressedData);
        KNOWN_CODE_STORAGE_CONTRACT.markBytecodeAsPublished(bytecodeHash);
    }
```
### Optimized code:

```diff
diff --git a/code/system-contracts/contracts/Compressor.sol b/code/system-contracts/contracts/Compressor.sol
index 9830f92..9f168f1 100644
--- a/code/system-contracts/contracts/Compressor.sol
+++ b/code/system-contracts/contracts/Compressor.sol
@@ -47,20 +47,21 @@ contract Compressor is ICompressor, ISystemContract {
     ) external payable onlyCallFromBootloader returns (bytes32 bytecodeHash) {
         unchecked {
             (bytes calldata dictionary, bytes calldata encodedData) = _decodeRawBytecode(_rawCompressedData);
-
+            uint256 encodedDataLength = encodedData.length;
+            uint256 dictionaryLength = dictionary.length ;
             require(
-                encodedData.length * 4 == _bytecode.length,
+                encodedDataLength * 4 == _bytecode.length,
                 "Encoded data length should be 4 times shorter than the original bytecode"
             );
 
             require(
-                dictionary.length / 8 <= encodedData.length / 2,
+                dictionaryLength / 8 <= encodedDataLength / 2,
                 "Dictionary should have at most the same number of entries as the encoded data"
             );
 
-            for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
+            for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedDataLength; encodedDataPointer += 2) {
                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
-                require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");
+                require(indexOfEncodedChunk < dictionaryLength, "Encoded chunk index is out of bounds");
 
                 uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);
                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);
```
### Instances - 3

### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L223C8-L232C6
```solidity
File: contracts/upgrades/BaseZkSyncUpgrade.sol
222:     function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure {
        require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");
        require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32"); //@audit may be we can cache length

        for (uint256 i = 0; i < _factoryDeps.length; ++i) {
            require(
                L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
                "Wrong factory dep hash"
            );
        }
    }
```
### Optimized code:

```diff
diff --git a/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol b/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
index ccdec34..951407b 100644
--- a/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
+++ b/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
@@ -220,10 +220,11 @@ abstract contract BaseZkSyncUpgrade is ZkSyncStateTransitionBase {
     /// @param _factoryDeps The list of factory deps
     /// @param _expectedHashes The list of expected bytecode hashes
     function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure {
-        require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");
-        require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");
+        uint256 factoryDeps_ = _factoryDeps.length;
+        require(factoryDeps_== _expectedHashes.length, "Wrong number of factory deps");
+        require(factoryDeps_ <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");
 
-        for (uint256 i = 0; i < _factoryDeps.length; ++i) {
+        for (uint256 i = 0; i < factoryDeps_; ++i) {
             require(
                 L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
                 "Wrong factory dep hash"
```
## [G-09] Use bytes32 instead of string for constant values can save gas in Solidity contracts.

### Details
Storing a bytes32 variable costs 20,000 gas (32 bytes * 200 gas per storage slot). In contrast, storing a string variable incurs additional gas proportional to the string's length, typically around 20,000 gas plus 5,000 gas per 256 bits (8 bytes) of string length.

### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26
```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
25: /// @dev Part of the IBase interface. Not used in this contract.
    string public constant override getName = "ValidatorTimelock"; //@audit use bytes32
```
## [G-10] State variables should be cached in stack variables rather than re-reading them from storage

### Details
caching state variables in local variables (stack variables) rather than re-reading them from storage can save gas in Solidity contracts. When you read a state variable from storage, it incurs gas costs because it involves an SSTORE or SLOAD operation, which are relatively expensive operations in terms of gas consumption.

### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L117C5-L120C6

```solidity
File: code/system-contracts/contracts/SystemContext.sol
117:     function getCurrentPubdataSpent() public view returns (uint256) {
        uint256 pubdataPublished = SystemContractHelper.getZkSyncMeta().pubdataPublished;
        return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0; //@audit cache basePubdataSpent
    }
```
### Optimized code:

```diff
diff --git a/code/system-contracts/contracts/SystemContext.sol b/code/system-contracts/contracts/SystemContext.sol
index 3d0a972..591b69c 100644
--- a/code/system-contracts/contracts/SystemContext.sol
+++ b/code/system-contracts/contracts/SystemContext.sol
@@ -86,7 +86,7 @@ contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContr
     }
 
     /// @notice Number of current transaction in block.
-    uint16 public txNumberInBlock;
+    uint16 public txNumberInBlock;
 
     /// @notice The current gas per pubdata byte
     uint256 public gasPerPubdataByte;
@@ -116,7 +116,8 @@ contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContr
 
     function getCurrentPubdataSpent() public view returns (uint256) {
         uint256 pubdataPublished = SystemContractHelper.getZkSyncMeta().pubdataPublished;
-        return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;
+        uint256 _basePubdataSpent = basePubdataSpent;
+        return pubdataPublished > _basePubdataSpent ? pubdataPublished - _basePubdataSpent : 0;
     }
```
### Instances -2

### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L277C4-L292C20

```solidity
File: system-contracts/contracts/SystemContext.sol
263: function _setVirtualBlock(
        uint128 _l2BlockNumber,
        uint128 _maxVirtualBlocksToCreate,
        uint128 _newTimestamp
    ) internal {
        if (virtualBlockUpgradeInfo.virtualBlockFinishL2Block != 0) {
            // No need to to do anything about virtual blocks anymore
            // All the info is the same as for L2 blocks.
            currentVirtualL2BlockInfo = currentL2BlockInfo;
            return;
        }

        BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;

        if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) { //@audit use memory variable instead of state variable
            uint128 currentBatchNumber = currentBatchInfo.number;

            // The virtual block is set for the first time. We can count it as 1 creation of a virtual block.
            // Note, that when setting the virtual block number we use the batch number to make a smoother upgrade from batch number to
            // the L2 block number.
            virtualBlockInfo.number = currentBatchNumber;
            // Remembering the batch number on which the upgrade to the virtual blocks has been done.
            virtualBlockUpgradeInfo.virtualBlockStartBatch = currentBatchNumber;

            require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");
            _maxVirtualBlocksToCreate -= 1;
        } else if (_maxVirtualBlocksToCreate == 0) {
            // The virtual blocks have been already initialized, but the operator didn't ask to create
            // any new virtual blocks. So we can just return.
            return;
        }

```
### Optimized code:

```diff
diff --git a/code/system-contracts/contracts/SystemContext.sol b/code/system-contracts/contracts/SystemContext.sol
index 3d0a972..c2d7e73 100644
--- a/code/system-contracts/contracts/SystemContext.sol
+++ b/code/system-contracts/contracts/SystemContext.sol
@@ -274,7 +274,7 @@ contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContr
 
         BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;
 
-        if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
+        if (virtualBlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
             uint128 currentBatchNumber = currentBatchInfo.number;
 
             // The virtual block is set for the first time. We can count it as 1 creation of a virtual block.
```

### Instances - 3

### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L122C6-L144C1

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol
114:   function createNewChain(
        uint256 _chainId,
        address _stateTransitionManager,
        address _baseToken,
        uint256, //_salt
        address _admin,
        bytes calldata _initData
    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
        require(_chainId != 0, "Bridgehub: chainId cannot be 0");
        require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");

        require(
            stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition not registered"
        );
        require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");
        require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

        require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

        stateTransitionManager[_chainId] = _stateTransitionManager;
        baseToken[_chainId] = _baseToken;

        IStateTransitionManager(_stateTransitionManager).createNewChain(
            _chainId,
            _baseToken,
            address(sharedBridge), //@audit cache state variable
            _admin,
            _initData
        );

        emit NewChain(_chainId, _stateTransitionManager, _admin);
        return _chainId;
    }
```
### Optimized code:

```diff
diff --git a/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol b/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol
index 201b42f..533a9c8 100644
--- a/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol
+++ b/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol
@@ -127,7 +127,8 @@ contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
             "Bridgehub: state transition not registered"
         );
         require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");
-        require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
+        address _sharedBridge = address(sharedBridge);
+        require(_sharedBridge != address(0), "Bridgehub: weth bridge not set");
 
         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");
 
@@ -137,7 +138,7 @@ contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
         IStateTransitionManager(_stateTransitionManager).createNewChain(
             _chainId,
             _baseToken,
-            address(sharedBridge),
+            _sharedBridge,
             _admin,
             _initData
         );
```
## [G-11] Use assembly for low level call

### Details
Using assembly for low-level calls can sometimes save gas compared to using Solidity's high-level abstraction. 
### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L131C3-L151C15

```solidity
File: system-contracts/contracts/DefaultAccount.sol
131: function _execute(Transaction calldata _transaction) internal {
        address to = address(uint160(_transaction.to));
        uint128 value = Utils.safeCastToU128(_transaction.value);
        bytes calldata data = _transaction.data;
        uint32 gas = Utils.safeCastToU32(gasleft());

        // Note, that the deployment method from the deployer contract can only be called with a "systemCall" flag.
        bool isSystemCall;
        if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) {
            bytes4 selector = bytes4(data[:4]);
            // Check that called function is the deployment method,
            // the others deployer method is not supposed to be called from the default account.
            isSystemCall =
                selector == DEPLOYER_SYSTEM_CONTRACT.create.selector ||
                selector == DEPLOYER_SYSTEM_CONTRACT.create2.selector ||
                selector == DEPLOYER_SYSTEM_CONTRACT.createAccount.selector ||
                selector == DEPLOYER_SYSTEM_CONTRACT.create2Account.selector;
        }
        bool success = EfficientCall.rawCall(gas, to, value, data, isSystemCall); //@audit use assembly
        if (!success) {
            EfficientCall.propagateRevert();
        }
    }       
```
### Optimized code:

```diff
diff --git a/code/system-contracts/contracts/DefaultAccount.sol b/code/system-contracts/contracts/DefaultAccount.sol
index 2257269..0057324 100644
--- a/code/system-contracts/contracts/DefaultAccount.sol
+++ b/code/system-contracts/contracts/DefaultAccount.sol
@@ -137,7 +137,10 @@ contract DefaultAccount is IAccount {
         // Note, that the deployment method from the deployer contract can only be called with a "systemCall" flag.
         bool isSystemCall;
         if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) {
-            bytes4 selector = bytes4(data[:4]);
+            bytes4 selector 
+            assembly {
+            selector := mload(add(data, 0x20))
+           }
             // Check that called function is the deployment method,
             // the others deployer method is not supposed to be called from the default account.
             isSystemCall =
@@ -146,7 +149,11 @@ contract DefaultAccount is IAccount {
                 selector == DEPLOYER_SYSTEM_CONTRACT.createAccount.selector ||
                 selector == DEPLOYER_SYSTEM_CONTRACT.create2Account.selector;
         }
-        bool success = EfficientCall.rawCall(gas, to, value, data, isSystemCall);
+        bool success;
+        assembly {
+        success := call(gas, to, value, add(data, 0x20), mload(data), 0, 0)
+        }
+
         if (!success) {
             EfficientCall.propagateRevert();
         }
```
## [G-12] Use storage instaed of memory when function visibility is external 

### Details
using arrays as function parameters with the external visibility specifier and passing them by reference (using memory keyword) can save gas compared to passing arrays by value (using calldata keyword), especially for large arrays.
### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L75

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol
74: function updateNonceOrdering(AccountNonceOrdering _nonceOrdering) external onlySystemCall {
        AccountInfo memory currentInfo = accountInfo[msg.sender]; //@audit use storage

        require(
            _nonceOrdering == AccountNonceOrdering.Arbitrary &&
                currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
            "It is only possible to change from sequential to arbitrary ordering"
        );

        currentInfo.nonceOrdering = _nonceOrdering;
        _storeAccountInfo(msg.sender, currentInfo);

        emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);
    }
```
### Optimized code:

```diff
74: function updateNonceOrdering(AccountNonceOrdering _nonceOrdering) external onlySystemCall {
-        AccountInfo memory currentInfo = accountInfo[msg.sender];
+        AccountInfo storage currentInfo = accountInfo[msg.sender];

        require(
            _nonceOrdering == AccountNonceOrdering.Arbitrary &&
                currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
            "It is only possible to change from sequential to arbitrary ordering"
        );

        currentInfo.nonceOrdering = _nonceOrdering;
        _storeAccountInfo(msg.sender, currentInfo);

        emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);
    }
```

### Instances -2

### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L27

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol
20:  fallback() external payable {
        Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
        // Check whether the data contains a "full" selector or it is empty.
        // Required because Diamond proxy finds a facet by function signature,
        // which is not defined for data length in range [1, 3].
        require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
        // Get facet from function selector
        Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig]; //@audit use storage 
        address facetAddress = facet.facetAddress;

        require(facetAddress != address(0), "F"); // Proxy has no facet for this selector
        require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen

```
### Optimized code:

```diff
20:  fallback() external payable {
        Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
        // Check whether the data contains a "full" selector or it is empty.
        // Required because Diamond proxy finds a facet by function signature,
        // which is not defined for data length in range [1, 3].
        require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
        // Get facet from function selector
-        Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];
+        Diamond.SelectorToFacet storage facet = diamondStorage.selectorToFacet[msg.sig];
        address facetAddress = facet.facetAddress;

        require(facetAddress != address(0), "F"); // Proxy has no facet for this selector
        require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen
```
## [G-13] For Operations that will not overflow, you could use unchecked

### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L347C9-L351C10

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
347:         if (!hyperbridgingEnabled[_chainId]) { //@audit unchecked
            // check that the chain has sufficient balance
            require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
            chainBalance[_chainId][_l1Token] -= _amount;
        }
```
### Instances - 2

### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L436C1-L441C10

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
437:   if (!hyperbridgingEnabled[_chainId]) {
            // Check that the chain has sufficient balance
            require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds //@auidt cache multiple error
            chainBalance[_chainId][l1Token] -= amount; //@audit unchecked
        }
```
## [G-14] Do not cache global variable in local variable

### Details
caching global variable in local variable is more gas consuming compare to use global variable itself
### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L329

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol
331:    uint256 value = msg.value; //@audit do not cache global value
```
## [G-15] No explicit increment operation is needed for numberOfLogsToProcess as it's done during assignment

### Details
The numberOfLogsToProcess counter is updated after assigning its value to logIdInMerkleTree.

### Proof of Code
No explicit increment operation is needed for numberOfLogsToProcess as it's done during assignment
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L109

```solidity
File: system-contracts/contracts/L1Messenger.sol
94:   function _processL2ToL1Log(L2ToL1Log memory _l2ToL1Log) internal returns (uint256 logIdInMerkleTree) {
        bytes32 hashedLog = keccak256(
            abi.encodePacked(
                _l2ToL1Log.l2ShardId,
                _l2ToL1Log.isService,
                _l2ToL1Log.txNumberInBlock,
                _l2ToL1Log.sender,
                _l2ToL1Log.key,
                _l2ToL1Log.value
            )
        );

        chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

        logIdInMerkleTree = numberOfLogsToProcess;
        numberOfLogsToProcess++; //@audit update after assign

        emit L2ToL1LogSent(_l2ToL1Log);
    }   
```
### Optimized code:

```diff
diff --git a/code/system-contracts/contracts/L1Messenger.sol b/code/system-contracts/contracts/L1Messenger.sol
index cda2c68..43e5a52 100644
--- a/code/system-contracts/contracts/L1Messenger.sol
+++ b/code/system-contracts/contracts/L1Messenger.sol
@@ -105,8 +105,7 @@ contract L1Messenger is IL1Messenger, ISystemContract {
 
         chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));
 
-        logIdInMerkleTree = numberOfLogsToProcess;
-        numberOfLogsToProcess++;
+        logIdInMerkleTree = numberOfLogsToProcess++;
 
         emit L2ToL1LogSent(_l2ToL1Log);
     }
```
## [G-16] Check previous then update state variable

### Details
first check if the new value is different from the current state before updating it. This way, unnecessary state updates can be avoided, which consume gas.
### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96C1-L99C6

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
96: function setExecutionDelay(uint32 _executionDelay) external onlyOwner {
        executionDelay = _executionDelay;
        emit NewExecutionDelay(_executionDelay); //@audit check already set
    }
```
### Instances - 2:
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L72C4-L75C5

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol  
73:   function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {
        stateTransitionManager = _stateTransitionManager; //@audit check before state update
    }
```
## [G-18] Use preincrement instaed of state variable for increment.

### Proof of Code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L483

```solidity
File: system-contracts/contracts/SystemContext.sol
482:  function incrementTxNumberInBatch() external onlyCallFromBootloader {
        txNumberInBlock += 1; //@audit use preincrement
    }
```
### Optimized code:

```diff
diff --git a/code/system-contracts/contracts/SystemContext.sol b/code/system-contracts/contracts/SystemContext.sol
index 3d0a972..8974ce6 100644
--- a/code/system-contracts/contracts/SystemContext.sol
+++ b/code/system-contracts/contracts/SystemContext.sol
@@ -480,7 +480,7 @@ contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContr
     }
 
     function incrementTxNumberInBatch() external onlyCallFromBootloader {
-        txNumberInBlock += 1;
+        ++txNumberInBlock;
     }
```

## [GAS-19] `abi.encode` is more efficient than `abi.encodePacked`
`abi.encode` uses less gas than `abi.encodePacked`: the gas saved depends on the number of arguments, with an average of ~90 per argument. Test available here.

<details>
<summary>There are 11 instances of this issue:</summary>

---
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /state-transition/chain-deps/facets/Executor.sol

461:                     abi.encodePacked(

517:             abi.encodePacked(

528:             abi.encodePacked(

548:             abi.encodePacked(

610:         bytes memory precompileInput = abi.encodePacked(_versionedHash, _openingPoint, _openingValueCommitmentProof);

655:                 abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Mailbox.sol
```solidity
File: /state-transition/chain-deps/facets/Mailbox.sol

113:             abi.encodePacked(_log.l2ShardId, _log.isService, _log.txNumberInBatch, _log.sender, _log.key, _log.value)

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/L1Messenger.sol
```solidity
File: /system-contracts/contracts/L1Messenger.sol

96:             abi.encodePacked(

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/libraries/TransactionHelper.sol
```solidity
File: /system-contracts/contracts/SystemContext.sol

234:         return keccak256(abi.encodePacked(uint32(_blockNumber)));

```

```solidity
File: /system-contracts/contracts/libraries/TransactionHelper.sol

133:                 keccak256(abi.encodePacked(_transaction.factoryDeps)),

142:         return keccak256(abi.encodePacked("\x19\x01", domainSeparator, structHash));

```

</details>


## [GAS-20] With assembly, .call (bool success) transfer can be done gas-optimized
When using assembly language, it is possible to call the transfer function of an Ethereum contract in a gas-optimized way by using the .call function with specific input parameters. The .call function takes a number of input parameters, including the address of the contract to call, the amount of Ether to transfer, and a specification of the gas limit for the call. By specifying a lower gas limit than the default, it is possible to reduce the gas cost of the transfer.


Instances of this issue:
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/governance/Governance.sol
```solidity
File: /governance/Governance.sol

174:         _execute(_operation.calls);

193:         _execute(_operation.calls);

226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/governance/Governance.sol
```solidity
File: /system-contracts/contracts/ContractDeployer.sol

231:             _deployment.callConstructor

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/libraries/SystemContractHelper.sol#L285
```solidity
File: /system-contracts/contracts/libraries/SystemContractHelper.sol

285:         meta.callerShardId = getCallerShardIdFromMeta(metaPacked);

```

## [GAS-21] Use assembly to emit events
We can use assembly to emit events efficiently by utilizing `scratch space` and the `free memory pointer`. This will allow us to potentially avoid memory expansion costs. Note: In order to do this optimization safely, we will need to cache and restore the free memory pointer.

<details>
<summary>There are 71 instances of this issue:</summary>

---
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1ERC20Bridge.sol#L155)
```solidity
File: /bridge/L1ERC20Bridge.sol

155:         emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);

199:         emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);

225:         emit WithdrawalFinalized(l1Receiver, l1Token, amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1SharedBridge.sol#L168)
```solidity
File: /bridge/L1SharedBridge.sol

168:         emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);

227:         emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);

239:         emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);

367:         emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);

454:         emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);

602:         emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridgehub/Bridgehub.sol#L56
```solidity
File: /bridgehub/Bridgehub.sol

56:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

68:         emit NewPendingAdmin(currentPendingAdmin, address(0));

69:         emit NewAdmin(previousAdmin, pendingAdmin);

145:         emit NewChain(_chainId, _stateTransitionManager, _admin);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/governance/Governance.sol#L47
```solidity
File: /governance/Governance.sol

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
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/StateTransitionManager.sol
```solidity
File: /state-transition/StateTransitionManager.sol

115:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

127:         emit NewPendingAdmin(currentPendingAdmin, address(0));

128:         emit NewAdmin(previousAdmin, pendingAdmin);

227:         emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);

235:         emit StateTransitionNewChain(_chainId, _stateTransitionContract);

287:         emit StateTransitionNewChain(_chainId, stateTransitionAddress);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/ValidatorTimelock.sol#L83
```solidity
File: /state-transition/ValidatorTimelock.sol

83:         emit ValidatorAdded(_chainId, _newValidator);

92:         emit ValidatorRemoved(_chainId, _validator);

98:         emit NewExecutionDelay(_executionDelay);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Admin.sol#L28
```solidity
File: /state-transition/chain-deps/facets/Admin.sol

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
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Admin.sol#L139
```solidity
File: /state-transition/chain-deps/facets/Executor.sol

135:         bytes memory emittedL2Logs = _newBatch.systemLogs;

142:         for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

144:             (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);

145:             (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);

146:             (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);

261:             emit BlockCommit(

299:             emit BlockCommit(

353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

436:         emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

496:         emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Mailbox.sol
```solidity
File: /state-transition/chain-deps/facets/Mailbox.sol

343:         emit NewPriorityRequest(

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/libraries/Diamond.sol

```solidity
File: /state-transition/libraries/Diamond.sol

121:         emit DiamondCut(facetCuts, initAddress, initCalldata);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/ContractDeployer.sol
```solidity
File: /system-contracts/contracts/ContractDeployer.sol

68:         emit AccountVersionUpdated(msg.sender, _version);

86:         emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);

355:         emit ContractDeployed(_sender, _bytecodeHash, _newAddress);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/L1Messenger.sol
```solidity
File: /system-contracts/contracts/L1Messenger.sol

111:         emit L2ToL1LogSent(_l2ToL1Log);

156:         emit L1MessageSent(msg.sender, hash, _message);

181:         emit BytecodeL1PublicationRequested(_bytecodeHash);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/NonceHolder.sol
```solidity
File: /system-contracts/contracts/NonceHolder.sol

96:         emit ValueSetUnderNonce(msg.sender, _key, _value);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/upgrades/BaseZkSyncUpgrade.sol
```solidity
File: /upgrades/BaseZkSyncUpgrade.sol

87:         emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);

104:         emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);

121:         emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);

137:         emit NewVerifier(address(oldVerifier), address(_newVerifier));

157:         emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

256:         emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/upgrades/BaseZkSyncUpgradeGenesis.sol

```solidity
File: /upgrades/BaseZkSyncUpgradeGenesis.sol

40:         emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);

67:         emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);

```
</details>


## [GAS-22] Use assembly for small keccak256 hashes, in order to save gas
Use assembly for small keccak256 hashes, in order to save gas

<details>
<summary>There are 18 instances of this issue:</summary>

---

```solidity
File: /bridge/L1ERC20Bridge.sol

76:         bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));

```

```solidity
File: /bridge/L1SharedBridge.sol

210:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));

341:                 bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));

598:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));

```

```solidity
File: /governance/Governance.sol

205:         return keccak256(abi.encode(_operation));

```

```solidity
File: /state-transition/StateTransitionManager.sol

100:         storedBatchZero = keccak256(abi.encode(batchZero));

102:         initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

138:         initialCutHash = keccak256(abi.encode(_diamondCut));

147:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

156:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

```

```solidity
File: /state-transition/chain-deps/facets/Admin.sol

104:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));

```

```solidity
File: /state-transition/chain-deps/facets/Executor.sol

313:             concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));

588:         return keccak256(abi.encode(_storedBatchInfo));

```

```solidity
File: /system-contracts/contracts/L1Messenger.sol

106:         chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

122:         chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

212:             reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));

```

```solidity
File: /system-contracts/contracts/SystemContext.sol

159:             hash = keccak256(abi.encode(_block));

403:         currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));

```
[[76]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1ERC20Bridge.sol#L76)
,[[210]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1SharedBridge.sol#L210)
,[[341]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1SharedBridge.sol#L341)
,[[598]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1SharedBridge.sol#L598)
,[[205]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/governance/Governance.sol#L205)
,[[100]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/StateTransitionManager.sol#L100)
,[[102]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/StateTransitionManager.sol#L102)
,[[138]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/StateTransitionManager.sol#L138)
,[[147]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/StateTransitionManager.sol#L147)
,[[156]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/StateTransitionManager.sol#L156)
,[[104]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Admin.sol#L104)
,[[313]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol#L313)
,[[588]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol#L588)
,[[106]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/L1Messenger.sol#L106)
,[[122]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/L1Messenger.sol#L122)
,[[212]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/L1Messenger.sol#L212)
,[[159]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/SystemContext.sol#L159)
,[[403]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/SystemContext.sol#L403)
,
</details>

## [GAS-23] Use uint256(1)/uint256(2) instead for true and false boolean states
Use uint256(1) and uint256(2) for true/false to avoid a Gwarmaccess (100 gas), and to avoid Gsset (20000 gas) when changing from ‘false’ to ‘true’, after having been ‘true’ in the past. See [source](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27).

<details>
<summary>There are 8 instances of this issue:</summary>

---
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1ERC20Bridge.sol
```solidity
File: /bridge/L1ERC20Bridge.sol

27:     mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridgehub/Bridgehub.sol
```solidity
File: /bridge/L1SharedBridge.sol

57:     mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))

61:     mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/ValidatorTimelock.sol
```solidity
File: /bridgehub/Bridgehub.sol

21:     mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;

23:     mapping(address _token => bool) public tokenIsRegistered;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol
```solidity
File: /state-transition/ValidatorTimelock.sol

50:     mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;

```

```solidity
File: /state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

74:     mapping(address validatorAddress => bool isValidator) validators;

114:     mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;

```
</details>


## [GAS-24] <array>.length should not be looked up in every loop of a for-loop
If not cached, the solidity compiler will always read the length of the array during each iteration. That is, if it is a storage array, this is an extra sload operation (100 additional extra gas for each iteration except for the first) and if it is a memory array, this is an extra mload operation (3 additional gas for each iteration except for the first).

<details>
<summary>There are 11 instances of this issue:</summary>

---
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/governance/Governance.sol
```solidity
File: /governance/Governance.sol

225:         for (uint256 i = 0; i < _calls.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/ValidatorTimelock.sol
```solidity
File: /state-transition/ValidatorTimelock.sol

116:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

135:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

185:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

209:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /state-transition/chain-deps/facets/Executor.sol

142:         for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

257:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

289:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

636:         for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/Compressor.sol
```solidity
File: /system-contracts/contracts/Compressor.sol

61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/upgrades/BaseZkSyncUpgrade.sol
```solidity
File: /upgrades/BaseZkSyncUpgrade.sol

226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {

```

</details>


## [GAS-25] For Operations that will not overflow, you could use unchecked

<details>
<summary>There are 77 instances of this issue:</summary>

---
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1ERC20Bridge.sol#L12)

```solidity
File: /bridge/L1SharedBridge.sol

439:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds //@auidt cache multiple error


```



</details>


## [GAS-26] Don't compare boolean expressions to boolean literals
true and false are constants and it is more expensive comparing a boolean against them than directly checking the returned boolean value. `if (<x> == true)` => `if (<x>)`, `if (<x> == false)` => `if (!<x>)`


Instances of this issue:

```solidity
File: /state-transition/ValidatorTimelock.sol

68:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");

```
[[68]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/ValidatorTimelock.sol#L68)
,
## [GAS-27] Multiplication/division by two should use bit shifting
X * 2 is equivalent to X << 1 and X / 2 is the same as X >> 1.
 The MUL and DIV opcodes cost 5 gas, whereas SHL and SHR only cost 3 gas.

<details>
<summary>There are 27 instances of this issue:</summary>

---
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/common/libraries/L2ContractHelper.sol
```solidity
File: /common/libraries/L2ContractHelper.sol

25:         uint256 bytecodeLenInWords = _bytecode.length / 32;

50:         codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/StateTransitionManager.sol
```solidity
File: /state-transition/StateTransitionManager.sol

106:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);

```

```solidity
File: /state-transition/chain-deps/DiamondInit.sol

51:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/DiamondInit.sol
```solidity
File: /state-transition/chain-deps/facets/Executor.sol

581:             blobAuxOutputWords[i * 2] = _blobHashes[i];

582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /state-transition/libraries/LibMap.sol

23:             uint256 mapValue = _map.map[_index / 8];

27:             uint256 bitOffset = (_index & 7) * 32;

43:             uint256 mapIndex = _index / 8;

48:             uint256 bitOffset = (_index & 7) * 32;

```

```solidity
File: /system-contracts/contracts/BootloaderUtilities.sol

97:                 vInt += 8 + block.chainid * 2;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/libraries/LibMap.sol
```solidity
File: /system-contracts/contracts/Compressor.sol

52:                 encodedData.length * 4 == _bytecode.length,

57:                 dictionary.length / 8 <= encodedData.length / 2,//@audit cache length

57:                 dictionary.length / 8 <= encodedData.length / 2,//@audit cache length

62:                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;

66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

203:             dictionary = _rawCompressedData[2:2 + dictionaryLen * 8];

204:             encodedData = _rawCompressedData[2 + dictionaryLen * 8:];

253:         number >>= (256 - (_calldataSlice.length * 8));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/BootloaderUtilities.sol
```solidity
File: /system-contracts/contracts/libraries/RLPEncoder.sol

37:                 uint256 shiftedVal = _val << (lbs * 8);

72:                 uint256 shiftedVal = uint256(_len) << (lbs * 8);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/Compressor.sol
```solidity
File: /system-contracts/contracts/libraries/SystemContractsCaller.sol

41: uint256 constant META_GAS_PER_PUBDATA_BYTE_OFFSET = 0 * 8;

42: uint256 constant META_HEAP_SIZE_OFFSET = 8 * 8;

43: uint256 constant META_AUX_HEAP_SIZE_OFFSET = 12 * 8;

44: uint256 constant META_SHARD_ID_OFFSET = 28 * 8;

45: uint256 constant META_CALLER_SHARD_ID_OFFSET = 29 * 8;

46: uint256 constant META_CODE_SHARD_ID_OFFSET = 30 * 8;

```

</details>


## [GAS-28] >=/ <= costs less gas than >/<
The compiler uses opcodes GT and ISZERO for solidity code that uses >, but only requires LT for >=,which saves 3 gas

<details>
<summary>There are 70 instances of this issue:</summary>

---

```solidity
File: /bridge/L1SharedBridge.sol

121:             require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");

129:             require(amount > 0, "ShB: 0 amount to transfer");

158:             require(msg.value == 0, "ShB m.v > 0 b d.it");

202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");

327:         require(_amount > 0, "y1");

501:         require(_l2ToL1message.length >= 56, "ShB wrong msg len"); // wrong messsage length  //@audit cache lemgth 

```

```solidity
File: /bridgehub/Bridgehub.sol

301:             _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,

329:         } else if (_refundRecipient.code.length > 0) {

```

```solidity
File: /governance/Governance.sol

111:         } else if (timestamp > block.timestamp) {

217:         require(_delay >= minDelay, "Proposed delay is less than minimum delay");

```

```solidity
File: /state-transition/ValidatorTimelock.sol

195:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

217:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

```

```solidity
File: /state-transition/chain-deps/DiamondProxy.sol

25:         require(msg.data.length >= 4 || msg.data.length == 0, "Ut");

```

```solidity
File: /state-transition/chain-deps/facets/Admin.sol

70:         require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");

117:             s.protocolVersion > _oldProtocolVersion,

```

```solidity
File: /state-transition/chain-deps/facets/Executor.sol

109:         uint256 batchTimestamp = _packedBatchAndL2BlockTimestamp >> 128;

429:         if (_proof.serializedProof.length > 0) {

482:         require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch

483:         require(_newLastBatch >= s.totalBatchesExecuted, "v2"); // Already executed batches cannot be reverted

492:         if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) {

631:         require(_pubdataCommitments.length > 0, "pl");

```

```solidity
File: /state-transition/chain-deps/facets/Mailbox.sol

158:         require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

272:         require(_mintValue >= baseCost + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost

277:         if (refundRecipient.code.length > 0) {

```

```solidity
File: /state-transition/libraries/Diamond.sol

107:             require(selectors.length > 0, "B"); // no functions for diamond cut

132:         require(_facet.code.length > 0, "G");

155:         require(_facet.code.length > 0, "K");

```

```solidity
File: /state-transition/libraries/LibMap.sol

30:             result = uint32(mapValue >> bitOffset);

54:             uint32 oldValue = uint32(mapValue >> bitOffset);

```

```solidity
File: /state-transition/libraries/Merkle.sol

24:         require(pathLength > 0, "xc");

```

```solidity
File: /state-transition/libraries/TransactionValidator.sol

115:         require(_totalGasLimit >= overhead, "my"); // provided gas limit doesn't cover transaction overhead

```

```solidity
File: /system-contracts/contracts/ComplexUpgrader.sol

24:         require(_delegateTo.code.length > 0, "Delegatee is an EOA");

```

```solidity
File: /system-contracts/contracts/Compressor.sol

146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

177:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

253:         number >>= (256 - (_calldataSlice.length * 8));

```

```solidity
File: /system-contracts/contracts/ContractDeployer.sol

48:             _address > address(MAX_SYSTEM_CONTRACT_ADDRESS) &&

303:         require(knownCodeMarker > 0, "The code hash is not known");

332:             if (value > 0) {

339:             if (value > 0) {

```

```solidity
File: /system-contracts/contracts/DefaultAccount.sol

139:         if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) {

```

```solidity
File: /system-contracts/contracts/L1Messenger.sol

222:         while (nodesOnCurrentLevel > 1) {

```

```solidity
File: /system-contracts/contracts/SystemContext.sol

119:         return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0; //@audit cache basePubdataSpent

144:         if (blockNumber <= _block || blockNumber - _block > 256) {

151:             _block >= currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block &&

152:             currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0

245:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

302:         if (virtualBlockInfo.number >= _l2BlockNumber) {

352:                 _l2BlockTimestamp >= currentBatchTimestamp,

355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

387:                 _l2BlockTimestamp > currentL2BlockTimestamp,

413:         require(currentBatchNumber > 0, "The current batch number must be greater than 0");

430:             _newTimestamp > currentBlockTimestamp,

451:         require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");

```

```solidity
File: /system-contracts/contracts/libraries/RLPEncoder.sol

86:             if (_number > type(uint128).max) {

87:                 _number >>= 128;

90:             if (_number > type(uint64).max) {

91:                 _number >>= 64;

94:             if (_number > type(uint32).max) {

95:                 _number >>= 32;

98:             if (_number > type(uint16).max) {

99:                 _number >>= 16;

102:             if (_number > type(uint8).max) {

```

```solidity
File: /system-contracts/contracts/libraries/SystemContractHelper.sol

219:         result = (shifted >> (256 - size));

```

```solidity
File: /system-contracts/contracts/libraries/TransactionHelper.sol

363:         require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");

368:                 _transaction.paymasterInput.length >= 68,

```

```solidity
File: /upgrades/BaseZkSyncUpgrade.sol

72:         require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

239:             _newProtocolVersion > previousProtocolVersion,

```

```solidity
File: /upgrades/BaseZkSyncUpgradeGenesis.sol

24:             _newProtocolVersion >= previousProtocolVersion,

52:         require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

```
[[121]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1SharedBridge.sol#L121)
,[[129]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1SharedBridge.sol#L129)
,[[363]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/libraries/TransactionHelper.sol#L363)
,[[368]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/libraries/TransactionHelper.sol#L368)
,[[72]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/upgrades/BaseZkSyncUpgrade.sol#L72)
,[[239]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/upgrades/BaseZkSyncUpgrade.sol#L239)
,[[24]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/upgrades/BaseZkSyncUpgradeGenesis.sol#L24)
,[[52]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/upgrades/BaseZkSyncUpgradeGenesis.sol#L52)
,
</details>


## [GAS-29] Use hardcode address instead of address(this) 
Instead of using address(this), it is more gas-efficient to pre-calculate and use the hardcoded address. Foundry’s script.sol and solmate’s LibRlp.sol contracts can help achieve this. References: https://book.getfoundry.sh/reference/forge-std/compute-create-address

<details>
<summary>There are 18 instances of this issue:</summary>

---
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1ERC20Bridge.sol
```solidity
File: /bridge/L1ERC20Bridge.sol

65:         uint256 amount = IERC20(_token).balanceOf(address(this));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1SharedBridge.sol
```solidity
File: /bridge/L1SharedBridge.sol

118:             uint256 balanceBefore = address(this).balance;

120:             uint256 balanceAfter = address(this).balance;

127:             uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

131:             uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

174:         uint256 balanceBefore = _token.balanceOf(address(this));

175:         _token.safeTransferFrom(_from, address(this), _amount);

176:         uint256 balanceAfter = _token.balanceOf(address(this));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1SharedBridge.sol
```solidity
File: /governance/Governance.sol

59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/StateTransitionManager.sol
```solidity
File: /state-transition/StateTransitionManager.sol

265:             bytes32(uint256(uint160(address(this)))),

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/libraries/TransactionHelper.sol
```solidity
File: /state-transition/chain-deps/facets/Mailbox.sol

41:         uint256 amount = address(this).balance;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/libraries/TransactionHelper.sol
```solidity
File: /system-contracts/contracts/ContractDeployer.sol

29:         require(msg.sender == address(this), "Callable only by self");

333:                 BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo(address(this), _newAddress, value);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/libraries/TransactionHelper.sol
```solidity
File: /system-contracts/contracts/DefaultAccount.sol

47:         if (codeAddress != address(this)) {

100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

188:         return recoveredAddress == address(this) && recoveredAddress != address(0);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/L1Messenger.sol
```solidity
File: /system-contracts/contracts/L1Messenger.sol

129:             sender: address(this),

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/libraries/TransactionHelper.sol
```solidity
File: /system-contracts/contracts/libraries/TransactionHelper.sol

377:             uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);

```
</details>


## [GAS-30] Don't initialize variables with default value

<details>
<summary>There are 35 instances of this issue:</summary>

---

```solidity
File: /governance/Governance.sol

225:         for (uint256 i = 0; i < _calls.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/governance/Governance.sol
```solidity
File: /state-transition/ValidatorTimelock.sol

116:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

135:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

185:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

209:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/ValidatorTimelock.sol
```solidity
File: /state-transition/chain-deps/facets/Executor.sol

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
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /state-transition/chain-deps/facets/Getters.sol

208:         for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /state-transition/chain-deps/facets/Mailbox.sol

356:         for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /state-transition/libraries/Diamond.sol

101:         for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {

138:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

158:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

178:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /state-transition/libraries/TransactionValidator.sol

92:         uint256 costForPubdata = 0;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /system-contracts/contracts/Compressor.sol

61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {

124:         uint256 numInitialWritesProcessed = 0;

127:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

159:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /system-contracts/contracts/ContractDeployer.sol

247:         uint256 sumOfValues = 0;

248:         for (uint256 i = 0; i < deploymentsLength; ++i) {

253:         for (uint256 i = 0; i < deploymentsLength; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /system-contracts/contracts/L1Messenger.sol

197:         uint256 calldataPtr = 0;

206:         for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

224:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

236:         for (uint256 i = 0; i < numberOfMessages; ++i) {

254:         for (uint256 i = 0; i < numberOfBytecodes; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /upgrades/BaseZkSyncUpgrade.sol

226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {

```
</details>


## [GAS-31] Long revert strings

<details>
<summary>There are 63 instances of this issue:</summary>

---
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /bridge/L1SharedBridge.sol

155:             require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");

195:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

427:             require(!alreadyFinalized, "Withdrawal is already finalized 2");

564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /bridgehub/Bridgehub.sol

102:         require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

225:                 require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /governance/Governance.sol

59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

65:         require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

172:         require(isOperationReady(id), "Operation must be ready before execution");

177:         require(isOperationReady(id), "Operation must be ready after execution");

191:         require(isOperationPending(id), "Operation must be pending before execution");

196:         require(isOperationPending(id), "Operation must be pending after execution");

216:         require(!isOperation(_id), "Operation with this proposal id already exists");

217:         require(_delay >= minDelay, "Proposed delay is less than minimum delay");

240:         require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /state-transition/StateTransitionManager.sol

256:         require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /state-transition/ValidatorTimelock.sol

62:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

68:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /state-transition/chain-deps/facets/Admin.sol

90:         require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol
```solidity
File: /state-transition/chain-deps/facets/Executor.sol

616:         require(success, "failed to call point evaluation precompile");

```

```solidity
File: /state-transition/chain-deps/facets/Mailbox.sol

39:         require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");

158:         require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

185:         require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");

206:         require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");

```

```solidity
File: /state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

22:         require(s.validators[msg.sender], "StateTransition Chain: not validator");

27:         require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

32:         require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

53:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");

```

```solidity
File: /system-contracts/contracts/AccountCodeStorage.sol

26:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

37:         require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");

48:         require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");

57:         require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");

```

```solidity
File: /system-contracts/contracts/ComplexUpgrader.sol

22:         require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");

```

```solidity
File: /system-contracts/contracts/Compressor.sol

63:                 require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

68:                 require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");

119:         require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");

156:         require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");

187:         require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");

230:                 require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");

```

```solidity
File: /system-contracts/contracts/ContractDeployer.sol

251:         require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");

265:         require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

350:             require(value == 0, "The value must be zero if we do not call the constructor");

```

```solidity
File: /system-contracts/contracts/DefaultAccount.sol

100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

202:         require(success, "Failed to pay the fee to the operator");

```

```solidity
File: /system-contracts/contracts/L1Messenger.sol

315:         require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");

```

```solidity
File: /system-contracts/contracts/NonceHolder.sol

66:         require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");

```

```solidity
File: /system-contracts/contracts/SystemContext.sol

242:         require(_isFirstInBatch, "Upgrade transaction must be first");

245:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

249:             require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");

287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

367:             require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");

368:             require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");

373:             require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");

385:             require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");

413:         require(currentBatchNumber > 0, "The current batch number must be greater than 0");

452:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");

```

```solidity
File: /system-contracts/contracts/libraries/SystemContractHelper.sol

319:         require(index < 10, "There are only 10 accessible registers");

```

```solidity
File: /system-contracts/contracts/libraries/TransactionHelper.sol

363:         require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");

```

```solidity
File: /upgrades/BaseZkSyncUpgrade.sol

190:         require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");

249:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

```

```solidity
File: /upgrades/BaseZkSyncUpgradeGenesis.sol

33:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

```
,[[33]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/upgrades/BaseZkSyncUpgradeGenesis.sol#L33)
,
</details>


## [GAS-32] Constructors can be marked payable
 Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment was not provided. A constructor can safely be marked as payable, since only the deployer would be able to pass funds, and the project itself would not pass any funds.

<details>
<summary>There are 17 instances of this issue:</summary>

---

```solidity
File: /bridge/L1ERC20Bridge.sol

55:     constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {

76:         bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));

79:         return L2ContractHelper.computeCreate2Address(l2Bridge, salt, l2TokenProxyBytecodeHash, constructorInputHash);

```

```solidity
File: /bridge/L1SharedBridge.sol

90:     constructor(

```

```solidity
File: /bridgehub/Bridgehub.sol

38:     constructor() reentrancyGuardInitializer {}

```

```solidity
File: /common/libraries/L2ContractHelper.sol

64:         bytes32 _constructorInputHash

68:             bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)

```

```solidity
File: /governance/Governance.sol

41:     constructor(address _admin, address _securityCouncil, uint256 _minDelay) {

```

```solidity
File: /state-transition/StateTransitionManager.sol

58:     constructor(address _bridgehub) reentrancyGuardInitializer {

```

```solidity
File: /state-transition/ValidatorTimelock.sol

55:     constructor(address _initialOwner, uint32 _executionDelay) {

```

```solidity
File: /state-transition/chain-deps/DiamondInit.sol

19:     constructor() reentrancyGuardInitializer {}

```

```solidity
File: /state-transition/chain-deps/DiamondProxy.sol

11:     constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {

```

```solidity
File: /system-contracts/contracts/AccountCodeStorage.sol

37:         require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");

57:         require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");

```

```solidity
File: /system-contracts/contracts/ContractDeployer.sol

103:         bytes32 constructorInputHash = EfficientCall.keccak(_input);

106:             bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, constructorInputHash)

350:             require(value == 0, "The value must be zero if we do not call the constructor");

```
[[55]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1ERC20Bridge.sol#L55)
,[[76]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1ERC20Bridge.sol#L76)
,[[79]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1ERC20Bridge.sol#L79)
,[[90]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1SharedBridge.sol#L90)
,[[38]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridgehub/Bridgehub.sol#L38)
,[[64]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/common/libraries/L2ContractHelper.sol#L64)
,[[68]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/common/libraries/L2ContractHelper.sol#L68)
,[[41]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/governance/Governance.sol#L41)
,[[58]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/StateTransitionManager.sol#L58)
,[[55]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/ValidatorTimelock.sol#L55)
,[[19]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/DiamondInit.sol#L19)
,[[11]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/DiamondProxy.sol#L11)
,[[37]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/AccountCodeStorage.sol#L37)
,[[57]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/AccountCodeStorage.sol#L57)
,[[103]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/ContractDeployer.sol#L103)
,[[106]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/ContractDeployer.sol#L106)
,[[350]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/ContractDeployer.sol#L350)
,
</details>


If needed, the values can be read from the verified contract source code, or if there are multiple values there can be a single getter function that [returns a tuple](https://github.com/code-423n4/2022-08-frax/blob/90f55a9ce4e25bceed3a74290b854341d8de6afa/src/contracts/FraxlendPair.sol#L156-L178) of the values of all currently-public constants. Saves **3406-3606 gas** in deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it's used, and not adding another entry to the method ID table


Instances of this issue:

```solidity
File: /state-transition/ValidatorTimelock.sol

26:     string public constant override getName = "ValidatorTimelock";

```

```solidity
File: /state-transition/chain-deps/facets/Admin.sol

20:     string public constant override getName = "AdminFacet";

```

```solidity
File: /state-transition/chain-deps/facets/Executor.sol

27:     string public constant override getName = "ExecutorFacet";

```

```solidity
File: /state-transition/chain-deps/facets/Getters.sol

25:     string public constant override getName = "GettersFacet";

```

```solidity
File: /state-transition/chain-deps/facets/Mailbox.sol

35:     string public constant override getName = "MailboxFacet";

```
[[26]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/ValidatorTimelock.sol#L26)
,[[20]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Admin.sol#L20)
,[[27]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol#L27)
,[[25]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Getters.sol#L25)
,[[35]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Mailbox.sol#L35)
,
## [GAS-33] Use shift Right/Left instead of division/multiplication if possible


Instances of this issue:

```solidity
File: /state-transition/StateTransitionManager.sol

11: import {IStateTransitionManager, StateTransitionManagerInitializeData} from "./IStateTransitionManager.sol";

```

```solidity
File: /state-transition/chain-deps/DiamondInit.sol

11: 

```

```solidity
File: /system-contracts/contracts/Compressor.sol

56:             require(

```
[[11]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/StateTransitionManager.sol#L11)
,[[11]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/DiamondInit.sol#L11)
,[[56]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/Compressor.sol#L56)
,


Instances of this issue:

```solidity
File: /common/libraries/L2ContractHelper.sol

41:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash

```
[[41]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/common/libraries/L2ContractHelper.sol#L41)
,
## [GAS-34] Using this to access functions results in an external call, wasting gas
External calls have an overhead of 100 gas, which can be avoided by not referencing the function using this. Contracts are allowed to override their parents' functions and change the visibility from external to public, so make this change if it's required in order to call the function internally.


Instances of this issue:

```solidity
File: /system-contracts/contracts/ContractDeployer.sol

254:             this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender); //@audit cache deployment[i]

```
[[254]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/ContractDeployer.sol#L254)
,

The unchecked keyword is new in solidity version 0.8.0, so this only applies to that version or higher, which these instances are. This saves 30-40 gas per loop


Instances of this issue:

```solidity
File: /state-transition/chain-deps/facets/Executor.sol

580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```

```solidity
File: /system-contracts/contracts/Compressor.sol

135:             numInitialWritesProcessed++;

144:             stateDiffPtr++;

```

```solidity
File: /system-contracts/contracts/L1Messenger.sol

109:         numberOfLogsToProcess++;

284:         calldataPtr++;

290:         calldataPtr++;

```
[[580]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol#L580)
,[[667]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol#L667)
,[[135]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/Compressor.sol#L135)
,[[144]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/Compressor.sol#L144)
,[[109]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/L1Messenger.sol#L109)
,[[284]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/L1Messenger.sol#L284)
,[[290]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/L1Messenger.sol#L290)
,
## [GAS-35] Use != 0 instead of > 0 for unsigned integer comparison

<details>
<summary>There are 25 instances of this issue:</summary>

---

```solidity
File: /bridge/L1SharedBridge.sol

129:             require(amount > 0, "ShB: 0 amount to transfer");

158:             require(msg.value == 0, "ShB m.v > 0 b d.it");

202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");

327:         require(_amount > 0, "y1");

```

```solidity
File: /bridgehub/Bridgehub.sol

329:         } else if (_refundRecipient.code.length > 0) {

```

```solidity
File: /state-transition/chain-deps/facets/Executor.sol

429:         if (_proof.serializedProof.length > 0) {

593:         return (_bitMap & (1 << _index)) > 0;

631:         require(_pubdataCommitments.length > 0, "pl");

```

```solidity
File: /state-transition/chain-deps/facets/Mailbox.sol

158:         require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

277:         if (refundRecipient.code.length > 0) {

```

```solidity
File: /state-transition/libraries/Diamond.sol

107:             require(selectors.length > 0, "B"); // no functions for diamond cut

132:         require(_facet.code.length > 0, "G");

155:         require(_facet.code.length > 0, "K");

```

```solidity
File: /state-transition/libraries/Merkle.sol

24:         require(pathLength > 0, "xc");

```

```solidity
File: /system-contracts/contracts/AccountCodeStorage.sol

102:         if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {

```

```solidity
File: /system-contracts/contracts/ComplexUpgrader.sol

24:         require(_delegateTo.code.length > 0, "Delegatee is an EOA");

```

```solidity
File: /system-contracts/contracts/ContractDeployer.sol

303:         require(knownCodeMarker > 0, "The code hash is not known");

332:             if (value > 0) {

339:             if (value > 0) {

```

```solidity
File: /system-contracts/contracts/NonceHolder.sol

156:         return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);

```

```solidity
File: /system-contracts/contracts/SystemContext.sol

152:             currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0

245:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

413:         require(currentBatchNumber > 0, "The current batch number must be greater than 0");

```
[[129]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1SharedBridge.sol#L129)
,[[158]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1SharedBridge.sol#L158)
,[[202]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1SharedBridge.sol#L202)
,[[327]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridge/L1SharedBridge.sol#L327)
,[[329]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/bridgehub/Bridgehub.sol#L329)
,[[429]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol#L429)
,[[593]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol#L593)
,[[631]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Executor.sol#L631)
,[[158]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Mailbox.sol#L158)
,[[277]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/chain-deps/facets/Mailbox.sol#L277)
,[[107]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/libraries/Diamond.sol#L107)
,[[132]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/libraries/Diamond.sol#L132)
,[[155]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/libraries/Diamond.sol#L155)
,[[24]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/state-transition/libraries/Merkle.sol#L24)
,[[102]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/AccountCodeStorage.sol#L102)
,[[24]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/ComplexUpgrader.sol#L24)
,[[303]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/ContractDeployer.sol#L303)
,[[332]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/ContractDeployer.sol#L332)
,[[339]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/ContractDeployer.sol#L339)
,[[156]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/NonceHolder.sol#L156)
,[[152]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/SystemContext.sol#L152)
,[[245]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/SystemContext.sol#L245)
,[[287]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/SystemContext.sol#L287)
,[[355]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/SystemContext.sol#L355)
,[[413]](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol/system-contracts/contracts/SystemContext.sol#L413)
,
</details>

