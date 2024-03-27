# [1] `lastL2BlockTimestamp` can be in future related to L1.

**File:** `Executor.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L114)
```solidity
114:         require(_previousBatchTimestamp < batchTimestamp, "h3");
115: 
116:         uint256 lastL2BlockTimestamp = _packedBatchAndL2BlockTimestamp & PACKED_L2_BLOCK_TIMESTAMP_MASK;
117: 
118:         // All L2 blocks have timestamps within the range of [batchTimestamp, lastL2BlockTimestamp].
119:         // So here we need to only double check that:
120:         // - The timestamp of the batch is not too small.
121:         // - The timestamp of the last L2 block is not too big.
122:         require(block.timestamp - COMMIT_TIMESTAMP_NOT_OLDER <= batchTimestamp, "h1"); // New batch timestamp is too small
123:         require(lastL2BlockTimestamp <= block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA, "h2"); // The last L2 block timestamp is too big
```

`_verifyBatchTimestamp()` verifies a few things. Firstly (line 114) - it checks if the new timestamp is bigger than the old one.
Then (lines 122-123) - it verifies if the timestamp is not older than `COMMIT_TIMESTAMP_NOT_OLDER` and not bigger than `COMMIT_TIMESTAMP_APPROXIMATION_DELTA`.
However, there's no check which verifies if the timestamp is not in the future. This basically means, that `lastL2BlockTimestamp` can be in future related to L1. The line responsible for that is: `require(lastL2BlockTimestamp <= block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA, "h2")`. Since this line checks if L2 timestamp is not too big, but it still can be big enough to be bigger than L1 timestamp.

Our recommendation is to implement additional check, which will verify that L2 timestamp is only in the past related to L1 timestamp.


# [2] `SystemContext.sol` defines `blockGasLimit` as `uint256`, while EVM defines it as `uint64`

**File:** `SystemContext.sol`

Some inconsistent behavior of the zkSyncVM with EVM was noticed during the code-review process. 

EVM defines gas limit as `uint64`:

```
https://github.com/ethereum/go-ethereum/blob/master/core/types/tx_legacy.go#L30

    Gas      uint64          // gas limit
```

while `SystemContext.sol` defines it as `uint256`:

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L36)
```solidity
36:     /// @notice The current block's gasLimit.
37:     uint256 public blockGasLimit = type(uint32).max;
```

This issue violates the goal of zkSync EVM, which should be compatible with EVM spec.

Our recommendation is to change line 37 from `uint256 public blockGasLimit = type(uint32).max;` to `uint64 public blockGasLimit = type(uint32).max;`

# [3] Implement EIP-712 phishing prevention for `EIP712_DOMAIN_TYPEHASH`

**File:** `TransactionHelper.sol`

[File: code/system-contracts/contracts/libraries/TransactionHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L82)
```solidity
82:     bytes32 constant EIP712_DOMAIN_TYPEHASH = keccak256("EIP712Domain(string name,string version,uint256 chainId)");
```

[EIP-712](https://eips.ethereum.org/EIPS/eip-712#definition-of-domainseparator) defines `address verifyingContract`, which is: `the address of the contract that will verify the signature. The user-agent may do contract specific phishing prevention`.
As described above , `verifyingContract` in `EIP712_DOMAIN_TYPEHASH` should be considered as a mechanism protecting from phishing attacks. The current implementation of `EIP712_DOMAIN_TYPEHASH`, however, does not implement it.

Our recommendation is to change above code to:

```
bytes32 constant EIP712_DOMAIN_TYPEHASH = keccak256("EIP712Domain(string name,string version,uint256 chainId,address verifyingContract)");
```

This change would also require to update the `domainSeparator` (line 138) to:

```
        bytes32 domainSeparator = keccak256(
            abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid, address(this))
        );
