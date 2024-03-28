**Note: These all are unique findings and not present in analyzer report. Gas Mentioned in these findings title is total gas saved by all instances of that finding covered in this report.**

# Gas Optimizations

## Table of Contents

- [G-01] [Struct variable can be packed into fewer storage slots by rearranging the order of variables in struct(**Gas Saved ~2000 Gas**)](#g-01-struct-variable-can-be-packed-into-fewer-storage-slots-by-rearranging-the-order-of-variables-in-structgas-saved-2000-gas)

- [G-02] [Remove `initializer` modifier check from `initialize` function in `L1SharedBridge` contract since `reentrancyGuardInitializer` will do `initializer`'s work also(**Saves ~24000 gas**)](#g-02-remove-initializer-modifier-check-from-initialize-function-in-l1sharedbridge-contract-since-reentrancyguardinitializer-will-do-initializers-work-alsosaves-24000-gas)

- [G-03] [State variables can be packed into fewer storage slots by truncating timestamp holding variables(**Gas Saved ~2000 GAS**)](#g-03-state-variables-can-be-packed-into-fewer-storage-slots-by-truncating-timestamp-holding-variablesgas-saved-2000-gas)

- [G-04] [Using `storage` instead of `memory` for taking storage arrays/structs inside loop(**Saves 1 Gcoldsload ~2100 Gas Per iteration**)](#g-04-using-storage-instead-of-memory-for-taking-storage-arraysstructs-inside-loopsaves-1-gcoldsload-2100-gas-per-iteration)

- [G-05] [State variables can be packed into fewer storage slot by reducing their size (**Saves ~2000 Gas**)](#g-05-state-variables-can-be-packed-into-fewer-storage-slot-by-reducing-their-size-saves-2000-gas)

- [G-06] [Call `_saveFacetIfNew(_facet)` function outside loop to avoid function call on every iteration, calling it inside loop is redundant wastes gas only(**Saves ~200 Gas Per iteration**)](#g-06-call-_savefacetifnew_facet-function-outside-loop-to-avoid-function-call-on-every-iteration-calling-it-inside-loop-is-redundant-wastes-gas-onlysaves-200-gas-per-iteration)

- [G-07] [Reduce the size of struct variables and pack them together to save storage slots (**Saves ~2000 Gas**)](#g-07-reduce-the-size-of-struct-variables-and-pack-them-together-to-save-storage-slots-saves-2000-gas)

- [G-08] [Multiple address/ID mappings can be combined into a single mapping of an address/ID to a struct and 2 values packed in struct saves 1 storage slot per mapping key(**Saves 1 Slot(~2000 Gas) Per Mapping key**)](#g-08-multiple-addressid-mappings-can-be-combined-into-a-single-mapping-of-an-addressid-to-a-struct-and-2-values-packed-in-struct-saves-1-storage-slot-per-mapping-keysaves-1-slot2000-gas-per-mapping-key)

- [G-09] [Refactor `BaseZkSyncUpgrade::_setL2SystemContractUpgrade` function to fail early and place the `require` statement in the starting of the function avoid multiple function calls when this require check fails](#g-09-refactor-basezksyncupgrade_setl2systemcontractupgrade-function-to-fail-early-and-place-the-require-statement-in-the-starting-of-the-function-avoid-multiple-function-calls-when-this-require-check-fails)

- [G-10] [Reduce the size of struct variables by truncating timestamp and pack them together to save storage slots (**Saves ~2000 Gas**)](#g-10-reduce-the-size-of-struct-variables-by-truncating-timestamp-and-pack-them-together-to-save-storage-slots-saves-2000-gas)

- [G-11] [Re-arrange the state variables to pack them into fewer storage slot (**Saves ~2000 Gas**)](#g-11-re-arrange-the-state-variables-to-pack-them-into-fewer-storage-slot-saves-2000-gas)

- [G-12] [Multiple accesses of the same mapping/array key/index should be cached (**Saves ~520 Gas**)](#g-12-multiple-accesses-of-the-same-mappingarray-keyindex-should-be-cached-saves-520-gas)

- [G-13] [Refactor `Bridgehub::requestL2TransactionTwoBridges` function to fail early if fails can avoid multiple function call both external and internal](#g-13-refactor-bridgehubrequestl2transactiontwobridges-function-to-fail-early-if-fails-can-avoid-multiple-function-call-both-external-and-internal)

- [G-14] [State variable can be marked constant which never changes or initialized (**Gas Saved ~6300 Gas**)](#g-14-state-variable-can-be-marked-constant-which-never-changes-or-initialized-gas-saved-6300-gas)

- [G-15] [Use Short-Circuiting around _||_ to avoid 1 function call half of the time to save gas.(**Total Saves ~30 Gas**)](#g-15-use-short-circuiting-around--to-avoid-1-function-call-half-of-the-time-to-save-gastotal-saves-30-gas)

- [G-16] [Refactor `BaseZkSyncUpgrade::_setVerifierParams` function to emit events before state change can save unnecessary memory variable creation and 3 MSTORE and 3 MLOADS](#g-16-refactor-basezksyncupgrade_setverifierparams-function-to-emit-events-before-state-change-can-save-unnecessary-memory-variable-creation-and-3-mstore-and-3-mloads)

- [G-17] [Avoid updating `storage` variable with same bool value check before updating(**Total Saves ~4200 Gas**)](#g-17-avoid-updating-storage-variable-with-same-bool-value-check-before-updatingtotal-saves-4200-gas)

- [G-18] [State variables should be cached in stack variables rather than re-reading them from storage(**Total Gas Saved ~300 Gas**)](#g-18-state-variables-should-be-cached-in-stack-variables-rather-than-re-reading-them-from-storagetotal-gas-saved-300-gas)

- [G-19] [Use `default` value directly instead of reading from `deleted state variables` (**Saves 2 SLOAD(~196 Gas)**)](#g-19-use-default-value-directly-instead-of-reading-from-deleted-state-variables-saves-2-sload196-gas)

- [G-20] [`Switch` the order of `require` statement to less consuming first (**Saves 1 function call and 1 SLOAD half of the times**)](#g-20-switch-the-order-of-require-statement-to-less-consuming-first-saves-1-function-call-and-1-sload-half-of-the-times)

- [G-21] [Do not emit storage variable cache the variable and use cached value](#g-21-do-not-emit-storage-variable-cache-the-variable-and-use-cached-value)

- [G-22] [Use operator short circuiting around _||_ and memory read first then storage read can **save Gcoldsload ~2100 Gas half of the times**](#g-22-use-operator-short-circuiting-around--and-memory-read-first-then-storage-read-can-save-gcoldsload-2100-gas-half-of-the-times)

- [G-23] [`require` statement can be marked `unchecked` because of previous check (**Gas Saved ~220 Gas(2 Checked subtraction)**)](#g-23require-statement-can-be-marked-unchecked-because-of-previous-check-gas-saved-220-gas2-checked-subtraction)

- [G-24] [Avoid unnecessary overriding of function when nothing is changed in overridden function from the parent one](#g-24-avoid-unnecessary-overriding-of-function-when-nothing-is-changed-in-overridden-function-from-the-parent-one)

- [G-25] [Use `calldata` instead of `memory` for function arguments that do not get mutated (**Gas Saved ~300 Gas**)](#g-25-use-calldata-instead-of-memory-for-function-arguments-that-do-not-get-mutated-gas-saved-300-gas)

- [G-26] [Use directly `constant` variables instead of caching them(**Saves ~10 Gas**)](#g-26-use-directly-constant-variables-instead-of-caching-themsaves-10-gas)

- [G-27] [Nesting if-statements is cheaper than using && (**Total Gas Saved ~60 Gas**)](#g-27-nesting-if-statements-is-cheaper-than-using--total-gas-saved-60-gas)

- [G-28] [Do not cache function call when it is used only once use the call directly saves extra stack variable creation and reading](#g-28-do-not-cache-function-call-when-it-is-used-only-once-use-the-call-directly-saves-extra-stack-variable-creation-and-reading)

- [G-29] [Using `storage` instead of `memory` for structs/arrays saves gas (**Saves ~100 Gas**)](#g-29-using-storage-instead-of-memory-for-structsarrays-saves-gas-saves-100-gas)

- [G-30] [Avoid zero value transfers when transferring/minting ERC20 tokens](#g-30-avoid-zero-value-transfers-when-transferringminting-erc20-tokens)

- [G-31] [Do not create stack variable if the value assigned into it is used only once, use that value directly (**Saves ~20 Gas**)](#g-31-do-not-create-stack-variable-if-the-value-assigned-into-it-is-used-only-once-use-that-value-directly-saves-20-gas)

- [G-32] [`require()`/`revert()` strings longer than `32 bytes`cost extra gas (**Gas Saved ~9 Gas**)](#g-32-requirerevert-strings-longer-than-32-bytescost-extra-gas-gas-saved-9-gas)

- [G-33] [Emit events before state change can save unnecessary stack variable creation](#g-33-emit-events-before-state-change-can-save-unnecessary-stack-variable-creation)

- [G-34] [Use custom error instead of `assert` Statements](#g-34-use-custom-error-instead-of-assert-statements)

- [G-35] [Do not cache local variable they are already cheaper to use](#g-35-do-not-cache-local-variable-they-are-already-cheaper-to-use)

- [G-36] [`address(this)` should be cached instead of re-calculating multiple times.](#g-36-addressthis-should-be-cached-instead-of-re-calculating-multiple-times)

- [G-37] [Do not emit events inside loop emit them outside of the loop (**Gas Saved ~600 Gas**)](#g‑37-do-not-emit-events-inside-loop-emit-them-outside-of-the-loop-gas-saved-600-gas)

## Auditor's Disclaimer :

_All these findings are good findings and 100% safe to implement at no security/logic risk. They all are found by thorough manual review. And this report is created by explaining high quality gas findings in detail._

## [G-01] Struct variable can be packed into fewer storage slots by rearranging the order of variables in struct(**Gas Saved ~2000 Gas**)

The EVM works with 32 byte words. Variables less than 32 bytes inside struct can be declared next to each other this will pack the values together into a single 32 byte storage slot (if values combined are <= 32 bytes) when struct variables declared in storage. If the variables packed together insdide struct are retrieved together in functions (more likely with structs), we will effectively save ~2000 gas with every subsequent SLOAD for that storage slot. This is due to us incurring a Gwarmaccess (100 gas) versus a Gcoldsload (2100 gas).

### Rearrange the order of `bool zkPorterIsAvailable` and place it next to `address __DEPRECATED_allowList` to pack them together in 1 slot save 1 storage slot.

```solidity
File : ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

66: struct ZkSyncStateTransitionStorage {
...
    /// @dev The smart contract that manages the list with permission to call contract functions
    address __DEPRECATED_allowList;
    /// @notice Part of the configuration parameters of ZKP circuits. Used as an input for the verifier smart contract
    VerifierParams verifierParams;
    /// @notice Bytecode hash of bootloader program.
    /// @dev Used as an input to zkp-circuit.
    bytes32 l2BootloaderBytecodeHash;
    /// @notice Bytecode hash of default account (bytecode for EOA).
    /// @dev Used as an input to zkp-circuit.
    bytes32 l2DefaultAccountBytecodeHash;
    /// @dev Indicates that the porter may be touched on L2 transactions.
    /// @dev Used as an input to zkp-circuit.
    bool zkPorterIsAvailable;
...
153: }

```

[ZkSyncStateTransitionStorage.sol#L66-L153](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L66-L153)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

66: struct ZkSyncStateTransitionStorage {
...
    /// @dev The smart contract that manages the list with permission to call contract functions
    address __DEPRECATED_allowList;
+    bool zkPorterIsAvailable;
    /// @notice Part of the configuration parameters of ZKP circuits. Used as an input for the verifier smart contract
    VerifierParams verifierParams;
    /// @notice Bytecode hash of bootloader program.
    /// @dev Used as an input to zkp-circuit.
    bytes32 l2BootloaderBytecodeHash;
    /// @notice Bytecode hash of default account (bytecode for EOA).
    /// @dev Used as an input to zkp-circuit.
    bytes32 l2DefaultAccountBytecodeHash;
    /// @dev Indicates that the porter may be touched on L2 transactions.
    /// @dev Used as an input to zkp-circuit.
-    bool zkPorterIsAvailable;
...
153: }

```

## [G-02] Remove `initializer` modifier check from `initialize` function in `L1SharedBridge` contract since `reentrancyGuardInitializer` will do `initializer`'s work also(**Saves ~24000 gas**)

Removing the `initializer` modifier from the `initialize` function since the first modifier is sufficient to stop re-calling of `initialize` function. It's indicated that the previous value of lockSlotOldValue is checked against 0 inside `reentrancyGuardInitializer` modifier, and after initialization this, it will never be zero from next time 1 or 2 always, ensuring that the function `initialize` will revert when called again. So where this `reentrancyGuardInitializer` modifier placed it will also do the work of `initializer` stopping function from re-calling
This optimization aims to enhance gas efficiency by ensuring that the initialize function is called only once.

### removing of unnecessary `initializer` modifier **saves ~24000 gas**

With this change, the function will still be protected against reentrancy.

```solidity
File : ethereum/contracts/bridge/L1SharedBridge.sol

104:    function initialize(
105:        address _owner,
106:        uint256 _eraFirstPostUpgradeBatch
107:    ) external reentrancyGuardInitializer initializer {
```

[L1SharedBridge.sol#L104-L107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L104-L107)

```solidity
File : ethereum/contracts/common/ReentrancyGuard.sol

41:    modifier reentrancyGuardInitializer() {
42:        _initializeReentrancyGuard();
43:        _;
44:    }
45:
46:    function _initializeReentrancyGuard() private {
47:        uint256 lockSlotOldValue;
48:
49:        // Storing an initial non-zero value makes deployment a bit more
50:        // expensive but in exchange every call to nonReentrant
51:        // will be cheaper.
52:        assembly {
53:            lockSlotOldValue := sload(LOCK_FLAG_ADDRESS)
54:            sstore(LOCK_FLAG_ADDRESS, _NOT_ENTERED)
55:        }
56:
57:        // Check that storage slot for reentrancy guard is empty to rule out possibility of slot conflict
58:        require(lockSlotOldValue == 0, "1B");//@audit it will ensure that function will not be called again since after 1st time
59:    }
```

[ReentrancyGuard.sol#L41-L59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L41-L59)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridge/L1SharedBridge.sol

104:    function initialize(
105:        address _owner,
106:        uint256 _eraFirstPostUpgradeBatch
-107:    ) external reentrancyGuardInitializer initializer {
+     ) external reentrancyGuardInitializer  {
```

## [G-03] State variables can be packed into fewer storage slots by truncating timestamp holding variables(**Gas Saved ~2000 GAS**)

The EVM works with 32 byte words. Variables less than 32 bytes can be declared next to each other in storage and this will pack the values together into a single 32 byte storage slot (if values combined are <= 32 bytes). If the variables packed together are retrieved together in functions , we will effectively save ~2000 gas with every subsequent SLOAD for that storage slot. This is due to us incurring a Gwarmaccess (100 gas) versus a Gcoldsload (2100 gas).

### Reduce the size of `minDelay` to `uint48` and `address securityCouncil` can be packed in a single slot `SAVES: ~2000 Gas, 1 SLOT`

To optimize gas usage and achieve storage packing the recommendation suggests declaring `minDelay` as a `uint48,` which is sufficient to hold any realistic time, and positioning it before the `address securityCouncil` variable. By doing so, the two variables can be packed into a single storage slot.

```solidity
File : ethereum/contracts/governance/Governance.sol

26:  address public securityCouncil;
...
34:  /// @notice The minimum delay in seconds for operations to be ready for execution.
35:  uint256 public minDelay;

```

[Governance.sol#L26-L35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L26-L35)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/governance/Governance.sol

+    /// @notice The minimum delay in seconds for operations to be ready for execution.
+    uint48 public minDelay;
26:  address public securityCouncil;
...
-34:  /// @notice The minimum delay in seconds for operations to be ready for execution.
-35:  uint256 public minDelay;

```

## [G-04] Using `storage` instead of `memory` for taking storage arrays/structs inside loop(**Saves 1 Gcoldsload ~2100 Gas Per iteration**)

Using a memory pointer for a storage struct/array will effectively load all the fields of that data type from storage (SLOAD) into memory (MSTORE). Using a storage pointer will allow you to read specific fields from storage as you need them. If you are not going to use all of the fields of your data type then you should use a storage pointer so that you don't incur extra Gcoldsload (2100 gas) for fields that you will never use.

### Taking `ds.facetToSelectors[facetAddr]` into storage can save 1 Gcoldsload + memory creation and load and store per iteration.(Almost **~2100 Gas Per iteration**)

Since Diamond.FacetToSelectors struct have two var. in it while only one of them (`bytes4[] selectors`) is used here. And other var.(`uint16 facetPosition`) never used so taking into memory will cause that unused var. to `Gcoldsload from storage unnecessarily on every iteration`. So it is better to take that struct into storage pointer and read that required variable only directly. By this it can avoid reading of one storage var. in struct per iteration. First time load of that var. for that iteration specific `facetAddr` causes 1 Gcoldsload. So Saves 1 Gcoldsload gas + memory var. creation load and store also.

```solidity
File : ethereum/contracts/state-transition/chain-deps/facets/Getters.so

208: for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {
209:            address facetAddr = ds.facets[i];
210:            Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];

```

[Getters.sol#L208-L210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208-L210)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/chain-deps/facets/Getters.so

208: for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {
209:            address facetAddr = ds.facets[i];
-210:            Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];
+           Diamond.FacetToSelectors storage facetToSelectors = ds.facetToSelectors[facetAddr];

```

## [G-05] State variables can be packed into fewer storage slot by reducing their size (**Saves ~2000 Gas**)

The EVM works with 32 byte words. Variables less than 32 bytes can be declared next to each other in storage and this will pack the values together into a single 32 byte storage slot (if values combined are <= 32 bytes). If the variables packed together are retrieved together in functions (more likely with structs), we will effectively save ~2000 gas with every subsequent SLOAD for that storage slot. This is due to us incurring a Gwarmaccess (100 gas) versus a Gcoldsload (2100 gas).

### Reduce size of `protocolVersion` to `uint48` and pack it with `address genesisUpgrade` in a single slot `Saves: ~2000 Gas, 1 Slot`

Since Considering the limited range needed for `protocolVersion`, which increases by 100 in one increment, uint48 indeed provides a sufficient range for representing this value.
`uint48` is very big number to hold version >2.8e12. It will allow to update versions ~2.8e10 times considering with max diff. 100. Which is much more than realistic updated versions even updated every block. So uint48 is more than sufficient to hold `protocolVersion`. SInce this check hows 2 consecutive versions no. difference cant be more than 100.

```solidity
File : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

236: function _setNewProtocolVersion(uint256 _newProtocolVersion) internal virtual {
...
242:    require(
243:        _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
244:        "Too big protocol version difference"
245:     );

```

[BaseZkSyncUpgrade.sol#L236-L245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L236-L245)

```solidity
File : ethereum/contracts/state-transition/StateTransitionManager.sol

39: address public genesisUpgrade;
40:
41:  /// @dev current protocolVersion
42: uint256 public protocolVersion;
```

[StateTransitionManager.sol#L39-L42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L39-L42)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/StateTransitionManager.sol

39: address public genesisUpgrade;
+   uint48 public protocolVersion;
40:
41:  /// @dev current protocolVersion
-42: uint256 public protocolVersion;
```

## [G-06] Call `_saveFacetIfNew(_facet)` function outside loop to avoid function call on every iteration, calling it inside loop is redundant wastes gas only(**Saves ~200 Gas Per iteration**)

Since `_facet` doesn't depends on loop iteration it is fixed for all iterations. So ifit new then it cvan be done in first time. If it is not new than it will not be updated in any iteration. So 1 call to `_saveFacetIfNew(_facet)` is enough outside loop.
No need to call `_saveFacetIfNew` with same `_facet` again and again if it is new it can be done outside of the loop.
Saves `_saveFacetIfNew` call every iteration. In this function it just read the length and check that against 0 again and again. Since updation will happen only first time if happen or never if \_facet already there.

```solidity
File : ethereum/contracts/state-transition/libraries/Diamond.sol

158: for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
159:            bytes4 selector = _selectors[i];
160:            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
161:            require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address
162:
163:            _removeOneFunction(oldFacet.facetAddress, selector);
164:            // Add facet to the list of facets if the facet address is a new one
165:            _saveFacetIfNew(_facet);
166:            _addOneFunction(_facet, selector, _isFacetFreezable);
167:        }

```

[Diamond.sol#L158-L167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158-L167)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/libraries/Diamond.sol

158: for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
159:            bytes4 selector = _selectors[i];
160:            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
161:            require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address
162:
163:            _removeOneFunction(oldFacet.facetAddress, selector);
164:            // Add facet to the list of facets if the facet address is a new one
-165:            _saveFacetIfNew(_facet);
166:            _addOneFunction(_facet, selector, _isFacetFreezable);
167:        }
+         _saveFacetIfNew(_facet);

```

## [G-07] Reduce the size of struct variables and pack them together to save storage slots (**Saves ~2000 Gas**)

The EVM works with 32 byte words. Variables less than 32 bytes inside struct can be declared next to each other this will pack the values together into a single 32 byte storage slot (if values combined are <= 32 bytes) when struct variables declared in storage. If the variables packed together insdide struct are retrieved together in functions (more likely with structs), we will effectively save ~2000 gas with every subsequent SLOAD for that storage slot. This is due to us incurring a Gwarmaccess (100 gas) versus a Gcoldsload (2100 gas).

### `SAVE: ~2000 GAS, 1 SLOT`

### `protocolVersion` can be reduced to `uint48` and pack with `address admin` SAVES: ~2000 Gas, 1 Slot

Since Considering the limited range needed for `protocolVersion`, which increases by 100 in one increment, uint48 indeed provides a sufficient range for representing this value.
`uint48` is very big number to hold version >2.8e12. It will allow to update versions ~2.8e10 times considering with max diff. 100. Which is much more than realistic updated versions even updated every block. So uint48 is more than sufficient to hold `protocolVersion`. SInce this check hows 2 consecutive versions no. difference cant be more than 100.

```solidity
File : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

236: function _setNewProtocolVersion(uint256 _newProtocolVersion) internal virtual {
...
242:    require(
243:        _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
244:        "Too big protocol version difference"
245:     );

```

[BaseZkSyncUpgrade.sol#L236-L245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L236-L245)

```solidity
File : ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

66: struct ZkSyncStateTransitionStorage {
...
123:    uint256 protocolVersion;
124:    /// @dev Hash of the system contract upgrade transaction. If 0, then no upgrade transaction needs to be done.
125:    bytes32 l2SystemContractsUpgradeTxHash;
126:    /// @dev Batch number where the upgrade transaction has happened. If 0, then no upgrade transaction has happened
127:    /// yet.
128:    uint256 l2SystemContractsUpgradeBatchNumber;
129:    /// @dev Address which will exercise non-critical changes to the Diamond Proxy (changing validator set & unfreezing)
130:    address admin;
...
153: }
```

[ZkSyncStateTransitionStorage.sol#L123-L130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L123-L130)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

66: struct ZkSyncStateTransitionStorage {
...
-123:    uint256 protocolVersion;
124:    /// @dev Hash of the system contract upgrade transaction. If 0, then no upgrade transaction needs to be done.
125:    bytes32 l2SystemContractsUpgradeTxHash;
126:    /// @dev Batch number where the upgrade transaction has happened. If 0, then no upgrade transaction has happened
127:    /// yet.
128:    uint256 l2SystemContractsUpgradeBatchNumber;
129:    /// @dev Address which will exercise non-critical changes to the Diamond Proxy (changing validator set & unfreezing)
+       uint48 protocolVersion;
130:    address admin;
...
153: }
```

## [G-08] Multiple address/ID mappings can be combined into a single mapping of an address/ID to a struct and 2 values packed in struct saves 1 storage slot per mapping key(**Saves 1 Slot(~2000 Gas) Per Mapping key**)

Saves a storage slot for the mapping. Depending on the circumstances and sizes of types, can avoid a Gsset (20000 gas) per mapping combined. Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Finally, if both fields are accessed in the same function, can save ~42 gas per access due to not having to recalculate the key's keccak256 hash (Gkeccak256 - 30 gas) and that calculation's associated stack operations

### `Saves 1 Storage Slot(~2000 Gas)` per mapping key

For `chainId` as key by combining mappings `l2Bridge` and `enabled` will be in one struct as one value for key. So `l2Bridge` and `enabled` will be pocked together in struct saves 1 Slot per mapping key.

```solidity
File : ethereum/contracts/bridge/L1SharedBridge.sol

47: /// @dev A mapping chainId => bridgeProxy. Used to store the bridge proxy's address, and to see if it has been deployed yet.
48:  mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;
...
60:  /// @dev Indicates whether the hyperbridging is enabled for a given chain.
61:  mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;

```

[L1SharedBridge.sol#L47-L61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L47-L61)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridge/L1SharedBridge.sol

+    struct BridgeInfo {
+        address l2Bridge;
+        bool enabled;
+    }

-47: /// @dev A mapping chainId => bridgeProxy. Used to store the bridge proxy's address, and to see if it has been deployed yet.
-48:  mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;
...
-60:  /// @dev Indicates whether the hyperbridging is enabled for a given chain.
-61:  mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;

+    mapping(uint256 => BridgeInfo) public bridgeInfoMap;

```

## [G-09] Refactor `BaseZkSyncUpgrade::_setL2SystemContractUpgrade` function to fail early and place the `require` statement in the starting of the function avoid multiple function calls when this require check fails

**Description:**
The current implementation of the `_setL2SystemContractUpgrade` function performs several validations and computations before executing the require statement to check the validity of the new protocol version. Placing the require statement at the beginning of the function allows for early termination if the condition fails, preventing unnecessary computations and function calls.

**Recommended Mitigation Steps:**
To optimize gas usage and improve code readability, it is recommended to move the require statement to the beginning of the `_setL2SystemContractUpgrade` function. This ensures that the validation of the new protocol version occurs first, avoiding unnecessary computations and function calls.

```solidity
File : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

180: function _setL2SystemContractUpgrade(
181:        L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
182:        bytes[] calldata _factoryDeps,
183:        uint256 _newProtocolVersion
184:    ) internal returns (bytes32) {
        // If the type is 0, it is considered as noop and so will not be required to be executed.
        if (_l2ProtocolUpgradeTx.txType == 0) {
            return bytes32(0);
        }

        require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");

        bytes memory encodedTransaction = abi.encode(_l2ProtocolUpgradeTx);

        TransactionValidator.validateL1ToL2Transaction(
            _l2ProtocolUpgradeTx,
            encodedTransaction,
            s.priorityTxMaxGasLimit,
            s.feeParams.priorityTxMaxPubdata
        );

        TransactionValidator.validateUpgradeTransaction(_l2ProtocolUpgradeTx);

        // We want the hashes of l2 system upgrade transactions to be unique.
        // This is why we require that the `nonce` field is unique to each upgrade.
205:      require(
206:        _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
207:        "The new protocol version should be included in the L2 system upgrade tx"
208:      );

```

[BaseZkSyncUpgrade.sol#L180-L208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L180-L208)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

180: function _setL2SystemContractUpgrade(
181:        L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
182:        bytes[] calldata _factoryDeps,
183:        uint256 _newProtocolVersion
184:    ) internal returns (bytes32) {

+     require(
+        _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
+        "The new protocol version should be included in the L2 system upgrade tx"
+      );
        // If the type is 0, it is considered as noop and so will not be required to be executed.
        if (_l2ProtocolUpgradeTx.txType == 0) {
            return bytes32(0);
        }

        require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");

        bytes memory encodedTransaction = abi.encode(_l2ProtocolUpgradeTx);

        TransactionValidator.validateL1ToL2Transaction(
            _l2ProtocolUpgradeTx,
            encodedTransaction,
            s.priorityTxMaxGasLimit,
            s.feeParams.priorityTxMaxPubdata
        );

        TransactionValidator.validateUpgradeTransaction(_l2ProtocolUpgradeTx);

        // We want the hashes of l2 system upgrade transactions to be unique.
        // This is why we require that the `nonce` field is unique to each upgrade.
-205:      require(
-206:        _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
-207:        "The new protocol version should be included in the L2 system upgrade tx"
-208:      );

```

## [G-10] Reduce the size of struct variables by truncating timestamp and pack them together to save storage slots (**Saves ~2000 Gas**)

### `SAVE: ~2000 GAS, 1 SLOT`

### `upgradeTimestamp` can be reduced to `uint64` since this hold time in seconds and uint64 is more than enough to hold any realistic time and pack with `address verifier` in one slot to save 1 slot(~2000 Gas).

```solidity
File : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

28: struct ProposedUpgrade {
29:    L2CanonicalTransaction l2ProtocolUpgradeTx;
30:    bytes[] factoryDeps;
31:    bytes32 bootloaderHash;
32:    bytes32 defaultAccountHash;
33:    address verifier;
34:    VerifierParams verifierParams;
35:    bytes l1ContractsUpgradeCalldata;
36:    bytes postUpgradeCalldata;
37:    uint256 upgradeTimestamp;
38:    uint256 newProtocolVersion;
39: }

```

[BaseZkSyncUpgrade.sol#L28-L39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L28-L39)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

28: struct ProposedUpgrade {
29:    L2CanonicalTransaction l2ProtocolUpgradeTx;
30:    bytes[] factoryDeps;
31:    bytes32 bootloaderHash;
32:    bytes32 defaultAccountHash;
33:    address verifier;
+      uint64 upgradeTimestamp;
34:    VerifierParams verifierParams;
35:    bytes l1ContractsUpgradeCalldata;
36:    bytes postUpgradeCalldata;
-37:    uint256 upgradeTimestamp;
38:    uint256 newProtocolVersion;
39: }

```

## [G-11] Re-arrange the state variables to pack them into fewer storage slot (**Saves ~2000 Gas**)

### Place `uint32 executionDelay` next to `stateTransitionManager` saves 1 SLOT

```solidity
File : ethereum/contracts/state-transition/ValidatorTimelock.sol

44:  IStateTransitionManager public stateTransitionManager;//@audit takes 20 bytes
...
52:  /// @dev The delay between committing and executing batches.
53:  uint32 public executionDelay;
```

[ValidatorTimelock.sol#L44-L53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L44-L53)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/ValidatorTimelock.sol

44:  IStateTransitionManager public stateTransitionManager;
+   uint32 public executionDelay;
...
52:  /// @dev The delay between committing and executing batches.
-53:  uint32 public executionDelay;
```

## [G-12] Multiple accesses of the same mapping/array key/index should be cached (**Saves ~520 Gas**)

The instances below point to the second+ access of a value inside a mapping/array key/index, within a function. Caching a mapping's value in a local storage or calldata variable when the value is accessed multiple times, saves ~42 gas per access due to not having to recalculate the key's keccak256 hash (Gkeccak256 - 30 gas) and that calculation's associated stack operations. Caching an array's struct avoids recalculating the array offsets into memory/calldata

### Cache l2BridgeAddress[_chainId] into a stack variable

```solidity
File : ethereum/contracts/bridge/L1SharedBridge.sol

188:  require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
...
221:     l2Contract: l2BridgeAddress[_chainId],

```

[L1SharedBridge.sol#L188-L221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188-L221)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridge/L1SharedBridge.sol

+    address chainIdToAddress = l2BridgeAddress[_chainId];

-188:  require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
+    require(chainIdToAddress != address(0), "ShB l2 bridge not deployed");
...
-221:     l2Contract: l2BridgeAddress[_chainId],
+       l2Contract: chainIdToAddress,

```

### Cache `chainBalance[_chainId][_l1Token]` mapping in stack variable

```solidity
File : ethereum/contracts/bridge/L1SharedBridge.sol

349: require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
350:     chainBalance[_chainId][_l1Token] -= _amount;

```

[ethereum/contracts/bridge/L1SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L349-L350)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridge/L1SharedBridge.sol

+    uint256 _chainBalance = chainBalance[_chainId][_l1Token];
-349: require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
-350:     chainBalance[_chainId][_l1Token] -= _amount;

+   require(_chainBalance >= _amount, "ShB n funds");
+     chainBalance[_chainId][_l1Token] = _chainBalance - _amount;


```

### Cache `chainBalance[_chainId][l1Token]` mapping in stack variable

```solidity
File : ethereum/contracts/bridge/L1SharedBridge.sol

439: require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds
440:     chainBalance[_chainId][l1Token] -= amount;


```

[L1SharedBridge.sol#L439-L440](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L439-L440)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridge/L1SharedBridge.sol

+  uint256 chainBalance = chainBalance[_chainId][l1Token];

-439: require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds
-440:     chainBalance[_chainId][l1Token] -= amount;
+    require(chainBalance >= amount, "ShB not enough funds 2"); // not enought funds
+        chainBalance[_chainId][l1Token] = chainBalance - amount;

```

### Cache `l2BridgeAddress[ERA_CHAIN_ID]` mapping saves 1 SLOAD and 1 SLOT calculation

```solidity
File : ethereum/contracts/bridge/L1SharedBridge.sol

563:   require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
    ...
586:            l2Contract: l2BridgeAddress[ERA_CHAIN_ID],

```

[L1SharedBridge.sol#L563-L586](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563-L586)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridge/L1SharedBridge.sol

+     address l2BridgeAddress_ERA_CHAIN_ID =l2BridgeAddress[ERA_CHAIN_ID];

-563:   require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
+       require(l2BridgeAddress_ERA_CHAIN_ID != address(0), "ShB b. n dep");
    ...
-586:            l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
+        l2Contract: l2BridgeAddress_ERA_CHAIN_ID,

```

## [G-13] Refactor `Bridgehub::requestL2TransactionTwoBridges` function to fail early if fails can avoid multiple function call both external and internal

The finding pertains to the `Bridgehub::requestL2TransactionTwoBridges` function within the `Bridgehub` contract. It identifies an opportunity to enhance gas efficiency by reordering function logic to fail early when necessary conditions are not met. By doing so, multiple unnecessary function calls, both external and internal, can be avoided.

**Description:**
The provided code snippet demonstrates the `requestL2TransactionTwoBridges` function which facilitates transactions between two bridges. At line 300, there's a requirement check ensuring `_request.secondBridgeAddress` is greater than a predefined minimum value (`BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS`). However, this check is performed after several function calls and operations.

**Recommended Mitigation Steps:**

To optimize gas usage and prevent unnecessary computation, the recommendation suggests moving the parameter check to the beginning of the function. By doing so, if the condition fails, the function will revert early, avoiding subsequent function calls, both external and internal.

```solidity
File : ethereum/contracts/bridgehub/Bridgehub.sol

262: function requestL2TransactionTwoBridges(
263:        L2TransactionRequestTwoBridgesOuter calldata _request
264:    ) external payable override nonReentrant returns (bytes32 canonicalTxHash) {
265:      {
            address token = baseToken[_request.chainId];
            uint256 baseTokenMsgValue;
            if (token == ETH_TOKEN_ADDRESS) {
                require(
                    msg.value == _request.mintValue + _request.secondBridgeValue,
                    "Bridgehub: msg.value mismatch 2"
                );
                baseTokenMsgValue = _request.mintValue;
            } else {
                require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3");
                baseTokenMsgValue = 0;
            }
            sharedBridge.bridgehubDepositBaseToken{value: baseTokenMsgValue}(
                _request.chainId,
                msg.sender,
                token,
                _request.mintValue
            );
        }

        address stateTransition = getStateTransition(_request.chainId);

        L2TransactionRequestTwoBridgesInner memory outputRequest = IL1SharedBridge(_request.secondBridgeAddress)
            .bridgehubDeposit{value: _request.secondBridgeValue}(
            _request.chainId,
            msg.sender,
            _request.l2Value,
            _request.secondBridgeCalldata
        );

        require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch");

        address refundRecipient = _actualRefundRecipient(_request.refundRecipient);

300:      require(
301:        _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
302:        "Bridgehub: second bridge address too low"
303:      );

```

[Bridgehub.sol#L262-L303](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L262-L303)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridgehub/Bridgehub.sol


262: function requestL2TransactionTwoBridges(
263:        L2TransactionRequestTwoBridgesOuter calldata _request
264:    ) external payable override nonReentrant returns (bytes32 canonicalTxHash) {
265:      {
+       require(
+             _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
+             "Bridgehub: second bridge address too low"
+         );
            address token = baseToken[_request.chainId];
            uint256 baseTokenMsgValue;
            if (token == ETH_TOKEN_ADDRESS) {
                require(
                    msg.value == _request.mintValue + _request.secondBridgeValue,
                    "Bridgehub: msg.value mismatch 2"
                );
                baseTokenMsgValue = _request.mintValue;
            } else {
                require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3");
                baseTokenMsgValue = 0;
            }
            sharedBridge.bridgehubDepositBaseToken{value: baseTokenMsgValue}(
                _request.chainId,
                msg.sender,
                token,
                _request.mintValue
            );
        }

        address stateTransition = getStateTransition(_request.chainId);

        L2TransactionRequestTwoBridgesInner memory outputRequest = IL1SharedBridge(_request.secondBridgeAddress)
            .bridgehubDeposit{value: _request.secondBridgeValue}(
            _request.chainId,
            msg.sender,
            _request.l2Value,
            _request.secondBridgeCalldata
        );

        require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch");

        address refundRecipient = _actualRefundRecipient(_request.refundRecipient);

-300:      require(
-301:        _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
-302:        "Bridgehub: second bridge address too low"
-303:      );

```

## [G-14] State variable can be marked constant which never changes or initialized (**Gas Saved ~6300 Gas**)

The solidity compiler will directly embed the values of constant variables into your contract bytecode, and therefore, will save you from incurring a Gsset (20000 gas) when you set storage variables during construction; a Gcoldsload (2100 gas) when you access storage variables for the first time in a transaction, and a Gwarmaccess (100 gas) for each subsequent access to that storage slot.

**Total Gas Saved: ~6300 Gas**
**Gas Per Instance: ~2100 Gas**

### `l2Bridge`, `l2TokenBeacon` and `l2TokenProxyBytecodeHash` are not changed in the entire contract So can be marked constant

```solidity
File : ethereum/contracts/bridge/L1ERC20Bridge.sol

35:     /// @dev The address that is used as a L2 bridge counterpart in zkSync Era.
36:    address public l2Bridge;
37:
38:    /// @dev The address that is used as a beacon for L2 tokens in zkSync Era.
39:    address public l2TokenBeacon;
40:
41:    /// @dev Stores the hash of the L2 token proxy contract's bytecode on zkSync Era.
42:    bytes32 public l2TokenProxyBytecodeHash;

```

[L1ERC20Bridge.sol#L35-L42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L35-L42)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridge/L1ERC20Bridge.sol

35:     /// @dev The address that is used as a L2 bridge counterpart in zkSync Era.
-36:    address public l2Bridge;
+       address public constant l2Bridge;
37:
38:    /// @dev The address that is used as a beacon for L2 tokens in zkSync Era.
-39:    address public l2TokenBeacon;
+       address public constant l2TokenBeacon;
40:
41:    /// @dev Stores the hash of the L2 token proxy contract's bytecode on zkSync Era.
-42:    bytes32 public l2TokenProxyBytecodeHash;
+       bytes32 public constant l2TokenProxyBytecodeHash;

```

## [G-15] Use Short-Circuiting around _||_ to avoid 1 function call half of the time to save gas.(**Total Saves ~30 Gas**)

### Use short-circuiting in `onlyOwnerOrSecurityCouncil` modifier to save function call

To save gas, rearrange the conditions in the if statement to check `msg.sender` against `securityCouncil` first, as this requires only a single `storage` read operation. Checking `msg.sender` against `owner()` involves an `function` call and an additional `storage` read operation, which can be avoided half of the times if `securityCouncil` is checked first.

```solidity
File : ethereum/contracts/governance/Governance.sol

71:   require(
72:         msg.sender == owner() || msg.sender == securityCouncil,
73:         "Only the owner and security council are allowed to call this function"
74:     );
```

[Governance.sol#L71-L74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L71-L74)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/governance/Governance.sol

71:   require(
-72:         msg.sender == owner() || msg.sender == securityCouncil,
+           msg.sender == securityCouncil || msg.sender == owner(),
73:         "Only the owner and security council are allowed to call this function"
74:     );
```

## [G-16] Refactor `BaseZkSyncUpgrade::_setVerifierParams` function to emit events before state change can save unnecessary memory variable creation and 3 MSTORE and 3 MLOADS

**Description:**
The code snippet updates the `verifierParams` state variable by assigning `_newVerifierParams` to it, creates a memory variable `oldVerifierParams`, and emits the NewVerifierParams event with both the old and new parameters. However, this approach results in unnecessary memory variable creation and additional storage operations.

**Recommended Mitigation Steps:**
To optimize gas usage and avoid unnecessary memory variable creation and storage operations, emit the `NewVerifierParams` event before updating the verifierParams state variable. And remove the memory variable `oldVerifierParams`.

```solidity
File : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

142:  function _setVerifierParams(VerifierParams calldata _newVerifierParams) private {
...
155:    VerifierParams memory oldVerifierParams = s.verifierParams;
156:    s.verifierParams = _newVerifierParams;
157:    emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

```

[BaseZkSyncUpgrade.sol#L155-L157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L155-L157)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

142:  function _setVerifierParams(VerifierParams calldata _newVerifierParams) private {
...
+      emit NewVerifierParams(s.verifierParams, _newVerifierParams);
-155:    VerifierParams memory oldVerifierParams = s.verifierParams;
156:    s.verifierParams = _newVerifierParams;
-157:    emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

```

## [G-17] Avoid updating `storage` variable with same bool value check before updating(**Total Saves ~4200 Gas**)

Since bool have true and false only two values it may happen that this value already present So check that before setting this.

```solidity
File : ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

45:    function setValidator(address _validator, bool _active) external onlyStateTransitionManager {
46:        s.validators[_validator] = _active;
47:        emit ValidatorStatusUpdate(_validator, _active);
48:    }
49:
50:    /// @inheritdoc IAdmin
51:    function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {
52:        // Change the porter availability
53:        s.zkPorterIsAvailable = _zkPorterIsAvailable;
54:        emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);
55:    }

```

[Admin.sol#L45-L55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L45-L55)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

45:    function setValidator(address _validator, bool _active) external onlyStateTransitionManager {
+    if(s.validators[_validator] != _active) {
46:        s.validators[_validator] = _active;
47:        emit ValidatorStatusUpdate(_validator, _active);
+        }
48:    }
49:
50:    /// @inheritdoc IAdmin
51:    function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {
+      if(s.zkPorterIsAvailable != _zkPorterIsAvailable) {
52:        // Change the porter availability
53:        s.zkPorterIsAvailable = _zkPorterIsAvailable;
+        }
54:        emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);
55:    }

```

## [G-18] State variables should be cached in stack variables rather than re-reading them from storage(**Total Gas Saved ~300 Gas**)

The instances below point to the second+ access of a state variable within a function. Caching of a state variable replaces each Gwarmaccess (100 gas) with a much cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses.

### Cache `address(sharedBridge)` to save 1 SLOAD

```solidity
File : ethereum/contracts/bridgehub/Bridgehub.sol

130:  require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
...
137:    IStateTransitionManager(_stateTransitionManager).createNewChain(
138:        _chainId,
139:        _baseToken,
140:        address(sharedBridge),
141:        _admin,
142:        _initData
143:     );

```

[Bridgehub.sol#L130-L143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130-L143)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridgehub/Bridgehub.sol

+     address _sharedBridge = address(sharedBridge);
-130:  require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
+     require(_sharedBridge != address(0), "Bridgehub: weth bridge not set");
...
137:    IStateTransitionManager(_stateTransitionManager).createNewChain(
138:        _chainId,
139:        _baseToken,
-140:        address(sharedBridge),
+            _sharedBridge,
141:        _admin,
142:        _initData
143:     );

```

### Cache `protocolVersion` to save 2 SLOAD(~200 Gas)

```solidity
File : ethereum/contracts/state-transition/StateTransitionManager.sol

177:    function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
...

        L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
...
            nonce: protocolVersion,
...
        });

        ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
...
            newProtocolVersion: protocolVersion
        });
...
        emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
228:    }
```

[StateTransitionManager.sol#L177-L228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177-L228)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/StateTransitionManager.sol

177:    function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
...
+     uint256 _protocolVersion = protocolVersion;

        L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
...
-192:            nonce: protocolVersion,
+            nonce: _protocolVersion,
...
        });

        ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
...
-216:            newProtocolVersion: protocolVersion
+            newProtocolVersion: _protocolVersion
        });
...
-227:        emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
+        emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, _protocolVersion);
228:    }
```

## [G-19] Use `default` value directly instead of reading from `deleted state variables` (**Saves 2 SLOAD(~196 Gas)**)

### 2 Instances

#### Instance 1

In the original code, the `pendingAdmin` state variable is deleted at line 66 using the delete keyword. However, at line 69, it emits an event `NewAdmin` with `pendingAdmin` as one of the parameters. Since `pendingAdmin` has been deleted, reading it would result in unnecessary gas consumption.

The recommended mitigation steps propose to emit the NewAdmin event with the default value directly (address(0)) instead of reading from the deleted `pendingAdmin`. This optimization saves approximately `97 gas (SLOAD) per execution`, enhancing the contract's efficiency.

```solidity
File : ethereum/contracts/bridgehub/Bridgehub.sol

66:  delete pendingAdmin;
67:
68:     emit NewPendingAdmin(currentPendingAdmin, address(0));
69:     emit NewAdmin(previousAdmin, pendingAdmin);
```

[Bridgehub.sol#L66-L69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L66-L69)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridgehub/Bridgehub.sol

66:  delete pendingAdmin;
67:
68:     emit NewPendingAdmin(currentPendingAdmin, address(0));
-69:     emit NewAdmin(previousAdmin, pendingAdmin);
+       emit NewAdmin(previousAdmin, address(0));
```

#### Instance 2

Like Instance 1.

```solidity
File : ethereum/contracts/state-transition/StateTransitionManager.sol

125:  delete pendingAdmin;
126:
127:        emit NewPendingAdmin(currentPendingAdmin, address(0));
128:        emit NewAdmin(previousAdmin, pendingAdmin);
129:    }

```

[StateTransitionManager.sol#L125-L129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L125-L129)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/StateTransitionManager.sol

125:  delete pendingAdmin;
126:
127:        emit NewPendingAdmin(currentPendingAdmin, address(0));
-128:        emit NewAdmin(previousAdmin, pendingAdmin);
+          emit NewAdmin(previousAdmin, address(0));
129:    }

```

## [G-20] `Switch` the order of `require` statement to less consuming first (**Saves 1 function call and 1 SLOAD half of the times**)

To optimize gas usage and potentially save one `function call` and one `SLOAD` operation half of the times, the recommendation advises switching the order of the require statements. By placing the check for `_delay >= minDelay` first, the contract can revert early in cases where the proposed `_delay` is less than the minimum delay, without incurring the additional gas cost of the `isOperation` function call.

```solidity
File : ethereum/contracts/governance/Governance.sol

215:  function _schedule(bytes32 _id, uint256 _delay) internal {
216:        require(!isOperation(_id), "Operation with this proposal id already exists");
217:        require(_delay >= minDelay, "Proposed delay is less than minimum delay");
```

[Governance.sol#L215-L217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L215-L217)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/governance/Governance.sol

215:  function _schedule(bytes32 _id, uint256 _delay) internal {
+        require(_delay >= minDelay, "Proposed delay is less than minimum delay");
216:        require(!isOperation(_id), "Operation with this proposal id already exists");
-217:        require(_delay >= minDelay, "Proposed delay is less than minimum delay");
```

## [G-21] Do not emit storage variable cache the variable and use cached value

Do not emit `protocolVersion` cache it and emit cached value.

```solidity
File : ethereum/contracts/state-transition/StateTransitionManager.sol

227:  emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);

```

[StateTransitionManager.sol#L227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/StateTransitionManager.sol

+     uint256 _protocolVersion = protocolVersion;
-227:  emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
+        emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, _protocolVersion);

```

## [G-22] Use operator short circuiting around _||_ and memory read first then storage read can **save Gcoldsload ~2100 Gas half of the times**

Check `!facet.isFreezable` first Since it takes less gas than `!diamondStorage.isFrozen`. If `!facet.isFreezable` is become true the second will not be checked.

```solidity
File : ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

31: require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen

```

[DiamondProxy.sol#L31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L31)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

-31: require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen
+    require(!facet.isFreezable || !diamondStorage.isFrozen, "q1"); // Facet is frozen

```

## [G-23]`require` statement can be marked `unchecked` because of previous check (**Gas Saved ~220 Gas(2 Checked subtraction)**)

There are two require statements checking conditions related to the new protocol version compared to the previous one. The second require statement ensures that the difference between the new and previous protocol versions does not exceed a certain threshold. However, since the first require statement already checks that the new version is greater than the previous one, it guarantees that the subtraction operation in the second require statement will not underflow.

**Gas Per Instance: ~110 Gas**

### 2 Instances

#### Instance 1

```solidity
File : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

238:   require(
239:       _newProtocolVersion > previousProtocolVersion,
240:       "New protocol version is not greater than the current one"
241:    );
242:   require(
243:       _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
244:       "Too big protocol version difference"
245:     );
```

[BaseZkSyncUpgrade.sol#L238-L245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L238-L245)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

238:   require(
239:       _newProtocolVersion > previousProtocolVersion,
240:       "New protocol version is not greater than the current one"
241:    );
-242:   require(
-243:       _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
-244:       "Too big protocol version difference"
-245:     );
+    unchecked{
+    require(
+       _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
+       "Too big protocol version difference"
+     );
+  }
```

#### Instance 2

```solidity
File : ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

22:  require(
23: // Genesis Upgrade difference: Note this is the only thing change > to >=
24:      _newProtocolVersion >= previousProtocolVersion,
25:      "New protocol version is not greater than the current one"
26:  );
27:  require(
28:      _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
29:      "Too big protocol version difference"
30:  );

```

[BaseZkSyncUpgradeGenesis.sol#L22-L30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22-L30)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

22:  require(
23: // Genesis Upgrade difference: Note this is the only thing change > to >=
24:      _newProtocolVersion >= previousProtocolVersion,
25:      "New protocol version is not greater than the current one"
26:  );
-27:  require(
-28:      _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
-29:      "Too big protocol version difference"
-30:  );
+  unchecked{
+    require(
+       _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
+       "Too big protocol version difference"
+     );
+  }

```

## [G-24] Avoid unnecessary overriding of function when nothing is changed in overridden function from the parent one

**Description:**
The function `_setNewProtocolVersion` is being overridden without any changes made to the implementation compared to the parent function. The overridden function simply duplicates the parent function's logic without introducing any modifications. This redundancy adds unnecessary complexity to the codebase and can potentially confuse developers.

**Recommended Mitigation Steps:**
To improve code clarity and reduce redundancy, it's recommended to remove the overridden function `_setNewProtocolVersion` if it serves no additional purpose other than duplicating the parent function's behavior.

```solidity
File : ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

20: function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
        uint256 previousProtocolVersion = s.protocolVersion;
        require(
            // Genesis Upgrade difference: Note this is the only thing change > to >=
            _newProtocolVersion >= previousProtocolVersion,
            "New protocol version is not greater than the current one"
        );
        require(
            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
            "Too big protocol version difference"
        );

        // If the previous upgrade had an L2 system upgrade transaction, we require that it is finalized.
        require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
        require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        );

        s.protocolVersion = _newProtocolVersion;
        emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
41:    }
```

[BaseZkSyncUpgradeGenesis.sol#L20-L41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20-L41)

**Recommended Mitigation Steps:**

Remove the function

```diff
File : ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

- 20: function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
-        uint256 previousProtocolVersion = s.protocolVersion;
-        require(
-            // Genesis Upgrade difference: Note this is the only thing change > to >=
-            _newProtocolVersion >= previousProtocolVersion,
-            "New protocol version is not greater than the current one"
-        );
-        require(
-            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
-            "Too big protocol version difference"
-        );
-
-        // If the previous upgrade had an L2 system upgrade transaction, we require that it is finalized.
-        require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
-        require(
-            s.l2SystemContractsUpgradeBatchNumber == 0,
-            "The batch number of the previous upgrade has not been cleaned"
-        );
-
-        s.protocolVersion = _newProtocolVersion;
-        emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
- 41:    }
```

## [G-25] Use `calldata` instead of `memory` for function arguments that do not get mutated (**Gas Saved ~300 Gas**)

Mark data types as calldata instead of memory where possible. This makes it so that the data is not automatically loaded into memory. If the data passed into the function does not need to be changed (like updating values in an array), it can be passed in as calldata. The one exception to this is if the argument must later be passed into another function that takes an argument that specifies memory storage.

```solidity
File : ethereum/contracts/bridgehub/Bridgehub.sol

164:  function proveL2LogInclusion(
165:    uint256 _chainId,
166:    uint256 _batchNumber,
167:    uint256 _index,
168:    L2Log memory _log

```

[Bridgehub.sol#L164-L168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L164-L168)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridgehub/Bridgehub.sol

164:  function proveL2LogInclusion(
165:    uint256 _chainId,
166:    uint256 _batchNumber,
167:    uint256 _index,
-168:    L2Log memory _log,
+       L2Log calldata _log,

```

## [G-26] Use directly `constant` variables instead of caching them(**Saves ~10 Gas**)

```solidity
File : ethereum/contracts/state-transition/libraries/Diamond.sol

87:  function getDiamondStorage() internal pure returns (DiamondStorage storage diamondStorage) {
88:     bytes32 position = DIAMOND_STORAGE_POSITION;
89:      assembly {
90:            diamondStorage.slot := position
91:        }

```

[Diamond.sol#L87-L91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L87-L91)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/libraries/Diamond.sol

87:  function getDiamondStorage() internal pure returns (DiamondStorage storage diamondStorage) {
-88:     bytes32 position = DIAMOND_STORAGE_POSITION;
89:      assembly {
-90:            diamondStorage.slot := position
+            diamondStorage.slot := DIAMOND_STORAGE_POSITION
91:        }

```

## [G-27] Nesting if-statements is cheaper than using && (**Total Gas Saved ~60 Gas**)

Using a nested if statement instead of logical AND (&&) can provide similar short-circuiting behavior whereas nested if is slightly more efficient.

**Total Gas Saved: ~60 Gas**
**Gas Saved Per Instance: ~30 Gas**

```solidity
FIle : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

147:  if (
148:        _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) &&
149:        _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) &&
150:        _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)
151:    ) {
152:        return;
153:   }
```

[BaseZkSyncUpgrade.sol#L147-L153](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L147-L153)

**Recommended Mitigation Steps:**

```diff
FIle : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

-147:  if (
-148:        _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) &&
-149:        _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) &&
-150:        _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)
-151:    ) {
-152:        return;
-153:   }
+ if (_newVerifierParams.recursionNodeLevelVkHash == bytes32(0)) {
+     if (_newVerifierParams.recursionLeafLevelVkHash == bytes32(0)) {
+         if (_newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)) {
+       return;
+     }
+   }
+  }
```

## [G-28] Do not cache function call when it is used only once use the call directly saves extra stack variable creation and reading

### 4 Instances

#### Instance 1,2,3 and 4

Do not cache `getStateTransition(_chainId)` function call into `stateTransition` stack variable since it is used only once.
call directly `getStateTransition(_chainId)` instead of caching it.

```solidity
File : ethereum/contracts/bridgehub/Bridgehub.sol

159:   address stateTransition = getStateTransition(_chainId);
160:   return IZkSyncStateTransition(stateTransition).proveL2MessageInclusion(_batchNumber, _index, _message, _proof);
...
...
171: address stateTransition = getStateTransition(_chainId);
172: return IZkSyncStateTransition(stateTransition).proveL2LogInclusion(_batchNumber, _index, _log, _proof);
...
...
185:  address stateTransition = getStateTransition(_chainId);
186:    return
187:    IZkSyncStateTransition(stateTransition).proveL1ToL2TransactionStatus(
...
...
204:  address stateTransition = getStateTransition(_chainId);
205:    return
206:       IZkSyncStateTransition(stateTransition).l2TransactionBaseCost(

```

[Bridgehub.sol#L159-L160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L159-L160), [Bridgehub.sol#L171-L172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L171-L172), [Bridgehub.sol#L185-L187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L185-L187), [Bridgehub.sol#L204-L206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L204-L206)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridgehub/Bridgehub.sol

-159:   address stateTransition = getStateTransition(_chainId);
-160:   return IZkSyncStateTransition(stateTransition).proveL2MessageInclusion(_batchNumber, _index, _message, _proof);
+      return IZkSyncStateTransition(getStateTransition(_chainId)).proveL2MessageInclusion(_batchNumber, _index, _message, _proof);
...
...
-171: address stateTransition = getStateTransition(_chainId);
-172: return IZkSyncStateTransition(stateTransition).proveL2LogInclusion(_batchNumber, _index, _log, _proof);
+  return IZkSyncStateTransition(getStateTransition(_chainId)).proveL2LogInclusion(_batchNumber, _index, _log, _proof);
...
...
-185:  address stateTransition = getStateTransition(_chainId);
186:    return
-187:    IZkSyncStateTransition(stateTransition).proveL1ToL2TransactionStatus(
+       IZkSyncStateTransition(getStateTransition(_chainId)).proveL1ToL2TransactionStatus(
...
...
-204:  address stateTransition = getStateTransition(_chainId);
205:    return
-206:       IZkSyncStateTransition(stateTransition).l2TransactionBaseCost(
+     IZkSyncStateTransition(getStateTransition(_chainId)).l2TransactionBaseCost(

```

## [G-29] Using `storage` instead of `memory` for structs/arrays saves gas (**Saves ~100 Gas**)

Using a memory pointer for a storage struct/array will effectively load all the fields of that data type from storage (SLOAD) into memory (MSTORE). Using a storage pointer will allow you to read specific fields from storage as you need them. If you are not going to use all of the fields of your data type then you should use a storage pointer so that you don't incur extra Gcoldsload (2100 gas) for fields that you will never use.

```solidity
File : ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

27:  Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];

```

[DiamondProxy.sol#L27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L27)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

-27:  Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];
+    Diamond.SelectorToFacet storage facet = diamondStorage.selectorToFacet[msg.sig];

```

## [G-30] Avoid zero value transfers when transferring/minting ERC20 tokens

In Solidity, performing unnecessary operations can consume more gas than needed, leading to cost inefficiencies. For instance, if a transfer function doesn't have a zero amount check and someone calls it with a zero amount, unnecessary gas will be consumed in executing the function, even though the state of the contract remains the same. By implementing a zero amount check, such unnecessary function calls can be avoided, thereby saving gas and making the contract more efficient. Amounts should be checked for 0 before calling a transfer Checking non-zero transfer values can avoid an expensive external call and save gas.

### Check amount is non 0 before transferring tokens in `tranferTokenToSharedBridge` function

```solidity
File : ethereum/contracts/bridge/L1ERC20Bridge.sol

67:  IERC20(_token).safeTransfer(address(sharedBridge), amount);
```

[L1ERC20Bridge.sol#L67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridge/L1ERC20Bridge.sol

+    require(amount > 0, "Amount can not be 0");
67:  IERC20(_token).safeTransfer(address(sharedBridge), amount);
```

### Check amount for non 0 in `_depositFunds` function

```solidity
File : ethereum/contracts/bridge/L1SharedBridge.sol

175:  _token.safeTransferFrom(_from, address(this), _amount);
```

[L1SharedBridge.sol#L175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175)
**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridge/L1SharedBridge.sol

+    require(_amount > 0, "Amount can not be 0");
175:  _token.safeTransferFrom(_from, address(this), _amount);
```

## [G-31] Do not create stack variable if the value assigned into it is used only once, use that value directly (**Saves ~20 Gas**)

If the variable is only accessed once, it's cheaper to use the assigned value directly that one time, and save the 3 gas the extra stack assignment would spend.

```solidity
File : ethereum/contracts/bridge/L1ERC20Bridge.sol

75:    function l2TokenAddress(address _l1Token) external view returns (address) {
76:        bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
77:        bytes32 salt = bytes32(uint256(uint160(_l1Token)));
78:
79:        return L2ContractHelper.computeCreate2Address(l2Bridge, salt, l2TokenProxyBytecodeHash, constructorInputHash);
```

[L1ERC20Bridge.sol#L75-L79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L75-L79)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/bridge/L1ERC20Bridge.sol

75:    function l2TokenAddress(address _l1Token) external view returns (address) {
-76:        bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
-77:        bytes32 salt = bytes32(uint256(uint160(_l1Token)));
78:
-79:        return L2ContractHelper.computeCreate2Address(l2Bridge, salt, l2TokenProxyBytecodeHash, constructorInputHash);
+         return L2ContractHelper.computeCreate2Address(l2Bridge, bytes32(uint256(uint160(_l1Token))), l2TokenProxyBytecodeHash, +      keccak256(abi.encode(l2TokenBeacon, "")));
```

## [G-32] `require()`/`revert()` strings longer than `32 bytes`cost extra gas (**Gas Saved ~9 Gas**)

Each extra memory word of bytes past the original 32 incurs an `MSTORE` which costs `3 gas`

```solidity
File : ethereum/contracts/governance/Governance.sol

59: require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
...
65: require(msg.sender == securityCouncil, "Only security council is allowed to call this function");
...
71: require(
72:          msg.sender == owner() || msg.sender == securityCouncil,
73:         "Only the owner and security council are allowed to call this function"
...

```

[Governance.sol#L59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59), [Governance.sol#L65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L65), [Governance.sol#L73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L7)

## [G-33] Emit events before state change can save unnecessary stack variable creation

Emit `NewVerifier` event before `oldVerifier` stack variable creation and remove `oldVerifier` variable creation.

```solidity
File : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

135:  IVerifier oldVerifier = s.verifier;
136:  s.verifier = _newVerifier;
137:  emit NewVerifier(address(oldVerifier), address(_newVerifier));
```

[BaseZkSyncUpgrade.sol#L135-L137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L135-L137)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

-135:  IVerifier oldVerifier = s.verifier;
+     emit NewVerifier(address(oldVerifier), address(_newVerifier));
136:  s.verifier = _newVerifier;
-137:  emit NewVerifier(address(oldVerifier), address(_newVerifier));
```

## [G-34] Use custom error instead of `assert` Statements

While assert statements are useful for detecting unexpected conditions during development and testing. require or custom error is more convenient to use here instead of assert and custom error takes lesser gas also.

```solidity
File : ethereum/contracts/state-transition/StateTransitionManager.sol

106:  assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
```

[StateTransitionManager.sol#L106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L106)

**Recommended Mitigation Steps:**

```diff
File : ethereum/contracts/state-transition/StateTransitionManager.sol

+   error INVALID();
 ...

-106:  assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
+     if(L2_TO_L1_LOG_SERIALIZE_SIZE == 2 * 32) revert INVALID();
```

## [G-35] Do not cache local variable they are already cheaper to use

Do not cache `facet.facetAddress` use it directly instead of caching it.

```solidity
File : ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

28: address facetAddress = facet.facetAddress;

```

[DiamondProxy.sol#L28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L28)

## [G-36] `address(this)` should be cached instead of re-calculating multiple times.

```solidity
File : ethereum/contracts/bridge/L1SharedBridge.sol

118: uint256 balanceBefore = address(this).balance;
            IMailbox(_target).transferEthToSharedBridge();
            uint256 balanceAfter = address(this).balance;
...
        } else {
            uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
            uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
            require(amount > 0, "ShB: 0 amount to transfer");
            IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);
131:            uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

```

[L1SharedBridge.sol#L118-L131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118-L131)

## [G‑37] Do not emit events inside loop emit them outside of the loop (**Gas Saved ~600 Gas**)

Emitting an event inside a loop performs a LOG op N times, where N is the loop length. Consider refactoring the code to emit the event only once at the end of loop. **Gas savings should be multiplied by the average loop length**.

```solidity
File : ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

257: for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
258:            _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));
259:
260:            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
261:            emit BlockCommit(
262:                _lastCommittedBatchData.batchNumber,
263:                _lastCommittedBatchData.batchHash,
264:                _lastCommittedBatchData.commitment
265:            );
...
...
289:  for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
 ...
299:            emit BlockCommit(
300:                _lastCommittedBatchData.batchNumber,
301:                _lastCommittedBatchData.batchHash,
302:                _lastCommittedBatchData.commitment
303:            );
304:        }
```

[Executor.sol#L257-L265)](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257-L265), [Executor.sol#L289-L304](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289-L304)
