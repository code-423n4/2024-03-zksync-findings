# Gas Report

Gas issues in [4naly3er-report](https://github.com/code-423n4/2024-03-zksync/blob/main/4naly3er-report.md) have been excluded.

## Summary

Total **831 instances** over **64 issues**with **796644** gas saved:

|ID|Issue|Instances|Gas|
|:--:|:---|:--:|:--:|
| [[G-01]](#g-01-use-storage-instead-of-memory-for-structsarrays) | Use `storage` instead of `memory` for structs/arrays | 9 | 37800 |
| [[G-02]](#g-02-constructors-can-be-marked-as-payable-to-save-deployment-gas) | Constructors can be marked as payable to save deployment gas | 8 | 168 |
| [[G-03]](#g-03-state-variables-only-set-in-their-definitions-should-be-declared-constant) | State variables only set in their definitions should be declared `constant` | 3 | 6291 |
| [[G-04]](#g-04-abiencode-is-less-efficient-than-abiencodepacked-for-non-address-arguments) | `abi.encode()` is less efficient than `abi.encodePacked()` for non-address arguments | 12 | - |
| [[G-05]](#g-05-comparing-booleans-to-true-or-false) | Comparing booleans to `true` or `false` | 1 | 9 |
| [[G-06]](#g-06-counting-down-in-for-statements-is-more-gas-efficient) | Counting down in for statements is more gas efficient | 8 | - |
| [[G-07]](#g-07-using-msg-globals-directly-rather-than-caching-the-value-saves-gas) | Using `msg` globals directly, rather than caching the value, saves gas | 1 | 10 |
| [[G-08]](#g-08-stack-variable-is-only-used-once) | Stack variable is only used once | 53 | 159 |
| [[G-09]](#g-09-do-not-cache-state-variables-that-are-used-only-once) | Do not cache state variables that are used only once | 14 | 42 |
| [[G-10]](#g-10-do-not-calculate-constants) | Do not calculate constants | 2 | - |
| [[G-11]](#g-11-use-of-emit-inside-a-loop) | Use of `emit` inside a loop | 3 | 1125 |
| [[G-12]](#g-12-emitting-literals-or-constants-wastes-gas) | Emitting literals or constants wastes gas | 6 | 48 |
| [[G-13]](#g-13-use-local-variables-for-emitting) | Use local variables for emitting | 9 | 900 |
| [[G-14]](#g-14-contract-storage-can-use-fewer-slots-by-changing-the-order-of-state-variables) | Contract storage can use fewer slots by changing the order of state variables | 1 | 20000 |
| [[G-15]](#g-15-structs-can-use-fewer-slots-by-changing-the-order-of-fields) | Structs can use fewer slots by changing the order of fields | 3 | 60000 |
| [[G-16]](#g-16-internal-functions-only-called-once-can-be-inlined-to-save-gas) | `internal` functions only called once can be inlined to save gas | 2 | 60 |
| [[G-17]](#g-17-inline-modifiers-that-are-only-used-once-to-save-gas) | Inline `modifier`s that are only used once to save gas | 7 | - |
| [[G-18]](#g-18-private-functions-only-used-once-can-be-inlined-to-save-gas) | Private functions only used once can be inlined to save gas | 6 | 180 |
| [[G-19]](#g-19-update-openzeppelin-dependency-to-save-gas) | Update OpenZeppelin dependency to save gas | 14 | - |
| [[G-20]](#g-20-arrayindex--amount-is-cheaper-than-arrayindex--arrayindex--amount-or-related-variants) | `array[index] += amount` is cheaper than `array[index] = array[index] + amount` (or related variants) | 1 | 38 |
| [[G-21]](#g-21-operator--costs-less-gas-than-operator-) | Operator `>=`/`<=` costs less gas than operator `>`/`<` | 17 | 51 |
| [[G-22]](#g-22-consider-pre-calculating-the-address-of-addressthis-to-save-gas) | Consider pre-calculating the address of `address(this)` to save gas | 11 | - |
| [[G-23]](#g-23-remove-empty-functions-to-save-gas) | Remove empty functions to save gas | 3 | - |
| [[G-24]](#g-24-usage-of-intsuints-smaller-than-32-bytes-incurs-overhead) | Usage of `int`s/`uint`s smaller than 32 bytes incurs overhead | 80 | 4400 |
| [[G-25]](#g-25-using-a-double-if-statement-instead-of-a-logical-and) | Using a double `if` statement instead of a logical AND(`&&`) | 2 | 60 |
| [[G-26]](#g-26-requirerevert-strings-longer-than-32-bytes-cost-extra-gas) | `require()`/`revert()` strings longer than 32 bytes cost extra gas | 52 | 156 |
| [[G-27]](#g-27-reduce-deployment-costs-by-tweaking-contracts-metadata) | Reduce deployment costs by tweaking contracts' metadata | 15 | - |
| [[G-28]](#g-28-divisions-can-be-unchecked-to-save-gas) | Divisions can be unchecked to save gas | 7 | 140 |
| [[G-29]](#g-29-use-assembly-to-validate-msgsender) | Use assembly to validate `msg.sender` | 27 | 324 |
| [[G-30]](#g-30-using-assembly-to-check-for-zero-can-save-gas) | Using assembly to check for zero can save gas | 62 | 372 |
| [[G-31]](#g-31-using-bitmaps-to-store-bool-arrays-or-regular-bool-mappings-can-save-gas) | Using bitmaps to store bool arrays or regular bool mappings can save gas | 1 | - |
| [[G-32]](#g-32-use--instead-of-new-bytes0-to-save-gas) | Use `""` instead of `new bytes(0)` to save gas | 8 | 2072 |
| [[G-33]](#g-33-consider-using-oz-enumerateset-in-place-of-nested-mappings) | Consider using OZ EnumerateSet in place of nested mappings | 7 | 7000 |
| [[G-34]](#g-34-use-x--y-instead-of-x--x--y-for-mapping-state-variables) | Use `x += y` instead of `x = x + y` for mapping state variables | 1 | 40 |
| [[G-35]](#g-35-consider-using-soladys-fixedpointmathlib) | Consider using solady's `FixedPointMathLib` | 1 | - |
| [[G-36]](#g-36-use-selfbalance-instead-of-addressxbalance) | Use `selfbalance()` instead of `address(x).balance` | 3 | 45 |
| [[G-37]](#g-37-avoid-zero-transfer-to-save-gas) | Avoid zero transfer to save gas | 4 | 400 |
| [[G-38]](#g-38-cache-addressthis-when-used-more-than-once) | Cache address(this) when used more than once | 7 | - |
| [[G-39]](#g-39-checking-constants-first-can-save-gas) | Checking constants first can save gas | 20 | - |
| [[G-40]](#g-40-state-variable-read-in-a-loop) | State variable read in a loop | 1 | 97 |
| [[G-41]](#g-41-unlimited-gas-consumption-risk-due-to-external-call-recipients) | Unlimited gas consumption risk due to external call recipients | 6 | - |
| [[G-42]](#g-42-optimize-names-to-save-gas) | Optimize names to save gas | 24 | 528 |
| [[G-43]](#g-43-reduce-gas-usage-by-moving-to-solidity-0819-or-later) | Reduce gas usage by moving to Solidity 0.8.19 or later | 22 | - |
| [[G-44]](#g-44-newer-versions-of-solidity-are-more-gas-efficient) | Newer versions of solidity are more gas efficient | 49 | - |
| [[G-45]](#g-45-avoid-updating-storage-when-the-value-hasnt-changed) | Avoid updating storage when the value hasn't changed | 20 | 16000 |
| [[G-46]](#g-46-same-cast-is-done-multiple-times) | Same cast is done multiple times | 5 | - |
| [[G-47]](#g-47-state-variables-that-are-used-multiple-times-in-a-function-should-be-cached-in-stack-variables) | State variables that are used multiple times in a function should be cached in stack variables | 14 | 3395 |
| [[G-48]](#g-48-use-solady-library-where-possible-to-save-gas) | Use solady library where possible to save gas | 14 | 14000 |
| [[G-49]](#g-49-contracts-can-use-fewer-storage-slots-by-truncating-state-variables) | Contracts can use fewer storage slots by truncating state variables | 2 | 40000 |
| [[G-50]](#g-50-structs-can-be-packed-into-fewer-storage-slots-by-truncating-fields) | Structs can be packed into fewer storage slots by truncating fields | 3 | 80000 |
| [[G-51]](#g-51-refactor-duplicated-requirerevert-checks-to-save-gas) | Refactor duplicated `require()`/`revert()` checks to save gas | 1 | - |
| [[G-52]](#g-52-using-constants-instead-of-enum-can-save-gas) | Using `constant`s instead of `enum` can save gas | 7 | - |
| [[G-53]](#g-53-assembly-use-scratch-space-for-building-calldata) | Assembly: Use scratch space for building calldata | 32 | 7040 |
| [[G-54]](#g-54-use-assembly-to-emit-events) | Use assembly to emit events | 53 | 2014 |
| [[G-55]](#g-55-use-assembly-to-compute-hashes-to-save-gas) | Use assembly to compute hashes to save gas | 2 | 160 |
| [[G-56]](#g-56-use-calldata-instead-of-memory-for-immutable-arguments) | Use `calldata` instead of `memory` for immutable arguments | 8 | 2400 |
| [[G-57]](#g-57-consider-using-soladys-gas-optimized-lib-for-math) | Consider Using Solady's Gas Optimized Lib for Math | 1 | - |
| [[G-58]](#g-58-do-while-is-cheaper-than-for-loops-when-the-initial-check-can-be-skipped) | `do`-`while` is cheaper than `for`-loops when the initial check can be skipped | 22 | - |
| [[G-59]](#g-59-consider-activating-via-ir-for-deploying) | Consider activating via-ir for deploying | 1 | - |
| [[G-60]](#g-60-avoid-unnecessary-public-variables) | Avoid Unnecessary Public Variables | 15 | 330000 |
| [[G-61]](#g-61-optimize-deployment-size-by-fine-tuning-ipfs-hash) | Optimize Deployment Size by Fine-tuning IPFS Hash | 15 | 159000 |
| [[G-62]](#g-62-multiple-accesses-of-a-memorycalldata-array-should-use-a-local-variable-cache) | Multiple accesses of a `memory`/`calldata` array should use a local variable cache | 15 | - |
| [[G-63]](#g-63-multiple-accesses-of-the-same-mapping-key-should-be-cached) | Multiple accesses of the same mapping key should be cached | 3 | 126 |
| [[G-64]](#g-64-consider-using-bytes32-rather-than-a-string) | Consider using `bytes32` rather than a `string` | 5 | - |

## Gas Optimizations

### [G-01] Use `storage` instead of `memory` for structs/arrays

When fetching data from a storage location, assigning the data to a `memory` variable causes all fields of the struct/array to be read from storage, which incurs a Gcoldsload (**2100 gas**) for *each* field of the struct/array. If the fields are read from the new memory variable, they incur an additional `MLOAD` rather than a cheap stack read. Instead of declaring the variable with the `memory` keyword, declaring the variable with the `storage` keyword and caching any fields that need to be re-read in stack variables, will be much cheaper, only incurring the Gcoldsload for the fields actually read. The only time it makes sense to read the whole struct/array into a `memory` variable, is if the full struct/array is being returned by the function, is being passed to a function that requires `memory`, or if the array/struct is being read from another `memory` array/struct.

<details>
<summary>There are 9 instances (click to show):</summary>

- *DiamondProxy.sol* ( [29-29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L29-L29) ):

```solidity
29:         Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];
```

- *Admin.sol* ( [74-74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L74-L74) ):

```solidity
74:         FeeParams memory oldFeeParams = s.feeParams;
```

- *Executor.sol* ( [398-398](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L398-L398) ):

```solidity
398:         VerifierParams memory verifierParams = s.verifierParams;
```

- *Getters.sol* ( [212-212](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L212-L212) ):

```solidity
212:             Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];
```

- *Mailbox.sol* ( [159-159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L159-L159) ):

```solidity
159:         FeeParams memory feeParams = s.feeParams;
```

- *Diamond.sol* ( [142-142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L142-L142), [162-162](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L162-L162), [182-182](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L182-L182) ):

```solidity
142:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

162:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

182:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
```

- *BaseZkSyncUpgrade.sol* ( [157-157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L157-L157) ):

```solidity
157:         VerifierParams memory oldVerifierParams = s.verifierParams;
```

</details>

### [G-02] Constructors can be marked as payable to save deployment gas

Payable functions cost less gas to execute, because the compiler does not have to add extra checks to ensure that no payment is provided. A constructor can be safely marked as payable, because only the deployer would be able to pass funds, and the project itself would not pass any funds.

<details>
<summary>There are 8 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [57-57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L57-L57) ):

```solidity
57:     constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
```

- *L1SharedBridge.sol* ( [92-96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L92-L96) ):

```solidity
92:     constructor(
93:         address _l1WethAddress,
94:         IBridgehub _bridgehub,
95:         IL1ERC20Bridge _legacyBridge
96:     ) reentrancyGuardInitializer {
```

- *Bridgehub.sol* ( [40-40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L40-L40) ):

```solidity
40:     constructor() reentrancyGuardInitializer {}
```

- *Governance.sol* ( [43-43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L43-L43) ):

```solidity
43:     constructor(address _admin, address _securityCouncil, uint256 _minDelay) {
```

- *StateTransitionManager.sol* ( [60-60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L60-L60) ):

```solidity
60:     constructor(address _bridgehub) reentrancyGuardInitializer {
```

- *ValidatorTimelock.sol* ( [57-57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57-L57) ):

```solidity
57:     constructor(address _initialOwner, uint32 _executionDelay) {
```

- *DiamondInit.sol* ( [21-21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L21-L21) ):

```solidity
21:     constructor() reentrancyGuardInitializer {}
```

- *DiamondProxy.sol* ( [13-13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L13-L13) ):

```solidity
13:     constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
```

</details>

### [G-03] State variables only set in their definitions should be declared `constant`

This can avoid a Gsset (**20000 gas**) on deployment (in constructor), and replaces the first access in each transaction (Gcoldsload - **2100 gas**) and each access thereafter (Gwarmacces - **100 gas**) with a `PUSH32` (**3 gas**).

There are 3 instances:

- *L1ERC20Bridge.sol* ( [38-38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L38-L38), [41-41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L41-L41), [44-44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L44-L44) ):

```solidity
38:     address public l2Bridge;

41:     address public l2TokenBeacon;

44:     bytes32 public l2TokenProxyBytecodeHash;
```

### [G-04] `abi.encode()` is less efficient than `abi.encodePacked()` for non-address arguments

<details>
<summary>There are 12 instances (click to show):</summary>

- *L1SharedBridge.sol* ( [260-260](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L260-L260) ):

```solidity
260:             bytes memory decimals = abi.encode(uint8(18));
```

- *Governance.sol* ( [207-207](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L207-L207) ):

```solidity
207:         return keccak256(abi.encode(_operation));
```

- *StateTransitionManager.sol* ( [102-102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102-L102), [104-104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L104-L104), [140-140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L140-L140), [149-149](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L149-L149), [158-158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L158-L158) ):

```solidity
102:         storedBatchZero = keccak256(abi.encode(batchZero));

104:         initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

140:         initialCutHash = keccak256(abi.encode(_diamondCut));

149:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

158:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
```

- *Admin.sol* ( [106-106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L106-L106) ):

```solidity
106:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
```

- *Executor.sol* ( [586-586](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L586-L586), [678-678](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L678-L678) ):

```solidity
586:         return keccak256(abi.encode(_storedBatchInfo));

678:         (bool success, bytes memory data) = s.blobVersionedHashRetriever.staticcall(abi.encode(_index));
```

- *Mailbox.sol* ( [325-325](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L325-L325) ):

```solidity
325:         bytes memory transactionEncoding = abi.encode(transaction);
```

- *BaseZkSyncUpgrade.sol* ( [194-194](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L194-L194) ):

```solidity
194:         bytes memory encodedTransaction = abi.encode(_l2ProtocolUpgradeTx);
```

</details>

### [G-05] Comparing booleans to `true` or `false`

The `true` and `false` are constants and it is more expensive comparing a boolean against them than checking the boolean value directly: `if (<x> == true)` => `if (<x>)`, `if (<x> == false)` => `if (!<x>)`.

There is 1 instance:

- *ValidatorTimelock.sol* ( [70](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L70) ):

```solidity
70:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
```

### [G-06] Counting down in for statements is more gas efficient

Looping downwards is more gas efficient because of how the EVM compares variables. When using a 'for' loop that counts down, comparing the end condition with zero is cheaper than comparing with another number. Therefore, it is recommended to restructure loops to count downwards whenever possible.

<details>
<summary>There are 8 instances (click to show):</summary>

- *Governance.sol* ( [227-227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L227-L227) ):

```solidity
227:         for (uint256 i = 0; i < _calls.length; ++i) {
```

- *ValidatorTimelock.sol* ( [118-118](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L118-L118), [137-137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L137-L137), [187-187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L187-L187), [211-211](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L211-L211) ):

```solidity
118:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

137:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

187:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

211:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```

- *Executor.sol* ( [578-578](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L578-L578), [665-665](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L665-L665) ):

```solidity
578:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

665:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```

- *BaseZkSyncUpgrade.sol* ( [228-228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L228-L228) ):

```solidity
228:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```

</details>

### [G-07] Using `msg` globals directly, rather than caching the value, saves gas

For example, use `msg.sender` directly rather than storing it to a local variable.

There is 1 instance:

- *L1SharedBridge.sol* ( [201-201](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L201-L201) ):

```solidity
201:             amount = msg.value;
```

### [G-08] Stack variable is only used once

If the variable is only accessed once, it's cheaper to use the assigned value directly that one time, and save the 3 gas the extra stack assignment would spend.

<details>
<summary>There are 53 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [79-79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L79-L79) ):

```solidity
/// @audit salt
79:         bytes32 salt = bytes32(uint256(uint160(_l1Token)));
```

- *L1SharedBridge.sol* ( [176-176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176-L176), [178-178](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L178-L178), [251-251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L251-L251), [258-258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L258-L258), [259-259](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L259-L259), [260-260](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L260-L260), [342-342](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L342-L342), [357-357](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L357-L357), [446-446](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L446-L446) ):

```solidity
/// @audit balanceBefore
176:         uint256 balanceBefore = _token.balanceOf(address(this));

/// @audit balanceAfter
178:         uint256 balanceAfter = _token.balanceOf(address(this));

/// @audit gettersData
251:         bytes memory gettersData = _getERC20Getters(_l1Token);

/// @audit name
258:             bytes memory name = bytes("Ether");

/// @audit symbol
259:             bytes memory symbol = bytes("ETH");

/// @audit decimals
260:             bytes memory decimals = abi.encode(uint8(18));

/// @audit dataHash
342:                 bytes32 dataHash = depositHappened[_chainId][_l2TxHash];

/// @audit callSuccess
357:             bool callSuccess;

/// @audit callSuccess
446:             bool callSuccess;
```

- *Bridgehub.sol* ( [55-55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55-L55), [66-66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L66-L66), [161-161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L161-L161), [173-173](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L173-L173), [187-187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L187-L187), [206-206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L206-L206) ):

```solidity
/// @audit oldPendingAdmin
55:         address oldPendingAdmin = pendingAdmin;

/// @audit previousAdmin
66:         address previousAdmin = admin;

/// @audit stateTransition
161:         address stateTransition = getStateTransition(_chainId);

/// @audit stateTransition
173:         address stateTransition = getStateTransition(_chainId);

/// @audit stateTransition
187:         address stateTransition = getStateTransition(_chainId);

/// @audit stateTransition
206:         address stateTransition = getStateTransition(_chainId);
```

- *ReentrancyGuard.sol* ( [49-49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L49-L49), [71-71](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L71-L71) ):

```solidity
/// @audit lockSlotOldValue
49:         uint256 lockSlotOldValue;

/// @audit _status
71:         uint256 _status;
```

- *L2ContractHelper.sol* ( [42-42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L42-L42), [68-68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L68-L68) ):

```solidity
/// @audit version
42:         uint8 version = uint8(_bytecodeHash[0]);

/// @audit senderBytes
68:         bytes32 senderBytes = bytes32(uint256(uint160(_sender)));
```

- *StateTransitionManager.sol* ( [114-114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L114-L114), [125-125](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L125-L125), [181-181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L181-L181), [182-182](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L182-L182), [221-221](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L221-L221), [257-257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L257-L257) ):

```solidity
/// @audit oldPendingAdmin
114:         address oldPendingAdmin = pendingAdmin;

/// @audit previousAdmin
125:         address previousAdmin = admin;

/// @audit uintEmptyArray
181:         uint256[] memory uintEmptyArray;

/// @audit bytesEmptyArray
182:         bytes[] memory bytesEmptyArray;

/// @audit emptyArray
221:         Diamond.FacetCut[] memory emptyArray;

/// @audit cutHashInput
257:         bytes32 cutHashInput = keccak256(_diamondCut);
```

- *ValidatorTimelock.sol* ( [185-185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185-L185), [209-209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209-L209) ):

```solidity
/// @audit delay
185:         uint256 delay = executionDelay; // uint32

/// @audit delay
209:         uint256 delay = executionDelay; // uint32
```

- *DiamondProxy.sol* ( [30-30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30-L30) ):

```solidity
/// @audit facetAddress
30:         address facetAddress = facet.facetAddress;
```

- *Admin.sol* ( [27-27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L27-L27), [38-38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L38-L38), [63-63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L63-L63), [74-74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L74-L74), [106-106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L106-L106) ):

```solidity
/// @audit oldPendingAdmin
27:         address oldPendingAdmin = s.pendingAdmin;

/// @audit previousAdmin
38:         address previousAdmin = s.admin;

/// @audit oldPriorityTxMaxGasLimit
63:         uint256 oldPriorityTxMaxGasLimit = s.priorityTxMaxGasLimit;

/// @audit oldFeeParams
74:         FeeParams memory oldFeeParams = s.feeParams;

/// @audit cutHashInput
106:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
```

- *Executor.sol* ( [398-398](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L398-L398), [505-505](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L505-L505), [543-543](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L543-L543), [615-615](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L615-L615) ):

```solidity
/// @audit verifierParams
398:         VerifierParams memory verifierParams = s.verifierParams;

/// @audit metadataHash
505:         bytes32 metadataHash = keccak256(_batchMetaParameters());

/// @audit l2ToL1LogsHash
543:         bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs);

/// @audit result
615:         (, uint256 result) = abi.decode(data, (uint256, uint256));
```

- *Getters.sol* ( [172-172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L172-L172) ):

```solidity
/// @audit selector0
172:             bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];
```

- *Mailbox.sol* ( [43-43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L43-L43), [44-44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L44-L44), [126-126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L126-L126), [273-273](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L273-L273) ):

```solidity
/// @audit amount
43:         uint256 amount = address(this).balance;

/// @audit sharedBridgeAddress
44:         address sharedBridgeAddress = s.baseTokenBridge;

/// @audit actualRootHash
126:         bytes32 actualRootHash = s.l2LogsRootHashes[_batchNumber];

/// @audit baseCost
273:         uint256 baseCost = _params.l2GasPrice * _params.l2GasLimit;
```

- *Diamond.sol* ( [102-102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L102-L102), [129-129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L129-L129), [139-139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L139-L139), [152-152](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L152-L152), [159-159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L159-L159), [175-175](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175-L175), [179-179](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L179-L179), [216-216](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L216-L216) ):

```solidity
/// @audit facetCutsLength
102:         uint256 facetCutsLength = facetCuts.length;

/// @audit ds
129:         DiamondStorage storage ds = getDiamondStorage();

/// @audit selectorsLength
139:         uint256 selectorsLength = _selectors.length;

/// @audit ds
152:         DiamondStorage storage ds = getDiamondStorage();

/// @audit selectorsLength
159:         uint256 selectorsLength = _selectors.length;

/// @audit ds
175:         DiamondStorage storage ds = getDiamondStorage();

/// @audit selectorsLength
179:         uint256 selectorsLength = _selectors.length;

/// @audit selector0
216:             bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];
```

- *BaseZkSyncUpgrade.sol* ( [137-137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L137-L137), [157-157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L157-L157) ):

```solidity
/// @audit oldVerifier
137:         IVerifier oldVerifier = s.verifier;

/// @audit oldVerifierParams
157:         VerifierParams memory oldVerifierParams = s.verifierParams;
```

</details>

### [G-09] Do not cache state variables that are used only once

It's cheaper to access the state variable directly if it is accessed only once. This can save some gas cost of the extra stack allocation.

<details>
<summary>There are 14 instances (click to show):</summary>

- *L1SharedBridge.sol* ( [342-342](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L342-L342) ):

```solidity
342:                 bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
```

- *Bridgehub.sol* ( [55-55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55-L55), [66-66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L66-L66) ):

```solidity
55:         address oldPendingAdmin = pendingAdmin;

66:         address previousAdmin = admin;
```

- *StateTransitionManager.sol* ( [114-114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L114-L114), [125-125](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L125-L125) ):

```solidity
114:         address oldPendingAdmin = pendingAdmin;

125:         address previousAdmin = admin;
```

- *Admin.sol* ( [27-27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L27-L27), [63-63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L63-L63), [74-74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L74-L74) ):

```solidity
27:         address oldPendingAdmin = s.pendingAdmin;

63:         uint256 oldPriorityTxMaxGasLimit = s.priorityTxMaxGasLimit;

74:         FeeParams memory oldFeeParams = s.feeParams;
```

- *Mailbox.sol* ( [44-44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L44-L44), [126-126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L126-L126) ):

```solidity
44:         address sharedBridgeAddress = s.baseTokenBridge;

126:         bytes32 actualRootHash = s.l2LogsRootHashes[_batchNumber];
```

- *BaseZkSyncUpgrade.sol* ( [102-102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L102-L102), [119-119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L119-L119), [137-137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L137-L137), [157-157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L157-L157) ):

```solidity
102:         bytes32 previousDefaultAccountBytecodeHash = s.l2DefaultAccountBytecodeHash;

119:         bytes32 previousBootloaderBytecodeHash = s.l2BootloaderBytecodeHash;

137:         IVerifier oldVerifier = s.verifier;

157:         VerifierParams memory oldVerifierParams = s.verifierParams;
```

</details>

### [G-10] Do not calculate constants

Due to how constant variables are implemented (replacements at compile-time), an expression assigned to a constant variable is recomputed each time that the variable is used, which wastes some gas.

There are 2 instances:

- *Config.sol* ( [16-16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L16-L16), [114-114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L114-L114) ):

```solidity
16: uint256 constant MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES = 4 + L2_TO_L1_LOG_SERIALIZE_SIZE * 512;

114: bytes32 constant TWO_BRIDGES_MAGIC_VALUE = bytes32(uint256(keccak256("TWO_BRIDGES_MAGIC_VALUE")) - 1);
```

### [G-11] Use of `emit` inside a loop

Emitting an event inside a loop performs a `LOG` op N times, where N is the loop length. Consider refactoring the code to emit the event only once at the end of loop. Gas savings should be multiplied by the average loop length.

There are 3 instances:

- *Executor.sol* ( [263-267](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L263-L267), [301-305](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L301-L305), [355-355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L355-L355) ):

```solidity
263:             emit BlockCommit(
264:                 _lastCommittedBatchData.batchNumber,
265:                 _lastCommittedBatchData.batchHash,
266:                 _lastCommittedBatchData.commitment
267:             );

301:             emit BlockCommit(
302:                 _lastCommittedBatchData.batchNumber,
303:                 _lastCommittedBatchData.batchHash,
304:                 _lastCommittedBatchData.commitment
305:             );

355:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
```

### [G-12] Emitting literals or constants wastes gas

Every event parameter costs `Glogdata` (**8 gas**) per byte. You can avoid this extra cost, in cases where you're emitting a literal or constant, by creating a second version of the event, which doesn't have the parameter (and have users look to the contract's variables for its value instead), and using the new event in the cases shown below.

<details>
<summary>There are 6 instances (click to show):</summary>

- *L1SharedBridge.sol* ( [604-604](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L604-L604) ):

```solidity
604:         emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
```

- *Bridgehub.sol* ( [70-70](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L70-L70) ):

```solidity
70:         emit NewPendingAdmin(currentPendingAdmin, address(0));
```

- *Governance.sol* ( [49-49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L49-L49), [52-52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L52-L52) ):

```solidity
49:         emit ChangeSecurityCouncil(address(0), _securityCouncil);

52:         emit ChangeMinDelay(0, _minDelay);
```

- *StateTransitionManager.sol* ( [129-129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L129-L129) ):

```solidity
129:         emit NewPendingAdmin(currentPendingAdmin, address(0));
```

- *Admin.sol* ( [42-42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L42-L42) ):

```solidity
42:         emit NewPendingAdmin(pendingAdmin, address(0));
```

</details>

### [G-13] Use local variables for emitting

Use the function/modifier's local copy of the state variable, rather than incurring an extra Gwarmaccess (**100 gas**). In the unlikely event that the state variable hasn't already been used by the function/modifier, consider whether it is really necessary to include it in the event, given the fact that it incurs a Gcoldsload (**2100 gas**), or whether it can be passed in to or back out of the functions that _do_ use it.

<details>
<summary>There are 9 instances (click to show):</summary>

- *Bridgehub.sol* ( [71-71](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L71-L71) ):

```solidity
/// @audit pendingAdmin
71:         emit NewAdmin(previousAdmin, pendingAdmin);
```

- *Governance.sol* ( [252-252](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L252-L252), [259-259](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L259-L259) ):

```solidity
/// @audit minDelay
252:         emit ChangeMinDelay(minDelay, _newDelay);

/// @audit securityCouncil
259:         emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```

- *StateTransitionManager.sol* ( [130-130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L130-L130), [229-229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L229-L229) ):

```solidity
/// @audit pendingAdmin
130:         emit NewAdmin(previousAdmin, pendingAdmin);

/// @audit protocolVersion
229:         emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
```

- *Executor.sol* ( [434-434](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L434-L434), [494-494](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L494-L494) ):

```solidity
/// @audit s
434:         emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

/// @audit s
/// @audit s
/// @audit s
494:         emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
```

</details>

### [G-14] Contract storage can use fewer slots by changing the order of state variables

The reduction of slots can reduce the gas consumption of each storage read/write operation. If variables occupying the same slot are written within the same transaction, avoids a separate Gsset (**20000 gas**). Reads of the variables can also be cheaper.

There is 1 instance:

- *ValidatorTimelock.sol* ( [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L24) ):

```solidity
/// @audit 4 slots -> 3 slots by new order:
///        32 B: mapping(uint256 => LibMap.Uint32Map) committedBatchTimestamp
///        32 B: mapping(uint256 _chainId => mapping(address _validator => bool)) validators
///        20 B: IStateTransitionManager stateTransitionManager
///        4 B: uint32 executionDelay
24: contract ValidatorTimelock is IExecutor, Ownable2Step {
```

### [G-15] Structs can use fewer slots by changing the order of fields

The reduction of slots can reduce the gas consumption of each storage read/write operation. Each slot saved can avoid an extra Gsset (**20000 gas**) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings.

<details>
<summary>There are 3 instances (click to show):</summary>

- *IStateTransitionManager.sol* ( [17-26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L17-L26) ):

```solidity
/// @audit 10 slots -> 9 slots by new order:
///        96 B: Diamond.DiamondCutData diamondCut
///        32 B: bytes32 genesisBatchHash
///        32 B: bytes32 genesisBatchCommitment
///        32 B: uint256 protocolVersion
///        20 B: address governor
///        8 B: uint64 genesisIndexRepeatedStorageChanges
///        20 B: address validatorTimelock
///        20 B: address genesisUpgrade
17: struct StateTransitionManagerInitializeData {
18:     address governor;
19:     address validatorTimelock;
20:     address genesisUpgrade;
21:     bytes32 genesisBatchHash;
22:     uint64 genesisIndexRepeatedStorageChanges;
23:     bytes32 genesisBatchCommitment;
24:     Diamond.DiamondCutData diamondCut;
25:     uint256 protocolVersion;
26: }
```

- *ZkSyncStateTransitionStorage.sol* ( [68-155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L68-L155) ):

```solidity
/// @audit 46 slots -> 45 slots by new order:
///        224 B: uint256[7] __DEPRECATED_diamondCutStorage
///        96 B: PriorityQueue.Queue priorityQueue
///        96 B: VerifierParams verifierParams
///        64 B: UpgradeStorage __DEPRECATED_upgrades
///        32 B: mapping(address validatorAddress => bool isValidator) validators
///        32 B: uint256 totalBatchesExecuted
///        32 B: uint256 totalBatchesVerified
///        32 B: uint256 totalBatchesCommitted
///        32 B: mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes
///        32 B: mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes
///        32 B: bytes32 l2BootloaderBytecodeHash
///        32 B: bytes32 l2DefaultAccountBytecodeHash
///        32 B: uint256 priorityTxMaxGasLimit
///        32 B: mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized
///        32 B: uint256 __DEPRECATED_lastWithdrawalLimitReset
///        32 B: uint256 __DEPRECATED_withdrawnAmountInWindow
///        32 B: mapping(address => uint256) __DEPRECATED_totalDepositedAmountPerUser
///        32 B: uint256 protocolVersion
///        32 B: bytes32 l2SystemContractsUpgradeTxHash
///        32 B: uint256 l2SystemContractsUpgradeBatchNumber
///        32 B: FeeParams feeParams
///        32 B: uint256 chainId
///        20 B: address __DEPRECATED_governor
///        1 B: bool zkPorterIsAvailable
///        20 B: address __DEPRECATED_pendingGovernor
///        20 B: IVerifier verifier
///        20 B: address __DEPRECATED_allowList
///        20 B: address admin
///        20 B: address pendingAdmin
///        20 B: address blobVersionedHashRetriever
///        20 B: address bridgehub
///        20 B: address stateTransitionManager
///        20 B: address baseToken
///        20 B: address baseTokenBridge
///        16 B: uint128 baseTokenGasPriceMultiplierNominator
///        16 B: uint128 baseTokenGasPriceMultiplierDenominator
68: struct ZkSyncStateTransitionStorage {
69:     /// @dev Storage of variables needed for deprecated diamond cut facet
70:     uint256[7] __DEPRECATED_diamondCutStorage;
71:     /// @notice Address which will exercise critical changes to the Diamond Proxy (upgrades, freezing & unfreezing). Replaced by STM
72:     address __DEPRECATED_governor;
73:     /// @notice Address that the governor proposed as one that will replace it
74:     address __DEPRECATED_pendingGovernor;
75:     /// @notice List of permitted validators
76:     mapping(address validatorAddress => bool isValidator) validators;
77:     /// @dev Verifier contract. Used to verify aggregated proof for batches
78:     IVerifier verifier;
79:     /// @notice Total number of executed batches i.e. batches[totalBatchesExecuted] points at the latest executed batch
80:     /// (batch 0 is genesis)
81:     uint256 totalBatchesExecuted;
82:     /// @notice Total number of proved batches i.e. batches[totalBatchesProved] points at the latest proved batch
83:     uint256 totalBatchesVerified;
84:     /// @notice Total number of committed batches i.e. batches[totalBatchesCommitted] points at the latest committed
85:     /// batch
86:     uint256 totalBatchesCommitted;
87:     /// @dev Stored hashed StoredBatch for batch number
88:     mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
89:     /// @dev Stored root hashes of L2 -> L1 logs
90:     mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;
91:     /// @dev Container that stores transactions requested from L1
92:     PriorityQueue.Queue priorityQueue;
...... OMITTED ......
131:     /// @dev Address which will exercise non-critical changes to the Diamond Proxy (changing validator set & unfreezing)
132:     address admin;
133:     /// @notice Address that the admin proposed as one that will replace admin role
134:     address pendingAdmin;
135:     /// @dev Fee params used to derive gasPrice for the L1->L2 transactions. For L2 transactions,
136:     /// the bootloader gives enough freedom to the operator.
137:     FeeParams feeParams;
138:     /// @dev Address of the blob versioned hash getter smart contract used for EIP-4844 versioned hashes.
139:     address blobVersionedHashRetriever;
140:     /// new fields
141:     /// @dev The chainId of the chain
142:     uint256 chainId;
143:     /// @dev The address of the bridgehub
144:     address bridgehub;
145:     /// @dev The address of the StateTransitionManager
146:     address stateTransitionManager;
147:     /// @dev The address of the baseToken contract. Eth is address(1)
148:     address baseToken;
149:     /// @dev The address of the baseTokenbridge. Eth also uses the shared bridge
150:     address baseTokenBridge;
151:     /// @notice gasPriceMultiplier for each baseToken, so that each L1->L2 transaction pays for its transaction on the destination
152:     /// we multiply by the nominator, and divide by the denominator
153:     uint128 baseTokenGasPriceMultiplierNominator;
154:     uint128 baseTokenGasPriceMultiplierDenominator;
155: }
```

- *IExecutor.sol* ( [85-94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L85-L94) ):

```solidity
/// @audit 8 slots -> 7 slots by new order:
///        32 B: bytes32 batchHash
///        32 B: uint256 numberOfLayer1Txs
///        32 B: bytes32 priorityOperationsHash
///        32 B: bytes32 l2LogsTreeRoot
///        32 B: uint256 timestamp
///        32 B: bytes32 commitment
///        8 B: uint64 batchNumber
///        8 B: uint64 indexRepeatedStorageChanges
85:     struct StoredBatchInfo {
86:         uint64 batchNumber;
87:         bytes32 batchHash;
88:         uint64 indexRepeatedStorageChanges;
89:         uint256 numberOfLayer1Txs;
90:         bytes32 priorityOperationsHash;
91:         bytes32 l2LogsTreeRoot;
92:         uint256 timestamp;
93:         bytes32 commitment;
94:     }
```

</details>

### [G-16] `internal` functions only called once can be inlined to save gas

If an `internal` function is only used once, there is no need to modularize it, unless the function calling it would otherwise be too long and complex. Not inlining costs 20 to 40 gas because of two extra JUMP instructions and additional stack operations needed for function calls.

There are 2 instances:

- *Executor.sol* ( [590-590](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L590-L590), [595-595](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L595-L595) ):

```solidity
590:     function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

595:     function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {
```

### [G-17] Inline `modifier`s that are only used once to save gas

Inline `modifier`s that are only used once can save gas.

There are 7 instances:

- *L1SharedBridge.sol* ( [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L76) ):

```solidity
76:     modifier onlyBridgehubOrEra(uint256 _chainId) {
```

- *Governance.sol* ( [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L66), [72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L72) ):

```solidity
66:     modifier onlySecurityCouncil() {

72:     modifier onlyOwnerOrSecurityCouncil() {
```

- *StateTransitionManager.sol* ( [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L65) ):

```solidity
65:     modifier onlyBridgehub() {
```

- *ZkSyncStateTransitionBase.sol* ( [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L33), [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L46), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L54) ):

```solidity
33:     modifier onlyBridgehub() {

46:     modifier onlyValidatorOrStateTransitionManager() {

54:     modifier onlyBaseTokenBridge() {
```

### [G-18] Private functions only used once can be inlined to save gas

If a `private` function is only used once, there is no need to modularize it, unless the function calling it would otherwise be too long and complex.

There are 6 instances:

- *ReentrancyGuard.sol* ( [48-48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L48-L48) ):

```solidity
48:     function _initializeReentrancyGuard() private {
```

- *Diamond.sol* ( [174-174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L174-L174) ):

```solidity
174:     function _removeFunctions(address _facet, bytes4[] memory _selectors) private {
```

- *BaseZkSyncUpgrade.sol* ( [94-94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L94-L94), [111-111](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L111-L111), [128-128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L128-L128), [224-224](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L224-L224) ):

```solidity
94:     function _setL2DefaultAccountBytecodeHash(bytes32 _l2DefaultAccountBytecodeHash) private {

111:     function _setL2BootloaderBytecodeHash(bytes32 _l2BootloaderBytecodeHash) private {

128:     function _setVerifier(IVerifier _newVerifier) private {

224:     function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure {
```

### [G-19] Update OpenZeppelin dependency to save gas

Every release contains new gas optimizations. Use the latest version to take advantage of this.

The imported version is `4.9.5`.

<details>
<summary>There are 14 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L7), [8](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L8) ):

```solidity
7: import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";

8: import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```

- *L1SharedBridge.sol* ( [7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L7), [8](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L8), [10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L10), [11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L11), [12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L12) ):

```solidity
7: import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";

8: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";

10: import {IERC20Metadata} from "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";

11: import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";

12: import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```

- *Bridgehub.sol* ( [7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L7) ):

```solidity
7: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```

- *Governance.sol* ( [7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L7) ):

```solidity
7: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```

- *StateTransitionManager.sol* ( [18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L18) ):

```solidity
18: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```

- *ValidatorTimelock.sol* ( [7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L7) ):

```solidity
7: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```

- *Mailbox.sol* ( [7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L7) ):

```solidity
7: import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
```

- *Diamond.sol* ( [7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L7) ):

```solidity
7: import {SafeCast} from "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

- *TransactionValidator.sol* ( [7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L7) ):

```solidity
7: import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
```

</details>

### [G-20] `array[index] += amount` is cheaper than `array[index] = array[index] + amount` (or related variants)

When updating a value in an array with arithmetic, using `array[index] += amount` is cheaper than `array[index] = array[index] + amount`.
This is because you avoid an additional `mload` when the array is stored in memory, and an `sload` when the array is stored in storage.
This can be applied for any arithmetic operation including `+=`, `-=`,`/=`,`*=`,`^=`,`&=`, `%=`, `<<=`,`>>=`, and `>>>=`.
This optimization can be particularly significant if the pattern occurs during a loop.

*Saves 28 gas for a storage array, 38 for a memory array*

There is 1 instance:

- *L1SharedBridge.sol* ( [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L135) ):

```solidity
135:             chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
```

### [G-21] Operator `>=`/`<=` costs less gas than operator `>`/`<`

The compiler uses opcodes `GT` and `ISZERO` for code that uses `>`, but only requires `LT` for `>=`. A similar behavior applies for `>`, which uses opcodes `LT` and `ISZERO`, but only requires `GT` for `<=`. It can [save **3 gas**](https://gist.github.com/IllIllI000/3dc79d25acccfa16dee4e83ffdc6ffde) for each.
It should be converted to the `<=`/`>=` equivalent when comparing against integer literals. In cases where a for-loop is being used, one can count down rather than up, in order to use the optimal operator.

<details>
<summary>There are 17 instances (click to show):</summary>

- *L1SharedBridge.sol* ( [131-131](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131-L131), [329-329](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L329-L329) ):

```solidity
131:             require(amount > 0, "ShB: 0 amount to transfer");

329:         require(_amount > 0, "y1");
```

- *Bridgehub.sol* ( [303-303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L303-L303), [331-331](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L331-L331) ):

```solidity
303:             _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,

331:         } else if (_refundRecipient.code.length > 0) {
```

- *L2ContractHelper.sol* ( [28-28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L28-L28) ):

```solidity
28:         require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words
```

- *Executor.sol* ( [430-430](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L430-L430), [578-578](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L578-L578), [591-591](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L591-L591), [629-629](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L629-L629), [665-665](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L665-L665) ):

```solidity
430:         if (_proof.serializedProof.length > 0) {

578:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

591:         return (_bitMap & (1 << _index)) > 0;

629:         require(_pubdataCommitments.length > 0, "pl");

665:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```

- *Mailbox.sol* ( [160-160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L160-L160), [279-279](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L279-L279) ):

```solidity
160:         require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

279:         if (refundRecipient.code.length > 0) {
```

- *Diamond.sol* ( [109-109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L109-L109), [134-134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L134-L134), [157-157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L157-L157) ):

```solidity
109:             require(selectors.length > 0, "B"); // no functions for diamond cut

134:         require(_facet.code.length > 0, "G");

157:         require(_facet.code.length > 0, "K");
```

- *Merkle.sol* ( [26-26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L26-L26), [27-27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L27-L27) ):

```solidity
26:         require(pathLength > 0, "xc");

27:         require(pathLength < 256, "bt");
```

</details>

### [G-22] Consider pre-calculating the address of `address(this)` to save gas

Use `foundry`'s [`script.sol`](https://book.getfoundry.sh/reference/forge-std/compute-create-address) or `solady`'s [`LibRlp.sol`](https://github.com/Vectorized/solady/blob/main/src/utils/LibRLP.sol) to save the value in a constant, which will avoid having to spend gas to push the value on the stack every time it's used.

<details>
<summary>There are 11 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [67-67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67-L67) ):

```solidity
67:         uint256 amount = IERC20(_token).balanceOf(address(this));
```

- *L1SharedBridge.sol* ( [120-120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120-L120), [122-122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L122-L122), [129-129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129-L129), [133-133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133-L133), [176-176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176-L176), [177-177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L177-L177), [178-178](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L178-L178) ):

```solidity
120:             uint256 balanceBefore = address(this).balance;

122:             uint256 balanceAfter = address(this).balance;

129:             uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

133:             uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

176:         uint256 balanceBefore = _token.balanceOf(address(this));

177:         _token.safeTransferFrom(_from, address(this), _amount);

178:         uint256 balanceAfter = _token.balanceOf(address(this));
```

- *Governance.sol* ( [61-61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L61-L61) ):

```solidity
61:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
```

- *StateTransitionManager.sol* ( [267-267](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L267-L267) ):

```solidity
267:             bytes32(uint256(uint160(address(this)))),
```

- *Mailbox.sol* ( [43-43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L43-L43) ):

```solidity
43:         uint256 amount = address(this).balance;
```

</details>

### [G-23] Remove empty functions to save gas

Empty function body in solidity is not recommended, remove it can save gas.

There are 3 instances:

- *L1ERC20Bridge.sol* ( [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L62) ):

```solidity
62:     function initialize() external reentrancyGuardInitializer {}
```

- *BaseZkSyncUpgrade.sol* ( [265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L265), [271](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L271) ):

```solidity
265:     function _upgradeL1Contract(bytes calldata _customCallDataForUpgrade) internal virtual {}

271:     function _postUpgrade(bytes calldata _customCallDataForUpgrade) internal virtual {}
```

### [G-24] Usage of `int`s/`uint`s smaller than 32 bytes incurs overhead

Using `ints`/`uints` smaller than 32 bytes may cost more gas. This is because the EVM operates on 32 bytes at a time, so if an element is smaller than 32 bytes, the EVM must perform more operations to reduce the size of the element from 32 bytes to the desired size.

<details>
<summary>There are 80 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [184-184](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L184-L184), [213-213](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L213-L213) ):

```solidity
/// @audit uint16
184:         uint16 _l2TxNumberInBatch,

/// @audit uint16
213:         uint16 _l2TxNumberInBatch,
```

- *L1SharedBridge.sol* ( [287-287](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L287-L287), [314-314](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L314-L314), [391-391](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L391-L391), [406-406](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L406-L406), [415-415](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L415-L415), [505-505](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L505-L505), [620-620](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L620-L620), [653-653](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L653-L653) ):

```solidity
/// @audit uint16
287:         uint16 _l2TxNumberInBatch,

/// @audit uint16
314:         uint16 _l2TxNumberInBatch,

/// @audit uint16
391:         uint16 _l2TxNumberInBatch,

/// @audit uint16
406:         uint16 l2TxNumberInBatch;

/// @audit uint16
415:         uint16 _l2TxNumberInBatch,

/// @audit uint32
505:         (uint32 functionSignature, uint256 offset) = UnsafeBytes.readUint32(_l2ToL1message, 0);

/// @audit uint16
620:         uint16 _l2TxNumberInBatch,

/// @audit uint16
653:         uint16 _l2TxNumberInBatch,
```

- *IL1ERC20Bridge.sol* ( [51-51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L51-L51), [58-58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L58-L58) ):

```solidity
/// @audit uint16
51:         uint16 _l2TxNumberInBatch,

/// @audit uint16
58:         uint16 _l2TxNumberInBatch,
```

- *IL1SharedBridge.sol* ( [83-83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L83-L83), [95-95](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L95-L95), [102-102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L102-L102), [111-111](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L111-L111) ):

```solidity
/// @audit uint16
83:         uint16 _l2TxNumberInBatch,

/// @audit uint16
95:         uint16 _l2TxNumberInBatch,

/// @audit uint16
102:         uint16 _l2TxNumberInBatch,

/// @audit uint16
111:         uint16 _l2TxNumberInBatch,
```

- *Bridgehub.sol* ( [183-183](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L183-L183) ):

```solidity
/// @audit uint16
183:         uint16 _l2TxNumberInBatch,
```

- *IBridgehub.sol* ( [32-32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L32-L32), [96-96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L96-L96) ):

```solidity
/// @audit uint256
32:     uint256 secondBridgeValue;

/// @audit uint16
96:         uint16 _l2TxNumberInBatch,
```

- *Messaging.sol* ( [26-26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L26-L26), [28-28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L28-L28), [40-40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L40-L40), [62-62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L62-L62) ):

```solidity
/// @audit uint8
26:     uint8 l2ShardId;

/// @audit uint16
28:     uint16 txNumberInBatch;

/// @audit uint16
40:     uint16 txNumberInBatch;

/// @audit uint64
62:     uint64 expirationTimestamp;
```

- *L2ContractHelper.sol* ( [42-42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L42-L42) ):

```solidity
/// @audit uint8
42:         uint8 version = uint8(_bytecodeHash[0]);
```

- *UnsafeBytes.sol* ( [21-21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L21-L21) ):

```solidity
/// @audit uint32
21:     function readUint32(bytes memory _bytes, uint256 _start) internal pure returns (uint32 result, uint256 offset) {
```

- *Governance.sol* ( [37-37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L37-L37) ):

```solidity
/// @audit uint256
37:     uint256 public minDelay;
```

- *IStateTransitionManager.sol* ( [22-22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L22-L22) ):

```solidity
/// @audit uint64
22:     uint64 genesisIndexRepeatedStorageChanges;
```

- *ValidatorTimelock.sol* ( [55-55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55-L55), [57-57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57-L57), [98-98](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98-L98), [117-117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L117-L117), [136-136](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L136-L136) ):

```solidity
/// @audit uint32
55:     uint32 public executionDelay;

/// @audit uint32
57:     constructor(address _initialOwner, uint32 _executionDelay) {

/// @audit uint32
98:     function setExecutionDelay(uint32 _executionDelay) external onlyOwner {

/// @audit uint32
117:             uint32 timestamp = uint32(block.timestamp);

/// @audit uint32
136:             uint32 timestamp = uint32(block.timestamp);
```

- *ZkSyncStateTransitionStorage.sol* ( [34-34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L34-L34), [35-35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L35-L35), [56-56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L56-L56), [57-57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L57-L57), [58-58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L58-L58), [59-59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L59-L59), [60-60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L60-L60), [153-153](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L153-L153), [154-154](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L154-L154) ):

```solidity
/// @audit uint40
34:     uint40 proposedUpgradeTimestamp;

/// @audit uint40
35:     uint40 currentProposalId;

/// @audit uint32
56:     uint32 batchOverheadL1Gas;

/// @audit uint32
57:     uint32 maxPubdataPerBatch;

/// @audit uint32
58:     uint32 maxL2GasPerBatch;

/// @audit uint32
59:     uint32 priorityTxMaxPubdata;

/// @audit uint64
60:     uint64 minimalL2GasPrice;

/// @audit uint128
153:     uint128 baseTokenGasPriceMultiplierNominator;

/// @audit uint128
154:     uint128 baseTokenGasPriceMultiplierDenominator;
```

- *Admin.sol* ( [81-81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L81-L81), [81-81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L81-L81), [82-82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L82-L82), [83-83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L83-L83) ):

```solidity
/// @audit uint128
81:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {

/// @audit uint128
81:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {

/// @audit uint128
82:         uint128 oldNominator = s.baseTokenGasPriceMultiplierNominator;

/// @audit uint128
83:         uint128 oldDenominator = s.baseTokenGasPriceMultiplierDenominator;
```

- *Executor.sol* ( [41-41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L41-L41), [590-590](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L590-L590), [595-595](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L595-L595) ):

```solidity
/// @audit uint8
41:         uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));

/// @audit uint8
590:     function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

/// @audit uint8
595:     function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {
```

- *Getters.sol* ( [69-69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L69-L69), [74-74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L74-L74) ):

```solidity
/// @audit uint128
69:     function baseTokenGasPriceMultiplierNominator() external view returns (uint128) {

/// @audit uint128
74:     function baseTokenGasPriceMultiplierDenominator() external view returns (uint128) {
```

- *Mailbox.sol* ( [80-80](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L80-L80), [183-183](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L183-L183) ):

```solidity
/// @audit uint16
80:         uint16 _l2TxNumberInBatch,

/// @audit uint16
183:         uint16 _l2TxNumberInBatch,
```

- *IAdmin.sol* ( [42-42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L42-L42), [42-42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L42-L42), [86-86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L86-L86), [87-87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L87-L87), [88-88](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L88-L88), [89-89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L89-L89) ):

```solidity
/// @audit uint128
42:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external;

/// @audit uint128
42:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external;

/// @audit uint128
86:         uint128 oldNominator,

/// @audit uint128
87:         uint128 oldDenominator,

/// @audit uint128
88:         uint128 newNominator,

/// @audit uint128
89:         uint128 newDenominator
```

- *IExecutor.sol* ( [36-36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L36-L36), [86-86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L86-L86), [88-88](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L88-L88), [92-92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L92-L92), [115-115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L115-L115), [116-116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L116-L116), [117-117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L117-L117) ):

```solidity
/// @audit uint256
36:     uint256 packedBatchAndL2BlockTimestamp;

/// @audit uint64
86:         uint64 batchNumber;

/// @audit uint64
88:         uint64 indexRepeatedStorageChanges;

/// @audit uint256
92:         uint256 timestamp;

/// @audit uint64
115:         uint64 batchNumber;

/// @audit uint64
116:         uint64 timestamp;

/// @audit uint64
117:         uint64 indexRepeatedStorageChanges;
```

- *IGetters.sol* ( [114-114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L114-L114), [117-117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L117-L117) ):

```solidity
/// @audit uint128
114:     function baseTokenGasPriceMultiplierNominator() external view returns (uint128);

/// @audit uint128
117:     function baseTokenGasPriceMultiplierDenominator() external view returns (uint128);
```

- *IMailbox.sol* ( [53-53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L53-L53), [67-67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L67-L67), [128-128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L128-L128) ):

```solidity
/// @audit uint16
53:         uint16 _l2TxNumberInBatch,

/// @audit uint16
67:         uint16 _l2TxNumberInBatch,

/// @audit uint64
128:         uint64 expirationTimestamp,
```

- *Diamond.sol* ( [34-34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L34-L34), [43-43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L43-L43), [210-210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L210-L210) ):

```solidity
/// @audit uint16
34:         uint16 selectorPosition;

/// @audit uint16
43:         uint16 facetPosition;

/// @audit uint16
210:         uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16();
```

- *LibMap.sol* ( [20-20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L20-L20), [40-40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L40-L40), [56-56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L56-L56) ):

```solidity
/// @audit uint32
20:     function get(Uint32Map storage _map, uint256 _index) internal view returns (uint32 result) {

/// @audit uint32
40:     function set(Uint32Map storage _map, uint256 _index, uint32 _value) internal {

/// @audit uint32
56:             uint32 oldValue = uint32(mapValue >> bitOffset);
```

- *PriorityQueue.sol* ( [14-14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L14-L14), [15-15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L15-L15) ):

```solidity
/// @audit uint64
14:     uint64 expirationTimestamp;

/// @audit uint192
15:     uint192 layer2Tip;
```

- *BaseZkSyncUpgrade.sol* ( [39-39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L39-L39) ):

```solidity
/// @audit uint256
39:     uint256 upgradeTimestamp;
```

- *AddressAliasHelper.sol* ( [24-24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L24-L24) ):

```solidity
/// @audit uint160
24:     uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
```

</details>

### [G-25] Using a double `if` statement instead of a logical AND(`&&`)

Using a double `if` statement instead of a logical AND (`&&`) can provide similar short-circuiting behavior whereas double if is slightly [more gas efficient](https://gist.github.com/DadeKuma/931ce6794a050201ec6544dbcc31316c).

There are 2 instances:

- *Executor.sol* ( [363-363](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L363-L363) ):

```solidity
363:         if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {
```

- *BaseZkSyncUpgrade.sol* ( [149-152](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L149-L152) ):

```solidity
149:         if (
150:             _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) &&
151:             _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) &&
152:             _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)
```

### [G-26] `require()`/`revert()` strings longer than 32 bytes cost extra gas

Each extra memory word of bytes past the original 32 [incurs an MSTORE](https://gist.github.com/hrkrshnn/ee8fabd532058307229d65dcd5836ddc#consider-having-short-revert-strings) which costs **3 gas**

<details>
<summary>There are 52 instances (click to show):</summary>

- *L1SharedBridge.sol* ( [77-80](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L77-L80), [157-157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L157-L157), [197-197](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L197-L197), [429-429](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L429-L429), [524-524](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L524-L524), [566-566](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L566-L566) ):

```solidity
77:         require(
78:             msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
79:             "L1SharedBridge: not bridgehub or era chain"
80:         );

157:             require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");

197:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

429:             require(!alreadyFinalized, "Withdrawal is already finalized 2");

524:             revert("ShB Incorrect message function selector");

566:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
```

- *Bridgehub.sol* ( [85-88](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L85-L88), [95-98](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L95-L98), [104-104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L104-L104), [127-130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L127-L130), [134-134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134-L134), [227-227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L227-L227), [302-305](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L302-L305) ):

```solidity
85:         require(
86:             !stateTransitionManagerIsRegistered[_stateTransitionManager],
87:             "Bridgehub: state transition already registered"
88:         );

95:         require(
96:             stateTransitionManagerIsRegistered[_stateTransitionManager],
97:             "Bridgehub: state transition not registered yet"
98:         );

104:         require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

127:         require(
128:             stateTransitionManagerIsRegistered[_stateTransitionManager],
129:             "Bridgehub: state transition not registered"
130:         );

134:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

227:                 require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");

302:         require(
303:             _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
304:             "Bridgehub: second bridge address too low"
305:         ); // to avoid calls to precompiles
```

- *Governance.sol* ( [61-61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L61-L61), [67-67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L67-L67), [73-76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L73-L76), [174-174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L174-L174), [179-179](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L179-L179), [193-193](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L193-L193), [198-198](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L198-L198), [218-218](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L218-L218), [219-219](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L219-L219), [242-242](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L242-L242) ):

```solidity
61:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

67:         require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

73:         require(
74:             msg.sender == owner() || msg.sender == securityCouncil,
75:             "Only the owner and security council are allowed to call this function"
76:         );

174:         require(isOperationReady(id), "Operation must be ready before execution");

179:         require(isOperationReady(id), "Operation must be ready after execution");

193:         require(isOperationPending(id), "Operation must be pending before execution");

198:         require(isOperationPending(id), "Operation must be pending after execution");

218:         require(!isOperation(_id), "Operation with this proposal id already exists");

219:         require(_delay >= minDelay, "Proposed delay is less than minimum delay");

242:         require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");
```

- *StateTransitionManager.sol* ( [258-258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L258-L258) ):

```solidity
258:         require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");
```

- *ValidatorTimelock.sol* ( [64-64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L64-L64), [70-70](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L70-L70) ):

```solidity
64:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

70:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
```

- *Admin.sol* ( [92-92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92-L92), [107-110](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L107-L110), [112-115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L112-L115), [118-121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L118-L121) ):

```solidity
92:         require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed

107:         require(
108:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
109:             "StateTransition: cutHash mismatch"
110:         );

112:         require(
113:             s.protocolVersion == _oldProtocolVersion,
114:             "StateTransition: protocolVersion mismatch in STC when upgrading"
115:         );

118:         require(
119:             s.protocolVersion > _oldProtocolVersion,
120:             "StateTransition: protocolVersion mismatch in STC after upgrading"
121:         );
```

- *Executor.sol* ( [228-231](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L228-L231), [614-614](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L614-L614) ):

```solidity
228:         require(
229:             IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
230:             "Executor facet: wrong protocol version"
231:         );

614:         require(success, "failed to call point evaluation precompile");
```

- *Mailbox.sol* ( [41-41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41-L41), [160-160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L160-L160), [187-187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L187-L187), [208-208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L208-L208) ):

```solidity
41:         require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");

160:         require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

187:         require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");

208:         require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");
```

- *ZkSyncStateTransitionBase.sol* ( [24-24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L24-L24), [29-29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L29-L29), [34-34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L34-L34), [39-42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L39-L42), [47-50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L47-L50), [55-55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L55-L55) ):

```solidity
24:         require(s.validators[msg.sender], "StateTransition Chain: not validator");

29:         require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

34:         require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

39:         require(
40:             msg.sender == s.admin || msg.sender == s.stateTransitionManager,
41:             "StateTransition Chain: Only by admin or state transition manager"
42:         );

47:         require(
48:             s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
49:             "StateTransition Chain: Only by validator or state transition manager"
50:         );

55:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
```

- *BaseZkSyncUpgrade.sol* ( [192-192](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L192-L192), [207-210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L207-L210), [240-243](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L240-L243), [244-247](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L244-L247), [251-251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L251-L251), [252-255](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L252-L255) ):

```solidity
192:         require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");

207:         require(
208:             _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
209:             "The new protocol version should be included in the L2 system upgrade tx"
210:         );

240:         require(
241:             _newProtocolVersion > previousProtocolVersion,
242:             "New protocol version is not greater than the current one"
243:         );

244:         require(
245:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
246:             "Too big protocol version difference"
247:         );

251:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

252:         require(
253:             s.l2SystemContractsUpgradeBatchNumber == 0,
254:             "The batch number of the previous upgrade has not been cleaned"
255:         );
```

- *BaseZkSyncUpgradeGenesis.sol* ( [24-28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L24-L28), [29-32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L29-L32), [35-35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L35-L35), [36-39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L36-L39) ):

```solidity
24:         require(
25:             // Genesis Upgrade difference: Note this is the only thing change > to >=
26:             _newProtocolVersion >= previousProtocolVersion,
27:             "New protocol version is not greater than the current one"
28:         );

29:         require(
30:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
31:             "Too big protocol version difference"
32:         );

35:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

36:         require(
37:             s.l2SystemContractsUpgradeBatchNumber == 0,
38:             "The batch number of the previous upgrade has not been cleaned"
39:         );
```

</details>

### [G-27] Reduce deployment costs by tweaking contracts' metadata

See [this](https://www.rareskills.io/post/solidity-metadata) link, at its bottom, for full details.

<details>
<summary>There are 15 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L21) ):

```solidity
21: contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {
```

- *L1SharedBridge.sol* ( [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L32) ):

```solidity
32: contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {
```

- *Bridgehub.sol* ( [18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L18) ):

```solidity
18: contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
```

- *Governance.sol* ( [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L22) ):

```solidity
22: contract Governance is IGovernance, Ownable2Step {
```

- *StateTransitionManager.sol* ( [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L27) ):

```solidity
27: contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {
```

- *ValidatorTimelock.sol* ( [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L24) ):

```solidity
24: contract ValidatorTimelock is IExecutor, Ownable2Step {
```

- *DiamondInit.sol* ( [19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19) ):

```solidity
19: contract DiamondInit is ZkSyncStateTransitionBase, IDiamondInit {
```

- *DiamondProxy.sol* ( [12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L12) ):

```solidity
12: contract DiamondProxy {
```

- *Admin.sol* ( [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20) ):

```solidity
20: contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {
```

- *Executor.sol* ( [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L24) ):

```solidity
24: contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {
```

- *Getters.sol* ( [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L22) ):

```solidity
22: contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {
```

- *Mailbox.sol* ( [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L32) ):

```solidity
32: contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {
```

- *ZkSyncStateTransitionBase.sol* ( [13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L13) ):

```solidity
13: contract ZkSyncStateTransitionBase is ReentrancyGuard {
```

- *DefaultUpgrade.sol* ( [12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L12) ):

```solidity
12: contract DefaultUpgrade is BaseZkSyncUpgrade {
```

- *GenesisUpgrade.sol* ( [13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L13) ):

```solidity
13: contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {
```

</details>

### [G-28] Divisions can be unchecked to save gas

The expression `type(int).min/(-1)` is the only case where division causes an overflow. Therefore, uncheck can be used to [save gas](https://gist.github.com/DadeKuma/3bc597338ae774b8b3bd43280d55271f) in scenarios where it is certain that such an overflow will not occur.

<details>
<summary>There are 7 instances (click to show):</summary>

- *L2ContractHelper.sol* ( [27-27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L27-L27) ):

```solidity
27:         uint256 bytecodeLenInWords = _bytecode.length / 32;
```

- *Mailbox.sol* ( [161-162](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L161-L162), [170-171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L170-L171), [173-173](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L173-L173), [174-174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L174-L174) ):

```solidity
161:         uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
162:             s.baseTokenGasPriceMultiplierDenominator;

170:             batchOverheadBaseToken /
171:             uint256(feeParams.maxPubdataPerBatch);

173:         uint256 l2GasPrice = feeParams.minimalL2GasPrice + batchOverheadBaseToken / uint256(feeParams.maxL2GasPerBatch);

174:         uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata;
```

- *Merkle.sol* ( [35-35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L35-L35) ):

```solidity
35:             _index /= 2;
```

- *TransactionValidator.sol* ( [32-32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L32-L32) ):

```solidity
32:         require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");
```

</details>

### [G-29] Use assembly to validate `msg.sender`

We can use assembly to efficiently validate msg.sender with the least amount of opcodes necessary. For more details check the following report [Here](https://code4rena.com/reports/2023-05-juicebox#g-06-use-assembly-to-validate-msgsender)

<details>
<summary>There are 27 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [66-66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L66-L66) ):

```solidity
66:         require(msg.sender == address(sharedBridge), "Not shared bridge");
```

- *L1SharedBridge.sol* ( [71-71](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L71-L71), [78-78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L78-L78), [78-78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L78-L78), [86-86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L86-L86), [140-140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L140-L140) ):

```solidity
71:         require(msg.sender == address(bridgehub), "ShB not BH");

78:             msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),

78:             msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),

86:         require(msg.sender == address(legacyBridge), "ShB not legacy bridge");

140:         require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");
```

- *Bridgehub.sol* ( [48-48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L48-L48), [48-48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L48-L48), [64-64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L64-L64), [330-330](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L330-L330) ):

```solidity
48:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

48:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

64:         require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

330:             _recipient = msg.sender == tx.origin ? msg.sender : AddressAliasHelper.applyL1ToL2Alias(msg.sender);
```

- *Governance.sol* ( [61-61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L61-L61), [67-67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L67-L67), [74-74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L74-L74), [74-74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L74-L74) ):

```solidity
61:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

67:         require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

74:             msg.sender == owner() || msg.sender == securityCouncil,

74:             msg.sender == owner() || msg.sender == securityCouncil,
```

- *StateTransitionManager.sol* ( [66-66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L66-L66), [72-72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L72-L72), [72-72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L72-L72), [123-123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L123-L123) ):

```solidity
66:         require(msg.sender == bridgehub, "StateTransition: only bridgehub");

72:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

72:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

123:         require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights
```

- *ValidatorTimelock.sol* ( [64-64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L64-L64) ):

```solidity
64:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");
```

- *Admin.sol* ( [36-36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L36-L36) ):

```solidity
36:         require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights
```

- *ZkSyncStateTransitionBase.sol* ( [18-18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L18-L18), [29-29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L29-L29), [34-34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L34-L34), [40-40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L40-L40), [40-40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L40-L40), [48-48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L48-L48), [55-55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L55-L55) ):

```solidity
18:         require(msg.sender == s.admin, "StateTransition Chain: not admin");

29:         require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

34:         require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

40:             msg.sender == s.admin || msg.sender == s.stateTransitionManager,

40:             msg.sender == s.admin || msg.sender == s.stateTransitionManager,

48:             s.validators[msg.sender] || msg.sender == s.stateTransitionManager,

55:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
```

</details>

### [G-30] Using assembly to check for zero can save gas

Using assembly to check for zero can save gas by allowing more direct access to the evm and reducing some of the overhead associated with high-level operations in solidity.

<details>
<summary>There are 62 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [143-143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L143-L143), [188-188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L188-L188) ):

```solidity
143:         require(_amount != 0, "0T"); // empty deposit

188:         require(amount != 0, "2T"); // empty deposit
```

- *L1SharedBridge.sol* ( [110-110](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L110-L110), [160-160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L160-L160), [190-190](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L190-L190), [202-202](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202-L202), [204-204](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L204-L204), [210-210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L210-L210), [565-565](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L565-L565), [580-580](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L580-L580) ):

```solidity
110:         require(_owner != address(0), "ShB owner 0");

160:             require(msg.value == 0, "ShB m.v > 0 b d.it");

190:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

202:             require(_depositAmount == 0, "ShB wrong withdraw amount");

204:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");

210:         require(amount != 0, "6T"); // empty deposit amount

565:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

580:             if (_refundRecipient == address(0)) {
```

- *Bridgehub.sol* ( [124-124](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L124-L124), [132-132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132-L132), [134-134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134-L134), [227-227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L227-L227), [328-328](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L328-L328) ):

```solidity
124:         require(_chainId != 0, "Bridgehub: chainId cannot be 0");

132:         require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

134:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

227:                 require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");

328:         if (_refundRecipient == address(0)) {
```

- *ReentrancyGuard.sol* ( [60-60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L60-L60) ):

```solidity
60:         require(lockSlotOldValue == 0, "1B");
```

- *L2ContractHelper.sol* ( [25-25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25-L25) ):

```solidity
25:         require(_bytecode.length % 32 == 0, "pq");
```

- *Governance.sol* ( [44-44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L44-L44), [109-109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L109-L109) ):

```solidity
44:         require(_admin != address(0), "Admin should be non zero address");

109:         if (timestamp == 0) {
```

- *StateTransitionManager.sol* ( [84-84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L84-L84), [248-248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L248-L248) ):

```solidity
84:         require(_initializeData.governor != address(0), "StateTransition: governor zero");

248:         if (stateTransition[_chainId] != address(0)) {
```

- *DiamondInit.sol* ( [27-27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27-L27), [28-28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L28-L28), [29-29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L29-L29) ):

```solidity
27:         require(address(_initializeData.verifier) != address(0), "vt");

28:         require(_initializeData.admin != address(0), "vy");

29:         require(_initializeData.validatorTimelock != address(0), "hc");
```

- *DiamondProxy.sol* ( [32-32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L32-L32) ):

```solidity
32:         require(facetAddress != address(0), "F"); // Proxy has no facet for this selector
```

- *Admin.sol* ( [92-92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92-L92) ):

```solidity
92:         require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed
```

- *Executor.sol* ( [193-193](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L193-L193), [286-286](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L286-L286), [293-293](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L293-L293), [631-631](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631-L631), [637-637](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L637-L637), [661-661](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L661-L661) ):

```solidity
193:         if (_expectedSystemContractUpgradeTxHash == bytes32(0)) {

286:         require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");

293:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);

631:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");

637:             require(blobVersionedHash != bytes32(0), "vh");

661:         require(versionedHash == bytes32(0), "lh");
```

- *Getters.sol* ( [171-171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L171-L171), [185-185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L185-L185) ):

```solidity
171:         if (selectorsArrayLen != 0) {

185:         require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");
```

- *Mailbox.sol* ( [277-277](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L277-L277) ):

```solidity
277:         address refundRecipient = _params.refundRecipient == address(0) ? _params.sender : _params.refundRecipient;
```

- *Diamond.sol* ( [143-143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L143-L143), [163-163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L163-L163), [177-177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L177-L177), [183-183](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L183-L183), [196-196](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L196-L196), [215-215](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L215-L215), [252-252](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L252-L252), [281-281](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L281-L281), [282-282](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L282-L282) ):

```solidity
143:             require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists

163:             require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

177:         require(_facet == address(0), "a1"); // facet address must be zero

183:             require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet

196:         if (selectorsLength == 0) {

215:         if (selectorPosition != 0) {

252:         if (lastSelectorPosition == 0) {

281:         if (_init == address(0)) {

282:             require(_calldata.length == 0, "H"); // Non-empty calldata for zero address
```

- *TransactionValidator.sol* ( [52-52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L52-L52), [53-53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L53-L53), [54-54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L54-L54), [55-55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55-L55), [56-56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L56-L56), [58-58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L58-L58), [59-59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L59-L59), [60-60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L60-L60), [61-61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L61-L61), [62-62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L62-L62) ):

```solidity
52:         require(_transaction.paymaster == 0, "uc");

53:         require(_transaction.value == 0, "ud");

54:         require(_transaction.maxFeePerGas == 0, "uq");

55:         require(_transaction.maxPriorityFeePerGas == 0, "ux");

56:         require(_transaction.reserved[0] == 0, "ue");

58:         require(_transaction.reserved[2] == 0, "ug");

59:         require(_transaction.reserved[3] == 0, "uo");

60:         require(_transaction.signature.length == 0, "uh");

61:         require(_transaction.paymasterInput.length == 0, "ul1");

62:         require(_transaction.reservedDynamic.length == 0, "um");
```

- *BaseZkSyncUpgrade.sol* ( [95-95](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L95-L95), [112-112](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L112-L112), [133-133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L133-L133), [188-188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L188-L188), [251-251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L251-L251), [253-253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L253-L253) ):

```solidity
95:         if (_l2DefaultAccountBytecodeHash == bytes32(0)) {

112:         if (_l2BootloaderBytecodeHash == bytes32(0)) {

133:         if (_newVerifier == IVerifier(address(0))) {

188:         if (_l2ProtocolUpgradeTx.txType == 0) {

251:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

253:             s.l2SystemContractsUpgradeBatchNumber == 0,
```

- *BaseZkSyncUpgradeGenesis.sol* ( [35-35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L35-L35), [37-37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L37-L37) ):

```solidity
35:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

37:             s.l2SystemContractsUpgradeBatchNumber == 0,
```

</details>

### [G-31] Using bitmaps to store bool arrays or regular bool mappings can save gas

Using a [BitMaps](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/618304cc01e718cbdd87059ce2978b748c15050f/contracts/utils/structs/BitMaps.sol) instead of a bool array or a regular bool mapping to store boolean states can save gas fees. This is because the bitmap can store 256 boolean values in a single slot instead of 256 slots, which can save gas when writing bool values or when reading multiple bool values from the same slot.

There is 1 instance:

- *L1SharedBridge.sol* ( [63-63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L63-L63) ):

```solidity
63:     mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;
```

### [G-32] Use `""` instead of `new bytes(0)` to save gas

The `""` has the same value as `new bytes(0)` but costs less gas.

There are 8 instances:

- *StateTransitionManager.sol* ( [198-198](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L198-L198), [200-200](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L200-L200), [201-201](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L201-L201), [215-215](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L215-L215), [216-216](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L216-L216) ):

```solidity
198:             signature: new bytes(0),

200:             paymasterInput: new bytes(0),

201:             reservedDynamic: new bytes(0)

215:             l1ContractsUpgradeCalldata: new bytes(0),

216:             postUpgradeCalldata: new bytes(0),
```

- *Mailbox.sol* ( [310-310](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L310-L310), [312-312](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L312-L312), [313-313](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L313-L313) ):

```solidity
310:             signature: new bytes(0),

312:             paymasterInput: new bytes(0),

313:             reservedDynamic: new bytes(0)
```

### [G-33] Consider using OZ EnumerateSet in place of nested mappings

Nested mappings and multi-dimensional arrays involve a double hashing process, which can be costly in terms of gas due to the repeated hashing and storage operations. An optimization approach is to manually concatenate keys and perform a single hash and storage operation, but this increases the risk of storage collisions, especially when there are other nested hash maps using the same key types. OpenZeppelin's EnumerableSet offers a solution by combining set operations with element enumeration, providing a gas-efficient and collision-resistant alternative for certain scenarios where nested mappings or multi-dimensional arrays are used in Solidity.

There are 7 instances:

- *L1ERC20Bridge.sol* ( [29-30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L29-L30), [34-35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L34-L35), [53-53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L53-L53) ):

```solidity
29:     mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
30:         public isWithdrawalFinalized;

34:     mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
35:         public depositAmount;

53:     mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;
```

- *L1SharedBridge.sol* ( [54-56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L54-L56), [59-60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L59-L60), [67-67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L67-L67) ):

```solidity
54:     mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
55:         public
56:         override depositHappened;

59:     mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
60:         public isWithdrawalFinalized;

67:     mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;
```

- *ValidatorTimelock.sol* ( [52-52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L52-L52) ):

```solidity
52:     mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```

### [G-34] Use `x += y` instead of `x = x + y` for mapping state variables

Using `+=` for mappings saves **40 gas** due to not having to recalculate the mapping's value's hash. The same applies to `-=`, `*=`, etc.

There is 1 instance:

- *L1SharedBridge.sol* ( [135-135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L135-L135) ):

```solidity
135:             chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
```

### [G-35] Consider using solady's `FixedPointMathLib`

Saves gas, and works to avoid unnecessary [overflows](https://github.com/Vectorized/solady/blob/9deb9ed36a27261a8745db5b7cd7f4cdc3b1cd4e/src/utils/FixedPointMathLib.sol#L436).

There is 1 instance:

- *Mailbox.sol* ( [161-162](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L161-L162) ):

```solidity
161:         uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
162:             s.baseTokenGasPriceMultiplierDenominator;
```

### [G-36] Use `selfbalance()` instead of `address(x).balance`

Use assembly when getting a contract's balance of ETH.
You can use `selfbalance()` instead of `address(x).balance` when getting your contract's balance of ETH to save gas.
Additionally, you can use `balance(address)` instead of `address.balance()` when getting an external contract's balance of ETH.
*Saves 15 gas when checking internal balance, 6 for external*.

There are 3 instances:

- *L1SharedBridge.sol* ( [120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120), [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L122) ):

```solidity
120:             uint256 balanceBefore = address(this).balance;

122:             uint256 balanceAfter = address(this).balance;
```

- *Mailbox.sol* ( [43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L43) ):

```solidity
43:         uint256 amount = address(this).balance;
```

### [G-37] Avoid zero transfer to save gas

In Solidity, unnecessary operations can waste gas. For example, a transfer function without a zero amount check uses gas even if called with a zero amount, since the contract state remains unchanged. Implementing a zero amount check avoids these unnecessary function calls, saving gas and improving efficiency.

There are 4 instances:

- *L1ERC20Bridge.sol* ( [69-69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L69-L69), [164-164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L164-L164) ):

```solidity
69:         IERC20(_token).safeTransfer(address(sharedBridge), amount);

164:         _token.safeTransferFrom(_from, address(sharedBridge), _amount);
```

- *L1SharedBridge.sol* ( [177-177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L177-L177), [454-454](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L454-L454) ):

```solidity
177:         _token.safeTransferFrom(_from, address(this), _amount);

454:             IERC20(l1Token).safeTransfer(l1Receiver, amount);
```

### [G-38] Cache address(this) when used more than once

Caching address(this) when used more than once can save gas.

There are 7 instances:

- *L1SharedBridge.sol* ( [120-120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120-L120), [122-122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L122-L122), [129-129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129-L129), [133-133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133-L133), [176-176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176-L176), [177-177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L177-L177), [178-178](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L178-L178) ):

```solidity
120:             uint256 balanceBefore = address(this).balance;

122:             uint256 balanceAfter = address(this).balance;

129:             uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

133:             uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

176:         uint256 balanceBefore = _token.balanceOf(address(this));

177:         _token.safeTransferFrom(_from, address(this), _amount);

178:         uint256 balanceAfter = _token.balanceOf(address(this));
```

### [G-39] Checking constants first can save gas

Checks that involve constants should come before checks that involve state variables, function calls, and calculations. By doing these checks first, the function is able to revert before wasting a Gcoldsload (**2100 gas***) in a function that may ultimately revert in the unhappy case.

<details>
<summary>There are 20 instances (click to show):</summary>

- *L1SharedBridge.sol* ( [329-329](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L329-L329), [566-566](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L566-L566) ):

```solidity
/// @audit should check before line 318
329:         require(_amount > 0, "y1");

/// @audit should check before line 565
566:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
```

- *Bridgehub.sol* ( [302-305](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L302-L305) ):

```solidity
/// @audit should check before line 268
302:         require(
303:             _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
304:             "Bridgehub: second bridge address too low"
305:         ); // to avoid calls to precompiles
```

- *Executor.sol* ( [233-233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L233-L233), [629-629](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L629-L629) ):

```solidity
/// @audit should check before line 229
233:         require(_newBatchesData.length == 1, "e4");

/// @audit should check before line 627
629:         require(_pubdataCommitments.length > 0, "pl");
```

- *Mailbox.sol* ( [245-245](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L245-L245) ):

```solidity
/// @audit should check before line 235
245:         require(_request.l2GasPerPubdataByteLimit == REQUIRED_L2_GAS_PRICE_PER_PUBDATA, "qp");
```

- *Diamond.sol* ( [134-134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L134-L134), [157-157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L157-L157), [177-177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L177-L177) ):

```solidity
/// @audit should check before line 129
134:         require(_facet.code.length > 0, "G");

/// @audit should check before line 152
157:         require(_facet.code.length > 0, "K");

/// @audit should check before line 175
177:         require(_facet == address(0), "a1"); // facet address must be zero
```

- *TransactionValidator.sol* ( [52-52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L52-L52), [53-53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L53-L53), [54-54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L54-L54), [55-55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55-L55), [56-56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L56-L56), [58-58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L58-L58), [59-59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L59-L59), [60-60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L60-L60), [61-61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L61-L61), [62-62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L62-L62) ):

```solidity
/// @audit should check before line 50
52:         require(_transaction.paymaster == 0, "uc");

/// @audit should check before line 50
53:         require(_transaction.value == 0, "ud");

/// @audit should check before line 50
54:         require(_transaction.maxFeePerGas == 0, "uq");

/// @audit should check before line 50
55:         require(_transaction.maxPriorityFeePerGas == 0, "ux");

/// @audit should check before line 50
56:         require(_transaction.reserved[0] == 0, "ue");

/// @audit should check before line 50
58:         require(_transaction.reserved[2] == 0, "ug");

/// @audit should check before line 50
59:         require(_transaction.reserved[3] == 0, "uo");

/// @audit should check before line 50
60:         require(_transaction.signature.length == 0, "uh");

/// @audit should check before line 50
61:         require(_transaction.paymasterInput.length == 0, "ul1");

/// @audit should check before line 50
62:         require(_transaction.reservedDynamic.length == 0, "um");
```

- *BaseZkSyncUpgrade.sol* ( [207-210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L207-L210) ):

```solidity
/// @audit should check before line 194
207:         require(
208:             _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
209:             "The new protocol version should be included in the L2 system upgrade tx"
210:         );
```

</details>

### [G-40] State variable read in a loop

The state variable should be cached in and read from a local variable, or accumulated in a local variable then written to storage once outside of the loop, rather than reading/updating it on every iteration of the loop, which will replace each Gwarmaccess (**100 gas**) with a much cheaper stack read.

There is 1 instance:

- *Executor.sol* ( [313-316](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313-L316) ):

```solidity
/// @audit s
313:         for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {
314:             PriorityOperation memory priorityOp = s.priorityQueue.popFront();
315:             concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));
316:         }
```

### [G-41] Unlimited gas consumption risk due to external call recipients

When calling an external function without specifying a gas limit , the called contract may consume all the remaining gas, causing the tx to be reverted. To mitigate this, it is recommended to explicitly set a gas limit when making low level external calls.

There are 6 instances:

- *L1SharedBridge.sol* ( [264-264](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L264-L264), [265-265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L265-L265), [266-266](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L266-L266) ):

```solidity
264:         (, bytes memory data1) = _token.staticcall(abi.encodeCall(IERC20Metadata.name, ()));

265:         (, bytes memory data2) = _token.staticcall(abi.encodeCall(IERC20Metadata.symbol, ()));

266:         (, bytes memory data3) = _token.staticcall(abi.encodeCall(IERC20Metadata.decimals, ()));
```

- *Governance.sol* ( [228-228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L228-L228) ):

```solidity
228:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```

- *Executor.sol* ( [610-610](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L610-L610), [678-678](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L678-L678) ):

```solidity
610:         (bool success, bytes memory data) = POINT_EVALUATION_PRECOMPILE_ADDR.staticcall(precompileInput);

678:         (bool success, bytes memory data) = s.blobVersionedHashRetriever.staticcall(abi.encode(_index));
```

### [G-42] Optimize names to save gas

`public`/`external` function names and `public` member variable names can be optimized to save gas. Below are the interfaces/abstract contracts that can be optimized so that the most frequently-called functions use the least amount of gas possible during method lookup. Method IDs that have two leading zero bytes can save 128 gas each during deployment, and renaming functions to have lower method IDs will save 22 gas per call, [per sorted position shifted](https://medium.com/joyso/solidity-how-does-function-name-affect-gas-consumption-in-smart-contract-47d270d8ac92).

<details>
<summary>There are 24 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L21) ):

```solidity
/// @audit initialize(), tranferTokenToSharedBridge(), l2TokenAddress(), deposit(), deposit(), claimFailedDeposit(), finalizeWithdrawal(), sharedBridge, isWithdrawalFinalized, depositAmount, l2Bridge, l2TokenBeacon, l2TokenProxyBytecodeHash
21: contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {
```

- *L1SharedBridge.sol* ( [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L32) ):

```solidity
/// @audit initialize(), transferFundsFromLegacy(), receiveEth(), initializeChainGovernance(), bridgehubDepositBaseToken(), bridgehubDeposit(), bridgehubConfirmL2Transaction(), claimFailedDeposit(), finalizeWithdrawal(), depositLegacyErc20Bridge(), finalizeWithdrawalLegacyErc20Bridge(), claimFailedDepositLegacyErc20Bridge(), l1WethAddress, bridgehub, legacyBridge, l2BridgeAddress, depositHappened, isWithdrawalFinalized
32: contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {
```

- *IL1ERC20Bridge.sol* ( [13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L13) ):

```solidity
/// @audit isWithdrawalFinalized(), deposit(), deposit(), claimFailedDeposit(), finalizeWithdrawal(), l2TokenAddress(), sharedBridge(), l2TokenBeacon(), l2Bridge(), depositAmount(), tranferTokenToSharedBridge()
13: interface IL1ERC20Bridge {
```

- *IL1SharedBridge.sol* ( [14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L14) ):

```solidity
/// @audit isWithdrawalFinalized(), depositLegacyErc20Bridge(), claimFailedDepositLegacyErc20Bridge(), claimFailedDeposit(), finalizeWithdrawalLegacyErc20Bridge(), finalizeWithdrawal(), l1WethAddress(), bridgehub(), legacyBridge(), l2BridgeAddress(), depositHappened(), bridgehubDeposit(), bridgehubDepositBaseToken(), bridgehubConfirmL2Transaction(), receiveEth()
14: interface IL1SharedBridge {
```

- *IL2Bridge.sol* ( [8](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L8) ):

```solidity
/// @audit finalizeDeposit(), withdraw(), l1TokenAddress(), l2TokenAddress(), l1Bridge()
8: interface IL2Bridge {
```

- *IWETH9.sol* ( [6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L6) ):

```solidity
/// @audit deposit(), withdraw()
6: interface IWETH9 {
```

- *Bridgehub.sol* ( [18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L18) ):

```solidity
/// @audit initialize(), setPendingAdmin(), acceptAdmin(), getStateTransition(), addStateTransitionManager(), removeStateTransitionManager(), addToken(), setSharedBridge(), createNewChain(), proveL2MessageInclusion(), proveL2LogInclusion(), proveL1ToL2TransactionStatus(), l2TransactionBaseCost(), requestL2TransactionDirect(), requestL2TransactionTwoBridges(), sharedBridge, stateTransitionManagerIsRegistered, tokenIsRegistered, stateTransitionManager, baseToken, admin
18: contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
```

- *IBridgehub.sol* ( [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L44) ):

```solidity
/// @audit setPendingAdmin(), acceptAdmin(), stateTransitionManagerIsRegistered(), stateTransitionManager(), tokenIsRegistered(), baseToken(), sharedBridge(), getStateTransition(), proveL2MessageInclusion(), proveL2LogInclusion(), proveL1ToL2TransactionStatus(), requestL2TransactionDirect(), requestL2TransactionTwoBridges(), l2TransactionBaseCost(), createNewChain(), addStateTransitionManager(), removeStateTransitionManager(), addToken(), setSharedBridge()
44: interface IBridgehub {
```

- *IL2ContractDeployer.sol* ( [11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L11) ):

```solidity
/// @audit forceDeployOnAddresses(), create2()
11: interface IL2ContractDeployer {
```

- *Governance.sol* ( [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L22) ):

```solidity
/// @audit isOperation(), isOperationPending(), isOperationReady(), isOperationDone(), getOperationState(), scheduleTransparent(), scheduleShadow(), cancel(), execute(), executeInstant(), hashOperation(), updateDelay(), updateSecurityCouncil(), securityCouncil, timestamps, minDelay
22: contract Governance is IGovernance, Ownable2Step {
```

- *IGovernance.sol* ( [10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/IGovernance.sol#L10) ):

```solidity
/// @audit isOperation(), isOperationPending(), isOperationReady(), isOperationDone(), getOperationState(), scheduleTransparent(), scheduleShadow(), cancel(), execute(), executeInstant(), hashOperation(), updateDelay(), updateSecurityCouncil()
10: interface IGovernance {
```

- *IStateTransitionManager.sol* ( [28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L28) ):

```solidity
/// @audit bridgehub(), setPendingAdmin(), acceptAdmin(), stateTransition(), storedBatchZero(), initialCutHash(), genesisUpgrade(), upgradeCutHash(), protocolVersion(), initialize(), setInitialCutHash(), setValidatorTimelock(), getChainAdmin(), createNewChain(), registerAlreadyDeployedStateTransition(), setNewVersionUpgrade(), setUpgradeDiamondCut(), freezeChain(), unfreezeChain()
28: interface IStateTransitionManager {
```

- *StateTransitionManager.sol* ( [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L27) ):

```solidity
/// @audit getChainAdmin(), initialize(), setPendingAdmin(), acceptAdmin(), setValidatorTimelock(), setInitialCutHash(), setNewVersionUpgrade(), setUpgradeDiamondCut(), freezeChain(), unfreezeChain(), revertBatches(), registerAlreadyDeployedStateTransition(), createNewChain(), bridgehub, stateTransition, storedBatchZero, initialCutHash, genesisUpgrade, protocolVersion, validatorTimelock, upgradeCutHash, admin
27: contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {
```

- *ValidatorTimelock.sol* ( [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L24) ):

```solidity
/// @audit setStateTransitionManager(), addValidator(), removeValidator(), setExecutionDelay(), getCommittedBatchTimestamp(), commitBatches(), commitBatchesSharedBridge(), revertBatches(), revertBatchesSharedBridge(), proveBatches(), proveBatchesSharedBridge(), executeBatches(), executeBatchesSharedBridge(), getName, stateTransitionManager, validators, executionDelay
24: contract ValidatorTimelock is IExecutor, Ownable2Step {
```

- *Admin.sol* ( [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20) ):

```solidity
/// @audit setPendingAdmin(), acceptAdmin(), setValidator(), setPorterAvailability(), setPriorityTxMaxGasLimit(), changeFeeParams(), setTokenMultiplier(), setValidiumMode(), upgradeChainFromVersion(), executeUpgrade(), freezeDiamond(), unfreezeDiamond(), getName
20: contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {
```

- *Executor.sol* ( [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L24) ):

```solidity
/// @audit commitBatches(), commitBatchesSharedBridge(), executeBatchesSharedBridge(), executeBatches(), proveBatches(), proveBatchesSharedBridge(), revertBatches(), revertBatchesSharedBridge(), getName
24: contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {
```

- *Getters.sol* ( [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L22) ):

```solidity
/// @audit getVerifier(), getAdmin(), getPendingAdmin(), getBridgehub(), getStateTransitionManager(), getBaseToken(), getBaseTokenBridge(), baseTokenGasPriceMultiplierNominator(), baseTokenGasPriceMultiplierDenominator(), getTotalBatchesCommitted(), getTotalBatchesVerified(), getTotalBatchesExecuted(), getTotalPriorityTxs(), getFirstUnprocessedPriorityTx(), getPriorityQueueSize(), priorityQueueFrontOperation(), isValidator(), l2LogsRootHash(), storedBatchHash(), getL2BootloaderBytecodeHash(), getL2DefaultAccountBytecodeHash(), getVerifierParams(), getProtocolVersion(), getL2SystemContractsUpgradeTxHash(), getL2SystemContractsUpgradeBatchNumber(), isDiamondStorageFrozen(), isFacetFreezable(), getPriorityTxMaxGasLimit(), isFunctionFreezable(), isEthWithdrawalFinalized(), getPubdataPricingMode(), facets(), facetFunctionSelectors(), facetAddresses(), facetAddress(), getTotalBlocksCommitted(), getTotalBlocksVerified(), getTotalBlocksExecuted(), storedBlockHash(), getL2SystemContractsUpgradeBlockNumber(), getName
22: contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {
```

- *Mailbox.sol* ( [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L32) ):

```solidity
/// @audit transferEthToSharedBridge(), bridgehubRequestL2Transaction(), proveL2MessageInclusion(), proveL2LogInclusion(), proveL1ToL2TransactionStatus(), l2TransactionBaseCost(), finalizeEthWithdrawal(), requestL2Transaction(), getName
32: contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {
```

- *IAdmin.sol* ( [15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L15) ):

```solidity
/// @audit setPendingAdmin(), acceptAdmin(), setValidator(), setPorterAvailability(), setPriorityTxMaxGasLimit(), changeFeeParams(), setTokenMultiplier(), setValidiumMode(), upgradeChainFromVersion(), executeUpgrade(), freezeDiamond(), unfreezeDiamond()
15: interface IAdmin is IZkSyncStateTransitionBase {
```

- *IExecutor.sol* ( [75](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L75) ):

```solidity
/// @audit commitBatches(), commitBatchesSharedBridge(), proveBatches(), proveBatchesSharedBridge(), executeBatches(), executeBatchesSharedBridge(), revertBatches(), revertBatchesSharedBridge()
75: interface IExecutor is IZkSyncStateTransitionBase {
```

- *IGetters.sol* ( [15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L15) ):

```solidity
/// @audit getVerifier(), getAdmin(), getPendingAdmin(), getBridgehub(), getStateTransitionManager(), getBaseToken(), getBaseTokenBridge(), getTotalBatchesCommitted(), getTotalBatchesVerified(), getTotalBatchesExecuted(), getTotalPriorityTxs(), getFirstUnprocessedPriorityTx(), getPriorityQueueSize(), priorityQueueFrontOperation(), isValidator(), l2LogsRootHash(), storedBatchHash(), getL2BootloaderBytecodeHash(), getL2DefaultAccountBytecodeHash(), getVerifierParams(), isDiamondStorageFrozen(), getProtocolVersion(), getL2SystemContractsUpgradeTxHash(), getL2SystemContractsUpgradeBatchNumber(), getPriorityTxMaxGasLimit(), isEthWithdrawalFinalized(), getPubdataPricingMode(), baseTokenGasPriceMultiplierNominator(), baseTokenGasPriceMultiplierDenominator(), facets(), facetFunctionSelectors(), facetAddresses(), facetAddress(), isFunctionFreezable(), isFacetFreezable()
15: interface IGetters is IZkSyncStateTransitionBase {
```

- *ILegacyGetters.sol* ( [13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L13) ):

```solidity
/// @audit getTotalBlocksCommitted(), getTotalBlocksVerified(), getTotalBlocksExecuted(), storedBlockHash(), getL2SystemContractsUpgradeBlockNumber()
13: interface ILegacyGetters is IZkSyncStateTransitionBase {
```

- *IMailbox.sol* ( [13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L13) ):

```solidity
/// @audit proveL2MessageInclusion(), proveL2LogInclusion(), proveL1ToL2TransactionStatus(), finalizeEthWithdrawal(), requestL2Transaction(), bridgehubRequestL2Transaction(), l2TransactionBaseCost(), transferEthToSharedBridge()
13: interface IMailbox is IZkSyncStateTransitionBase {
```

- *IVerifier.sol* ( [17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L17) ):

```solidity
/// @audit verify(), verificationKeyHash()
17: interface IVerifier {
```

</details>

### [G-43] Reduce gas usage by moving to Solidity 0.8.19 or later

Solidity version 0.8.19 introduced a number of gas optimizations, refer to the [Solidity 0.8.19 Release Announcement](https://soliditylang.org/blog/2023/02/22/solidity-0.8.19-release-announcement) for details.

<details>
<summary>There are 22 instances (click to show):</summary>

- *IL1ERC20Bridge.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IL1SharedBridge.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IL2Bridge.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IWETH9.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IBridgehub.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *Config.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *L2ContractAddresses.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *Messaging.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IL2ContractDeployer.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IGovernance.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/IGovernance.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IStateTransitionManager.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *ZkSyncStateTransitionStorage.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IAdmin.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IDiamondInit.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IExecutor.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IGetters.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *ILegacyGetters.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IMailbox.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IVerifier.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IZkSyncStateTransition.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IZkSyncStateTransitionBase.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IDefaultUpgrade.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

</details>

### [G-44] Newer versions of solidity are more gas efficient

The solidity language continues to pursue more efficient gas optimization schemes. Adopting a [newer version of solidity](https://github.com/ethereum/solc-js/tags) can be more gas efficient.

<details>
<summary>There are 49 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *L1SharedBridge.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IL1ERC20Bridge.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IL1SharedBridge.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IL2Bridge.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IWETH9.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *Bridgehub.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IBridgehub.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *Config.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *L2ContractAddresses.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *Messaging.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *ReentrancyGuard.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IL2ContractDeployer.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *L2ContractHelper.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *UncheckedMath.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *UnsafeBytes.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *Governance.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IGovernance.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/IGovernance.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IStateTransitionManager.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *StateTransitionManager.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *ValidatorTimelock.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *DiamondInit.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *DiamondProxy.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *ZkSyncStateTransitionStorage.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *Admin.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *Executor.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *Getters.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *Mailbox.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *ZkSyncStateTransitionBase.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IAdmin.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IDiamondInit.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IExecutor.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IGetters.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *ILegacyGetters.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IMailbox.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IVerifier.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IZkSyncStateTransition.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IZkSyncStateTransitionBase.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *Diamond.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *LibMap.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *Merkle.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *PriorityQueue.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *TransactionValidator.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *BaseZkSyncUpgrade.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *BaseZkSyncUpgradeGenesis.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *DefaultUpgrade.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *GenesisUpgrade.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *IDefaultUpgrade.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

- *AddressAliasHelper.sol* ( [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L1) ):

```solidity
1: pragma solidity 0.8.20;
```

</details>

### [G-45] Avoid updating storage when the value hasn't changed

Manipulating storage in solidity is gas-intensive. It can be optimized by avoiding unnecessary storage updates when the new value equals the existing value.
If the old value is equal to the new value, not re-storing the value will avoid a Gsreset (**2900 gas**), potentially at the expense of a Gcoldsload (**2100 gas**) or a Gwarmaccess (**100 gas**).

<details>
<summary>There are 20 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [156-156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L156-L156) ):

```solidity
156:         depositAmount[msg.sender][_l1Token][l2TxHash] = _amount;
```

- *L1SharedBridge.sol* ( [145-145](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L145-L145), [602-602](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L602-L602) ):

```solidity
145:         l2BridgeAddress[_chainId] = _l2BridgeAddress;

602:         depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;
```

- *Bridgehub.sol* ( [57-57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L57-L57), [67-67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L67-L67), [111-111](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L111-L111), [137-137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L137-L137) ):

```solidity
57:         pendingAdmin = _newPendingAdmin;

67:         admin = currentPendingAdmin;

111:         sharedBridge = IL1SharedBridge(_sharedBridge);

137:         baseToken[_chainId] = _baseToken;
```

- *Governance.sol* ( [221-221](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L221-L221), [253-253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L253-L253), [260-260](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L260-L260) ):

```solidity
221:         timestamps[_id] = block.timestamp + _delay;

253:         minDelay = _newDelay;

260:         securityCouncil = _newSecurityCouncil;
```

- *StateTransitionManager.sol* ( [116-116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L116-L116), [126-126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L126-L126), [135-135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L135-L135), [140-140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L140-L140), [149-149](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L149-L149), [150-150](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L150-L150), [158-158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L158-L158), [236-236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L236-L236) ):

```solidity
116:         pendingAdmin = _newPendingAdmin;

126:         admin = currentPendingAdmin;

135:         validatorTimelock = _validatorTimelock;

140:         initialCutHash = keccak256(abi.encode(_diamondCut));

149:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

150:         protocolVersion = _newProtocolVersion;

158:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

236:         stateTransition[_chainId] = _stateTransitionContract;
```

- *ValidatorTimelock.sol* ( [76-76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L76-L76), [99-99](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L99-L99) ):

```solidity
76:         stateTransitionManager = _stateTransitionManager;

99:         executionDelay = _executionDelay;
```

</details>

### [G-46] Same cast is done multiple times

It's cheaper to do it once, and store the result to a variable. The examples below are the second+ instance of a given cast of the variable.

There are 5 instances:

- *L1SharedBridge.sol* ( [511](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L511) ):

```solidity
511:         } else if (bytes4(functionSignature) == IL1ERC20Bridge.finalizeWithdrawal.selector) {
```

- *Executor.sol* ( [42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L42), [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L61), [151](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L151), [175](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L175) ):

```solidity
42:         require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us");

61:         } else if (pubdataSource == uint8(PubdataSource.Calldata)) {

151:             require(!_checkBit(processedLogs, uint8(logKey)), "kp");

175:                 logOutput.numberOfLayer1Txs = uint256(logValue);
```

### [G-47] State variables that are used multiple times in a function should be cached in stack variables

When performing multiple operations on a state variable in a function, it is recommended to cache it first. Either multiple reads or multiple writes to a state variable can save gas by caching it on the stack.
Caching of a state variable replaces each Gwarmaccess (100 gas) with a much cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses.
*Saves 100 gas per instance*.

<details>
<summary>There are 14 instances (click to show):</summary>

- *L1SharedBridge.sol* ( [106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L106) ):

```solidity
/// @audit _owner: 2 reads
106:     function initialize(
```

- *Bridgehub.sol* ( [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62), [116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L116) ):

```solidity
/// @audit pendingAdmin: 2 reads 1 writes
62:     function acceptAdmin() external {

/// @audit sharedBridge: 2 reads
116:     function createNewChain(
```

- *StateTransitionManager.sol* ( [121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L121), [179](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L179) ):

```solidity
/// @audit pendingAdmin: 2 reads 1 writes
121:     function acceptAdmin() external {

/// @audit protocolVersion: 3 reads
179:     function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
```

- *Admin.sol* ( [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L102) ):

```solidity
/// @audit s.protocolVersion: 2 reads
102:     function upgradeChainFromVersion(
```

- *Executor.sol* ( [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L217), [388](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L388), [479](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L479) ):

```solidity
/// @audit s.totalBatchesCommitted: 2 reads 1 writes
217:     function _commitBatches(

/// @audit s.totalBatchesVerified: 2 reads 1 writes
/// @audit s.storedBatchHashes: 2 reads
388:     function _proveBatches(

/// @audit s.totalBatchesVerified: 2 reads 1 writes
/// @audit s.totalBatchesCommitted: 2 reads 1 writes
/// @audit s.totalBatchesExecuted: 2 reads
479:     function _revertBatches(uint256 _newLastBatch) internal {
```

- *Mailbox.sol* ( [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158), [199](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L199) ):

```solidity
/// @audit s.baseTokenGasPriceMultiplierDenominator: 2 reads
158:     function _deriveL2GasPrice(uint256 _l1GasPrice, uint256 _gasPerPubdata) internal view returns (uint256) {

/// @audit s.chainId: 2 reads
199:     function requestL2Transaction(
```

</details>

### [G-48] Use solady library where possible to save gas

The following OpenZeppelin imports have a Solady equivalent, as such they can be used to save GAS as Solady modules have been specifically designed to be as GAS efficient as possible.

<details>
<summary>There are 14 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [7-7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L7-L7), [8-8](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L8-L8) ):

```solidity
7: import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";

8: import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```

- *L1SharedBridge.sol* ( [7-7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L7-L7), [8-8](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L8-L8), [10-10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L10-L10), [11-11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L11-L11), [12-12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L12-L12) ):

```solidity
7: import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";

8: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";

10: import {IERC20Metadata} from "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";

11: import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";

12: import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```

- *Bridgehub.sol* ( [7-7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L7-L7) ):

```solidity
7: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```

- *Governance.sol* ( [7-7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L7-L7) ):

```solidity
7: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```

- *StateTransitionManager.sol* ( [18-18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L18-L18) ):

```solidity
18: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```

- *ValidatorTimelock.sol* ( [7-7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L7-L7) ):

```solidity
7: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```

- *Mailbox.sol* ( [7-7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L7-L7) ):

```solidity
7: import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
```

- *Diamond.sol* ( [7-7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L7-L7) ):

```solidity
7: import {SafeCast} from "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

- *TransactionValidator.sol* ( [7-7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L7-L7) ):

```solidity
7: import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
```

</details>

### [G-49] Contracts can use fewer storage slots by truncating state variables

Some state variables can be safely modified so that the contract uses fewer storage slots. Each saved slot can avoid an extra Gsset (**20000 gas**) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings.

There are 2 instances:

- *Governance.sol* ( [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L22) ):

```solidity
/// @audit Truncate `minDelay` to `uint32`
/// @audit Fewer storage usage (3 slots -> 2 slots):
///        32 B: mapping(bytes32 operationId => uint256 executionTimestamp) timestamps
///        20 B: address securityCouncil
///        4 B: uint32 minDelay
22: contract Governance is IGovernance, Ownable2Step {
```

- *ValidatorTimelock.sol* ( [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L24) ):

```solidity
/// @audit Truncate `executionDelay` to `uint32`
/// @audit Fewer storage usage (4 slots -> 3 slots):
///        32 B: mapping(uint256 => LibMap.Uint32Map) committedBatchTimestamp
///        32 B: mapping(uint256 _chainId => mapping(address _validator => bool)) validators
///        20 B: IStateTransitionManager stateTransitionManager
///        4 B: uint32 executionDelay
24: contract ValidatorTimelock is IExecutor, Ownable2Step {
```

### [G-50] Structs can be packed into fewer storage slots by truncating fields

Some struct fields  can be safely modified so that the struct variable uses fewer storage slots. Each saved slot can avoid an extra Gsset (20000 gas) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings.

<details>
<summary>There are 3 instances (click to show):</summary>

- *IBridgehub.sol* ( [24-34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L24-L34) ):

```solidity
/// @audit Truncate `secondBridgeValue` to `uint32`
/// @audit Fewer storage usage (9 slots -> 8 slots):
///        32 B: uint256 chainId
///        32 B: uint256 mintValue
///        32 B: uint256 l2Value
///        32 B: uint256 l2GasLimit
///        32 B: uint256 l2GasPerPubdataByteLimit
///        32 B: bytes secondBridgeCalldata
///        20 B: address refundRecipient
///        4 B: uint32 secondBridgeValue
///        20 B: address secondBridgeAddress
24: struct L2TransactionRequestTwoBridgesOuter {
25:     uint256 chainId;
26:     uint256 mintValue;
27:     uint256 l2Value;
28:     uint256 l2GasLimit;
29:     uint256 l2GasPerPubdataByteLimit;
30:     address refundRecipient;
31:     address secondBridgeAddress;
32:     uint256 secondBridgeValue;
33:     bytes secondBridgeCalldata;
34: }
```

- *IExecutor.sol* ( [85-94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L85-L94) ):

```solidity
/// @audit Truncate `timestamp` to `uint32`
/// @audit Fewer storage usage (8 slots -> 6 slots):
///        32 B: bytes32 batchHash
///        32 B: uint256 numberOfLayer1Txs
///        32 B: bytes32 priorityOperationsHash
///        32 B: bytes32 l2LogsTreeRoot
///        32 B: bytes32 commitment
///        8 B: uint64 batchNumber
///        8 B: uint64 indexRepeatedStorageChanges
///        4 B: uint32 timestamp
85:     struct StoredBatchInfo {
86:         uint64 batchNumber;
87:         bytes32 batchHash;
88:         uint64 indexRepeatedStorageChanges;
89:         uint256 numberOfLayer1Txs;
90:         bytes32 priorityOperationsHash;
91:         bytes32 l2LogsTreeRoot;
92:         uint256 timestamp;
93:         bytes32 commitment;
94:     }
```

- *BaseZkSyncUpgrade.sol* ( [30-41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L30-L41) ):

```solidity
/// @audit Truncate `upgradeTimestamp` to `uint32`
/// @audit Fewer storage usage (30 slots -> 29 slots):
///        608 B: L2CanonicalTransaction l2ProtocolUpgradeTx
///        96 B: VerifierParams verifierParams
///        32 B: bytes[] factoryDeps
///        32 B: bytes32 bootloaderHash
///        32 B: bytes32 defaultAccountHash
///        32 B: bytes l1ContractsUpgradeCalldata
///        32 B: bytes postUpgradeCalldata
///        32 B: uint256 newProtocolVersion
///        20 B: address verifier
///        4 B: uint32 upgradeTimestamp
30: struct ProposedUpgrade {
31:     L2CanonicalTransaction l2ProtocolUpgradeTx;
32:     bytes[] factoryDeps;
33:     bytes32 bootloaderHash;
34:     bytes32 defaultAccountHash;
35:     address verifier;
36:     VerifierParams verifierParams;
37:     bytes l1ContractsUpgradeCalldata;
38:     bytes postUpgradeCalldata;
39:     uint256 upgradeTimestamp;
40:     uint256 newProtocolVersion;
41: }
```

</details>

### [G-51] Refactor duplicated `require()`/`revert()` checks to save gas

Duplicate `require()`/`revert()` checks can be refactored into a modifier or function, saving deployment costs.

There is 1 instance:

- *ValidatorTimelock.sol* ( [197-197](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L197-L197) ):

```solidity
/// @audit Duplicated on line 219
197:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
```

### [G-52] Using `constant`s instead of `enum` can save gas

`Enum` is expensive and it is [more efficient to use constants](https://www.codehawks.com/finding/clm84992q02j9w9ruebun36d9) instead. An illustrative example of this approach can be found in the [ReentrancyGuard.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/181d518609a9f006fcb97af63e6952e603cf100e/contracts/utils/ReentrancyGuard.sol#L34-L35).

<details>
<summary>There are 7 instances (click to show):</summary>

- *Messaging.sol* ( [10-13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L10-L13) ):

```solidity
10: enum TxStatus {
11:     Failure,
12:     Success
13: }
```

- *IGovernance.sol* ( [16-21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/IGovernance.sol#L16-L21) ):

```solidity
16:     enum OperationState {
17:         Unset,
18:         Waiting,
19:         Ready,
20:         Done
21:     }
```

- *ZkSyncStateTransitionStorage.sol* ( [14-18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L14-L18), [41-44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L41-L44) ):

```solidity
14: enum UpgradeState {
15:     None,
16:     Transparent,
17:     Shadow
18: }

41: enum PubdataPricingMode {
42:     Rollup,
43:     Validium
44: }
```

- *IExecutor.sol* ( [10-21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L10-L21), [24-27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L24-L27) ):

```solidity
10: enum SystemLogKey {
11:     L2_TO_L1_LOGS_TREE_ROOT_KEY,
12:     TOTAL_L2_TO_L1_PUBDATA_KEY,
13:     STATE_DIFF_HASH_KEY,
14:     PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY,
15:     PREV_BATCH_HASH_KEY,
16:     CHAINED_PRIORITY_TXN_HASH_KEY,
17:     NUMBER_OF_LAYER_1_TXS_KEY,
18:     BLOB_ONE_HASH_KEY,
19:     BLOB_TWO_HASH_KEY,
20:     EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY
21: }

24: enum PubdataSource {
25:     Calldata,
26:     Blob
27: }
```

- *Diamond.sol* ( [82-86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L82-L86) ):

```solidity
82:     enum Action {
83:         Add,
84:         Replace,
85:         Remove
86:     }
```

</details>

### [G-53] Assembly: Use scratch space for building calldata

If an external call's calldata can fit into two or fewer words, use the scratch space to build the calldata, rather than allowing Solidity to do a memory expansion.

<details>
<summary>There are 32 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [67-67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67-L67), [163-163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L163-L163), [165-165](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L165-L165) ):

```solidity
67:         uint256 amount = IERC20(_token).balanceOf(address(this));

163:         uint256 balanceBefore = _token.balanceOf(address(sharedBridge));

165:         uint256 balanceAfter = _token.balanceOf(address(sharedBridge));
```

- *L1SharedBridge.sol* ( [121-121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L121-L121), [129-129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129-L129), [130-130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L130-L130), [132-132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132-L132), [133-133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133-L133), [140-140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L140-L140), [176-176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176-L176), [178-178](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L178-L178), [197-197](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L197-L197), [398-398](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L398-L398), [425-428](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L425-L428), [469-469](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L469-L469), [510-510](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L510-L510), [597-597](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L597-L597) ):

```solidity
121:             IMailbox(_target).transferEthToSharedBridge();

129:             uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

130:             uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));

132:             IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);

133:             uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

140:         require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");

176:         uint256 balanceBefore = _token.balanceOf(address(this));

178:         uint256 balanceAfter = _token.balanceOf(address(this));

197:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

398:             require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");

425:             bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
426:                 _l2BatchNumber,
427:                 _l2MessageIndex
428:             );

469:             bool baseTokenWithdrawal = (l1Token == bridgehub.baseToken(_chainId));

510:             l1Token = bridgehub.baseToken(_chainId);

597:             l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
```

- *Bridgehub.sol* ( [78-78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L78-L78), [240-252](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L240-L252), [306-318](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L306-L318) ):

```solidity
78:         return IStateTransitionManager(stateTransitionManager[_chainId]).stateTransition(_chainId);

240:         canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction(
241:             BridgehubL2TransactionRequest({
242:                 sender: msg.sender,
243:                 contractL2: _request.l2Contract,
244:                 mintValue: _request.mintValue,
245:                 l2Value: _request.l2Value,
246:                 l2Calldata: _request.l2Calldata,
247:                 l2GasLimit: _request.l2GasLimit,
248:                 l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
249:                 factoryDeps: _request.factoryDeps,
250:                 refundRecipient: refundRecipient
251:             })
252:         );

306:         canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction(
307:             BridgehubL2TransactionRequest({
308:                 sender: _request.secondBridgeAddress,
309:                 contractL2: outputRequest.l2Contract,
310:                 mintValue: _request.mintValue,
311:                 l2Value: _request.l2Value,
312:                 l2Calldata: outputRequest.l2Calldata,
313:                 l2GasLimit: _request.l2GasLimit,
314:                 l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
315:                 factoryDeps: outputRequest.factoryDeps,
316:                 refundRecipient: refundRecipient
317:             })
318:         );
```

- *Governance.sol* ( [228-228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L228-L228) ):

```solidity
228:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```

- *StateTransitionManager.sol* ( [77-77](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L77-L77), [163-163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L163-L163), [168-168](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L168-L168), [173-173](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L173-L173), [228-228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L228-L228), [279-279](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L279-L279) ):

```solidity
77:         return IZkSyncStateTransition(stateTransition[_chainId]).getAdmin();

163:         IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();

168:         IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();

173:         IZkSyncStateTransition(stateTransition[_chainId]).revertBatches(_newLastBatch);

228:         IAdmin(_chainContract).executeUpgrade(cutData);

279:         DiamondProxy stateTransitionContract = new DiamondProxy{salt: bytes32(0)}(block.chainid, diamondCut);
```

- *ValidatorTimelock.sol* ( [64-64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L64-L64), [228-228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L228-L228) ):

```solidity
64:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

228:         address contractAddress = stateTransitionManager.stateTransition(_chainId);
```

- *Admin.sol* ( [108-108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L108-L108) ):

```solidity
108:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
```

- *Executor.sol* ( [229-229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L229-L229) ):

```solidity
229:             IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
```

- *Mailbox.sol* ( [45-45](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L45-L45) ):

```solidity
45:         IL1SharedBridge(sharedBridgeAddress).receiveEth{value: amount}(ERA_CHAIN_ID);
```

</details>

### [G-54] Use assembly to emit events

To efficiently emit events, it's possible to utilize assembly by making use of scratch space and the free memory pointer. This approach has the advantage of potentially avoiding the costs associated with memory expansion.

However, it's important to note that in order to safely optimize this process, it is preferable to cache and restore the free memory pointer.

A good example of such practice can be seen in [Solady's](https://github.com/Vectorized/solady/blob/main/src/tokens/ERC1155.sol#L167) codebase.

<details>
<summary>There are 53 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [157-157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L157-L157), [201-201](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L201-L201), [227-227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L227-L227) ):

```solidity
157:         emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);

201:         emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);

227:         emit WithdrawalFinalized(l1Receiver, l1Token, amount);
```

- *L1SharedBridge.sol* ( [170-170](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L170-L170), [241-241](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L241-L241), [369-369](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L369-L369), [456-456](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L456-L456) ):

```solidity
170:         emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);

241:         emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);

369:         emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);

456:         emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);
```

- *Bridgehub.sol* ( [58-58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L58-L58), [70-70](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L70-L70), [71-71](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L71-L71), [147-147](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L147-L147) ):

```solidity
58:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

70:         emit NewPendingAdmin(currentPendingAdmin, address(0));

71:         emit NewAdmin(previousAdmin, pendingAdmin);

147:         emit NewChain(_chainId, _stateTransitionManager, _admin);
```

- *Governance.sol* ( [49-49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L49-L49), [52-52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L52-L52), [134-134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L134-L134), [146-146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L146-L146), [159-159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L159-L159), [182-182](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L182-L182), [201-201](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L201-L201), [252-252](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L252-L252), [259-259](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L259-L259) ):

```solidity
49:         emit ChangeSecurityCouncil(address(0), _securityCouncil);

52:         emit ChangeMinDelay(0, _minDelay);

134:         emit TransparentOperationScheduled(id, _delay, _operation);

146:         emit ShadowOperationScheduled(_id, _delay);

159:         emit OperationCancelled(_id);

182:         emit OperationExecuted(id);

201:         emit OperationExecuted(id);

252:         emit ChangeMinDelay(minDelay, _newDelay);

259:         emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```

- *StateTransitionManager.sol* ( [117-117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L117-L117), [129-129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L129-L129), [130-130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L130-L130), [229-229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L229-L229), [237-237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L237-L237), [289-289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L289-L289) ):

```solidity
117:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

129:         emit NewPendingAdmin(currentPendingAdmin, address(0));

130:         emit NewAdmin(previousAdmin, pendingAdmin);

229:         emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);

237:         emit StateTransitionNewChain(_chainId, _stateTransitionContract);

289:         emit StateTransitionNewChain(_chainId, stateTransitionAddress);
```

- *ValidatorTimelock.sol* ( [85-85](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L85-L85), [94-94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L94-L94), [100-100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L100-L100) ):

```solidity
85:         emit ValidatorAdded(_chainId, _newValidator);

94:         emit ValidatorRemoved(_chainId, _validator);

100:         emit NewExecutionDelay(_executionDelay);
```

- *Admin.sol* ( [30-30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L30-L30), [42-42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L42-L42), [43-43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L43-L43), [49-49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L49-L49), [56-56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L56-L56), [65-65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L65-L65), [77-77](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L77-L77), [94-94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L94-L94), [117-117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L117-L117), [127-127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L127-L127), [141-141](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L141-L141), [151-151](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L151-L151) ):

```solidity
30:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

42:         emit NewPendingAdmin(pendingAdmin, address(0));

43:         emit NewAdmin(previousAdmin, pendingAdmin);

49:         emit ValidatorStatusUpdate(_validator, _active);

56:         emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);

65:         emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);

77:         emit NewFeeParams(oldFeeParams, _newFeeParams);

94:         emit ValidiumModeStatusUpdate(_validiumMode);

117:         emit ExecuteUpgrade(_diamondCut);

127:         emit ExecuteUpgrade(_diamondCut);

141:         emit Freeze();

151:         emit Unfreeze();
```

- *Executor.sol* ( [263-267](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L263-L267), [301-305](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L301-L305), [355-355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L355-L355), [434-434](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L434-L434) ):

```solidity
263:             emit BlockCommit(
264:                 _lastCommittedBatchData.batchNumber,
265:                 _lastCommittedBatchData.batchHash,
266:                 _lastCommittedBatchData.commitment
267:             );

301:             emit BlockCommit(
302:                 _lastCommittedBatchData.batchNumber,
303:                 _lastCommittedBatchData.batchHash,
304:                 _lastCommittedBatchData.commitment
305:             );

355:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

434:         emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);
```

- *BaseZkSyncUpgrade.sol* ( [89-89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L89-L89), [106-106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L106-L106), [123-123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L123-L123), [139-139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L139-L139), [159-159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L159-L159), [258-258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L258-L258) ):

```solidity
89:         emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);

106:         emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);

123:         emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);

139:         emit NewVerifier(address(oldVerifier), address(_newVerifier));

159:         emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

258:         emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
```

- *BaseZkSyncUpgradeGenesis.sol* ( [42-42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L42-L42), [69-69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L69-L69) ):

```solidity
42:         emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);

69:         emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);
```

</details>

### [G-55] Use assembly to compute hashes to save gas

If the arguments to the encode call can fit into the scratch space (two words or fewer), then it's more efficient to use assembly to generate the hash (**80 gas**):

`keccak256(abi.encodePacked(x, y))` -> `assembly {mstore(0x00, a); mstore(0x20, b); let hash := keccak256(0x00, 0x40); }`

There are 2 instances:

- *L1ERC20Bridge.sol* ( [78-78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L78-L78) ):

```solidity
78:         bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
```

- *Executor.sol* ( [315-315](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L315-L315) ):

```solidity
315:             concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));
```

### [G-56] Use `calldata` instead of `memory` for immutable arguments

Mark data types as `calldata` instead of `memory` where possible. This makes it so that the data is not automatically loaded into memory. If the data passed into the function does not need to be changed (like updating values in an array), it can be passed in as `calldata`. The one exception to this is if the argument must later be passed into another function that takes an argument that specifies `memory` storage.

<details>
<summary>There are 8 instances (click to show):</summary>

- *Bridgehub.sol* ( [166-172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L166-L172) ):

```solidity
/// @audit _log
166:     function proveL2LogInclusion(
167:         uint256 _chainId,
168:         uint256 _batchNumber,
169:         uint256 _index,
170:         L2Log memory _log,
171:         bytes32[] calldata _proof
172:     ) external view override returns (bool) {
```

- *IBridgehub.sol* ( [83-89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L83-L89) ):

```solidity
/// @audit _log
83:     function proveL2LogInclusion(
84:         uint256 _chainId,
85:         uint256 _batchNumber,
86:         uint256 _index,
87:         L2Log memory _log,
88:         bytes32[] calldata _proof
89:     ) external view returns (bool);
```

- *Executor.sol* ( [201-204](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L201-L204), [209-213](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L209-L213) ):

```solidity
/// @audit _lastCommittedBatchData
201:     function commitBatches(
202:         StoredBatchInfo memory _lastCommittedBatchData,
203:         CommitBatchInfo[] calldata _newBatchesData
204:     ) external nonReentrant onlyValidator {

/// @audit _lastCommittedBatchData
209:     function commitBatchesSharedBridge(
210:         uint256, // _chainId
211:         StoredBatchInfo memory _lastCommittedBatchData,
212:         CommitBatchInfo[] calldata _newBatchesData
213:     ) external nonReentrant onlyValidator {
```

- *Mailbox.sol* ( [49-51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L49-L51), [56-61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L56-L61), [66-71](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L66-L71) ):

```solidity
/// @audit _request
49:     function bridgehubRequestL2Transaction(
50:         BridgehubL2TransactionRequest memory _request
51:     ) external payable onlyBridgehub returns (bytes32 canonicalTxHash) {

/// @audit _message
56:     function proveL2MessageInclusion(
57:         uint256 _batchNumber,
58:         uint256 _index,
59:         L2Message memory _message,
60:         bytes32[] calldata _proof
61:     ) public view returns (bool) {

/// @audit _log
66:     function proveL2LogInclusion(
67:         uint256 _batchNumber,
68:         uint256 _index,
69:         L2Log memory _log,
70:         bytes32[] calldata _proof
71:     ) external view returns (bool) {
```

- *IMailbox.sol* ( [33-38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L33-L38) ):

```solidity
/// @audit _log
33:     function proveL2LogInclusion(
34:         uint256 _batchNumber,
35:         uint256 _index,
36:         L2Log memory _log,
37:         bytes32[] calldata _proof
38:     ) external view returns (bool);
```

</details>

### [G-57] Consider Using Solady's Gas Optimized Lib for Math

In instances where many similar mathematical operations are performed, consider using Solady's math lib to benefit from the gas saving it can introduce.

There is 1 instance:

- *TransactionValidator.sol* ( [100-100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L100-L100) ):

```solidity
100:             costForPubdata += _numberOfFactoryDependencies * L1_TX_DELTA_FACTORY_DEPS_PUBDATA * _l2GasPricePerPubdata;
```

### [G-58] `do`-`while` is cheaper than `for`-loops when the initial check can be skipped

`for (uint256 i; i < len; ++i){ ... }` -> `do { ...; ++i } while (i < len);`

<details>
<summary>There are 22 instances (click to show):</summary>

- *Governance.sol* ( [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L227) ):

```solidity
227:         for (uint256 i = 0; i < _calls.length; ++i) {
```

- *ValidatorTimelock.sol* ( [118](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L118), [137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L137), [187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L187), [211](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L211) ):

```solidity
118:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

137:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

187:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

211:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```

- *Executor.sol* ( [144](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L144), [259](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L259), [291](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L291), [313](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353), [407](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L407), [578](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L578), [634](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L634), [665](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L665) ):

```solidity
144:         for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

259:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

291:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

313:         for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {

353:         for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {

407:         for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {

578:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

634:         for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {

665:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```

- *Getters.sol* ( [210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L210) ):

```solidity
210:         for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {
```

- *Mailbox.sol* ( [358](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L358) ):

```solidity
358:         for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {
```

- *Diamond.sol* ( [103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L103), [140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L140), [160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L160), [180](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L180) ):

```solidity
103:         for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {

140:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

160:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

180:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
```

- *Merkle.sol* ( [31](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L31) ):

```solidity
31:         for (uint256 i; i < pathLength; i = i.uncheckedInc()) {
```

- *BaseZkSyncUpgrade.sol* ( [228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L228) ):

```solidity
228:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```

</details>

### [G-59] Consider activating via-ir for deploying

By using `--via-ir` or `{"viaIR": true}`, the compiler is able to use more advanced [multi-function optimizations](https://docs.soliditylang.org/en/v0.8.17/ir-breaking-changes.html#solidity-ir-based-codegen-changes), for extra gas savings.

There is 1 instance:

- Global finding

### [G-60] Avoid Unnecessary Public Variables

Public state variables automatically generate getter functions, increasing contract size and potentially leading to higher deployment and interaction costs. To optimize gas usage and contract efficiency, minimize the use of public variables unless external access is necessary. Instead, use internal or private visibility combined with explicit getter functions when required. This practice not only reduces contract size but also provides better control over data access and manipulation, enhancing security and readability. Prioritize lean, efficient contracts to ensure cost-effectiveness and better performance on the blockchain.

<details>
<summary>There are 15 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [38-38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L38-L38), [41-41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L41-L41), [44-44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L44-L44) ):

```solidity
38:     address public l2Bridge;

41:     address public l2TokenBeacon;

44:     bytes32 public l2TokenProxyBytecodeHash;
```

- *Bridgehub.sol* ( [20-20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L20-L20), [34-34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L34-L34) ):

```solidity
20:     IL1SharedBridge public sharedBridge;

34:     address public admin;
```

- *Governance.sol* ( [28-28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L28-L28), [37-37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L37-L37) ):

```solidity
28:     address public securityCouncil;

37:     uint256 public minDelay;
```

- *StateTransitionManager.sol* ( [35-35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L35-L35), [38-38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L38-L38), [41-41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L41-L41), [44-44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L44-L44), [47-47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L47-L47), [53-53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L53-L53) ):

```solidity
35:     bytes32 public storedBatchZero;

38:     bytes32 public initialCutHash;

41:     address public genesisUpgrade;

44:     uint256 public protocolVersion;

47:     address public validatorTimelock;

53:     address public admin;
```

- *ValidatorTimelock.sol* ( [46-46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L46-L46), [55-55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55-L55) ):

```solidity
46:     IStateTransitionManager public stateTransitionManager;

55:     uint32 public executionDelay;
```

</details>

### [G-61] Optimize Deployment Size by Fine-tuning IPFS Hash

Optimizing the deployment size of a smart contract is vital to minimize gas costs, and one way to achieve this is by fine-tuning the IPFS hash appended by the Solidity compiler as metadata. This metadata, consisting of 53 bytes, increases the gas required for contract deployment by approximately 10,600 gas due to bytecode costs, and additionally, up to 848 gas due to calldata costs, depending on the proportion of zero and non-zero bytes. Utilize the --no-cbor-metadata compiler flag to prevent the compiler from appending metadata. However, this approach has a drawback as it can complicate the contract verification process on block explorers like Etherscan, potentially reducing transparency.

<details>
<summary>There are 15 instances (click to show):</summary>

- *L1ERC20Bridge.sol* ( [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L21) ):

```solidity
21: contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {
```

- *L1SharedBridge.sol* ( [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L32) ):

```solidity
32: contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {
```

- *Bridgehub.sol* ( [18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L18) ):

```solidity
18: contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
```

- *Governance.sol* ( [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L22) ):

```solidity
22: contract Governance is IGovernance, Ownable2Step {
```

- *StateTransitionManager.sol* ( [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L27) ):

```solidity
27: contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {
```

- *ValidatorTimelock.sol* ( [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L24) ):

```solidity
24: contract ValidatorTimelock is IExecutor, Ownable2Step {
```

- *DiamondInit.sol* ( [19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19) ):

```solidity
19: contract DiamondInit is ZkSyncStateTransitionBase, IDiamondInit {
```

- *DiamondProxy.sol* ( [12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L12) ):

```solidity
12: contract DiamondProxy {
```

- *Admin.sol* ( [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20) ):

```solidity
20: contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {
```

- *Executor.sol* ( [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L24) ):

```solidity
24: contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {
```

- *Getters.sol* ( [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L22) ):

```solidity
22: contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {
```

- *Mailbox.sol* ( [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L32) ):

```solidity
32: contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {
```

- *ZkSyncStateTransitionBase.sol* ( [13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L13) ):

```solidity
13: contract ZkSyncStateTransitionBase is ReentrancyGuard {
```

- *DefaultUpgrade.sol* ( [12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L12) ):

```solidity
12: contract DefaultUpgrade is BaseZkSyncUpgrade {
```

- *GenesisUpgrade.sol* ( [13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L13) ):

```solidity
13: contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {
```

</details>

### [G-62] Multiple accesses of a `memory`/`calldata` array should use a local variable cache

The instances below point to the second+ access of a value inside a storage array, within a function. Caching an array index value in a local `storage` or `calldata` variable when the value is accessed [multiple times](https://gist.github.com/IllIllI000/ec23a57daa30a8f8ca8b9681c8ccefb0), saves **~42 gas per access** due to not having to recalculate the array's keccak256 hash (`Gkeccak256` - **30 gas**) and that calculation's associated stack operations.

<details>
<summary>There are 15 instances (click to show):</summary>

- *Governance.sol* ( [228-228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L228-L228), [228-228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L228-L228), [228-228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L228-L228) ):

```solidity
/// @audit _calls...[]
228:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

/// @audit _calls...[]
228:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

/// @audit _calls...[]
228:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```

- *Executor.sol* ( [57-57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L57-L57), [68-68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L68-L68), [354-354](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L354-L354), [355-355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L355-L355), [355-355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L355-L355), [355-355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L355-L355), [410-410](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L410-L410), [414-414](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L414-L414), [667-667](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667-L667), [667-667](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667-L667), [668-668](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L668-L668), [668-668](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L668-L668) ):

```solidity
/// @audit blobHashes...[]
57:             blobHashes[0] = logOutput.blob1Hash;

/// @audit blobHashes...[]
68:             blobHashes[0] = logOutput.blob1Hash;

/// @audit _batchesData...[]
354:             _executeOneBatch(_batchesData[i], i);

/// @audit _batchesData...[]
355:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

/// @audit _batchesData...[]
355:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

/// @audit _batchesData...[]
355:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

/// @audit _committedBatches...[]
410:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],

/// @audit _committedBatches...[]
414:             bytes32 currentBatchCommitment = _committedBatches[i].commitment;

/// @audit _blobHashes...[]
667:                 (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||

/// @audit blobCommitments...[]
667:                 (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||

/// @audit _blobHashes...[]
668:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),

/// @audit blobCommitments...[]
668:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
```

</details>

### [G-63] Multiple accesses of the same mapping key should be cached

Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Even if the values can't be packed, if both fields are accessed in the same function (as is the case for these instances), combining them can save **~42 gas per access** due to [not having to recalculate the key's keccak256 hash](https://gist.github.com/IllIllI000/639032d73e35d7e968ff58d8784bc445) (Gkeccak256 - 30 gas) and that calculation's associated stack operations.

There are 3 instances:

- *L1SharedBridge.sol* ( [135-135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L135-L135) ):

```solidity
/// @audit `chainBalance[_targetChainId]` is accessed on line 135, 124, 135, 125
135:             chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
```

### [G-64] Consider using `bytes32` rather than a `string`

Using the `bytes` types for fixed-length strings is more efficient than having the EVM have to incur the overhead of string processing. Consider whether the value _needs_ to be a `string`. A good reason to keep it as a `string` would be if the variable is defined in an interface that this project does not own.

There are 5 instances:

- *ValidatorTimelock.sol* ( [28-28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L28-L28) ):

```solidity
28:     string public constant override getName = "ValidatorTimelock";
```

- *Admin.sol* ( [22-22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L22-L22) ):

```solidity
22:     string public constant override getName = "AdminFacet";
```

- *Executor.sol* ( [29-29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L29-L29) ):

```solidity
29:     string public constant override getName = "ExecutorFacet";
```

- *Getters.sol* ( [27-27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L27-L27) ):

```solidity
27:     string public constant override getName = "GettersFacet";
```

- *Mailbox.sol* ( [37-37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L37-L37) ):

```solidity
37:     string public constant override getName = "MailboxFacet";
```