```

# [4] `Diamond.sol` violates EIP-2535

**File:** `Diamond.sol`

According to EIP-2535:
```
If the action is Replace, update the function selector mapping for each functionSelectors item to the facetAddress. If any of the functionSelectors had a value equal to facetAddress or the selector was unset, revert instead.
```

The current implementation does not revert when we try to replace a selector's facet with the same facet, but it emits `DiamondCut()` instead.

[File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L160)
```solidity
160:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
161:             require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address
162: 
163:             _removeOneFunction(oldFacet.facetAddress, selector);
164:             // Add facet to the list of facets if the facet address is a new one
165:             _saveFacetIfNew(_facet);
166:             _addOneFunction(_facet, selector, _isFacetFreezable);
```

Our recommendation is to add additional `require` when `action` is `Replace`. It should verify that we are not replacing selector's facet with the same facet. E.g., below line of code should fix this issue: `require(oldFacet.facetAddress != _facet)`.


# [5] Some transactions might be lost forever when processing by the bootloader

**File:** `bootloader.yul`

The bootloader expects that the transactions are in a continuous array, however this exception is nowhere enforced.
If - transactions weren't in the continuous array, the loop will `break`, ignoring the rest transactions. The ignored transaction will be lost forever, instead of being added to the L2 block.

Our recommendation is to revert the transaction (instead of `break`) when transactions are not in the continuous array. The `revert` will enforce the assumption that all transactions are in a continuous array - and if they weren't - operation will simply revert, without losing the rest of the transactions.

[File: code/system-contracts/bootloader/bootloader.yul](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/bootloader/bootloader.yul#L3960)
```solidity
3960:                 let execute := mload(txPtr)
3961: 
3962:                 debugLog("txPtr", txPtr)
3963:                 debugLog("execute", execute)
3964:                 
3965:                 if iszero(execute) {
3966:                     // We expect that all transactions that are executed
3967:                     // are continuous in the array.
3968:                     break
3969:                 }                
```

At line `3968` - revert the transaction, instead of `break`.

# [6] `Governance.sol` does not support ERC-721 and ERC-1155

**File:** `Governance.sol`

[File: code/contracts/ethereum/contracts/governance/Governance.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L20)
```solidity
20: contract Governance is IGovernance, Ownable2Step {
```

The Governance does not support ERC-721 and ERC-1155, since it misses the implementation of  `onERC721Received()`, `onERC1155Received()`, `onERC1155BatchReceived()` functions. This basically means, that proposals related to transfers of these tokens might not correctly work.

For the reference - please check Open Zeppelins `TimelockController.sol` - which implements additional `onERC721Received()`, `onERC1155Received()`, `onERC1155BatchReceived()` functions.


# [7] `executeInstant()` might not execute instantly when predecessor is not yet executed

**File:** `Governance.sol`

Function `executeInstant()` is supposed to execute operations instantly. However, it might revert when its predecessor is not yet finalized. This violates the `executeInstant()` functionality, since it might not be able to instantly execute some operations.

[File: code/contracts/ethereum/contracts/governance/Governance.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L186)
```solidity
186:     function executeInstant(Operation calldata _operation) external payable onlySecurityCouncil {
187:         bytes32 id = hashOperation(_operation);
188:         // Check if the predecessor operation is completed.
189:         _checkPredecessorDone(_operation.predecessor);
```

[File: code/contracts/ethereum/contracts/governance/Governance.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L239)
```solidity
239:     function _checkPredecessorDone(bytes32 _predecessorId) internal view {
240:         require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");
241:     }
```

When `isOperationDone(_predecessorId)` returns false, `_checkPredecessorDone()` will revert, thus `executeInstant()` will also revert.
Our recommendation is to remove the `_checkPredecessorDone(_operation.predecessor)` from the `executeInstant()`.

# [8] Setting new verifier does not check if all committed batches are verified

**File:** `BaseZkSyncUpgrade.sol`

[File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L126)
```solidity
126:     function _setVerifier(IVerifier _newVerifier) private {
127:         // An upgrade to the verifier must be done carefully to ensure there aren't batches in the committed state
128:         // during the transition. If verifier is upgraded, it will immediately be used to prove all committed batches.
129:         // Batches committed expecting the old verifier will fail. Ensure all commited batches are finalized before the
130:         // verifier is upgraded.
131:         if (_newVerifier == IVerifier(address(0))) {
132:             return;
133:         }
134: 
135:         IVerifier oldVerifier = s.verifier;
136:         s.verifier = _newVerifier;
137:         emit NewVerifier(address(oldVerifier), address(_newVerifier));
138:     }
```

When new verifier is being set, there's no check if all committed batches are already verified. Since batches are proved in the same order as they were committed - the new validator may stuck.

1. `_setVerifier()` is being called when there are still some not verified batches
2. New verifier has different logic than the old one, thus it cannot verify the old batched
3. New verifier cannot proceed to verifying different batches, because they are still non-verified batches left
4. New verified has stuck - unless someone reverts the old, non-verified batches.

Our recommendation is to verify that `s.totalBatchesVerified` is the same as `s.totalBatchesCommitted`. Only then, it should be possible to set new verifier.

# [9] `storedBatchHash()` might return reverted batches

**File:** `Getters.sol`

Function `_revertBatches()` from `Executor.sol` can be used to revert batches. However, when we call function `storedBatchHash()`, it does not take into consideration that some batches might be reverted:

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L122)
```solidity
122:     function storedBatchHash(uint256 _batchNumber) external view returns (bytes32) { 
123:         return s.storedBatchHashes[_batchNumber];
124:     }
```

The result returned by `storedBatchHash()` is incorrect when it's called on reverted batch. It will return that reverted batch is still valid.

Our recommendation is to implement additional check which will verify if `_batchNumber` is reverted, before returning `s.storedBatchHashes[_batchNumber]`.


# [10] `increaseMinNonce()` may overflow, due to addition in `unchecked` block

**File:** `NonceHolder.sol`

[File: code/system-contracts/contracts/NonceHolder.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L65)
```solidity
65:     function increaseMinNonce(uint256 _value) public onlySystemCall returns (uint256 oldMinNonce) {
66:         require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");
67: 
68:         uint256 addressAsKey = uint256(uint160(msg.sender));
69:         uint256 oldRawNonce = rawNonces[addressAsKey];
70: 
71:         unchecked {
72:             rawNonces[addressAsKey] = (oldRawNonce + _value);
73:         }
```

Every time `increaseMinNonce()` is called, the unchecked addition (lines 71-73) is being made: `rawNonces[addressAsKey] = (oldRawNonce + _value)`.
Please notice, that the only protection from the overflow (line 66): `require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");` is not sufficient. 
The line 66 basically states, that we cannot increase `rawNonces[addressAsKey]` more than `MAXIMAL_MIN_NONCE_INCREMENT`. However, it's still possible to call `increaseMinNonce(MAXIMAL_MIN_NONCE_INCREMENT)` multiple of times.

It's possible to call `increaseMinNonce(MAXIMAL_MIN_NONCE_INCREMENT)` multiple of times (each call will fulfill the condition at line 66, thus function won't revert) - but on every call `rawNonces[addressAsKey]` will be bigger and bigger.
E.g. after the first call, `rawNonces[addressAsKey] = MAXIMAL_MIN_NONCE_INCREMENT`, after the 2nd call: `rawNonces[addressAsKey] = 2 * MAXIMAL_MIN_NONCE_INCREMENT`, etc. until it finally overflows.
Since the addition is being made in the unchecked block, function will silently overflow, instead of reverting - thus at some point it might return incorrect results.


# [11] `s.l2SystemContractsUpgradeTxHash` is not deleted in `_revertBatches()`.

**File:** `Executor.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L492)
```solidity
492:         if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) {
493:             delete s.l2SystemContractsUpgradeBatchNumber;
494:         }
```

When `s.l2SystemContractsUpgradeBatchNumber > _newLastBatch`, function should clear both `s.l2SystemContractsUpgradeBatchNumber` and `s.l2SystemContractsUpgradeTxHash`. However, as noticed at line 493 - it deletes only `s.l2SystemContractsUpgradeBatchNumber`.
For comparison, please take a look at `_executeBatch()`, where both values are being reseted:

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L361)
```solidity
361:         if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {
362:             delete s.l2SystemContractsUpgradeTxHash;
363:             delete s.l2SystemContractsUpgradeBatchNumber;
364:         }
```

When function `_revertBatches()` is being called, both `s.l2SystemContractsUpgradeBatchNumber` and `s.l2SystemContractsUpgradeTxHash` should be cleared.

# [12] Check return value of `staticcall` in `_getERC20Getters()`

**File:** `L1SharedBridge.sol`

[File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L262)
```solidity
262:         (, bytes memory data1) = _token.staticcall(abi.encodeCall(IERC20Metadata.name, ()));  
263:         (, bytes memory data2) = _token.staticcall(abi.encodeCall(IERC20Metadata.symbol, ()));
264:         (, bytes memory data3) = _token.staticcall(abi.encodeCall(IERC20Metadata.decimals, ())); 
265:         return abi.encode(data1, data2, data3);
```

There's no check if `staticcall` failed or succeeded. This basically means, that even when the `staticcall` reverts, `_getERC20Getters()` will treat `data` as successful response.
Our recommendation is to verify the return value of `staticcall`.


# [13] `decodeString()` in `L2StandardERC20.sol` won't work with ERC-20 tokens with non-string metadata

**File:** `L2StandardERC20.sol`

[File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L75)
```solidity
75:         try this.decodeString(nameBytes) returns (string memory nameString) {  
76:             decodedName = nameString;
77:         } catch {
78:             getters.ignoreName = true;
79:         }
80: 
81:         try this.decodeString(symbolBytes) returns (string memory symbolString) {
82:             decodedSymbol = symbolString;
83:         } catch {
84:             getters.ignoreSymbol = true;
85:         }
```

Some tokens (e.g. MKR) have metadata fields (name / symbol) encoded as bytes32 instead of the string prescribed by the ERC20 specification. Those tokens won't correctly work with `decodeString()` as it accepts `string` instead of `bytes`.

[File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L178)
```solidity
178:     function decodeString(bytes memory _input) external pure returns (string memory result) { 
179:         (result) = abi.decode(_input, (string));
180:     }
```

Consider reimplementing above code, so that it would accept either string or bytes. If you do not plan to support such tokens - explicitly list them as not-supported.


# [14] `isFacetFreezable()` should revert when non-existing faces was provided

**File:** `Getters.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L163)
```solidity
163:     function isFacetFreezable(address _facet) external view returns (bool isFreezable) {  
164:         Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();
165: 
166:         // There is no direct way to get whether the facet address is freezable,
167:         // so we get it from one of the selectors that are associated with the facet.
168:         uint256 selectorsArrayLen = ds.facetToSelectors[_facet].selectors.length;
169:         if (selectorsArrayLen != 0) {
170:             bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];
171:             isFreezable = ds.selectorToFacet[selector0].isFreezable;
172:         }
173:     }
```

According to the comment section and function's name - `isFacetFreezable()` should return `true` - when facet is freezable or `false` when it is not freezable.
Above code-base will, however, return `false` also for facet which does not exist. This might lead to confusion and potentially breaks future integrations, because non-existing facets are neither freezable, nor non-freezable.
When facet is non-existing, it's not possible to establish if it's freezable or not, thus function should revert for that case, instead of returning `false`.

# [15] `L1_GAS_PER_PUBDATA_BYTE` should not be constant, since it might be changed in the future

**File:** `bootloader.yul`

[File: code/system-contracts/bootloader/bootloader.yul](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/bootloader/bootloader.yul#L101)
```solidity
101:             /// @dev The number of L1 gas needed to be spent for
102:             /// L1 byte. While a single pubdata byte costs `16` gas, 
103:             /// we demand at least 17 to cover up for the costs of additional
104:             /// hashing of it, etc.
105:             function L1_GAS_PER_PUBDATA_BYTE() -> ret {
106:                 ret := 17
107:             }
```

The current implementation assumes that the gas cost is constant and will never be changed in the future. This assumption is, however incorrect. There are some proposals (e.g. EIP-4488) which suggests the gas cost reduction. By having `L1_GAS_PER_PUBDATA_BYTE()` as a constant (returning constant value `17`) - it won't be possible to alter this value in the future.
Our recommendation is to improve the code flexibility and re-implement this functions so that it could be changed in the future.


# [16] `DiamondProxy` doesn't check for the contract existence before the delegatecall

**File:** `DiamondProxy.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L27)
```solidity
27:         Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];
28:         address facetAddress = facet.facetAddress;
29: 
30:         require(facetAddress != address(0), "F"); // Proxy has no facet for this selector
31:         require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen
32: 
33:         assembly {
34:             // The pointer to the free memory slot
35:             let ptr := mload(0x40)
36:             // Copy function signature and arguments from calldata at zero position into memory at pointer position
37:             calldatacopy(ptr, 0, calldatasize())
38:             // Delegatecall method of the implementation contract returns 0 on error
39:             let result := delegatecall(gas(), facetAddress, ptr, calldatasize(), 0, 0)
```

The current implementation verifies only if `facetAddress` is not `address(0)` (line 30). However, there's no contract existence check.
When proxy tries to delegate to an address (line 39) which is not a contract - the fallback function will return success, thus the silent failure will occur. It's recommended to add additional check which will be responsible for verification the contract's code before degate-calling it.


# [17] Unsafe memory reading in `_processL2Logs()`

**Files:** `Executor.sol`, `UnsafeBytes.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142)
```solidity
142:         for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
143:             // Extract the values to be compared to/used such as the log sender, key, and value
144:             (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
145:             (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
146:             (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);
```

As demonstrated above, function `_processL2Logs()` utilizes `UnsafeBytes` library. The library straightforwardly warns that it might go out of bounds:

[File: code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L11)
```solidity
11:  * @dev WARNING!
12:  * 1) Functions don't check the length of the bytes array, so it can go out of bounds.
13:  * The user of the library must check for bytes length before using any functions from the library!
```

Function `_processL2Logs()` does not check for bytes length before using `UnsafeBytes` functions - even it's explicitly recommended to do that (see line 12).

The loop in `_processL2Logs()` increments by `L2_TO_L1_LOG_SERIALIZE_SIZE`, however function does not verify if `emittedL2Logs` are divisible by `L2_TO_L1_LOG_SERIALIZE_SIZE`. This basically means, that when `emittedL2Logs` are not divisible by `L2_TO_L1_LOG_SERIALIZE_SIZE`, function may try to read any random values from out of bounds array. Our recommendation is to add additional `require` check, which will verify if `emittedL2Logs` length is divisible by `L2_TO_L1_LOG_SERIALIZE_SIZE`. If it's not, function should revert.

Since the attack scenario is rather theoretical - the severity of this issue was evaluated as Low and is included in the QA Report.


# [18] Tokens might be minted to `address(0)`, because there's no `address(0)`-check

**File:** `L2SharedBridge.sol`

[File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L079)
```solidity
079:     function finalizeDeposit(
080:         address _l1Sender,
081:         address _l2Receiver,
082:         address _l1Token,
083:         uint256 _amount,
084:         bytes calldata _data
085:     ) external payable override {
[...]
104:         IL2StandardToken(expectedL2Token).bridgeMint(_l2Receiver, _amount);
105:         emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);
106:     }
```

Function `finalizeDeposit()` does not verify if provided `_l2Receiver` is not `address(0)`. This basically means that it's possible to call `bridgeMint()` on `address(0)`, thus mint tokens to `address(0)`.


# [19] Proof verification in `Executor.sol` is performed twice 

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

When `_proof.serializedProof.length > 0` function will call `_verifyProof(proofPublicInput, _proof)` twice - at 430 and 433.
Performing the same execution of code twice is redundant and should be removed.


# [20] Unsafe downcast in `_processL2Logs()`

**File:** `Executor.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L145)
```solidity
145:             (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
146:             (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);
147: 
148:             // Ensure that the log hasn't been processed already
149:             require(!_checkBit(processedLogs, uint8(logKey)), "kp");
```

Variable `logKey` is declared as `uint256` and is retrieved from `emittedL2Logs` at line 145.
Then, at line 149 - `logKey` is downcasted to `uint8`. Since `logKey` is received via `UnsafeBytes.readUint256()` (line 145) - nothing guarantees that its value is lower than `type(uint8).max`. This means, that downcasting it at line 149 might silently underflow leading to incorrect results.


# [21] `lengthRoundedByWords()` may silently overflow

**File:** `bootloader.yul`

[File: code/system-contracts/bootloader/bootloader.yul](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/bootloader/bootloader.yul#L561)
```solidity
561:             function lengthRoundedByWords(len) -> ret {
562:                 let neededWords := div(add(len, 31), 32)
563:                 ret := safeMul(neededWords, 32, "xv")
564:             }
```

When `len` is greater than `type(uint256).max - 30` - line 562 might silently overflow and might start returning `0`. This will lead to incorrect results returned by `lengthRoundedByWords()`. Since function already uses safe math (`safeMul()` ad line 563) - it's recommended to use `safeAdd()` at line 562 too.


# [22] `increaseMinNonce()` won't revert when value is 0

**File:** `NonceHolder.sol`

[File: code/system-contracts/contracts/NonceHolder.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L65)
```solidity
65:     function increaseMinNonce(uint256 _value) public onlySystemCall returns (uint256 oldMinNonce) {
66:         require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");
67: 
68:         uint256 addressAsKey = uint256(uint160(msg.sender));
69:         uint256 oldRawNonce = rawNonces[addressAsKey];
70: 
71:         unchecked {
72:             rawNonces[addressAsKey] = (oldRawNonce + _value);
73:         }
74: 
75:         (, oldMinNonce) = _splitRawNonce(oldRawNonce);
76:     }
```

Providing `0` as `value` parameter won't increase the nonce at all. It's recommend to revert when `value` is `0`. Otherwise, it would be possible to call `increaseMinNonce(0)` every time without any effect 


# [23] `getCodeSize()` and `getCodeHash()` may overflow due to lack of input validation

**File:** `AccountCodeStorage.sol`

[File: code/system-contracts/contracts/AccountCodeStorage.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L117)
```solidity
117:     function getCodeSize(uint256 _input) external view override returns (uint256 codeSize) {
118:         // We consider the account bytecode size of the last 20 bytes of the input, because
119:         // according to the spec "If EXTCODESIZE of A is X, then EXTCODESIZE of A + 2**160 is X".
120:         address account = address(uint160(_input));
```

[File: code/system-contracts/contracts/AccountCodeStorage.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L89)
```solidity
89:     function getCodeHash(uint256 _input) external view override returns (bytes32) {  
90:         // We consider the account bytecode hash of the last 20 bytes of the input, because
91:         // according to the spec "If EXTCODEHASH of A is X, then EXTCODEHASH of A + 2**160 is X".
92:         address account = address(uint160(_input));
```

None of above function verifies if `_input` is not greater than `type(uint160).max`. Since both functions perform downcasting `uint256` to `uint160` - whenever user provided `_input` is greater than `type(uint160).max` - the value will overflow.
Our recommendation is to add additional `require`, which would verify that `_input` never exceeds `type(uint160).max`.

# [24] `updateDelay()` can be set to `0` - which disables the delay

**File:** `Governance.sol`

[File: code/contracts/ethereum/contracts/governance/Governance.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L249)
```solidity
249:     function updateDelay(uint256 _newDelay) external onlySelf {
250:         emit ChangeMinDelay(minDelay, _newDelay);
251:         minDelay = _newDelay;
252:     }
```

Ability to set `minDelay` to `0`, basically removes the delay protection. It allows the administrator (`onlySelf`) to update the delay to `0` - and the - immediately execute transactions.


# [25] Incorrect comparison operator in `_proveL2LogInclusion()`

**File:** `Mailbox.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L110)
```solidity
110:         require(_batchNumber <= s.totalBatchesExecuted, "xx");
```

Because the maximum `_batchNumber` which can be verified is `s.totalBatchesExecuted - 1`, line: `require(_batchNumber <= s.totalBatchesExecuted, "xx");` should be changed to: `require(_batchNumber < s.totalBatchesExecuted, "xx");`

# [26] Missing `address(0)` checks in the constructor

**Files:** `L1ERC20Bridge.sol`, `Governance.sol`

Make sure that user-supplied parameters are not `address(0)`.

[File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L56)
```solidity
56:         sharedBridge = _sharedBridge;
```

[File: code/contracts/ethereum/contracts/governance/Governance.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L46)
```solidity
46:         securityCouncil = _securityCouncil;
```

# [27] Missing `address(0)` checks in functions

**Files:** `Governance.sol`, `SystemContext.sol`, `ValidatorTimelock.sol`

Make sure that user-supplied parameters are not `address(0)`.

It's possible to set new validator to `address(0)`:

[File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L78)
```solidity
78:     function addValidator(uint256 _chainId, address _newValidator) external onlyChainAdmin(_chainId) {
79:         if (validators[_chainId][_newValidator]) {
80:             revert AddressAlreadyValidator(_chainId);
81:         }
82:         validators[_chainId][_newValidator] = true;
83:         emit ValidatorAdded(_chainId, _newValidator);
84:     }
```

It's possible to set origin to `address(0)`.

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L099)
```solidity
099:     function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {
100:         origin = _newOrigin;
101:     }
102: 
```


It's possible to set security council to `address(0)`

[File: code/contracts/ethereum/contracts/governance/Governance.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L256)
```solidity
256:     function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
257:         emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
258:         securityCouncil = _newSecurityCouncil;
259:     }
```

# [28] Conflict `require` statements in `DiamondProxy.sol` may lead to revert

**File:** `DiamondProxy.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25)
```solidity
25:         require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
26:         // Get facet from function selector
27:         Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];
28:         address facetAddress = facet.facetAddress;
29: 
30:         require(facetAddress != address(0), "F"); // Proxy has no facet for this selector
```
`DiamondProxy` utilizes `fallback()` to delegate call to its facets.
The first `require` (line 25) allows to delegate either with `msg.data` or with empty `msg.data` (`msg.data.length == 0`).
However, please notice, that when `msg.data.length` is empty, then `diamondStorage.selectorToFacet[msg.sig].facetAddress` will be `address(0)`. This constitutes some issue, because the next `require` - at line 30 - checks `facetAddress` against `address(0)`.
This behavior suggests that two require statements conflict with each other. Whenever `msg.data.length == 0`, then `facet.facetAddress == address(0)`, thus line 30 will revert.

# [29] Incorrect `MINIBLOCK_HASHES_TO_STORE` constant value in `SystemContext.sol`

**File:** `SystemContext.sol`

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L20)
```solidity
20:     /// We could either:
21:     /// - Store the latest 256 hashes (and strictly rely that we do not accidentally override the hash of the block 256 blocks ago)
22:     /// - Store the latest 257 blocks' hashes.
23:     uint256 internal constant MINIBLOCK_HASHES_TO_STORE = 257;
```

Protocol stores the latest 257 blocks' hashes. This is even confirmed by the function names: `_getLatest257L2blockHash()`.
However, please notice, that `MINIBLOCK_HASHES_TO_STORE` is used as an array's max index:

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L212)
```solidity
212:     function _setL2BlockHash(uint256 _block, bytes32 _hash) internal {
213:         l2BlockHash[_block % MINIBLOCK_HASHES_TO_STORE] = _hash;
214:     }
```

Since every array starts from `0`, if we want to store 257 blocks' hashes, the  `MINIBLOCK_HASHES_TO_STORE` should be set to 256 (instead of 257). `l2BlockHash` from 0 to 256 is 257 blocks' hashes.


# [30] `setGasPrice()` can set gas price to 0

**File:** `SystemContext.sol`

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L105)
```solidity
105:     function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {
106:         gasPrice = _gasPrice;
107:     }
```

Function `setGasPrice()` does not perform any validation of the `_gasPrice` value. It's possible to set the gas price to `0`. Our recommendation is add additional line which won't let setting the gas price to 0: `require(_gasPrice > 0, "gas price cannot be 0");`.

# [31] Function `validateBytes()` reverts instead of returning `0`

**File:** `bootloader.yul`

[File: code/system-contracts/bootloader/bootloader.yul](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/bootloader/bootloader.yul#L3424)
```solidity
3424:                     // If last word contains some unintended bits
3425:                     // return 0
3426:                     if and(lastWord, mask) {
3427:                         assertionError("bad bytes encoding")
3428:                     }
```

According to the comment at line 3424 - function should return with `0` - instead, because of the `assertionError()` at line 3427 - it reverts.

# [32] Implement some boundary checks for `setExecutionDelay()`

**File:** `ValidatorTimelock.sol`

[File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96)
```solidity
96:     function setExecutionDelay(uint32 _executionDelay) external onlyOwner {
97:         executionDelay = _executionDelay;
98:         emit NewExecutionDelay(_executionDelay);
99:     }
```

It's possible to set execution delay to extremely large value or very small value (e.g. 0). It's recommended to set some min and max value of `executionDelay` and perform verification of it.
It should not be possible to set `executionDelay` to too huge (or too small) value.

# [33] Clean local variable before using them in inline assembly

**File:** `EfficientCall.sol`

Function `rawMimicCall()` clears variables before calling `call` in inline assembler:

[File: code/system-contracts/contracts/libraries/EfficientCall.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L204)
```solidity
204:             // Clearing values before usage in assembly, since Solidity
205:             // doesn't do it by default
206:             _whoToMimic := and(_whoToMimic, cleanupMask)
```

However, there are some places, where this cleaning is missing. Every local variable should be cleaned before usage in the inline assembly.

There's no cleaning of `_address` in `rawCall()`:
[File: code/system-contracts/contracts/libraries/EfficientCall.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L134)
```solidity
134:             address callAddr = RAW_FAR_CALL_BY_REF_CALL_ADDRESS;
135:             assembly {
136:                 success := call(_address, callAddr, 0, 0, 0xFFFF, 0, 0)
```

[File: code/system-contracts/contracts/libraries/EfficientCall.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L148)
```solidity
148:             assembly {
149:                 success := call(msgValueSimulator, callAddr, _value, _address, 0xFFFF, forwardMask, 0)
150:             }
```

In `rawMimicCall()` only `_whoToMimic` is cleaned, but `_address` is not cleaned:

[File: code/system-contracts/contracts/libraries/EfficientCall.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L208)
```solidity
208:             success := call(_address, callAddr, 0, 0, _whoToMimic, 0, 0)
209:         }
```

In `rawStaticCall()` `_address` is not cleaned:

[File: code/system-contracts/contracts/libraries/EfficientCall.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L163)
```solidity
163:         assembly {
164:             success := staticcall(_address, callAddr, 0, 0xFFFF, 0, 0)
165:         }
```

In `rawDelegateCall()` `_address` is not cleaned:

[File: code/system-contracts/contracts/libraries/EfficientCall.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L177)
```solidity
177:         assembly {
178:             success := delegatecall(_address, callAddr, 0, 0xFFFF, 0, 0)
179:         }
```

# [34] Implement time locks for critical operations in `Admin.sol`

**File:** `Admin.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L133)
```
133:     function freezeDiamond() external onlyAdminOrStateTransitionManager {
134:         Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
[...]
143:     function unfreezeDiamond() external onlyAdminOrStateTransitionManager {
144:         Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
```

Functions `freezeDiamond() `and `unfreezeDiamond()` misses time lock controls. It's recommended that it should not be possible to execute critical operations instantly, without giving users any time to react for the changes. Freezing and unfreezing Diamond should be considered as critical operations which should be protected by the timelock.


# [35] Consider using 2-step procedure to update security council

**File:** `Governance.sol`

[File: code/contracts/ethereum/contracts/governance/Governance.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L256)
```solidity
256:     function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
257:         emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
258:         securityCouncil = _newSecurityCouncil;
259:     }
```

Use 2-step procedure to update the security council. For the reference, please check that the 2-step procedure is implemented, i.e., in `Admin.sol` file (see functions `setPendingAdmin()` and `acceptAdmin()`).



# [36] Remove `debugLog()` from production code in `bootloader.yul`

There's no need for `bootloader.yul` to contain debug logs in the production code.

For the report readability, we provide the `grep` command which finds every occurrence of `debugLog` in `bootloader.yul` - which should be removed.
```
% grep debugLog -ri . | wc -l
      87
```

# [37] Storage values shouldn't be updated when value is not being changed

**Files:** `ValidatorTimelock.sol`, `Bridgehub.sol`, `Admin.sol`, `Governance.sol`, `ContractDeployer.sol`, `StateTransitionManager.sol`, `SystemContext.sol`

It's recommended to add additional `require` statement, which will verify if the value is really changed, before we will store it in the storage variables
E.g., let's consider a function `setChainId()` from `SystemContext.sol`. When `chainId` is `1` and we will call `setChainId(1)`, function will re-store the same value. It's recommended to add additional `require` which will detect that there's nothing to update:

```
require(_newChainId != chainId, "Nothing to update");
```


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

# [38] Functions which updates important storage variables should emit events

**Files:** `ValidatorTimelock.sol`, `StateTransitionManager.sol`, `Bridgehub.sol`

During the code-review process, it was detected that some functions do not emit events when some state variables are being updated. The list of functions which should emit event is listed below:

[File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108)
```solidity
108:     function setSharedBridge(address _sharedBridge) external onlyOwner {
109:         sharedBridge = IL1SharedBridge(_sharedBridge);
110:     }
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
[...]
```

[File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L73)
```solidity
73:     function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {
74:         stateTransitionManager = _stateTransitionManager;
75:     }
```

# [39] Incorrect revert string in `BaseZkSyncUpgradeGenesis.sol`

**File:** `BaseZkSyncUpgradeGenesis.sol`

[File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22)
```solidity
22:         require(
23:             // Genesis Upgrade difference: Note this is the only thing change > to >=
24:             _newProtocolVersion >= previousProtocolVersion,
25:             "New protocol version is not greater than the current one"
26:         );
```

As the comment section explains, the only difference from `code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol` is the `>=` operator.
`BaseZkSyncUpgrade.sol` uses: `_newProtocolVersion > previousProtocolVersion`.
`BaseZkSyncUpgradeGenesis` uses: `_newProtocolVersion >= previousProtocolVersion`, thus, as mentioned in the comment section, `>` has been changed to `>=`. However, the revert string was not changed and is the same as in `BaseZkSyncUpgrade.sol`.
Since now `_newProtocolVersion >= previousProtocolVersion`, the revert string should be changed to: `"New protocol version is not greater or equal than the current one"`.


# [40] Incorrect description of `VM_HOOK_TX_HAS_ENDED()` in `bootloader.yul`

**File:** `bootloader.yul`

[File: code/system-contracts/bootloader/bootloader.yul](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/bootloader/bootloader.yul#L3767)
```solidity
3767:             /// @notice The id of the VM hook that notifies the operator that the transaction's execution has started.
3768:             function VM_HOOK_TX_HAS_ENDED() -> ret { 
3769:                 ret := 4
3770:             }
```

Function `VM_HOOK_TX_HAS_ENDED()` - as its name suggests notifies the operator that the transaction's execution has ended (change `has started` to `has ended`).



# [41] Incorrect comment for `create()`

**File:** `ContractDeployer.sol`

[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L143)
```solidity
143:     /// @dev This method also accepts nonce as one of its parameters.
144:     /// It is not used anywhere and it needed simply for the consistency for the compiler
145:     /// Note: this method may be callable only in system mode,
146:     /// that is checked in the `createAccount` by `onlySystemCall` modifier.
147:     function create(
148:         bytes32 _salt,
149:         bytes32 _bytecodeHash,
150:         bytes calldata _input
151:     ) external payable override returns (address) {
```

Since the parameter accepts `salt`, it would be better to change `@dev` NatSpec from `also accepts nonce` to `also accepts salt`.


# [42] Incorrect NatSpec in `_executedBatchIdx()`

**File:** `Executor.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L320)
```solidity
320:     /// @dev _executedBatchIdx is an index in the array of the batches that we want to execute together
321:     function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {
```

`_executedBatchIdx` is a parameter passed to the function, thus `@dev _executedBatchIdx` should be changed to `@param _executedBatchIdx`


# [43] Uncompleted comment in `ContractDeployer.sol`

**File:** `ContractDeployer.sol`

[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L306)
```solidity
306:     /// @notice Ensures that the _newAddress and assigns a new contract hash to it
```

The NatSpec comment seems to miss the word describing `_newAddress`.
`Ensures that the _newAddress and assigns` should be changed to: `Ensures that the _newAddress exists and assigns`


# [44] Incorrect comment in `TransactionHelper.sol` 

**File:** `TransactionHelper.sol`

[File: code/system-contracts/contracts/libraries/TransactionHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L17)
```solidity
17: /// @dev The type id of legacy transactions.
18: uint8 constant LEGACY_TX_TYPE = 0x0;
19: /// @dev The type id of legacy transactions.
20: uint8 constant EIP_2930_TX_TYPE = 0x01; 
```
Comment at line 19 seems to be copy-pasted from line 17. Actually, it should be: `/// @dev The type id of EIP-2930 transactions.`, since `EIP_2930_TX_TYPE` is related to EIP-2930.


# [45] Unused constant `MAX_MSG_VALUE` in `Constants.sol`

**File:** `Constants.sol`

Constant `MAX_MSG_VALUE` defined in `Constants.sol` is not used anywhere, thus should be removed:

```
% grep MAX_MSG_VALUE -ri .
./system-contracts/contracts/Constants.sol:uint256 constant MAX_MSG_VALUE = 2 ** 128 - 1; 
```

[File: code/system-contracts/contracts/Constants.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L93)
```solidity
93: /// @dev The maximal msg.value that context can have
94: uint256 constant MAX_MSG_VALUE = 2 ** 128 - 1;
```



# [46] Redundant variables in `bootloader.yul` should be removed

**File:** `bootloader.yul`

[File: code/system-contracts/bootloader/bootloader.yul](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/bootloader/bootloader.yul#L1419)
```solidity
1419:                 let innerTxDataOffset := add(txDataOffset, 32)  
1420:                 debugLog("Starting validation", 0)
1421: 
1422:                 accountValidateTx(txDataOffset)
1423:                 debugLog("Tx validation complete", 1)
1424:                 
1425:                 ensurePayment(txDataOffset, gasPrice)
1426:                 
1427:                 ret := 1
1428:             }
```

In function `ZKSYNC_NEAR_CALL_validateTx()` variable `innerTxDataOffset` is nowhere used. We can directly call `add(txDataOffset, 32)`, instead of assigning it to `innerTxDataOffset`.



# [47] Typo in variable name in `bootloader.yul`

**File:** `bootloader.yul`

[File: code/system-contracts/bootloader/bootloader.yul](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/bootloader/bootloader.yul#L2350)
```solidity
2350:                 let innerTxDataOffst := add(txDataOffset, 32)
2351:                 let from := getFrom(innerTxDataOffst)
2352:                 ensureAccount(from)
2353: 
2354:                 // The nonce should be unique for each transaction.
2355:                 let nonce := getNonce(innerTxDataOffst)
```

`innerTxDataOffst` should actually be `innerTxDataOffset` (missing letter `e` in the variable name).



# [48] Remove code related to local testing 

**Files:** `DiamondInit.sol`, `StateTransitionManager.sol`

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

Remove code related to local testing, which won't work in the production.

# [49] Constants should be uppercased

**File:** `ValidatorTimelock.sol`

Please notice that this is additional instance which was not detected by the bot. The bot detected `AddressAliasHelper.sol` only, while this issue is about `ValidatorTimelock.sol`.

[File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26)
```solidity
26:     string public constant override getName = "ValidatorTimelock";
```

According to the Solidity style guide, `getName` should be changed to `GET_NAME` - because it's a constant.



# [50] Incorrect variable name in `SystemContext.sol`

**File:** `SystemContext.sol`

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L450)
```solidity
450:         (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();
```

Since `getBatchNumberAndTimestamp()` returns the current batch number and the current batch timestamp, variable names `previousBatchNumber` and `previousBatchTimestamp` may be misleading.
Those variables are being updated later - but at the time of `getBatchNumberAndTimestamp()` execution they still contain the current values.


# [51] Function `_commintOneBatch` should be named differently

**File:** `Executor.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L32)
```solidity
32:     function _commitOneBatch( 
33:         StoredBatchInfo memory _previousBatch,
34:         CommitBatchInfo calldata _newBatch,
35:         bytes32 _expectedSystemContractUpgradeTxHash
36:     ) internal view returns (StoredBatchInfo memory) {
```

The name of the function suggests, that it commits one batch - however, this function is a `view` function, thus it doesn't change the state on the blockchain. This is even confirmed in the function's NatSpec: `@notice Does not change storage`.

# [52] Incorrect NatSpec for `_isValidSignature()`

**File:** `DefaultAccount.sol`

[File: code/system-contracts/contracts/DefaultAccount.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L158)
```solidity
158:     /// @return EIP1271_SUCCESS_RETURN_VALUE if the signaure is correct. It reverts otherwise.
159:     function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {
```

When signature is correct, function returns `EIP1271_SUCCESS_RETURN_VALUE`. In any other cases, function either return `false` or reverts. The current NatSpec's comments does not mention that `_isValidSIgnature()` might return `false`. The NatSpec should be changed to: `@return EIP1271_SUCCESS_RETURN_VALUE if the signaure is correct. It returns false or reverts otherwise`

# [53] `IMailbox.sol` does not implement functions from `Mailbox.sol`

**File:** `Mailbox.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L196)
```solidity
196:     ///  @inheritdoc IMailbox
197:     function requestL2Transaction(
```

According to the NatSpec, function `requestL2Transaction()` should be implemented in `IMailbox.sol`. However, `IMailbox.sol` does not implement this function, the only one `IMailbox.sol` implements is `finalizeEthWithdrawal()`.
Our recommendation is to add missing `requestL2Transaction()` to `IMailbox.sol`.



# [54] `Getters.sol` missing implementing some getters

**File:** `Getters.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L20)
```solidity
20: contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {
```

File `Getters.sol` does not implement function `getZkPorterIsAvailable()` responsible for getting the `zkPorterIsAvailable` value. This variable can be set in `Admin.sol` by calling `setPorterAvailability()`, thus `Getters.sol` should implement a getter to expose `zkPorterIsAvailable` value.

# [55] Change the name of events related to Blocks

**File:** `IExecutor.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L186)
```solidity
186:     /// @notice Event emitted when a batch is committed
[...]
191:     event BlockCommit(uint256 indexed batchNumber, bytes32 indexed batchHash, bytes32 indexed commitment);
192: 
193:     /// @notice Event emitted when batches are verified
[...]
197:     event BlocksVerification(uint256 indexed previousLastVerifiedBatch, uint256 indexed currentLastVerifiedBatch);
198: 
199:     /// @notice Event emitted when a batch is executed
[...]
204:     event BlockExecution(uint256 indexed batchNumber, bytes32 indexed batchHash, bytes32 indexed commitment);
205: 
206:     /// @notice Event emitted when batches are reverted
[...]
211:     event BlocksRevert(uint256 totalBatchesCommitted, uint256 totalBatchesVerified, uint256 totalBatchesExecuted);
```

The current implementation uses batches instead of blocks - thus it would increase the code readability to change the names from `Block*` to `Batch*`. This is even confirmed in the NatSpec of the events:
line 186 - `Event emitted when a batch is committed` - change `event BlockCommit()` to `even BatchCommit()`.
line 193 - `Event emitted when batches are verified` - change `event BlocksVerification()` to `event BatchVerification`().
line 199 - `Event emitted when a batch is executed` - change `event BlockExecution()` to `event BatchExecution()`.
line 206 - `Event emitted when batches are reverted` - change `event BlocksRevert()` to `event BatchRevert()`.


# [56] else-block is not required in `getOperationState()`

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

The `else` instruction at line 113 can be removed. When previous conditions won't be fulfilled, function will still return `OperationState.Ready`. Getting rid of redundant `else` instruction simplifies the code, thus it's highly recommended.


# [57] Do not add a `return` statement when the function defines a named return variable

**File:** `NonceHolder.sol`

Once the return variable has been assigned (or has its default value), there is no need to explicitly return it at the end of the function, since it's returned automatically.

[File: code/system-contracts/contracts/NonceHolder.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L125)
```solidity
125:     function getDeploymentNonce(address _address) external view returns (uint256 deploymentNonce) {
126:         uint256 addressAsKey = uint256(uint160(_address));
127:         (deploymentNonce, ) = _splitRawNonce(rawNonces[addressAsKey]);
128: 
129:         return deploymentNonce;
130:     }
```

# [58] Use `gas` instead of `ergs`

**Files:** `Constants.sol`, `GasBoundCaller.sol`

The current implementation uses `gas` term, instead of `ergs`. However, there are some places, where `ergs` were not updated to `gas`:

[File: code/system-contracts/contracts/GasBoundCaller.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L16)
```solidity
16:     /// @notice We assume that no more than `CALL_ENTRY_OVERHEAD` ergs are used for the O(1) operations at the start
17:     /// of execution of the contract, such as abi decoding the parameters, jumping to the correct function, etc.
18:     uint256 constant CALL_ENTRY_OVERHEAD = 800;
19:     /// @notice We assume that no more than `CALL_RETURN_OVERHEAD` ergs are used for the O(1) operations at the end of the execution,
```

[File: code/system-contracts/contracts/Constants.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L37)
```solidity
37: /// @dev The number of ergs that need to be spent for a single byte of pubdata regardless of the pubdata price.
```

# [59] Use `delete` instead of assigning variable to their default values

**File:** `Admin.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L147)
```solidity
147:         diamondStorage.isFrozen = false;
```

It's recommended to use `delete` keyword, when some variable/mapping/struct fields needs to be cleared and assigned to its default value.

# [60] `ISystemContract.sol` should be interface, instead of `abstract`

**File:** `ISystemContract.sol`

[File: code/system-contracts/contracts/interfaces/ISystemContract.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L17)
```solidity
17: abstract contract ISystemContract {
```

File `ISystemContract.sol` is inside `interfaces` directory - which suggests it should be an interface. Moreover its name `ISystemContract.sol` also suggests it should be an interface. However, file `ISystemContract.sol` contains an implementation of `abstract` contract.
Our recommendation is to stick to the Solidity style guide and do not put abstract contracts into `intterfaces` directory - among other files which implement interfaces only.


# [61] Links in the NatSpec point to non-existing websites

**File:** `ReentrancyGuard.sol`

[File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L19)
```solidity
19:  * to protect against it, check out our blog post
20:  * https://blog.openzeppelin.com/reentrancy-after-istanbul/[Reentrancy After Istanbul].
```

The link from line 20 points to the non-existing webpage (404 error code). Whenever inserting links to the external websites, make sure that they always point to the current, fresh version of the webpage. The correct link should be: `https://blog.openzeppelin.com/reentrancy-after-istanbul`.

# [62] Implement modifiers instead of repeating the same code twice

**File:** `Address.sol`

[File: code/system-contracts/contracts/openzeppelin/utils/Address.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/openzeppelin/utils/Address.sol#L61)
```solidity
61:         require(
62:             address(this).balance >= amount,
63:             "Address: insufficient balance"
64:         );
```

[File: code/system-contracts/contracts/openzeppelin/utils/Address.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/openzeppelin/utils/Address.sol#L155)
```solidity
155:         require(
156:             address(this).balance >= value,
157:             "Address: insufficient balance for call"
158:         );
```

Repeated checks can be easily re-implemented as modifiers.

# [63] Simplify expression by using de Morgan's laws

**File:** `DiamondProxy.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L31)
```solidity
31:         require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen
```

According to de Morgan's laws: `!A || !B <=> !(A & B)`, which means it's possible to remove one negation from above expression. This allows to simplify some expressions, e.g., above expression from `DiamondProxy.sol` at line 31 can be rewritten to:

```
require(!(diamondStorage.isFrozen && facet.isFreezable), "q1"); // Facet is frozen
```



# [64] Rename variable in `setNewBatch()`

**File:** `SystemContext.sol`

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L458)
```solidity
458:         // Setting new block number and timestamp
459:         BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp});
```

The whole function `setNewBatch()` names blocks as batches (actually, the whole `SystemContext.sol`) uses term `batch` instead of `block`. Thus it would improve the code readability when we will change the name of the `newBlockInfo` variable to `newBatchInfo`.




# [65] Use `require` instead of `assert`

**Files:** `RLPEncoder.sol`, `DiamondInit.sol`, `Executor.sol`, `DefaultAccount.sol`

[File: code/system-contracts/contracts/DefaultAccount.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L222)
```solidity
222:         assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS);
```

[File: code/system-contracts/contracts/libraries/RLPEncoder.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L50)
```solidity
50:         assert(_len != 1);
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L51)
```solidity
51:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32); 
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L426)
```solidity
426:         assert(block.chainid != 1); 
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L426)
```solidity
426:         assert(block.chainid != 1); 
```


# [66] Use descriptive `require` strings

Whenever code base uses `require()`, it should provide a descriptive string - why the revert happens. However, across the whole code-base, there are multiple of `require` statements with non-descriptive strings, e.g.:

```
./contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol: require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
./contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol: require(blobVersionedHash != bytes32(0), "vh");
```

For the report readability, we provide a simple `grep` which allows to detect those instances:

```
% grep "require(" -ri . | grep '"' | tr -s ' ' | grep .sol | grep -E "\".{1,4}\"" | wc -l
     138
```

# [67] Use named mappings

**Files:** `StateTransitionManager.sol`, `ContractDeployer.sol`, `ValidatorTimelock.sol`

Using named mapping increases the code readability.

[File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L30)
```solidity
30:     mapping(uint256 => address) public stateTransition;
[...]
48:     mapping(uint256 => bytes32) public upgradeCutHash;
```

[File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L47)
```solidity
47:     mapping(uint256 => LibMap.Uint32Map) internal committedBatchTimestamp;
```


[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L26)
```solidity
26:     mapping(address => AccountInfo) internal accountInfo;
```

# [68] Import specified identifier, instead of the whole file

It's recommended to specify what we're importing: `import {Test} from "File.sol"` instead of importing the whole file: `import "File.sol"`.

For the report readability, we provide a simple `grep` which allows to detect affected instances:

```
% grep "import \"" -ri . | grep ".sol" | grep -v "/test" | wc -l
      61
```

# [69] Missing `@NatSpec` declarations

Across the whole code-base, it was noticed that multiple of functions missed proper `@NatSpec`.
A lot of functions miss `@author`, `@dev`, `@notice` tags. Make sure that every function has proper `@NatSpec`.

# [70] Remove testing code from the production

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

As both NatSpec comment and the code-base suggests, above code is related to the testing environment. This code allows to manually set the blocks's number and timestamp.
It's recommended to remove any testing-related code from the production.
The severity of this issue was estimated as Informative only, since this method implements `onlyCallFromBootloader` - thus it's not possible to call it directly. Nonetheless, having testing code on the production is considered as bad practice.


# [71] Use descriptive comments when packing/unpacking integers

**File:** `SystemContractsCaller.sol`

Packing/unpacking integers may be very vague to the reader. It's recommended to provide a detailed description of each of the unpacked values. Our recommendation is to add detailed comment, which will describe how exactly the `farCallAbi` and `farCallAbiWithEmptyFarPtr` is being packed.

[File: code/contracts/zksync/contracts/SystemContractsCaller.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L115)
```solidity
115:         farCallAbi |= dataOffset;
116:         farCallAbi |= (uint256(memoryPage) << 32);
117:         farCallAbi |= (uint256(dataStart) << 64);
118:         farCallAbi |= (uint256(dataLength) << 96);
```

[File: code/contracts/zksync/contracts/SystemContractsCaller.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L128)
```solidity
128:         farCallAbiWithEmptyFatPtr |= (uint256(gasPassed) << 192);
129:         farCallAbiWithEmptyFatPtr |= (uint256(forwardingMode) << 224);
130:         farCallAbiWithEmptyFatPtr |= (uint256(shardId) << 232);
131:         if (isConstructorCall) {
132:             farCallAbiWithEmptyFatPtr |= (1 << 240);
133:         }
134:         if (isSystemCall) {
135:             farCallAbiWithEmptyFatPtr |= (1 << 248);
```


# [72] Sort contract addresses based on the offset

**File:** `L2ContractHelper.sol`

[File: code/contracts/zksync/contracts/L2ContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L70)
```solidity
70: address constant BOOTLOADER_ADDRESS = address(SYSTEM_CONTRACTS_OFFSET + 0x01);
71: address constant MSG_VALUE_SYSTEM_CONTRACT = address(SYSTEM_CONTRACTS_OFFSET + 0x09);
72: address constant DEPLOYER_SYSTEM_CONTRACT = address(SYSTEM_CONTRACTS_OFFSET + 0x06);
73: 
74: IL2Messenger constant L2_MESSENGER = IL2Messenger(address(SYSTEM_CONTRACTS_OFFSET + 0x08));
75: 
76: IBaseToken constant L2_BASE_TOKEN_ADDRESS = IBaseToken(address(SYSTEM_CONTRACTS_OFFSET + 0x0a));
```

To increase the readability of the code, it will be much better to sort the addresses based on the offset:

```
address constant BOOTLOADER_ADDRESS = address(SYSTEM_CONTRACTS_OFFSET + 0x01);
address constant DEPLOYER_SYSTEM_CONTRACT = address(SYSTEM_CONTRACTS_OFFSET + 0x06);
IL2Messenger constant L2_MESSENGER = IL2Messenger(address(SYSTEM_CONTRACTS_OFFSET + 0x08));
address constant MSG_VALUE_SYSTEM_CONTRACT = address(SYSTEM_CONTRACTS_OFFSET + 0x09);
IBaseToken constant L2_BASE_TOKEN_ADDRESS = IBaseToken(address(SYSTEM_CONTRACTS_OFFSET + 0x0a));
```

# [73] Keep proper structure in `IBridgehub.sol`

**File:** `IBridgehub.sol`

[File: code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L45)
```solidity
45:     event NewPendingAdmin(address indexed oldPendingAdmin, address indexed newPendingAdmin);
46: 
47:     /// @notice Admin changed
48:     event NewAdmin(address indexed oldAdmin, address indexed newAdmin);
```

[File: code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L131)
```solidity
131:     function setSharedBridge(address _sharedBridge) external;
132: 
133:     event NewChain(uint256 indexed chainId, address stateTransitionManager, address indexed chainGovernance);
```
As demonstrated above, interface firstly lists all events, then all functions. The only exception is the `NewChain` event which is listed as the last one in the interface.
Our recommendation is to always group functions and events. Please consider moving `NewChain` event from line 133 above (to lines 45-48) - where other events are.


# [74]  Remove todo code

**File:** `IZkSyncStateTransition.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L12)
```solidity
12: // kl to do remove this, needed for the server for now
13: import "../libraries/Diamond.sol";
14: 
15: interface IZkSyncStateTransition is IAdmin, IExecutor, IGetters, IMailbox {
16:     // KL todo: need this in the server for now
```


# [75] Typos 

**Files:** `SystemContractHelper.sol`, `DefaultAccount.sol`, `IPaymasterFlow.sol`

[File: code/system-contracts/contracts/libraries/SystemContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L242)
```solidity
242:     /// of the auxilary heap in bytes.
243:     /// @param meta Packed representation of the ZkSyncMeta.
244:     /// @return auxHeapSize The size of the auxilary memory in bytes byte.
245:     /// @dev You can read more on auxilary memory in the VM1.2 documentation.
```

`auxilary` should be changed to `auxiliary`.

[File: code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L10)
```solidity
10:  * @notice This is NOT an interface to be implementated
```

`implementated` should be change to `implemented`.


[File: code/system-contracts/contracts/DefaultAccount.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L158)
```solidity
158:     /// @return EIP1271_SUCCESS_RETURN_VALUE if the signaure is correct. It reverts otherwise.
```

`signaure` should be changed to `signature`.

# [76] Incorrect grammar

**Files:** `L2BaseToken.sol`, `DefaultAccount.sol`, `ISystemContext.sol`

[File: code/system-contracts/contracts/interfaces/ISystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L18)
```solidity
18:     /// @dev It will used for the L1 batch -> L2 block migration in Q3 2023 only.
```

`It will used` should be changed to `It will be used`.

[File: code/system-contracts/contracts/DefaultAccount.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L96)
```solidity
96:         // The fact there is are enough balance for the account
```

`there is are enough` should be changed to `there is enough`


[File: code/system-contracts/contracts/L2BaseToken.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L104)
```solidity
104:             // This is safe, since this contract holds the ether balances, and if user
105:             // send a `msg.value` it will be added to the contract (`this`) balance.
```

`if user send` should be changed to `if user sends`.

