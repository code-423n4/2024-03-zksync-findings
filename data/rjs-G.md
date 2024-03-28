# Summary

## Gas Optimizations
| # | Title | Instances |
| - | - | - |
| G-01 | [Assembly: Check `msg.sender` using `xor` and the scratch space](#g-01-assembly-check-msgsender-using-xor-and-the-scratch-space) | 37 |
| G-02 | [Assembly: Checks for `address(0x0)` are more efficient in assembly](#g-02-assembly-checks-for-address0x0-are-more-efficient-in-assembly) | 32 |
| G-03 | [Assembly: Use scratch space for building calldata](#g-03-assembly-use-scratch-space-for-building-calldata) | 71 |
| G-04 | [Assembly: Use scratch space for calculating small `keccak256` hashes](#g-04-assembly-use-scratch-space-for-calculating-small-keccak256-hashes) | 1 |
| G-05 | [Assembly: Use scratch space when building emitted events with two data arguments](#g-05-assembly-use-scratch-space-when-building-emitted-events-with-two-data-arguments) | 27 |
| G-06 | [Assigning to structs can be more efficient](#g-06-assigning-to-structs-can-be-more-efficient) | 25 |
| G-07 | [Avoid updating storage when the value hasn't changed](#g-07-avoid-updating-storage-when-the-value-hasnt-changed) | 51 |
| G-08 | [Cache multiple accesses of mapping/array values](#g-08-cache-multiple-accesses-of-mappingarray-values) | 60 |
| G-09 | [Cache state variables accessed multiple times in the same function](#g-09-cache-state-variables-accessed-multiple-times-in-the-same-function) | 90 |
| G-10 | [Calculation results within a function can be cached to save gas](#g-10-calculation-results-within-a-function-can-be-cached-to-save-gas) | 2 |
| G-11 | [Consider changing some `public` variables to `private`/`internal`](#g-11-consider-changing-some-public-variables-to-privateinternal) | 55 |
| G-12 | [Consider merging sequential for loops](#g-12-consider-merging-sequential-for-loops) | 4 |
| G-13 | [Consider pre-calculating the address of `address(this)` to save gas](#g-13-consider-pre-calculating-the-address-of-addressthis-to-save-gas) | 23 |
| G-14 | [Consider using OpenZeppelin `EnumerateSet` in place of nested mappings](#g-14-consider-using-openzeppelin-enumerateset-in-place-of-nested-mappings) | 10 |
| G-15 | [Constructors can be marked `payable`](#g-15-constructors-can-be-marked-payable) | 11 |
| G-16 | [Declare variables outside loops to save gas](#g-16-declare-variables-outside-loops-to-save-gas) | 52 |
| G-17 | [Default bool values are manually reset](#g-17-default-bool-values-are-manually-reset) | 3 |
| G-18 | [Default int values are manually reset](#g-18-default-int-values-are-manually-reset) | 3 |
| G-19 | [Detect zero value transfers to save gas](#g-19-detect-zero-value-transfers-to-save-gas) | 5 |
| G-20 | [Divisions can be `unchecked` to save gas](#g-20-divisions-can-be-unchecked-to-save-gas) | 14 |
| G-21 | [Don’t compare boolean expressions to boolean literals](#g-21-dont-compare-boolean-expressions-to-boolean-literals) | 3 |
| G-22 | [Duplicated `require()`/`revert()` checks should be refactored to a modifier or function to save deployment gas](#g-22-duplicated-requirerevert-checks-should-be-refactored-to-a-modifier-or-function-to-save-deployment-gas) | 17 |
| G-23 | [Emitting constants wastes gas](#g-23-emitting-constants-wastes-gas) | 6 |
| G-24 | [Enable IR-based code generation](#g-24-enable-ir-based-code-generation) | 71 |
| G-25 | [Events should be emitted outside of loops](#g-25-events-should-be-emitted-outside-of-loops) | 3 |
| G-26 | [Function names can be optimized to save gas](#g-26-function-names-can-be-optimized-to-save-gas) | 37 |
| G-27 | [Function result should be cached](#g-27-function-result-should-be-cached) | 8 |
| G-28 | [Functions guaranteed to revert when called by normal users can be marked `payable`](#g-28-functions-guaranteed-to-revert-when-called-by-normal-users-can-be-marked-payable) | 90 |
| G-29 | [Inline `internal` functions that are only called once](#g-29-inline-internal-functions-that-are-only-called-once) | 83 |
| G-30 | [Inline `modifier`s that are only used once, to save gas](#g-30-inline-modifiers-that-are-only-used-once-to-save-gas) | 25 |
| G-31 | [It costs more gas to initialize non-`constant`/non-`immutable` state variables to zero/false than to let the default of zero/false be applied](#g-31-it-costs-more-gas-to-initialize-non-constantnon-immutable-state-variables-to-zerofalse-than-to-let-the-default-of-zerofalse-be-applied) | 5 |
| G-32 | [Iterating backwards in a `for` statement saves gas](#g-32-iterating-backwards-in-a-for-statement-saves-gas) | 18 |
| G-33 | [Mappings are cheaper to use than storage arrays](#g-33-mappings-are-cheaper-to-use-than-storage-arrays) | 1 |
| G-34 | [Merge events to save gas](#g-34-merge-events-to-save-gas) | 8 |
| G-35 | [Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct`](#g-35-multiple-addressid-mappings-can-be-combined-into-a-single-mapping-of-an-addressid-to-a-struct) | 13 |
| G-36 | [Multiple accesses of a mapping/array should use a local variable cache](#g-36-multiple-accesses-of-a-mappingarray-should-use-a-local-variable-cache) | 35 |
| G-37 | [Nesting `if`-statements is cheaper than using `&&`](#g-37-nesting-if-statements-is-cheaper-than-using-) | 12 |
| G-38 | [Not using the named return variable is confusing and can waste gas](#g-38-not-using-the-named-return-variable-is-confusing-and-can-waste-gas) | 4 |
| G-39 | [Only emit event in setter function if the state variable was changed](#g-39-only-emit-event-in-setter-function-if-the-state-variable-was-changed) | 22 |
| G-40 | [Operator `>=`/`<=` costs less gas than operator `>`/`<`](#g-40-operator--costs-less-gas-than-operator-) | 98 |
| G-41 | [Public functions not used internally can be marked as external to save gas](#g-41-public-functions-not-used-internally-can-be-marked-as-external-to-save-gas) | 19 |
| G-42 | [Redundant type conversion](#g-42-redundant-type-conversion) | 17 |
| G-43 | [Refactor modifiers to call a local function](#g-43-refactor-modifiers-to-call-a-local-function) | 33 |
| G-44 | [Remove empty functions to save gas](#g-44-remove-empty-functions-to-save-gas) | 7 |
| G-45 | [Replace OpenZeppelin components with Solady equivalents to save gas](#g-45-replace-openzeppelin-components-with-solady-equivalents-to-save-gas) | 4 |
| G-46 | [Same cast is done multiple times](#g-46-same-cast-is-done-multiple-times) | 50 |
| G-47 | [Simple checks for zero can be done using assembly to save gas](#g-47-simple-checks-for-zero-can-be-done-using-assembly-to-save-gas) | 67 |
| G-48 | [Splitting `require()` statements that use `&&` saves gas](#g-48-splitting-require-statements-that-use--saves-gas) | 5 |
| G-49 | [Stack variable is only used once](#g-49-stack-variable-is-only-used-once) | 96 |
| G-50 | [Structs can be packed into fewer storage slots](#g-50-structs-can-be-packed-into-fewer-storage-slots) | 9 |
| G-51 | [Subtraction can potentially be marked `unchecked` to save gas](#g-51-subtraction-can-potentially-be-marked-unchecked-to-save-gas) | 69 |
| G-52 | [The result of function calls should be cached rather than re-calling the function](#g-52-the-result-of-function-calls-should-be-cached-rather-than-re-calling-the-function) | 55 |
| G-53 | [Time-related state variables can use smaller integer data types to save gas](#g-53-time-related-state-variables-can-use-smaller-integer-data-types-to-save-gas) | 1 |
| G-54 | [Usage of non-`uint256`/`int256` types uses more gas](#g-54-usage-of-non-uint256int256-types-uses-more-gas) | 99 |
| G-55 | [Use != 0 instead of > 0](#g-55-use--0-instead-of--0) | 24 |
| G-56 | [Use Solady library where possible to save gas](#g-56-use-solady-library-where-possible-to-save-gas) | 11 |
| G-57 | [Use `<<` to efficiently multiple by powers of `2`](#g-57-use--to-efficiently-multiple-by-powers-of-2) | 31 |
| G-58 | [Use `>>` to efficiently divide by powers of `2`](#g-58-use--to-efficiently-divide-by-powers-of-2) | 6 |
| G-59 | [Use `Array.unsafeAccess()` to avoid repeated array length checks](#g-59-use-arrayunsafeaccess-to-avoid-repeated-array-length-checks) | 10 |
| G-60 | [Use `calldata` instead of `memory` for function arguments that are read only](#g-60-use-calldata-instead-of-memory-for-function-arguments-that-are-read-only) | 45 |
| G-61 | [Use `private` rather than `public` for constants](#g-61-use-private-rather-than-public-for-constants) | 5 |
| G-62 | [Use `uint256(1)`/`uint256(2)` instead of `true`/`false` to save gas for changes](#g-62-use-uint2561uint2562-instead-of-truefalse-to-save-gas-for-changes) | 6 |
| G-63 | [Use assembly to calculate hashes](#g-63-use-assembly-to-calculate-hashes) | 61 |
| G-64 | [Use assembly to perform external calls, in order to save gas](#g-64-use-assembly-to-perform-external-calls-in-order-to-save-gas) | 13 |
| G-65 | [Use assembly to write storage values](#g-65-use-assembly-to-write-storage-values) | 99 |
| G-66 | [Use custom errors rather than `revert()`/`require()` strings to save gas](#g-66-use-custom-errors-rather-than-revertrequire-strings-to-save-gas) | 99 |
| G-67 | [Use local variables for emitting](#g-67-use-local-variables-for-emitting) | 12 |
| G-68 | [Use more recent OpenZeppelin version for gas boost](#g-68-use-more-recent-openzeppelin-version-for-gas-boost) | 25 |
| G-69 | [Use named `return` parameters](#g-69-use-named-return-parameters) | 99 |
| G-70 | [Use nested `if`s instead of `&&`](#g-70-use-nested-ifs-instead-of-) | 7 |
| G-71 | [Use of low-level `call()` can be optimized with assembly](#g-71-use-of-low-level-call-can-be-optimized-with-assembly) | 7 |
| G-72 | [Using `bool`s for storage incurs overhead](#g-72-using-bools-for-storage-incurs-overhead) | 6 |
| G-73 | [Using `storage` instead of `memory` for structs/arrays saves gas](#g-73-using-storage-instead-of-memory-for-structsarrays-saves-gas) | 2 |
| G-74 | [Using assembly's `selfbalance()` is cheaper than `address(this).balance`](#g-74-using-assemblys-selfbalance-is-cheaper-than-addressthisbalance) | 4 |
| G-75 | [`++i` costs less gas than `i++`, especially when it's used in `for`-loops (`--i`/`i--` too)](#g-75-i-costs-less-gas-than-i-especially-when-its-used-in-for-loops---ii---too) | 8 |
| G-76 | [`++i`/`i++` should be `unchecked{++i}`/`unchecked{i++}` when it is not possible for them to overflow, as is the case when used in `for`- and `while`-loops](#g-76-ii-should-be-uncheckediuncheckedi-when-it-is-not-possible-for-them-to-overflow-as-is-the-case-when-used-in-for--and-while-loops) | 18 |
| G-77 | [`<array>.length` should not be looked up in every loop of a `for`-loop](#g-77-arraylength-should-not-be-looked-up-in-every-loop-of-a-for-loop) | 8 |
| G-78 | [`<x> += <y>` costs more gas than `<x> = <x> + <y>` for state variables](#g-78-x--y-costs-more-gas-than-x--x--y-for-state-variables) | 11 |
| G-79 | [`abi.encode()` is less efficient than `abi.encodepacked()` for non-address arguments](#g-79-abiencode-is-less-efficient-than-abiencodepacked-for-non-address-arguments) | 34 |
| G-80 | [`do`-`while` is cheaper than `for`-loops when the initial check can be skipped](#g-80-do-while-is-cheaper-than-for-loops-when-the-initial-check-can-be-skipped) | 35 |
| G-81 | [require()`/`revert()` strings longer than 32 bytes cost extra gas](#g-81-requirerevert-strings-longer-than-32-bytes-cost-extra-gas) | 70 |

# Gas Optimizations

## [G-01] Assembly: Check `msg.sender` using `xor` and the scratch space

We can use assembly to efficiently validate `msg.sender` with the least amount of opcodes necessary. For more details check the following report [here](https://code4rena.com/reports/2023-05-juicebox#g-06-use-assembly-to-validate-msgsender).

*Instances: 37*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

  64 |  require(msg.sender == address(sharedBridge), "Not shared bridge");
```
GitHub: [64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

  69 |  require(msg.sender == address(bridgehub), "ShB not BH");

  75 |  require(
  76 |      msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
  77 |      "L1SharedBridge: not bridgehub or era chain"
  78 |  );

  84 |  require(msg.sender == address(legacyBridge), "ShB not legacy bridge");

 138 |  require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");
```
GitHub: [69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69), [75-78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75-L78), [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L84), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

  46 |  require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

  62 |  require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights
```
GitHub: [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

  59 |  require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

  65 |  require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

  71 |  require(
  72 |      msg.sender == owner() || msg.sender == securityCouncil,
  73 |      "Only the owner and security council are allowed to call this function"
  74 |  );
```
GitHub: [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L59), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L65), [71-74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L71-L74)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

  66 |  require(msg.sender == bridgehub, "StateTransition: only bridgehub");

  72 |  require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

 123 |  require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights
```
GitHub: [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L66), [72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L72), [123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L123)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

  62 |  require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");
```
GitHub: [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

  34 |  require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights
```
GitHub: [34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

  16 |  require(msg.sender == s.admin, "StateTransition Chain: not admin");

  27 |  require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

  32 |  require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

  37 |  require(
  38 |      msg.sender == s.admin || msg.sender == s.stateTransitionManager,
  39 |      "StateTransition Chain: Only by admin or state transition manager"
  40 |  );

  45 |  require(
  46 |      s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
  47 |      "StateTransition Chain: Only by validator or state transition manager"
  48 |  );

  53 |  require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
```
GitHub: [16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32), [37-40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L37-L40), [45-48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45-L48), [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53)


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

  26 |  require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
GitHub: [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L26)


```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

  22 |  require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");
```
GitHub: [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L22)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

  29 |  require(msg.sender == address(this), "Callable only by self");

 239 |  require(
 240 |      msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
 241 |      "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
 242 |  );
```
GitHub: [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L29), [239-242](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L239-L242)


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

  29 |  if (msg.sender != BOOTLOADER_FORMAL_ADDRESS) {
```
GitHub: [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L29)


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

  35 |  require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
GitHub: [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L35)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

  20 |  require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");
```
GitHub: [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L20)


```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

  33 |  require(
  34 |      msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
  35 |          msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
  36 |          msg.sender == BOOTLOADER_FORMAL_ADDRESS,
  37 |      "Only system contracts with special access can call this method"
  38 |  );
```
GitHub: [33-38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L33-L38)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

 136 |  require(
 137 |      msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
 138 |      "Only the contract deployer can increment the deployment nonce"
 139 |  );
```
GitHub: [136-139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L136-L139)


```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

  41 |  require(msg.sender == caller, "Inappropriate caller");

  48 |  require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");

  55 |  require(msg.sender == FORCE_DEPLOYER);
```
GitHub: [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L41), [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L48), [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L55)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

 120 |  require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");

 130 |  require(msg.sender == l2Bridge, "xnt"); // Only L2 bridge can call this method
```
GitHub: [120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L130)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

  22 |  require(msg.sender == BOOTLOADER_ADDRESS, "Only bootloader can call this contract");
```
GitHub: [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L22)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

  65 |  require(msg.sender == l2Bridge, "permission denied"); // Only L2 bridge can call this method
```
GitHub: [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L65)


## [G-02] Assembly: Checks for `address(0x0)` are more efficient in assembly

Using assembly to check for zero can save gas by allowing more direct access to the evm and reducing some of the overhead associated with high-level operations in solidity.

*Instances: 32*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 108 |  require(_owner != address(0), "ShB owner 0");

 188 |  require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

 563 |  require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

 578 |  if (_refundRecipient == address(0)) {
```
GitHub: [108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L108), [188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188), [563](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563), [578](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L578)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 130 |  require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

 132 |  require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

 326 |  if (_refundRecipient == address(0)) {
```
GitHub: [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132), [326](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L326)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

  42 |  require(_admin != address(0), "Admin should be non zero address");
```
GitHub: [42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L42)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

  84 |  require(_initializeData.governor != address(0), "StateTransition: governor zero");

 248 |  if (stateTransition[_chainId] != address(0)) {
```
GitHub: [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L84), [248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L248)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

  25 |  require(address(_initializeData.verifier) != address(0), "vt");

  26 |  require(_initializeData.admin != address(0), "vy");

  27 |  require(_initializeData.validatorTimelock != address(0), "hc");
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L26), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

  30 |  require(facetAddress != address(0), "F"); // Proxy has no facet for this selector
```
GitHub: [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

 183 |  require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");
```
GitHub: [183](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

 275 |  address refundRecipient = _params.refundRecipient == address(0) ? _params.sender : _params.refundRecipient;
```
GitHub: [275](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L275)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 141 |  require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists

 161 |  require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

 175 |  require(_facet == address(0), "a1"); // facet address must be zero

 181 |  require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet

 279 |  if (_init == address(0)) {
```
GitHub: [141](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L141), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L161), [175](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175), [181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L181), [279](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L279)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_4844.sol

  17 |  require(0x0000000000000000000000000000000000001337 != address(0), "b9");
```
GitHub: [17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_4844.sol#L17)


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

 188 |  return recoveredAddress == address(this) && recoveredAddress != address(0);
```
GitHub: [188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L188)


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

 406 |  if (address(uint160(_transaction.paymaster)) != address(0)) {
```
GitHub: [406](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L406)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

  55 |  require(_l1Bridge != address(0), "bf");

  57 |  require(_aliasedOwner != address(0), "sf");

  68 |  require(_l1LegecyBridge != address(0), "bf2");

  96 |  if (currentL1Token == address(0)) {

 129 |  require(l1Token != address(0), "yh");
```
GitHub: [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L57), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L68), [96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L96), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L129)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

  51 |  require(_l1Address != address(0), "in6"); // Should be non-zero address
```
GitHub: [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

  50 |  require(_l2Bridge != address(0), "L2 bridge address cannot be zero");

  51 |  require(_l1Address != address(0), "L1 WETH token address cannot be zero");
```
GitHub: [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L50), [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L51)


## [G-03] Assembly: Use scratch space for building calldata

If an external call's calldata can fit into two or fewer words, use the scratch space to build the calldata, rather than allowing Solidity to do a memory expansion.

*Instances: 71*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

  65 |  uint256 amount = IERC20(_token).balanceOf(address(this));

  67 |  IERC20(_token).safeTransfer(address(sharedBridge), amount);

 161 |  uint256 balanceBefore = _token.balanceOf(address(sharedBridge));

 163 |  uint256 balanceAfter = _token.balanceOf(address(sharedBridge));
```
GitHub: [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L161), [163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L163)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 119 |  IMailbox(_target).transferEthToSharedBridge();

 127 |  uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

 128 |  uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));

 130 |  IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);

 131 |  uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

 138 |  require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");

 174 |  uint256 balanceBefore = _token.balanceOf(address(this));

 176 |  uint256 balanceAfter = _token.balanceOf(address(this));

 195 |  require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

 362 |  IERC20(_l1Token).safeTransfer(_depositSender, _amount);

 396 |  require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");

 423 |  bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
 424 |      _l2BatchNumber,
 425 |      _l2MessageIndex
 426 |  );

 452 |  IERC20(l1Token).safeTransfer(l1Receiver, amount);

 467 |  bool baseTokenWithdrawal = (l1Token == bridgehub.baseToken(_chainId));

 508 |  l1Token = bridgehub.baseToken(_chainId);

 595 |  l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
```
GitHub: [119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L119), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127), [128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L128), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L130), [131](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L174), [176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176), [195](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195), [362](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L362), [396](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L396), [423-426](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L423-L426), [452](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L452), [467](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L467), [508](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L508), [595](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L595)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

  76 |  return IStateTransitionManager(stateTransitionManager[_chainId]).stateTransition(_chainId);

 238 |  canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction(
 239 |      BridgehubL2TransactionRequest({
 240 |          sender: msg.sender,
 241 |          contractL2: _request.l2Contract,
 242 |          mintValue: _request.mintValue,
 243 |          l2Value: _request.l2Value,
 244 |          l2Calldata: _request.l2Calldata,
 245 |          l2GasLimit: _request.l2GasLimit,
 246 |          l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
 247 |          factoryDeps: _request.factoryDeps,
 248 |          refundRecipient: refundRecipient
 249 |      })
 250 |  );

 304 |  canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction(
 305 |      BridgehubL2TransactionRequest({
 306 |          sender: _request.secondBridgeAddress,
 307 |          contractL2: outputRequest.l2Contract,
 308 |          mintValue: _request.mintValue,
 309 |          l2Value: _request.l2Value,
 310 |          l2Calldata: outputRequest.l2Calldata,
 311 |          l2GasLimit: _request.l2GasLimit,
 312 |          l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
 313 |          factoryDeps: outputRequest.factoryDeps,
 314 |          refundRecipient: refundRecipient
 315 |      })
 316 |  );
```
GitHub: [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L76), [238-250](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L238-L250), [304-316](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L304-L316)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

  77 |  return IZkSyncStateTransition(stateTransition[_chainId]).getAdmin();

 163 |  IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();

 168 |  IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();

 173 |  IZkSyncStateTransition(stateTransition[_chainId]).revertBatches(_newLastBatch);

 228 |  IAdmin(_chainContract).executeUpgrade(cutData);
```
GitHub: [77](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L77), [163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L163), [168](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L168), [173](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L173), [228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L228)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

  62 |  require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

 226 |  address contractAddress = stateTransitionManager.stateTransition(_chainId);
```
GitHub: [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L226)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 106 |  cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
```
GitHub: [106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L106)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 227 |  IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
```
GitHub: [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L227)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

  43 |  IL1SharedBridge(sharedBridgeAddress).receiveEth{value: amount}(ERA_CHAIN_ID);
```
GitHub: [43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L43)


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

 102 |  if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {
```
GitHub: [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L102)


```solidity
File: code/system-contracts/contracts/Compressor.sol

  73 |  L1_MESSENGER_CONTRACT.sendToL1(_rawCompressedData);

  74 |  KNOWN_CODE_STORAGE_CONTRACT.markBytecodeAsPublished(bytecodeHash);
```
GitHub: [73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L73), [74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L74)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

  49 |  ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getRawCodeHash(_address) == 0

 168 |  NONCE_HOLDER_SYSTEM_CONTRACT.incrementDeploymentNonce(msg.sender);

 188 |  uint256 senderNonce = NONCE_HOLDER_SYSTEM_CONTRACT.incrementDeploymentNonce(msg.sender);

 254 |  this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);

 269 |  ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0,

 273 |  require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied");

 302 |  uint256 knownCodeMarker = KNOWN_CODE_STORAGE_CONTRACT.getMarker(_bytecodeHash);

 312 |  ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.storeAccountConstructingCodeHash(_newAddress, constructingBytecodeHash);

 345 |  ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.markAccountCodeHashAsConstructed(_newAddress);

 348 |  IMMUTABLE_SIMULATOR_SYSTEM_CONTRACT.setImmutables(_newAddress, immutables);

 352 |  ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.storeAccountConstructedCodeHash(_newAddress, _bytecodeHash);
```
GitHub: [49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L49), [168](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L168), [188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L188), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L254), [269](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L269), [273](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L273), [302](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L302), [312](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L312), [345](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L345), [348](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L348), [352](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L352)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

  51 |  L1_MESSENGER_CONTRACT.requestBytecodeL1Publication(_bytecodeHash);
```
GitHub: [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L51)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

  78 |  txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),

 128 |  txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),

 317 |  PUBDATA_CHUNK_PUBLISHER.chunkAndPublishPubdata(totalL2ToL1Pubdata);
```
GitHub: [78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L78), [128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L128), [317](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L317)


```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

  77 |  L1_MESSENGER_CONTRACT.sendToL1(message);

  90 |  L1_MESSENGER_CONTRACT.sendToL1(message);
```
GitHub: [77](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L77), [90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L90)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

  83 |  IContractDeployer.AccountInfo memory accountInfo = DEPLOYER_SYSTEM_CONTRACT.getAccountInfo(msg.sender);
```
GitHub: [83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L83)


```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

  51 |  uint256 pubdataPublishedBefore = REAL_SYSTEM_CONTEXT_CONTRACT.getCurrentPubdataSpent();

  59 |  uint256 pubdataPublishedAfter = REAL_SYSTEM_CONTEXT_CONTRACT.getCurrentPubdataSpent();

  67 |  uint256 pubdataPrice = REAL_SYSTEM_CONTEXT_CONTRACT.gasPerPubdataByte();
```
GitHub: [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L51), [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L59), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L67)


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

 377 |  uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);

 382 |  IERC20(token).safeApprove(paymaster, 0);

 383 |  IERC20(token).safeApprove(paymaster, minAllowance);
```
GitHub: [377](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377), [382](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L382), [383](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L383)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

  66 |  l2TokenBeacon.transferOwnership(_aliasedOwner);

 104 |  IL2StandardToken(expectedL2Token).bridgeMint(_l2Receiver, _amount);

 113 |  L2StandardERC20(address(l2Token)).bridgeInitialize(_l1Token, _data);

 126 |  IL2StandardToken(_l2Token).bridgeBurn(msg.sender, _amount);
```
GitHub: [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L66), [104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L104), [113](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L113), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L126)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

  75 |  try this.decodeString(nameBytes) returns (string memory nameString) {

  81 |  try this.decodeString(symbolBytes) returns (string memory symbolString) {

  93 |  try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {

 120 |  require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");
```
GitHub: [75](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L75), [81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L81), [93](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L93), [120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120)


```solidity
File: code/contracts/zksync/contracts/ForceDeployUpgrader.sol

  14 |  IContractDeployer(DEPLOYER_SYSTEM_CONTRACT).forceDeployOnAddresses{value: msg.value}(_forceDeployments);
```
GitHub: [14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L14)


```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

  91 |  return L2_MESSENGER.sendToL1(_message);
```
GitHub: [91](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L91)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

  35 |  uint256 providedAllowance = IERC20(token).allowance(userAddress, thisAddress);
```
GitHub: [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L35)


## [G-04] Assembly: Use scratch space for calculating small `keccak256` hashes

If the arguments to the encode call can fit into the scratch space (two words or fewer), then it's more efficient to use assembly to generate the hash (**80 gas**):
`keccak256(abi.encodePacked(x, y))` -> `assembly {mstore(0x00, a); mstore(0x20, b); let hash := keccak256(0x00, 0x40); }`

*Instances: 1*

```solidity
File: code/system-contracts/contracts/SystemContext.sol

 159 |  hash = keccak256(abi.encode(_block));
```
GitHub: [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L159)


## [G-05] Assembly: Use scratch space when building emitted events with two data arguments

To efficiently emit events, it's possible to utilize assembly by making use of scratch space and the free memory pointer. This approach has the advantage of potentially avoiding the costs associated with memory expansion.

However, it's important to note that in order to safely optimize this process, it is preferable to cache and restore the free memory pointer.

A good example of such practice can be seen in [Solady's](https://github.com/Vectorized/solady/blob/main/src/tokens/ERC1155.sol#L167) codebase.

*Instances: 27*

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

  56 |  emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

  68 |  emit NewPendingAdmin(currentPendingAdmin, address(0));

  69 |  emit NewAdmin(previousAdmin, pendingAdmin);
```
GitHub: [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L56), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68), [69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

  47 |  emit ChangeSecurityCouncil(address(0), _securityCouncil);

  50 |  emit ChangeMinDelay(0, _minDelay);

 250 |  emit ChangeMinDelay(minDelay, _newDelay);

 257 |  emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```
GitHub: [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L47), [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L50), [250](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L250), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L257)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 117 |  emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

 129 |  emit NewPendingAdmin(currentPendingAdmin, address(0));

 130 |  emit NewAdmin(previousAdmin, pendingAdmin);

 237 |  emit StateTransitionNewChain(_chainId, _stateTransitionContract);

 289 |  emit StateTransitionNewChain(_chainId, stateTransitionAddress);
```
GitHub: [117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L117), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L129), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L130), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L237), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L289)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

  83 |  emit ValidatorAdded(_chainId, _newValidator);

  92 |  emit ValidatorRemoved(_chainId, _validator);
```
GitHub: [83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L83), [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L92)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

  28 |  emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

  40 |  emit NewPendingAdmin(pendingAdmin, address(0));

  41 |  emit NewAdmin(previousAdmin, pendingAdmin);

  47 |  emit ValidatorStatusUpdate(_validator, _active);

  63 |  emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);
```
GitHub: [28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L28), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L41), [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L47), [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L63)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 436 |  emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);
```
GitHub: [436](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 137 |  emit NewVerifier(address(oldVerifier), address(_newVerifier));

 256 |  emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
```
GitHub: [137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L137), [256](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L256)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

  40 |  emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
```
GitHub: [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L40)


```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

  67 |  emit Mint(_account, _amount);
```
GitHub: [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L67)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

 147 |  emit BridgeMint(_to, _amount);

 156 |  emit BridgeBurn(_from, _amount);
```
GitHub: [147](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L147), [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L156)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

  86 |  emit BridgeBurn(_from, _amount);
```
GitHub: [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L86)


## [G-06] Assigning to structs can be more efficient

By changing the pattern of assigning value to the structure, gas savings of ~130 per instance are achieved. In addition, this use will provide significant savings in distribution costs.  

Instead of:

```solidity     
MyStruct memory myStruct = MyStruct(_a, _b, _c); 
```

write  

```solidity     
MyStruct memory myStruct;     
myStruct.a = _a;     
myStruct.b = _b;     
myStruct.c = _c; 
```


*Instances: 25*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Assign struct fields individually to save gas
 219 |  request = L2TransactionRequestTwoBridgesInner({
 220 |      magicValue: TWO_BRIDGES_MAGIC_VALUE,
 221 |      l2Contract: l2BridgeAddress[_chainId],
 222 |      l2Calldata: l2TxCalldata,
 223 |      factoryDeps: new bytes[](0),
 224 |      txDataHash: txDataHash
 225 |  });

     |  // @audit-issue Assign struct fields individually to save gas
 430 |  MessageParams memory messageParams = MessageParams({
 431 |      l2BatchNumber: _l2BatchNumber,
 432 |      l2MessageIndex: _l2MessageIndex,
 433 |      l2TxNumberInBatch: _l2TxNumberInBatch
 434 |  });

     |  // @audit-issue Assign struct fields individually to save gas
 470 |  l2ToL1Message = L2Message({
 471 |      txNumberInBatch: _messageParams.l2TxNumberInBatch,
 472 |      sender: l2Sender,
 473 |      data: _message
 474 |  });

     |  // @audit-issue Assign struct fields individually to save gas
 584 |  L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
 585 |      chainId: ERA_CHAIN_ID,
 586 |      l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
 587 |      mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
 588 |      l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
 589 |      l2Calldata: l2TxCalldata,
 590 |      l2GasLimit: _l2TxGasLimit,
 591 |      l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
 592 |      factoryDeps: new bytes[](0),
 593 |      refundRecipient: refundRecipient
 594 |  });
```
GitHub: [219-225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L219-L225), [430-434](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L430-L434), [470-474](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L470-L474), [584-594](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L584-L594)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Assign struct fields individually to save gas
 239 |  BridgehubL2TransactionRequest({
 240 |      sender: msg.sender,
 241 |      contractL2: _request.l2Contract,
 242 |      mintValue: _request.mintValue,
 243 |      l2Value: _request.l2Value,
 244 |      l2Calldata: _request.l2Calldata,
 245 |      l2GasLimit: _request.l2GasLimit,
 246 |      l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
 247 |      factoryDeps: _request.factoryDeps,
 248 |      refundRecipient: refundRecipient
 249 |  })

     |  // @audit-issue Assign struct fields individually to save gas
 305 |  BridgehubL2TransactionRequest({
 306 |      sender: _request.secondBridgeAddress,
 307 |      contractL2: outputRequest.l2Contract,
 308 |      mintValue: _request.mintValue,
 309 |      l2Value: _request.l2Value,
 310 |      l2Calldata: outputRequest.l2Calldata,
 311 |      l2GasLimit: _request.l2GasLimit,
 312 |      l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
 313 |      factoryDeps: outputRequest.factoryDeps,
 314 |      refundRecipient: refundRecipient
 315 |  })
```
GitHub: [239-249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L239-L249), [305-315](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L305-L315)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Assign struct fields individually to save gas
  92 |  IExecutor.StoredBatchInfo memory batchZero = IExecutor.StoredBatchInfo(
  93 |      0,
  94 |      _initializeData.genesisBatchHash,
  95 |      _initializeData.genesisIndexRepeatedStorageChanges,
  96 |      0,
  97 |      EMPTY_STRING_KECCAK,
  98 |      DEFAULT_L2_LOGS_TREE_ROOT_HASH,
  99 |      0,
 100 |      _initializeData.genesisBatchCommitment
 101 |  );

     |  // @audit-issue Assign struct fields individually to save gas
 184 |  L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
 185 |      txType: SYSTEM_UPGRADE_L2_TX_TYPE,
 186 |      from: uint256(uint160(L2_FORCE_DEPLOYER_ADDR)),
 187 |      to: uint256(uint160(L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR)),
 188 |      gasLimit: 72000000,
 189 |      gasPerPubdataByteLimit: REQUIRED_L2_GAS_PRICE_PER_PUBDATA,
 190 |      maxFeePerGas: uint256(0),
 191 |      maxPriorityFeePerGas: uint256(0),
 192 |      paymaster: uint256(0),
 193 |      // Note, that the priority operation id is used as "nonce" for L1->L2 transactions
 194 |      nonce: protocolVersion,
 195 |      value: 0,
 196 |      reserved: [uint256(0), 0, 0, 0],
 197 |      data: systemContextCalldata,
 198 |      signature: new bytes(0),
 199 |      factoryDeps: uintEmptyArray,
 200 |      paymasterInput: new bytes(0),
 201 |      reservedDynamic: new bytes(0)
 202 |  });

     |  // @audit-issue Assign struct fields individually to save gas
 204 |  ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
 205 |      l2ProtocolUpgradeTx: l2ProtocolUpgradeTx,
 206 |      factoryDeps: bytesEmptyArray,
 207 |      bootloaderHash: bytes32(0),
 208 |      defaultAccountHash: bytes32(0),
 209 |      verifier: address(0),
 210 |      verifierParams: VerifierParams({
 211 |          recursionNodeLevelVkHash: bytes32(0),
 212 |          recursionLeafLevelVkHash: bytes32(0),
 213 |          recursionCircuitsSetVksHash: bytes32(0)
 214 |      }),
 215 |      l1ContractsUpgradeCalldata: new bytes(0),
 216 |      postUpgradeCalldata: new bytes(0),
 217 |      upgradeTimestamp: 0,
 218 |      newProtocolVersion: protocolVersion
 219 |  });

     |  // @audit-issue Assign struct fields individually to save gas
 210 |  verifierParams: VerifierParams({
 211 |      recursionNodeLevelVkHash: bytes32(0),
 212 |      recursionLeafLevelVkHash: bytes32(0),
 213 |      recursionCircuitsSetVksHash: bytes32(0)
 214 |  }),

     |  // @audit-issue Assign struct fields individually to save gas
 222 |  Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({
 223 |      facetCuts: emptyArray,
 224 |      initAddress: genesisUpgrade,
 225 |      initCalldata: abi.encodeCall(IDefaultUpgrade.upgrade, (proposedUpgrade))
 226 |  });
```
GitHub: [92-101](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L92-L101), [184-202](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L184-L202), [204-219](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L204-L219), [210-214](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L210-L214), [222-226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L222-L226)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Assign struct fields individually to save gas
  87 |  StoredBatchInfo(
  88 |      _newBatch.batchNumber,
  89 |      _newBatch.newStateRoot,
  90 |      _newBatch.indexRepeatedStorageChanges,
  91 |      _newBatch.numberOfLayer1Txs,
  92 |      _newBatch.priorityOperationsHash,
  93 |      logOutput.l2LogsTreeRoot,
  94 |      _newBatch.timestamp,
  95 |      commitment
  96 |  );
```
GitHub: [87-96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L87-L96)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-issue Assign struct fields individually to save gas
 212 |  result[i] = Facet(facetAddr, facetToSelectors.selectors);
```
GitHub: [212](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L212)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Assign struct fields individually to save gas
  92 |  L2Log memory l2Log = L2Log({
  93 |      l2ShardId: 0,
  94 |      isService: true,
  95 |      txNumberInBatch: _l2TxNumberInBatch,
  96 |      sender: L2_BOOTLOADER_ADDRESS,
  97 |      key: _l2TxHash,
  98 |      value: bytes32(uint256(_status))
  99 |  });

     |  // @audit-issue Assign struct fields individually to save gas
 132 |  L2Log({
 133 |      l2ShardId: 0,
 134 |      isService: true,
 135 |      txNumberInBatch: _message.txNumberInBatch,
 136 |      sender: L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR,
 137 |      key: bytes32(uint256(uint160(_message.sender))),
 138 |      value: keccak256(_message.data)
 139 |  });

     |  // @audit-issue Assign struct fields individually to save gas
 208 |  BridgehubL2TransactionRequest({
 209 |      sender: msg.sender,
 210 |      contractL2: _contractL2,
 211 |      mintValue: msg.value,
 212 |      l2Value: _l2Value,
 213 |      l2GasLimit: _l2GasLimit,
 214 |      l2Calldata: _calldata,
 215 |      l2GasPerPubdataByteLimit: _l2GasPerPubdataByteLimit,
 216 |      factoryDeps: _factoryDeps,
 217 |      refundRecipient: _refundRecipient
 218 |  })

     |  // @audit-issue Assign struct fields individually to save gas
 294 |  transaction = L2CanonicalTransaction({
 295 |      txType: PRIORITY_OPERATION_L2_TX_TYPE,
 296 |      from: uint256(uint160(_priorityOpParams.sender)),
 297 |      to: uint256(uint160(_priorityOpParams.contractAddressL2)),
 298 |      gasLimit: _priorityOpParams.l2GasLimit,
 299 |      gasPerPubdataByteLimit: _priorityOpParams.l2GasPricePerPubdata,
 300 |      maxFeePerGas: uint256(_priorityOpParams.l2GasPrice),
 301 |      maxPriorityFeePerGas: uint256(0),
 302 |      paymaster: uint256(0),
 303 |      // Note, that the priority operation id is used as "nonce" for L1->L2 transactions
 304 |      nonce: uint256(_priorityOpParams.txId),
 305 |      value: _priorityOpParams.l2Value,
 306 |      reserved: [_priorityOpParams.valueToMint, uint256(uint160(_priorityOpParams.refundRecipient)), 0, 0],
 307 |      data: _calldata,
 308 |      signature: new bytes(0),
 309 |      factoryDeps: _hashFactoryDeps(_factoryDeps),
 310 |      paymasterInput: new bytes(0),
 311 |      reservedDynamic: new bytes(0)
 312 |  });

     |  // @audit-issue Assign struct fields individually to save gas
 335 |  PriorityOperation({
 336 |      canonicalTxHash: canonicalTxHash,
 337 |      expirationTimestamp: _priorityOpParams.expirationTimestamp,
 338 |      layer2Tip: uint192(0) // TODO: Restore after fee modeling will be stable. (SMA-1230)
 339 |  })
```
GitHub: [92-99](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L92-L99), [132-139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L132-L139), [208-218](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L208-L218), [294-312](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L294-L312), [335-339](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L335-L339)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

     |  // @audit-issue Assign struct fields individually to save gas
 218 |  ds.selectorToFacet[_selector] = SelectorToFacet({
 219 |      facetAddress: _facet,
 220 |      selectorPosition: selectorPosition,
 221 |      isFreezable: _isSelectorFreezable
 222 |  });
```
GitHub: [218-222](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L218-L222)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol

     |  // @audit-issue Assign struct fields individually to save gas
  36 |  FeeParams({
  37 |      pubdataPricingMode: PubdataPricingMode.Rollup,
  38 |      batchOverheadL1Gas: 1000000,
  39 |      maxPubdataPerBatch: 120000,
  40 |      maxL2GasPerBatch: 80000000,
  41 |      priorityTxMaxPubdata: 99000,
  42 |      minimalL2GasPrice: 250000000
  43 |  })
```
GitHub: [36-43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol#L36-L43)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Assign struct fields individually to save gas
  75 |  L2ToL1Log memory l2ToL1Log = L2ToL1Log({
  76 |      l2ShardId: 0,
  77 |      isService: _isService,
  78 |      txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),
  79 |      sender: msg.sender,
  80 |      key: _key,
  81 |      value: _value
  82 |  });

     |  // @audit-issue Assign struct fields individually to save gas
 125 |  L2ToL1Log memory l2ToL1Log = L2ToL1Log({
 126 |      l2ShardId: 0,
 127 |      isService: true,
 128 |      txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),
 129 |      sender: address(this),
 130 |      key: bytes32(uint256(uint160(msg.sender))),
 131 |      value: hash
 132 |  });
```
GitHub: [75-82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L75-L82), [125-132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L125-L132)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Assign struct fields individually to save gas
 316 |  currentL2BlockInfo = BlockInfo({number: _l2BlockNumber, timestamp: _l2BlockTimestamp});

     |  // @audit-issue Assign struct fields individually to save gas
 459 |  BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp});

     |  // @audit-issue Assign struct fields individually to save gas
 476 |  BlockInfo memory newBlockInfo = BlockInfo({number: uint128(_number), timestamp: uint128(_newTimestamp)});
```
GitHub: [316](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L316), [459](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L459), [476](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L476)


## [G-07] Avoid updating storage when the value hasn't changed

If the old value is equal to the new value, not re-storing the value will avoid a `Gsreset` (2900 gas), potentially at the expense of a `Gcoldsload` (2100 gas) or a `Gwarmaccess` (100 gas). Min = `Gsreset` - `Gcoldsload`, Max = `Gsreset` - `Gwarmaccess`.

*Instances: 51*

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-info Contains state variable assignments
  51 |  function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  55 |      pendingAdmin = _newPendingAdmin;

     |  // @audit-info Contains state variable assignments
  82 |  function addStateTransitionManager(address _stateTransitionManager) external onlyOwner {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  87 |      stateTransitionManagerIsRegistered[_stateTransitionManager] = true;

     |  // @audit-info Contains state variable assignments
  92 |  function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  97 |      stateTransitionManagerIsRegistered[_stateTransitionManager] = false;

     |  // @audit-info Contains state variable assignments
 101 |  function addToken(address _token) external onlyOwner {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 103 |      tokenIsRegistered[_token] = true;

     |  // @audit-info Contains state variable assignments
 108 |  function setSharedBridge(address _sharedBridge) external onlyOwner {
     |      // @audit-issue Consider checking if the value has changed first
 109 |      sharedBridge = IL1SharedBridge(_sharedBridge);
```
GitHub: [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55), [87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L87), [97](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L97), [103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L103), [109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L109)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-info Contains state variable assignments
 249 |  function updateDelay(uint256 _newDelay) external onlySelf {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 251 |      minDelay = _newDelay;

     |  // @audit-info Contains state variable assignments
 256 |  function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 258 |      securityCouncil = _newSecurityCouncil;
```
GitHub: [251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L251), [258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L258)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-info Contains state variable assignments
 112 |  function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 116 |      pendingAdmin = _newPendingAdmin;

     |  // @audit-info Contains state variable assignments
 134 |  function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {
     |      // @audit-issue Consider checking if the value has changed first
 135 |      validatorTimelock = _validatorTimelock;

     |  // @audit-info Contains state variable assignments
 139 |  function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {
     |      // @audit-issue Consider checking if the value has changed first
 140 |      initialCutHash = keccak256(abi.encode(_diamondCut));

     |  // @audit-info Contains state variable assignments
 144 |  function setNewVersionUpgrade(
 145 |      Diamond.DiamondCutData calldata _cutData,
 146 |      uint256 _oldProtocolVersion,
 147 |      uint256 _newProtocolVersion
 148 |  ) external onlyOwner {
     |      // @audit-issue Consider checking if the value has changed first
 149 |      upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
     |      // @audit-issue Consider checking if the value has changed first
 150 |      protocolVersion = _newProtocolVersion;

     |  // @audit-info Contains state variable assignments
 154 |  function setUpgradeDiamondCut(
 155 |      Diamond.DiamondCutData calldata _cutData,
 156 |      uint256 _oldProtocolVersion
 157 |  ) external onlyOwner {
     |      // @audit-issue Consider checking if the value has changed first
 158 |      upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
```
GitHub: [116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L116), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L135), [140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L140), [149](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L149), [150](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L150), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L158)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-info Contains state variable assignments
  73 |  function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {
     |      // @audit-issue Consider checking if the value has changed first
  74 |      stateTransitionManager = _stateTransitionManager;

     |  // @audit-info Contains state variable assignments
  78 |  function addValidator(uint256 _chainId, address _newValidator) external onlyChainAdmin(_chainId) {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  82 |      validators[_chainId][_newValidator] = true;

     |  // @audit-info Contains state variable assignments
  87 |  function removeValidator(uint256 _chainId, address _validator) external onlyChainAdmin(_chainId) {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  91 |      validators[_chainId][_validator] = false;

     |  // @audit-info Contains state variable assignments
  96 |  function setExecutionDelay(uint32 _executionDelay) external onlyOwner {
     |      // @audit-issue Consider checking if the value has changed first
  97 |      executionDelay = _executionDelay;
```
GitHub: [74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L74), [82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L82), [91](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L91), [97](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L97)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-info Contains state variable assignments
  23 |  function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  27 |      s.pendingAdmin = _newPendingAdmin;

     |  // @audit-info Contains state variable assignments
  45 |  function setValidator(address _validator, bool _active) external onlyStateTransitionManager {
     |      // @audit-issue Consider checking if the value has changed first
  46 |      s.validators[_validator] = _active;

     |  // @audit-info Contains state variable assignments
  51 |  function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  53 |      s.zkPorterIsAvailable = _zkPorterIsAvailable;

     |  // @audit-info Contains state variable assignments
  58 |  function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  62 |      s.priorityTxMaxGasLimit = _newPriorityTxMaxGasLimit;

     |  // @audit-info Contains state variable assignments
  67 |  function changeFeeParams(FeeParams calldata _newFeeParams) external onlyAdminOrStateTransitionManager {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  73 |      s.feeParams = _newFeeParams;

     |  // @audit-info Contains state variable assignments
  79 |  function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  83 |      s.baseTokenGasPriceMultiplierNominator = _nominator;
     |      // @audit-issue Consider checking if the value has changed first
  84 |      s.baseTokenGasPriceMultiplierDenominator = _denominator;

     |  // @audit-info Contains state variable assignments
  89 |  function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  91 |      s.feeParams.pubdataPricingMode = _validiumMode;
```
GitHub: [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L27), [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L46), [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L53), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L62), [73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L73), [83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L83), [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L84), [91](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L91)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-info Contains state variable assignments
  92 |  function _setL2DefaultAccountBytecodeHash(bytes32 _l2DefaultAccountBytecodeHash) private {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 103 |      s.l2DefaultAccountBytecodeHash = _l2DefaultAccountBytecodeHash;

     |  // @audit-info Contains state variable assignments
 109 |  function _setL2BootloaderBytecodeHash(bytes32 _l2BootloaderBytecodeHash) private {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 120 |      s.l2BootloaderBytecodeHash = _l2BootloaderBytecodeHash;

     |  // @audit-info Contains state variable assignments
 126 |  function _setVerifier(IVerifier _newVerifier) private {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 136 |      s.verifier = _newVerifier;

     |  // @audit-info Contains state variable assignments
 142 |  function _setVerifierParams(VerifierParams calldata _newVerifierParams) private {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 156 |      s.verifierParams = _newVerifierParams;

     |  // @audit-info Contains state variable assignments
 180 |  function _setL2SystemContractUpgrade(
 181 |      L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
 182 |      bytes[] calldata _factoryDeps,
 183 |      uint256 _newProtocolVersion
 184 |  ) internal returns (bytes32) {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 214 |      s.l2SystemContractsUpgradeTxHash = l2ProtocolUpgradeTxHash;

     |  // @audit-info Contains state variable assignments
 236 |  function _setNewProtocolVersion(uint256 _newProtocolVersion) internal virtual {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 255 |      s.protocolVersion = _newProtocolVersion;
```
GitHub: [103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L103), [120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L120), [136](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L136), [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L156), [214](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L214), [255](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L255)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

     |  // @audit-info Contains state variable assignments
  20 |  function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  39 |      s.protocolVersion = _newProtocolVersion;
```
GitHub: [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L39)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol

     |  // @audit-info Contains state variable assignments
  20 |  function changeFeeParams(FeeParams memory _newFeeParams) private {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  26 |      s.feeParams = _newFeeParams;
```
GitHub: [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol#L26)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-info Contains state variable assignments
  65 |  function updateAccountVersion(AccountAbstractionVersion _version) external onlySystemCall {
     |      // @audit-issue Consider checking if the value has changed first
  66 |      accountInfo[msg.sender].supportedAAVersion = _version;
```
GitHub: [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L66)


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

     |  // @audit-info Contains state variable assignments
  34 |  function setImmutables(address _dest, ImmutableData[] calldata _immutables) external override {
  :  |
     |              // @audit-issue Consider checking if the value has changed first
  41 |              immutableDataStorage[uint256(uint160(_dest))][index] = value;
```
GitHub: [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L41)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-info Contains state variable assignments
  82 |  function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
  94 |      nonceValues[addressAsKey][_key] = _value;
```
GitHub: [94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L94)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-info Contains state variable assignments
  84 |  function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {
     |      // @audit-issue Consider checking if the value has changed first
  85 |      chainId = _newChainId;

     |  // @audit-info Contains state variable assignments
  99 |  function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {
     |      // @audit-issue Consider checking if the value has changed first
 100 |      origin = _newOrigin;

     |  // @audit-info Contains state variable assignments
 105 |  function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {
     |      // @audit-issue Consider checking if the value has changed first
 106 |      gasPrice = _gasPrice;

     |  // @audit-info Contains state variable assignments
 112 |  function setPubdataInfo(uint256 _gasPerPubdataByte, uint256 _basePubdataSpent) external onlyCallFromBootloader {
     |      // @audit-issue Consider checking if the value has changed first
 113 |      basePubdataSpent = _basePubdataSpent;
     |      // @audit-issue Consider checking if the value has changed first
 114 |      gasPerPubdataByte = _gasPerPubdataByte;

     |  // @audit-info Contains state variable assignments
 212 |  function _setL2BlockHash(uint256 _block, bytes32 _hash) internal {
     |      // @audit-issue Consider checking if the value has changed first
 213 |      l2BlockHash[_block % MINIBLOCK_HASHES_TO_STORE] = _hash;

     |  // @audit-info Contains state variable assignments
 263 |  function _setVirtualBlock(
 264 |      uint128 _l2BlockNumber,
 265 |      uint128 _maxVirtualBlocksToCreate,
 266 |      uint128 _newTimestamp
 267 |  ) internal {
  :  |
     |          // @audit-issue Consider checking if the value has changed first
 271 |          currentVirtualL2BlockInfo = currentL2BlockInfo;
  :  |
     |          // @audit-issue Consider checking if the value has changed first
 285 |          virtualBlockUpgradeInfo.virtualBlockStartBatch = currentBatchNumber;
  :  |
     |          // @audit-issue Consider checking if the value has changed first
 303 |          virtualBlockUpgradeInfo.virtualBlockFinishL2Block = _l2BlockNumber;
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 307 |      currentVirtualL2BlockInfo = virtualBlockInfo;

     |  // @audit-info Contains state variable assignments
 314 |  function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 316 |      currentL2BlockInfo = BlockInfo({number: _l2BlockNumber, timestamp: _l2BlockTimestamp});
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 322 |      currentL2BlockTxsRollingHash = bytes32(0);

     |  // @audit-info Contains state variable assignments
 444 |  function setNewBatch(
 445 |      bytes32 _prevBatchHash,
 446 |      uint128 _newTimestamp,
 447 |      uint128 _expectedNewNumber,
 448 |      uint256 _baseFee
 449 |  ) external onlyCallFromBootloader {
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 456 |      batchHashes[previousBatchNumber] = _prevBatchHash;
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 461 |      currentBatchInfo = newBlockInfo;
  :  |
     |      // @audit-issue Consider checking if the value has changed first
 463 |      baseFee = _baseFee;
```
GitHub: [85](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L85), [100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L100), [106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L106), [113](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L113), [114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L114), [213](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L213), [271](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L271), [285](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L285), [303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L303), [307](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L307), [316](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L316), [322](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L322), [456](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L456), [461](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L461), [463](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L463)


## [G-08] Cache multiple accesses of mapping/array values

Caching a mapping's value in a local `storage` or `calldata` variable when the value is accessed multiple times, saves ~42 gas per access due to not having to recalculate the key's keccak256 hash (Gkeccak256 - 30 gas) and that calculation's associated stack operations. Caching an array's struct avoids recalculating the array offsets into memory/calldata.

*Instances: 60*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-info Contains multiple accesses to state
 176 |  function claimFailedDeposit(
 177 |      address _depositSender,
 178 |      address _l1Token,
 179 |      bytes32 _l2TxHash,
 180 |      uint256 _l2BatchNumber,
 181 |      uint256 _l2MessageIndex,
 182 |      uint16 _l2TxNumberInBatch,
 183 |      bytes32[] calldata _merkleProof
 184 |  ) external nonReentrant {
     |      // @audit-issue Cache this value
 185 |      uint256 amount = depositAmount[_depositSender][_l1Token][_l2TxHash];
  :  |
     |      // @audit-issue Cache this value
 187 |      delete depositAmount[_depositSender][_l1Token][_l2TxHash];
  :  |
     |      // @audit-issue Cache this value
 185 |      uint256 amount = depositAmount[_depositSender][_l1Token][_l2TxHash];
  :  |
     |      // @audit-issue Cache this value
 187 |      delete depositAmount[_depositSender][_l1Token][_l2TxHash];
  :  |
     |      // @audit-issue Cache this value
 185 |      uint256 amount = depositAmount[_depositSender][_l1Token][_l2TxHash];
  :  |
     |      // @audit-issue Cache this value
 187 |      delete depositAmount[_depositSender][_l1Token][_l2TxHash];
```
GitHub: [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L185), [187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L187), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L185), [187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L187), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L185), [187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L187)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-info Contains multiple accesses to state
 116 |  function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
  :  |
     |              // @audit-issue Cache this value
 123 |              chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
  :  |
     |          // @audit-issue Cache this value
 133 |          chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;

     |  // @audit-info Contains multiple accesses to state
 182 |  function bridgehubDeposit(
 183 |      uint256 _chainId,
 184 |      address _prevMsgSender,
 185 |      uint256, // l2Value, needed for Weth deposits in the future
 186 |      bytes calldata _data
 187 |  ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
     |      // @audit-issue Cache this value
 188 |      require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
  :  |
     |              // @audit-issue Cache this value
 221 |              l2Contract: l2BridgeAddress[_chainId],

     |  // @audit-info Contains multiple accesses to state
 303 |  function _claimFailedDeposit(
 304 |      bool _checkedInLegacyBridge,
 305 |      uint256 _chainId,
 306 |      address _depositSender,
 307 |      address _l1Token,
 308 |      uint256 _amount,
 309 |      bytes32 _l2TxHash,
 310 |      uint256 _l2BatchNumber,
 311 |      uint256 _l2MessageIndex,
 312 |      uint16 _l2TxNumberInBatch,
 313 |      bytes32[] calldata _merkleProof
 314 |  ) internal nonReentrant {
  :  |
     |              // @audit-issue Cache this value
 340 |              bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
  :  |
     |              // @audit-issue Cache this value
 343 |              delete depositHappened[_chainId][_l2TxHash];
  :  |
     |              // @audit-issue Cache this value
 340 |              bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
  :  |
     |              // @audit-issue Cache this value
 343 |              delete depositHappened[_chainId][_l2TxHash];

     |  // @audit-info Contains multiple accesses to state
 554 |  function depositLegacyErc20Bridge(
 555 |      address _prevMsgSender,
 556 |      address _l2Receiver,
 557 |      address _l1Token,
 558 |      uint256 _amount,
 559 |      uint256 _l2TxGasLimit,
 560 |      uint256 _l2TxGasPerPubdataByte,
 561 |      address _refundRecipient
 562 |  ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
     |      // @audit-issue Cache this value
 563 |      require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
  :  |
     |              // @audit-issue Cache this value
 586 |              l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
```
GitHub: [123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L123), [133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133), [188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188), [221](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L221), [340](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L340), [343](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L343), [340](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L340), [343](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L343), [563](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563), [586](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L586)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-info Contains multiple accesses to state
 224 |  function _execute(Call[] calldata _calls) internal {
  :  |
     |          // @audit-issue Cache this value
     |          // @audit-issue Cache this value
     |          // @audit-issue Cache this value
 226 |          (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```
GitHub: [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-info Contains multiple accesses to state
 349 |  function _executeBatches(StoredBatchInfo[] calldata _batchesData) internal {
  :  |
     |          // @audit-issue Cache this value
 352 |          _executeOneBatch(_batchesData[i], i);
     |          // @audit-issue Cache this value
     |          // @audit-issue Cache this value
     |          // @audit-issue Cache this value
 353 |          emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

     |  // @audit-info Contains multiple accesses to state
 386 |  function _proveBatches(
 387 |      StoredBatchInfo calldata _prevBatch,
 388 |      StoredBatchInfo[] calldata _committedBatches,
 389 |      ProofInput calldata _proof
 390 |  ) internal {
  :  |
     |      // @audit-issue Cache this value
 402 |      require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");
  :  |
     |              // @audit-issue Cache this value
     |              // @audit-issue Cache this value
 408 |              _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
  :  |
     |          // @audit-issue Cache this value
 412 |          bytes32 currentBatchCommitment = _committedBatches[i].commitment;

     |  // @audit-info Contains multiple accesses to state
 625 |  function _verifyBlobInformation(
 626 |      bytes calldata _pubdataCommitments,
 627 |      bytes32[] memory _blobHashes
 628 |  ) internal view returns (bytes32[] memory blobCommitments) {
  :  |
     |              // @audit-issue Cache this value
 669 |              (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
     |                  // @audit-issue Cache this value
 670 |                  (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
  :  |
     |              // @audit-issue Cache this value
 669 |              (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
     |                  // @audit-issue Cache this value
 670 |                  (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
```
GitHub: [352](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L352), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353), [402](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L402), [408](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L408), [408](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L408), [412](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L412), [669](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L669), [670](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670), [669](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L669), [670](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-info Contains multiple accesses to state
 163 |  function isFacetFreezable(address _facet) external view returns (bool isFreezable) {
  :  |
     |      // @audit-issue Cache this value
 168 |      uint256 selectorsArrayLen = ds.facetToSelectors[_facet].selectors.length;
  :  |
     |          // @audit-issue Cache this value
 170 |          bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];

     |  // @audit-info Contains multiple accesses to state
 181 |  function isFunctionFreezable(bytes4 _selector) external view returns (bool) {
  :  |
     |      // @audit-issue Cache this value
 183 |      require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");
     |      // @audit-issue Cache this value
 184 |      return ds.selectorToFacet[_selector].isFreezable;
```
GitHub: [168](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L168), [170](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L170), [183](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183), [184](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L184)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

     |  // @audit-info Contains multiple accesses to state
  96 |  function diamondCut(DiamondCutData memory _diamondCut) internal {
  :  |
     |          // @audit-issue Cache this value
 102 |          Action action = facetCuts[i].action;
     |          // @audit-issue Cache this value
 103 |          address facet = facetCuts[i].facet;
     |          // @audit-issue Cache this value
 104 |          bool isFacetFreezable = facetCuts[i].isFreezable;
     |          // @audit-issue Cache this value
 105 |          bytes4[] memory selectors = facetCuts[i].selectors;

     |  // @audit-info Contains multiple accesses to state
 205 |  function _addOneFunction(address _facet, bytes4 _selector, bool _isSelectorFreezable) private {
  :  |
     |      // @audit-issue Cache this value
 208 |      uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16();
  :  |
     |          // @audit-issue Cache this value
 214 |          bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];
  :  |
     |      // @audit-issue Cache this value
 223 |      ds.facetToSelectors[_facet].selectors.push(_selector);

     |  // @audit-info Contains multiple accesses to state
 228 |  function _removeOneFunction(address _facet, bytes4 _selector) private {
  :  |
     |      // @audit-issue Cache this value
 232 |      uint256 selectorPosition = ds.selectorToFacet[_selector].selectorPosition;
  :  |
     |      // @audit-issue Cache this value
 247 |      delete ds.selectorToFacet[_selector];
  :  |
     |      // @audit-issue Cache this value
 233 |      uint256 lastSelectorPosition = ds.facetToSelectors[_facet].selectors.length - 1;
  :  |
     |          // @audit-issue Cache this value
 237 |          bytes4 lastSelector = ds.facetToSelectors[_facet].selectors[lastSelectorPosition];
  :  |
     |      // @audit-issue Cache this value
 244 |      ds.facetToSelectors[_facet].selectors.pop();
```
GitHub: [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L102), [103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L103), [104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L104), [105](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L105), [208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L208), [214](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L214), [223](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L223), [232](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L232), [247](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L247), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L233), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L237), [244](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L244)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

     |  // @audit-info Contains multiple accesses to state
  18 |  function calculateRoot(
  19 |      bytes32[] calldata _path,
  20 |      uint256 _index,
  21 |      bytes32 _itemHash
  22 |  ) internal pure returns (bytes32) {
  :  |
     |              // @audit-issue Cache this value
  31 |              ? _efficientHash(currentHash, _path[i])
     |              // @audit-issue Cache this value
  32 |              : _efficientHash(_path[i], currentHash);
```
GitHub: [31](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L31), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L32)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

     |  // @audit-info Contains multiple accesses to state
  72 |  function popFront(Queue storage _queue) internal returns (PriorityOperation memory priorityOperation) {
  :  |
     |      // @audit-issue Cache this value
  78 |      priorityOperation = _queue.data[head];
     |      // @audit-issue Cache this value
  79 |      delete _queue.data[head];
```
GitHub: [78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L78), [79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L79)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-info Contains multiple accesses to state
 110 |  function verifyCompressedStateDiffs(
 111 |      uint256 _numberOfStateDiffs,
 112 |      uint256 _enumerationIndexSize,
 113 |      bytes calldata _stateDiffs,
 114 |      bytes calldata _compressedStateDiffs
 115 |  ) external payable onlyCallFrom(address(L1_MESSENGER_CONTRACT)) returns (bytes32 stateDiffHash) {
  :  |
     |          // @audit-issue Cache this value
 143 |          uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
  :  |
     |          // @audit-issue Cache this value
 174 |          uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
```
GitHub: [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L143), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L174)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-info Contains multiple accesses to state
 238 |  function forceDeployOnAddresses(ForceDeployment[] calldata _deployments) external payable {
  :  |
     |          // @audit-issue Cache this value
 249 |          sumOfValues += _deployments[i].value;
  :  |
     |          // @audit-issue Cache this value
     |          // @audit-issue Cache this value
 254 |          this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
```
GitHub: [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L249), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L254), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L254)


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

     |  // @audit-info Contains multiple accesses to state
  34 |  function setImmutables(address _dest, ImmutableData[] calldata _immutables) external override {
  :  |
     |              // @audit-issue Cache this value
  39 |              uint256 index = _immutables[i].index;
     |              // @audit-issue Cache this value
  40 |              bytes32 value = _immutables[i].value;
```
GitHub: [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L39), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L40)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-info Contains multiple accesses to state
 194 |  function publishPubdataAndClearState(
 195 |      bytes calldata _totalL2ToL1PubdataAndStateDiffs
 196 |  ) external onlyCallFromBootloader {
  :  |
     |          // @audit-issue Cache this value
 280 |          uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
  :  |
     |      // @audit-issue Cache this value
 289 |      uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));
```
GitHub: [280](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L280), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L289)


## [G-09] Cache state variables accessed multiple times in the same function

The instances below point to the second+ access of a state variable within a function. Caching of a state variable replaces each Gwarmaccess (100 gas) with a much cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses.

*Instances: 90*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 176 |  function claimFailedDeposit(
 177 |      address _depositSender,
 178 |      address _l1Token,
 179 |      bytes32 _l2TxHash,
 180 |      uint256 _l2BatchNumber,
 181 |      uint256 _l2MessageIndex,
 182 |      uint16 _l2TxNumberInBatch,
 183 |      bytes32[] calldata _merkleProof
 184 |  ) external nonReentrant {
     |      // @audit-issue depositAmount read #1
 185 |      uint256 amount = depositAmount[_depositSender][_l1Token][_l2TxHash];
  :  |
     |      // @audit-issue depositAmount read #2
 187 |      delete depositAmount[_depositSender][_l1Token][_l2TxHash];
```
GitHub: [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L185), [187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L187)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 116 |  function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
  :  |
     |              // @audit-issue chainBalance read #1
 123 |              chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
  :  |
     |          // @audit-issue chainBalance read #2
 133 |          chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;

 182 |  function bridgehubDeposit(
 183 |      uint256 _chainId,
 184 |      address _prevMsgSender,
 185 |      uint256, // l2Value, needed for Weth deposits in the future
 186 |      bytes calldata _data
 187 |  ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
     |      // @audit-issue l2BridgeAddress read #1
 188 |      require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
  :  |
     |              // @audit-issue l2BridgeAddress read #2
 221 |              l2Contract: l2BridgeAddress[_chainId],

 303 |  function _claimFailedDeposit(
 304 |      bool _checkedInLegacyBridge,
 305 |      uint256 _chainId,
 306 |      address _depositSender,
 307 |      address _l1Token,
 308 |      uint256 _amount,
 309 |      bytes32 _l2TxHash,
 310 |      uint256 _l2BatchNumber,
 311 |      uint256 _l2MessageIndex,
 312 |      uint16 _l2TxNumberInBatch,
 313 |      bytes32[] calldata _merkleProof
 314 |  ) internal nonReentrant {
  :  |
     |              // @audit-issue depositHappened read #1
 340 |              bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
  :  |
     |              // @audit-issue depositHappened read #2
 343 |              delete depositHappened[_chainId][_l2TxHash];

 554 |  function depositLegacyErc20Bridge(
 555 |      address _prevMsgSender,
 556 |      address _l2Receiver,
 557 |      address _l1Token,
 558 |      uint256 _amount,
 559 |      uint256 _l2TxGasLimit,
 560 |      uint256 _l2TxGasPerPubdataByte,
 561 |      address _refundRecipient
 562 |  ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
     |      // @audit-issue l2BridgeAddress read #1
 563 |      require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
  :  |
     |              // @audit-issue l2BridgeAddress read #2
 586 |              l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
```
GitHub: [123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L123), [133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133), [188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188), [221](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L221), [340](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L340), [343](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L343), [563](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563), [586](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L586)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

  60 |  function acceptAdmin() external {
     |      // @audit-issue pendingAdmin read #1
  61 |      address currentPendingAdmin = pendingAdmin;
  :  |
     |      // @audit-issue pendingAdmin read #2
  66 |      delete pendingAdmin;
  :  |
     |      // @audit-issue pendingAdmin read #3
  69 |      emit NewAdmin(previousAdmin, pendingAdmin);

 114 |  function createNewChain(
 115 |      uint256 _chainId,
 116 |      address _stateTransitionManager,
 117 |      address _baseToken,
 118 |      uint256, //_salt
 119 |      address _admin,
 120 |      bytes calldata _initData
 121 |  ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
  :  |
     |      // @audit-issue sharedBridge read #1
 130 |      require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
  :  |
     |          // @audit-issue sharedBridge read #2
 140 |          address(sharedBridge),
```
GitHub: [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L61), [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L66), [69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130), [140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L140)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 121 |  function acceptAdmin() external {
     |      // @audit-issue pendingAdmin read #1
 122 |      address currentPendingAdmin = pendingAdmin;
  :  |
     |      // @audit-issue pendingAdmin read #2
 127 |      delete pendingAdmin;
  :  |
     |      // @audit-issue pendingAdmin read #3
 130 |      emit NewAdmin(previousAdmin, pendingAdmin);

 179 |  function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
  :  |
     |          // @audit-issue protocolVersion read #1
 194 |          nonce: protocolVersion,
  :  |
     |          // @audit-issue protocolVersion read #2
 218 |          newProtocolVersion: protocolVersion
  :  |
     |      // @audit-issue protocolVersion read #3
 229 |      emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
```
GitHub: [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L122), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L127), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L130), [194](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L194), [218](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L218), [229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L229)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

  32 |  function acceptAdmin() external {
     |      // @audit-issue s read #1
  33 |      address pendingAdmin = s.pendingAdmin;
  :  |
     |      // @audit-issue s read #2
  36 |      address previousAdmin = s.admin;
  :  |
     |      // @audit-issue s read #3
  38 |      delete s.pendingAdmin;

  79 |  function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {
     |      // @audit-issue s read #1
  80 |      uint128 oldNominator = s.baseTokenGasPriceMultiplierNominator;
     |      // @audit-issue s read #2
  81 |      uint128 oldDenominator = s.baseTokenGasPriceMultiplierDenominator;

 100 |  function upgradeChainFromVersion(
 101 |      uint256 _oldProtocolVersion,
 102 |      Diamond.DiamondCutData calldata _diamondCut
 103 |  ) external onlyAdminOrStateTransitionManager {
  :  |
     |          // @audit-issue s read #1
 106 |          cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
  :  |
     |          // @audit-issue s read #2
 111 |          s.protocolVersion == _oldProtocolVersion,
  :  |
     |          // @audit-issue s read #3
 117 |          s.protocolVersion > _oldProtocolVersion,
```
GitHub: [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L33), [36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L36), [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L38), [80](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L80), [81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L81), [106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L106), [111](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L111), [117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L117)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 215 |  function _commitBatches(
 216 |      StoredBatchInfo memory _lastCommittedBatchData,
 217 |      CommitBatchInfo[] calldata _newBatchesData
 218 |  ) internal {
  :  |
     |          // @audit-issue s read #1
     |          // @audit-issue s read #2
 227 |          IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
  :  |
     |      // @audit-issue s read #3
     |      // @audit-issue s read #4
 233 |      require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data
  :  |
     |      // @audit-issue s read #5
 235 |      bytes32 systemContractsUpgradeTxHash = s.l2SystemContractsUpgradeTxHash;
  :  |
     |      // @audit-issue s read #6
 237 |      if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {
  :  |
     |      // @audit-issue s read #7
 247 |      s.totalBatchesCommitted = s.totalBatchesCommitted + _newBatchesData.length;

 321 |  function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {
  :  |
     |      // @audit-issue s read #1
 323 |      require(currentBatchNumber == s.totalBatchesExecuted + _executedBatchIdx + 1, "k"); // Execute batches in order
  :  |
     |          // @audit-issue s read #2
 325 |          _hashStoredBatchInfo(_storedBatch) == s.storedBatchHashes[currentBatchNumber],

 349 |  function _executeBatches(StoredBatchInfo[] calldata _batchesData) internal {
  :  |
     |      // @audit-issue s read #1
 356 |      uint256 newTotalBatchesExecuted = s.totalBatchesExecuted + nBatches;
  :  |
     |      // @audit-issue s read #2
 358 |      require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.
  :  |
     |      // @audit-issue s read #3
 360 |      uint256 batchWhenUpgradeHappened = s.l2SystemContractsUpgradeBatchNumber;
  :  |
     |          // @audit-issue s read #4
 362 |          delete s.l2SystemContractsUpgradeTxHash;
     |          // @audit-issue s read #5
 363 |          delete s.l2SystemContractsUpgradeBatchNumber;

 386 |  function _proveBatches(
 387 |      StoredBatchInfo calldata _prevBatch,
 388 |      StoredBatchInfo[] calldata _committedBatches,
 389 |      ProofInput calldata _proof
 390 |  ) internal {
  :  |
     |      // @audit-issue s read #1
 392 |      uint256 currentTotalBatchesVerified = s.totalBatchesVerified;
  :  |
     |      // @audit-issue s read #2
 396 |      VerifierParams memory verifierParams = s.verifierParams;
  :  |
     |      // @audit-issue s read #3
 402 |      require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");
  :  |
     |              // @audit-issue s read #4
 408 |              _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
  :  |
     |      // @audit-issue s read #5
 421 |      require(currentTotalBatchesVerified <= s.totalBatchesCommitted, "q");
  :  |
     |      // @audit-issue s read #6
 436 |      emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

 481 |  function _revertBatches(uint256 _newLastBatch) internal {
     |      // @audit-issue s read #1
 482 |      require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch
     |      // @audit-issue s read #2
 483 |      require(_newLastBatch >= s.totalBatchesExecuted, "v2"); // Already executed batches cannot be reverted
  :  |
     |      // @audit-issue s read #3
 485 |      if (_newLastBatch < s.totalBatchesVerified) {
  :  |
     |      // @audit-issue s read #4
 492 |      if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) {
     |          // @audit-issue s read #5
 493 |          delete s.l2SystemContractsUpgradeBatchNumber;
  :  |
     |      // @audit-issue s read #6
     |      // @audit-issue s read #7
     |      // @audit-issue s read #8
 496 |      emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);

 525 |  function _batchMetaParameters() internal view returns (bytes memory) {
     |      // @audit-issue s read #1
 526 |      bytes32 l2DefaultAccountBytecodeHash = s.l2DefaultAccountBytecodeHash;
  :  |
     |              // @audit-issue s read #2
 529 |              s.zkPorterIsAvailable,
     |              // @audit-issue s read #3
 530 |              s.l2BootloaderBytecodeHash,
```
GitHub: [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L227), [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L227), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L233), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L233), [235](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L235), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L237), [247](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L247), [323](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L323), [325](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L325), [356](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L356), [358](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L358), [360](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L360), [362](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L362), [363](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L363), [392](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L392), [396](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L396), [402](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L402), [408](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L408), [421](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L421), [436](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436), [482](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L482), [483](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L483), [485](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L485), [492](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L492), [493](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L493), [496](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496), [496](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496), [496](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496), [526](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L526), [529](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L529), [530](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L530)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

  38 |  function transferEthToSharedBridge() external onlyBaseTokenBridge {
     |      // @audit-issue s read #1
  39 |      require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");
  :  |
     |      // @audit-issue s read #2
  42 |      address sharedBridgeAddress = s.baseTokenBridge;

 104 |  function _proveL2LogInclusion(
 105 |      uint256 _batchNumber,
 106 |      uint256 _index,
 107 |      L2Log memory _log,
 108 |      bytes32[] calldata _proof
 109 |  ) internal view returns (bool) {
     |      // @audit-issue s read #1
 110 |      require(_batchNumber <= s.totalBatchesExecuted, "xx");
  :  |
     |      // @audit-issue s read #2
 124 |      bytes32 actualRootHash = s.l2LogsRootHashes[_batchNumber];

 156 |  function _deriveL2GasPrice(uint256 _l1GasPrice, uint256 _gasPerPubdata) internal view returns (uint256) {
     |      // @audit-issue s read #1
 157 |      FeeParams memory feeParams = s.feeParams;
     |      // @audit-issue s read #2
 158 |      require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");
     |      // @audit-issue s read #3
 159 |      uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
     |          // @audit-issue s read #4
 160 |          s.baseTokenGasPriceMultiplierDenominator;

 178 |  function finalizeEthWithdrawal(
 179 |      uint256 _l2BatchNumber,
 180 |      uint256 _l2MessageIndex,
 181 |      uint16 _l2TxNumberInBatch,
 182 |      bytes calldata _message,
 183 |      bytes32[] calldata _merkleProof
 184 |  ) external nonReentrant {
     |      // @audit-issue s read #1
 185 |      require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");
     |      // @audit-issue s read #2
 186 |      IL1SharedBridge(s.baseTokenBridge).finalizeWithdrawal(

 197 |  function requestL2Transaction(
 198 |      address _contractL2,
 199 |      uint256 _l2Value,
 200 |      bytes calldata _calldata,
 201 |      uint256 _l2GasLimit,
 202 |      uint256 _l2GasPerPubdataByteLimit,
 203 |      bytes[] calldata _factoryDeps,
 204 |      address _refundRecipient
 205 |  ) external payable returns (bytes32 canonicalTxHash) {
     |      // @audit-issue s read #1
 206 |      require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");
  :  |
     |      // @audit-issue s read #2
 220 |      IL1SharedBridge(s.baseTokenBridge).bridgehubDepositBaseToken{value: msg.value}(
     |          // @audit-issue s read #3
 221 |          s.chainId,

 316 |  function _writePriorityOp(
 317 |      WritePriorityOpParams memory _priorityOpParams,
 318 |      bytes memory _calldata,
 319 |      bytes[] memory _factoryDeps
 320 |  ) internal returns (bytes32 canonicalTxHash) {
  :  |
     |          // @audit-issue s read #1
 328 |          s.priorityTxMaxGasLimit,
     |          // @audit-issue s read #2
 329 |          s.feeParams.priorityTxMaxPubdata
  :  |
     |      // @audit-issue s read #3
 334 |      s.priorityQueue.pushBack(
```
GitHub: [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39), [42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L42), [110](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L110), [124](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L124), [157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L157), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158), [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L159), [160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L160), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L185), [186](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L186), [206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L206), [220](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L220), [221](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L221), [328](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L328), [329](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L329), [334](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L334)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 180 |  function _setL2SystemContractUpgrade(
 181 |      L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
 182 |      bytes[] calldata _factoryDeps,
 183 |      uint256 _newProtocolVersion
 184 |  ) internal returns (bytes32) {
  :  |
     |          // @audit-issue s read #1
 197 |          s.priorityTxMaxGasLimit,
     |          // @audit-issue s read #2
 198 |          s.feeParams.priorityTxMaxPubdata

 236 |  function _setNewProtocolVersion(uint256 _newProtocolVersion) internal virtual {
     |      // @audit-issue s read #1
 237 |      uint256 previousProtocolVersion = s.protocolVersion;
  :  |
     |      // @audit-issue s read #2
 249 |      require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
  :  |
     |          // @audit-issue s read #3
 251 |          s.l2SystemContractsUpgradeBatchNumber == 0,
```
GitHub: [197](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L197), [198](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L198), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L237), [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L249), [251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L251)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

  20 |  function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
     |      // @audit-issue s read #1
  21 |      uint256 previousProtocolVersion = s.protocolVersion;
  :  |
     |      // @audit-issue s read #2
  33 |      require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
  :  |
     |          // @audit-issue s read #3
  35 |          s.l2SystemContractsUpgradeBatchNumber == 0,
```
GitHub: [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L21), [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33), [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L35)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

  94 |  function _processL2ToL1Log(L2ToL1Log memory _l2ToL1Log) internal returns (uint256 logIdInMerkleTree) {
  :  |
     |      // @audit-issue numberOfLogsToProcess read #1
 108 |      logIdInMerkleTree = numberOfLogsToProcess;
     |      // @audit-issue numberOfLogsToProcess read #2
 109 |      numberOfLogsToProcess++;
```
GitHub: [108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L108), [109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L109)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

 117 |  function getCurrentPubdataSpent() public view returns (uint256) {
  :  |
     |      // @audit-issue basePubdataSpent read #1
     |      // @audit-issue basePubdataSpent read #2
 119 |      return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;

 263 |  function _setVirtualBlock(
 264 |      uint128 _l2BlockNumber,
 265 |      uint128 _maxVirtualBlocksToCreate,
 266 |      uint128 _newTimestamp
 267 |  ) internal {
  :  |
     |      // @audit-issue currentVirtualL2BlockInfo read #1
 275 |      BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;
  :  |
     |      // @audit-issue currentVirtualL2BlockInfo read #2
 277 |      if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
```
GitHub: [119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L119), [119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L119), [275](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L275), [277](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L277)


## [G-10] Calculation results within a function can be cached to save gas

Cache the results of calculations within a function rather than repeating them.

*Instances: 2*

```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-info Duplicates of this operation were detected
 127 |  for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
  :  |
     |  // @audit-issue First seen at code/system-contracts/contracts/Compressor.sol:127
 159 |  for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
```
GitHub: [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L159)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-info Duplicates of this operation were detected
  56 |  require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
  :  |
     |  // @audit-issue First seen at code/contracts/zksync/contracts/bridge/L2SharedBridge.sol:56
  58 |  require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
```
GitHub: [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L58)


## [G-11] Consider changing some `public` variables to `private`/`internal`

Public state variables in Solidity automatically generate getter functions, increasing deployment costs.
                    
Examples of variables that probably don't need to be public - anybody who needs to inspect them can check the on-chain contract storage:

* Factories
* Controllers
* Governance
* Owner, roles, etc.



*Instances: 55*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  23 |  IL1SharedBridge public immutable override sharedBridge;

     |  // @audit-issue Reconsider whether this variable has to be public
  27 |  mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
  28 |      public isWithdrawalFinalized;

     |  // @audit-issue Reconsider whether this variable has to be public
  32 |  mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
  33 |      public depositAmount;

     |  // @audit-issue Reconsider whether this variable has to be public
  36 |  address public l2Bridge;

     |  // @audit-issue Reconsider whether this variable has to be public
  39 |  address public l2TokenBeacon;

     |  // @audit-issue Reconsider whether this variable has to be public
  42 |  bytes32 public l2TokenProxyBytecodeHash;
```
GitHub: [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L23), [27-28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27-L28), [32-33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L32-L33), [36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L36), [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L39), [42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L42)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  34 |  address public immutable override l1WethAddress;

     |  // @audit-issue Reconsider whether this variable has to be public
  37 |  IBridgehub public immutable override bridgehub;

     |  // @audit-issue Reconsider whether this variable has to be public
  40 |  IL1ERC20Bridge public immutable override legacyBridge;

     |  // @audit-issue Reconsider whether this variable has to be public
  48 |  mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;

     |  // @audit-issue Reconsider whether this variable has to be public
  52 |  mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
  53 |      public
  54 |      override depositHappened;

     |  // @audit-issue Reconsider whether this variable has to be public
  57 |  mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
  58 |      public isWithdrawalFinalized;
```
GitHub: [34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L34), [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L37), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L40), [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L48), [52-54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L52-L54), [57-58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57-L58)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  18 |  IL1SharedBridge public sharedBridge;

     |  // @audit-issue Reconsider whether this variable has to be public
  21 |  mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;

     |  // @audit-issue Reconsider whether this variable has to be public
  23 |  mapping(address _token => bool) public tokenIsRegistered;

     |  // @audit-issue Reconsider whether this variable has to be public
  26 |  mapping(uint256 _chainId => address) public stateTransitionManager;

     |  // @audit-issue Reconsider whether this variable has to be public
  29 |  mapping(uint256 _chainId => address) public baseToken;

     |  // @audit-issue Reconsider whether this variable has to be public
  32 |  address public admin;
```
GitHub: [18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L18), [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21), [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L23), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L26), [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L29), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L32)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  26 |  address public securityCouncil;

     |  // @audit-issue Reconsider whether this variable has to be public
  32 |  mapping(bytes32 operationId => uint256 executionTimestamp) public timestamps;

     |  // @audit-issue Reconsider whether this variable has to be public
  35 |  uint256 public minDelay;
```
GitHub: [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L26), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L32), [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L35)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  29 |  address public immutable bridgehub;

     |  // @audit-issue Reconsider whether this variable has to be public
  32 |  mapping(uint256 => address) public stateTransition;

     |  // @audit-issue Reconsider whether this variable has to be public
  35 |  bytes32 public storedBatchZero;

     |  // @audit-issue Reconsider whether this variable has to be public
  38 |  bytes32 public initialCutHash;

     |  // @audit-issue Reconsider whether this variable has to be public
  41 |  address public genesisUpgrade;

     |  // @audit-issue Reconsider whether this variable has to be public
  44 |  uint256 public protocolVersion;

     |  // @audit-issue Reconsider whether this variable has to be public
  47 |  address public validatorTimelock;

     |  // @audit-issue Reconsider whether this variable has to be public
  50 |  mapping(uint256 => bytes32) public upgradeCutHash;

     |  // @audit-issue Reconsider whether this variable has to be public
  53 |  address public admin;
```
GitHub: [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L29), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L32), [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L35), [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L38), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L41), [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L44), [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L47), [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L50), [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L53)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  26 |  string public constant override getName = "ValidatorTimelock";

     |  // @audit-issue Reconsider whether this variable has to be public
  44 |  IStateTransitionManager public stateTransitionManager;

     |  // @audit-issue Reconsider whether this variable has to be public
  50 |  mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;

     |  // @audit-issue Reconsider whether this variable has to be public
  53 |  uint32 public executionDelay;
```
GitHub: [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26), [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L44), [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50), [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L53)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  20 |  string public constant override getName = "AdminFacet";
```
GitHub: [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  27 |  string public constant override getName = "ExecutorFacet";
```
GitHub: [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  25 |  string public constant override getName = "GettersFacet";
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  35 |  string public constant override getName = "MailboxFacet";
```
GitHub: [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35)


```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  23 |  uint256 public override totalSupply;
```
GitHub: [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L23)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  26 |  uint256 public chainId;

     |  // @audit-issue Reconsider whether this variable has to be public
  30 |  address public origin;

     |  // @audit-issue Reconsider whether this variable has to be public
  34 |  uint256 public gasPrice;

     |  // @audit-issue Reconsider whether this variable has to be public
  37 |  uint256 public blockGasLimit = type(uint32).max;

     |  // @audit-issue Reconsider whether this variable has to be public
  41 |  address public coinbase = BOOTLOADER_FORMAL_ADDRESS;

     |  // @audit-issue Reconsider whether this variable has to be public
  44 |  uint256 public difficulty = 2.5e15;

     |  // @audit-issue Reconsider whether this variable has to be public
  48 |  uint256 public baseFee;

     |  // @audit-issue Reconsider whether this variable has to be public
  89 |  uint16 public txNumberInBlock;

     |  // @audit-issue Reconsider whether this variable has to be public
  92 |  uint256 public gasPerPubdataByte;
```
GitHub: [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L26), [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L30), [34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L34), [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L37), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L41), [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L44), [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L48), [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L89), [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L92)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  25 |  address public override l1Bridge;

     |  // @audit-issue Reconsider whether this variable has to be public
  29 |  UpgradeableBeacon public l2TokenBeacon;

     |  // @audit-issue Reconsider whether this variable has to be public
  35 |  mapping(address l2TokenAddress => address l1TokenAddress) public override l1TokenAddress;
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L25), [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L29), [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L35)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  34 |  address public override l2Bridge;

     |  // @audit-issue Reconsider whether this variable has to be public
  37 |  address public override l1Address;
```
GitHub: [34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L34), [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L37)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

     |  // @audit-issue Reconsider whether this variable has to be public
  25 |  address public override l2Bridge;

     |  // @audit-issue Reconsider whether this variable has to be public
  28 |  address public override l1Address;
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L25), [28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L28)


## [G-12] Consider merging sequential for loops

Merging multiple `for` loops within a function in Solidity can enhance efficiency and reduce gas costs, especially when they share a common iterating variable or perform related operations. By minimizing redundant iterations over the same data set, execution becomes more cost-effective. However, while merging can optimize gas usage and simplify logic, it may also increase code complexity. Therefore, careful balance between optimization and maintainability is essential, along with thorough testing to ensure the refactored code behaves as expected.

*Instances: 4*

```solidity
File: code/system-contracts/contracts/Compressor.sol

     |      // @audit-info Context
 110 |      function verifyCompressedStateDiffs(
 111 |          uint256 _numberOfStateDiffs,
 112 |          uint256 _enumerationIndexSize,
 113 |          bytes calldata _stateDiffs,
 114 |          bytes calldata _compressedStateDiffs
 115 |      ) external payable onlyCallFrom(address(L1_MESSENGER_CONTRACT)) returns (bytes32 stateDiffHash) {
  :  |
     |  // @audit-issue Duplicated loop control structure
 127 |          for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
 128 |              bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
 129 |              uint64 enumIndex = stateDiff.readUint64(84);
 130 |              if (enumIndex != 0) {
 131 |                  // It is a repeated write, so we skip it.
 132 |                  continue;
 133 |              }
 135 |              numInitialWritesProcessed++;
 137 |              bytes32 derivedKey = stateDiff.readBytes32(52);
 138 |              uint256 initValue = stateDiff.readUint256(92);
 139 |              uint256 finalValue = stateDiff.readUint256(124);
 140 |              require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");
 141 |              stateDiffPtr += 32;
 143 |              uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
 144 |              stateDiffPtr++;
 145 |              uint8 operation = metadata & OPERATION_BITMASK;
 146 |              uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
 147 |              _verifyValueCompression(
 148 |                  initValue,
 149 |                  finalValue,
 150 |                  operation,
 151 |                  _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
 152 |              );
 153 |              stateDiffPtr += len;
 154 |          }
  :  |
     |  // @audit-issue Duplicated loop control structure
 159 |          for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
 160 |              bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
 161 |              uint64 enumIndex = stateDiff.readUint64(84);
 162 |              if (enumIndex == 0) {
 163 |                  continue;
 164 |              }
 166 |              uint256 initValue = stateDiff.readUint256(92);
 167 |              uint256 finalValue = stateDiff.readUint256(124);
 168 |              uint256 compressedEnumIndex = _sliceToUint256(
 169 |                  _compressedStateDiffs[stateDiffPtr:stateDiffPtr + _enumerationIndexSize]
 170 |              );
 171 |              require(enumIndex == compressedEnumIndex, "rw: enum key mismatch");
 172 |              stateDiffPtr += _enumerationIndexSize;
 174 |              uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
 175 |              stateDiffPtr += 1;
 176 |              uint8 operation = metadata & OPERATION_BITMASK;
 177 |              uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
 178 |              _verifyValueCompression(
 179 |                  initValue,
 180 |                  finalValue,
 181 |                  operation,
 182 |                  _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
 183 |              );
 184 |              stateDiffPtr += len;
 185 |          }
```
GitHub: [127-154](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L127-L154), [159-185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L159-L185)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-info Context
 238 |  function forceDeployOnAddresses(ForceDeployment[] calldata _deployments) external payable {
  :  |
     |      // @audit-issue Duplicated loop control structure
 248 |      for (uint256 i = 0; i < deploymentsLength; ++i) {
 249 |          sumOfValues += _deployments[i].value;
 250 |      }
  :  |
     |      // @audit-issue Duplicated loop control structure
 253 |      for (uint256 i = 0; i < deploymentsLength; ++i) {
 254 |          this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
 255 |      }
```
GitHub: [248-250](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L248-L250), [253-255](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L253-L255)


## [G-13] Consider pre-calculating the address of `address(this)` to save gas

Instead of using `address(this)`, it is more gas-efficient to pre-calculate and use the hardcoded address. Foundry's `script.sol` and solmate's `LibRlp.sol` contracts can help achieve this.
Refrences:-[book.getfoundry](https://book.getfoundry.sh/reference/forge-std/compute-create-address)-[twitter](https://twitter.com/transmissions11/status/1518507047943245824).

*Instances: 23*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Pre-calculate & hardcode instead
  65 |  uint256 amount = IERC20(_token).balanceOf(address(this));
```
GitHub: [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Pre-calculate & hardcode instead
 118 |  uint256 balanceBefore = address(this).balance;

     |  // @audit-issue Pre-calculate & hardcode instead
 120 |  uint256 balanceAfter = address(this).balance;

     |  // @audit-issue Pre-calculate & hardcode instead
 127 |  uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

     |  // @audit-issue Pre-calculate & hardcode instead
 131 |  uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

     |  // @audit-issue Pre-calculate & hardcode instead
 174 |  uint256 balanceBefore = _token.balanceOf(address(this));

     |  // @audit-issue Pre-calculate & hardcode instead
 175 |  _token.safeTransferFrom(_from, address(this), _amount);

     |  // @audit-issue Pre-calculate & hardcode instead
 176 |  uint256 balanceAfter = _token.balanceOf(address(this));
```
GitHub: [118](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118), [120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127), [131](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L174), [175](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175), [176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Pre-calculate & hardcode instead
  59 |  require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
```
GitHub: [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L59)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Pre-calculate & hardcode instead
 267 |  bytes32(uint256(uint160(address(this)))),
```
GitHub: [267](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L267)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Pre-calculate & hardcode instead
  41 |  uint256 amount = address(this).balance;
```
GitHub: [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Pre-calculate & hardcode instead
  29 |  require(msg.sender == address(this), "Callable only by self");

     |  // @audit-issue Pre-calculate & hardcode instead
 333 |  BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo(address(this), _newAddress, value);
```
GitHub: [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L29), [333](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L333)


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

     |  // @audit-issue Pre-calculate & hardcode instead
  47 |  if (codeAddress != address(this)) {

     |  // @audit-issue Pre-calculate & hardcode instead
 100 |  require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

     |  // @audit-issue Pre-calculate & hardcode instead
 188 |  return recoveredAddress == address(this) && recoveredAddress != address(0);
```
GitHub: [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L47), [100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L100), [188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L188)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Pre-calculate & hardcode instead
 129 |  sender: address(this),
```
GitHub: [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L129)


```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

     |  // @audit-issue Pre-calculate & hardcode instead
  98 |  /// So the balance of `address(this)` is always bigger or equal to the `msg.value`!

     |  // @audit-issue Pre-calculate & hardcode instead
 106 |  balance[address(this)] -= amount;
```
GitHub: [98](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L98), [106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L106)


```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

     |  // @audit-issue Pre-calculate & hardcode instead
  60 |  require(to != address(this), "MsgValueSimulator calls itself");
```
GitHub: [60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L60)


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

     |  // @audit-issue Pre-calculate & hardcode instead
 377 |  uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);
```
GitHub: [377](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-issue Pre-calculate & hardcode instead
 153 |  L2ContractHelper.computeCreate2Address(address(this), salt, l2TokenProxyBytecodeHash, constructorInputHash);
```
GitHub: [153](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L153)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

     |  // @audit-issue Pre-calculate & hardcode instead
  33 |  address thisAddress = address(this);
```
GitHub: [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L33)


## [G-14] Consider using OpenZeppelin `EnumerateSet` in place of nested mappings

Nested mappings and multi-dimensional arrays in Solidity operate through a process of double hashing, wherein the original storage slot and the first key are concatenated and hashed, and then this hash is again concatenated with the second key and hashed. This process can be quite gas expensive due to the double-hashing operation and subsequent storage operation (sstore).

A possible optimization involves manually concatenating the keys followed by a single hash operation and an sstore. However, this technique introduces the risk of storage collision, especially when there are other nested hash maps in the contract that use the same key types. Because Solidity is unaware of the number and structure of nested hash maps in a contract, it follows a conservative approach in computing the storage slot to avoid possible collisions.

OpenZeppelin's EnumerableSet provides a potential solution to this problem. It creates a data structure that combines the benefits of set operations with the ability to enumerate stored elements, which is not natively available in Solidity. EnumerableSet handles the element uniqueness internally and can therefore provide a more gas-efficient and collision-resistant alternative to nested mappings or multi-dimensional arrays in certain scenarios.

*Instances: 10*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Consider replacing with OZ `EnumerateSet`
  27 |  mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
  28 |      public isWithdrawalFinalized;

     |  // @audit-issue Consider replacing with OZ `EnumerateSet`
  32 |  mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
  33 |      public depositAmount;

     |  // @audit-issue Consider replacing with OZ `EnumerateSet`
  51 |  mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;
```
GitHub: [27-28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27-L28), [32-33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L32-L33), [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L51)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Consider replacing with OZ `EnumerateSet`
  52 |  mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
  53 |      public
  54 |      override depositHappened;

     |  // @audit-issue Consider replacing with OZ `EnumerateSet`
  57 |  mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
  58 |      public isWithdrawalFinalized;

     |  // @audit-issue Consider replacing with OZ `EnumerateSet`
  65 |  mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;
```
GitHub: [52-54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L52-L54), [57-58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57-L58), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L65)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Consider replacing with OZ `EnumerateSet`
  50 |  mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
GitHub: [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

     |  // @audit-issue Consider replacing with OZ `EnumerateSet`
 114 |  mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;
```
GitHub: [114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L114)


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

     |  // @audit-issue Consider replacing with OZ `EnumerateSet`
  21 |  mapping(uint256 contractAddress => mapping(uint256 index => bytes32 value)) internal immutableDataStorage;
```
GitHub: [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L21)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-issue Consider replacing with OZ `EnumerateSet`
  41 |  mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;
```
GitHub: [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L41)


## [G-15] Constructors can be marked `payable`

Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided. A constructor can safely be marked as payable, since only the deployer would be able to pass funds, and the project itself would not pass any funds.

*Instances: 11*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Consider marking payable to save gas
  55 |  constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
```
GitHub: [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Consider marking payable to save gas
  90 |  constructor(
  91 |      address _l1WethAddress,
  92 |      IBridgehub _bridgehub,
  93 |      IL1ERC20Bridge _legacyBridge
  94 |  ) reentrancyGuardInitializer {
```
GitHub: [90-94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90-L94)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Consider marking payable to save gas
  38 |  constructor() reentrancyGuardInitializer {}
```
GitHub: [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Consider marking payable to save gas
  41 |  constructor(address _admin, address _securityCouncil, uint256 _minDelay) {
```
GitHub: [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L41)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Consider marking payable to save gas
  60 |  constructor(address _bridgehub) reentrancyGuardInitializer {
```
GitHub: [60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L60)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Consider marking payable to save gas
  55 |  constructor(address _initialOwner, uint32 _executionDelay) {
```
GitHub: [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

     |  // @audit-issue Consider marking payable to save gas
  19 |  constructor() reentrancyGuardInitializer {}
```
GitHub: [19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

     |  // @audit-issue Consider marking payable to save gas
  11 |  constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
```
GitHub: [11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-issue Consider marking payable to save gas
  41 |  constructor() {
```
GitHub: [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L41)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

     |  // @audit-issue Consider marking payable to save gas
  40 |  constructor() {
```
GitHub: [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L40)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

     |  // @audit-issue Consider marking payable to save gas
  31 |  constructor() {
```
GitHub: [31](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L31)


## [G-16] Declare variables outside loops to save gas

In some cases, it is possible to save gas by declaring variables outside a loop. Careful testing will be necessary to determine if these instances will save gas in this contracts typical usage scenarios.

*Instances: 52*

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-info Context
 225 |  for (uint256 i = 0; i < _calls.length; ++i) {
     |      // @audit-issue Measure gas with variable declared outside loop
 226 |      (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```
GitHub: [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-info Context
 185 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {
     |      // @audit-issue Measure gas with variable declared outside loop
 186 |      uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
 187 |          _newBatchesData[i].batchNumber
 188 |      );

     |  // @audit-info Context
 209 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {
     |      // @audit-issue Measure gas with variable declared outside loop
 210 |      uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
```
GitHub: [186-188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L186-L188), [210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L210)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-info Context
 142 |  for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
 144 |      (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
     |      // @audit-issue Measure gas with variable declared outside loop
 145 |      (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
     |      // @audit-issue Measure gas with variable declared outside loop
 146 |      (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);

     |  // @audit-info Context
 289 |  for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
 291 |      bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);

     |  // @audit-info Context
 311 |  for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {
     |      // @audit-issue Measure gas with variable declared outside loop
 312 |      PriorityOperation memory priorityOp = s.priorityQueue.popFront();

     |  // @audit-info Context
 405 |  for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
 412 |      bytes32 currentBatchCommitment = _committedBatches[i].commitment;

     |  // @audit-info Context
 636 |  for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {
     |      // @audit-issue Measure gas with variable declared outside loop
 637 |      bytes32 blobVersionedHash = _getBlobVersionedHash(versionedHashIndex);
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
 643 |      bytes32 openingPoint = bytes32(
 644 |          uint256(uint128(bytes16(_pubdataCommitments[i:i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET])))
 645 |      );
```
GitHub: [144](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L144), [145](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L145), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L146), [291](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L291), [312](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L312), [412](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L412), [637](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L637), [643-645](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L643-L645)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-info Context
 208 |  for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {
     |      // @audit-issue Measure gas with variable declared outside loop
 209 |      address facetAddr = ds.facets[i];
     |      // @audit-issue Measure gas with variable declared outside loop
 210 |      Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];
```
GitHub: [209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L209), [210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L210)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-info Context
 356 |  for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {
     |      // @audit-issue Measure gas with variable declared outside loop
 357 |      bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);
```
GitHub: [357](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L357)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

     |  // @audit-info Context
 101 |  for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {
     |      // @audit-issue Measure gas with variable declared outside loop
 102 |      Action action = facetCuts[i].action;
     |      // @audit-issue Measure gas with variable declared outside loop
 103 |      address facet = facetCuts[i].facet;
     |      // @audit-issue Measure gas with variable declared outside loop
 104 |      bool isFacetFreezable = facetCuts[i].isFreezable;
     |      // @audit-issue Measure gas with variable declared outside loop
 105 |      bytes4[] memory selectors = facetCuts[i].selectors;

     |  // @audit-info Context
 138 |  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
     |      // @audit-issue Measure gas with variable declared outside loop
 139 |      bytes4 selector = _selectors[i];
     |      // @audit-issue Measure gas with variable declared outside loop
 140 |      SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

     |  // @audit-info Context
 158 |  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
     |      // @audit-issue Measure gas with variable declared outside loop
 159 |      bytes4 selector = _selectors[i];
     |      // @audit-issue Measure gas with variable declared outside loop
 160 |      SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

     |  // @audit-info Context
 178 |  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
     |      // @audit-issue Measure gas with variable declared outside loop
 179 |      bytes4 selector = _selectors[i];
     |      // @audit-issue Measure gas with variable declared outside loop
 180 |      SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
```
GitHub: [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L102), [103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L103), [104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L104), [105](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L105), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L139), [140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L140), [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L159), [160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L160), [179](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L179), [180](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L180)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-info Context
  61 |  for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
     |      // @audit-issue Measure gas with variable declared outside loop
  62 |      uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
  65 |      uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);
     |      // @audit-issue Measure gas with variable declared outside loop
  66 |      uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

     |  // @audit-info Context
 127 |  for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
     |      // @audit-issue Measure gas with variable declared outside loop
 128 |      bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
     |      // @audit-issue Measure gas with variable declared outside loop
 129 |      uint64 enumIndex = stateDiff.readUint64(84);
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
 137 |      bytes32 derivedKey = stateDiff.readBytes32(52);
     |      // @audit-issue Measure gas with variable declared outside loop
 138 |      uint256 initValue = stateDiff.readUint256(92);
     |      // @audit-issue Measure gas with variable declared outside loop
 139 |      uint256 finalValue = stateDiff.readUint256(124);
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
 143 |      uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
 145 |      uint8 operation = metadata & OPERATION_BITMASK;
     |      // @audit-issue Measure gas with variable declared outside loop
 146 |      uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

     |  // @audit-info Context
 159 |  for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
     |      // @audit-issue Measure gas with variable declared outside loop
 160 |      bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
     |      // @audit-issue Measure gas with variable declared outside loop
 161 |      uint64 enumIndex = stateDiff.readUint64(84);
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
 166 |      uint256 initValue = stateDiff.readUint256(92);
     |      // @audit-issue Measure gas with variable declared outside loop
 167 |      uint256 finalValue = stateDiff.readUint256(124);
     |      // @audit-issue Measure gas with variable declared outside loop
 168 |      uint256 compressedEnumIndex = _sliceToUint256(
 169 |          _compressedStateDiffs[stateDiffPtr:stateDiffPtr + _enumerationIndexSize]
 170 |      );
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
 174 |      uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
 176 |      uint8 operation = metadata & OPERATION_BITMASK;
     |      // @audit-issue Measure gas with variable declared outside loop
 177 |      uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
```
GitHub: [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L62), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L65), [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L66), [128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L128), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L129), [137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L137), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L138), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L139), [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L143), [145](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L145), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L146), [160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L160), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L161), [166](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L166), [167](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L167), [168-170](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L168-L170), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L174), [176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L176), [177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L177)


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

     |  // @audit-info Context
  38 |  for (uint256 i = 0; i < immutablesLength; ++i) {
     |      // @audit-issue Measure gas with variable declared outside loop
  39 |      uint256 index = _immutables[i].index;
     |      // @audit-issue Measure gas with variable declared outside loop
  40 |      bytes32 value = _immutables[i].value;
```
GitHub: [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L39), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L40)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-info Context
 206 |  for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {
     |      // @audit-issue Measure gas with variable declared outside loop
 207 |      bytes32 hashedLog = EfficientCall.keccak(
 208 |          _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + L2_TO_L1_LOG_SERIALIZE_SIZE]
 209 |      );

     |  // @audit-info Context
 236 |  for (uint256 i = 0; i < numberOfMessages; ++i) {
     |      // @audit-issue Measure gas with variable declared outside loop
 237 |      uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
 239 |      bytes32 hashedMessage = EfficientCall.keccak(
 240 |          _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentMessageLength]
 241 |      );

     |  // @audit-info Context
 254 |  for (uint256 i = 0; i < numberOfBytecodes; ++i) {
     |      // @audit-issue Measure gas with variable declared outside loop
 255 |      uint32 currentBytecodeLength = uint32(
 256 |          bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])
 257 |      );

     |  // @audit-info Context
 222 |  while (nodesOnCurrentLevel > 1) {
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
 224 |      for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {
```
GitHub: [207-209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L207-L209), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L237), [239-241](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L239-L241), [255-257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L255-L257), [224](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L224)


```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

     |  // @audit-info Context
  36 |  for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
     |      // @audit-issue Measure gas with variable declared outside loop
  37 |      uint256 start = BLOB_SIZE_BYTES * i;
  :  |
     |      // @audit-issue Measure gas with variable declared outside loop
  45 |      bytes32 blobHash;
```
GitHub: [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L37), [45](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L45)


## [G-17] Default bool values are manually reset

Using .delete is better than resetting a Solidity variable to its default value manually because it frees up storage space on the Ethereum blockchain, resulting in gas cost savings.

*Instances: 3*

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Consider using delete
  97 |  stateTransitionManagerIsRegistered[_stateTransitionManager] = false;
```
GitHub: [97](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L97)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Consider using delete
  91 |  validators[_chainId][_validator] = false;
```
GitHub: [91](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L91)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue Consider using delete
 147 |  diamondStorage.isFrozen = false;
```
GitHub: [147](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L147)


## [G-18] Default int values are manually reset

Using .delete is better than resetting a Solidity variable to its default value manually because it frees up storage space on the Ethereum blockchain, resulting in gas cost savings.

*Instances: 3*

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Consider using delete
 276 |  baseTokenMsgValue = 0;
```
GitHub: [276](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L276)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Consider using delete
 330 |  numberOfLogsToProcess = 0;
```
GitHub: [330](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L330)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Consider using delete
 487 |  txNumberInBlock = 0;
```
GitHub: [487](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L487)


## [G-19] Detect zero value transfers to save gas

Detecting and aborting zero value transfers will save at least 100 gas.

*Instances: 5*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

  67 |  IERC20(_token).safeTransfer(address(sharedBridge), amount);

 162 |  _token.safeTransferFrom(_from, address(sharedBridge), _amount);
```
GitHub: [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67), [162](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L162)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 175 |  _token.safeTransferFrom(_from, address(this), _amount);

 452 |  IERC20(l1Token).safeTransfer(l1Receiver, amount);
```
GitHub: [175](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175), [452](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L452)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

  50 |  try IERC20(token).transferFrom(userAddress, thisAddress, amount) {} catch (bytes memory revertReason) {
```
GitHub: [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L50)


## [G-20] Divisions can be `unchecked` to save gas

The expression `type(int).min/(-1)` is the only case where division causes an overflow. Therefore, uncheck can be used to save gas in scenarios where it is certain that such an overflow will not occur.

*Instances: 14*

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 159 |  uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
 160 |      s.baseTokenGasPriceMultiplierDenominator;

     |  // @audit-issue Use unchecked to save gas, if possible
 168 |  batchOverheadBaseToken /
 169 |  uint256(feeParams.maxPubdataPerBatch);

     |  // @audit-issue Use unchecked to save gas, if possible
 171 |  uint256 l2GasPrice = feeParams.minimalL2GasPrice + batchOverheadBaseToken / uint256(feeParams.maxL2GasPerBatch);

     |  // @audit-issue Use unchecked to save gas, if possible
 172 |  uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata;
```
GitHub: [159-160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L159-L160), [168-169](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L168-L169), [171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L171), [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L172)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  25 |  uint256 bytecodeLenInWords = _bytecode.length / 32;
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  23 |  uint256 mapValue = _map.map[_index / 8];

     |  // @audit-issue Use unchecked to save gas, if possible
  43 |  uint256 mapIndex = _index / 8;
```
GitHub: [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L23), [43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L43)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  30 |  require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");
```
GitHub: [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L30)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  57 |  dictionary.length / 8 <= encodedData.length / 2,

     |  // @audit-issue Use unchecked to save gas, if possible
  57 |  dictionary.length / 8 <= encodedData.length / 2,
```
GitHub: [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L57), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L57)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  51 |  return KECCAK_ROUND_GAS_COST * (_length / KECCAK_ROUND_NUMBER_OF_BYTES + 1);

     |  // @audit-issue Use unchecked to save gas, if possible
  62 |  return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1);
```
GitHub: [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L51), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L62)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 180 |  deploymentNonce = _rawMinNonce / DEPLOY_NONCE_MULTIPLIER;
```
GitHub: [180](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L180)


```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  86 |  uint256 lengthInWords = _bytecode.length / 32;
```
GitHub: [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L86)


## [G-21] Don’t compare boolean expressions to boolean literals

For cases of: `if (<x> == true)`, use `if (<x>)` instead
For cases of: `if (<x> == false)`, use `if (!<x>)` instead.

*Instances: 3*

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Replace literal binary comparison with unary expression
  68 |  require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
```
GitHub: [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Replace literal binary comparison with unary expression
  21 |  * parameters `senderAddress == this`, `marker == true`, `key == msg.sender`, `value == keccak256(message)`.
```
GitHub: [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L21)


```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

     |  // @audit-issue Replace literal binary comparison with unary expression
  14 |  * parameters `senderAddress == this`, `isService == true`, `key == msg.sender`, `value == keccak256(message)`.
```
GitHub: [14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L14)


## [G-22] Duplicated `require()`/`revert()` checks should be refactored to a modifier or function to save deployment gas

This will cost more runtime gas, but will reduce deployment gas when the function is (optionally called via a modifier) called more than once as is the case for the examples below. Most projects do not make this trade-off, but it's available nonetheless.

*Instances: 17*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
 143 |  require(amount == _amount, "3T"); // The token has non-standard transfer logic

File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
     |      // @audit-issue First seen at code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol:143
 161 |      require(amount == _amount, "3T"); // The token has non-standard transfer logic
```
GitHub: [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L161)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
  46 |  require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
     |  // @audit-issue First seen at code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol:46
  72 |  require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");
```
GitHub: [72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L72)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
  62 |  require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
     |  // @audit-issue First seen at code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol:62
 123 |  require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights
```
GitHub: [123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L123)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
 195 |  require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
  :  |
     |  // @audit-issue First seen at code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol:195
 217 |  require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
```
GitHub: [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L217)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
  70 |  require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");

File: code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol
     |  // @audit-issue First seen at code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol:70
  23 |  require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");
```
GitHub: [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol#L23)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
  72 |  require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol
     |  // @audit-issue First seen at code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol:72
  52 |  require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");
```
GitHub: [52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L52)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
 242 |  require(
 243 |      _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
 244 |      "Too big protocol version difference"
 245 |  );

File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol
     |  // @audit-issue First seen at code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol:242
  27 |  require(
  28 |      _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
  29 |      "Too big protocol version difference"
  30 |  );
```
GitHub: [27-30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L27-L30)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
 249 |  require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol
     |  // @audit-issue First seen at code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol:249
  33 |  require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
```
GitHub: [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
 250 |  require(
 251 |      s.l2SystemContractsUpgradeBatchNumber == 0,
 252 |      "The batch number of the previous upgrade has not been cleaned"
 253 |  );

File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol
     |  // @audit-issue First seen at code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol:250
  34 |  require(
  35 |      s.l2SystemContractsUpgradeBatchNumber == 0,
  36 |      "The batch number of the previous upgrade has not been cleaned"
  37 |  );
```
GitHub: [34-37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L34-L37)


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
  26 |  require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

File: code/system-contracts/contracts/ImmutableSimulator.sol
     |  // @audit-issue First seen at code/system-contracts/contracts/AccountCodeStorage.sol:26
  35 |  require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
GitHub: [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L35)


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
  92 |  require(vInt == 27 || vInt == 28, "Invalid v value");
  :  |
     |  // @audit-issue First seen at code/system-contracts/contracts/BootloaderUtilities.sol:92
 191 |  require(vInt == 27 || vInt == 28, "Invalid v value");
  :  |
     |  // @audit-issue First seen at code/system-contracts/contracts/BootloaderUtilities.sol:92
 286 |  require(vInt == 27 || vInt == 28, "Invalid v value");
```
GitHub: [191](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L191), [286](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L286)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
  23 |  require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");

File: code/system-contracts/contracts/libraries/TransactionHelper.sol
     |  // @audit-issue First seen at code/contracts/zksync/contracts/TestnetPaymaster.sol:23
 363 |  require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");
```
GitHub: [363](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L363)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
  66 |  revert("Unsupported paymaster flow");

File: code/system-contracts/contracts/libraries/TransactionHelper.sol
     |  // @audit-issue First seen at code/contracts/zksync/contracts/TestnetPaymaster.sol:66
 388 |  revert("Unsupported paymaster flow");
```
GitHub: [388](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L388)


```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
  28 |  require(_x <= type(uint32).max, "Overflow");

File: code/system-contracts/contracts/libraries/Utils.sol
     |  // @audit-issue First seen at code/contracts/zksync/contracts/SystemContractsCaller.sol:28
  27 |  require(_x <= type(uint32).max, "Overflow");
```
GitHub: [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L27)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
  56 |  require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
  :  |
     |  // @audit-issue First seen at code/contracts/zksync/contracts/bridge/L2SharedBridge.sol:56
  58 |  require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
```
GitHub: [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L58)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

     |  // @audit-info Duplicates of this require()/revert() were detected
  84 |  require(success, "Failed withdrawal");
  :  |
     |  // @audit-issue First seen at code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol:84
 109 |  require(success, "Failed withdrawal");
```
GitHub: [109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L109)


## [G-23] Emitting constants wastes gas

Every event parameter costs `Glogdata` (**8 gas**) per byte. You can avoid this extra cost, in cases where you're emitting a constant, by creating a new version of the event which doesn't have the parameter (and have users look to the contract's variables for its value instead). Alternatively, in the case of boolean constants, two events can be created - one representing the `true` case and one representing the `false` case.

*Instances: 6*

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

  68 |  emit NewPendingAdmin(currentPendingAdmin, address(0));
```
GitHub: [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

  47 |  emit ChangeSecurityCouncil(address(0), _securityCouncil);

  50 |  emit ChangeMinDelay(0, _minDelay);
```
GitHub: [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L47), [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L50)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 129 |  emit NewPendingAdmin(currentPendingAdmin, address(0));
```
GitHub: [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L129)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

  40 |  emit NewPendingAdmin(pendingAdmin, address(0));
```
GitHub: [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

  61 |  emit Initialize(name_, symbol_, 18);
```
GitHub: [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L61)


## [G-24] Enable IR-based code generation

By using `--via-ir` or `{"viaIR": true}`, the compiler is able to use more advanced [multi-function optimizations](https://docs.soliditylang.org/en/v0.8.17/ir-breaking-changes.html#solidity-ir-based-codegen-changes), for extra gas savings.

> 🔴 IR-based code generation was not observed to be enabled in the configuration.


*Instances: 71*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  pragma solidity 0.8.20;
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: Apache-2.0
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/governance/IGovernance.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/IGovernance.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: UNLICENSED
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/common/Config.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  pragma solidity 0.8.20;
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/common/L2ContractAddresses.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/common/Messaging.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: Apache-2.0
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/Verifier.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/Verifier.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_4844.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  pragma solidity 0.8.20;
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_4844.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  pragma solidity 0.8.20;
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/common/Dependencies.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Dependencies.sol#L1)


```solidity
File: code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: UNLICENSED
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L1)


```solidity
File: code/system-contracts/contracts/Constants.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Constants.sol#L1)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L1)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L1)


```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L1)


```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L1)


```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L1)


```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L1)


```solidity
File: code/contracts/zksync/contracts/interfaces/IPaymaster.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L1)


```solidity
File: code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L1)


```solidity
File: code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: Apache-2.0
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L1)


```solidity
File: code/contracts/zksync/contracts/ForceDeployUpgrader.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT OR Apache-2.0
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L1)


```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L1)


```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L1)


```solidity
File: code/contracts/zksync/contracts/Dependencies.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/Dependencies.sol#L1)


```solidity
File: code/contracts/zksync/contracts/Config.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  pragma solidity 0.8.20;
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/Config.sol#L1)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L1)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

     |  // @audit-issue Enable viaIR for this file
   1 |  // SPDX-License-Identifier: MIT
```
GitHub: [1](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L1)


## [G-25] Events should be emitted outside of loops

Emitting an event has an overhead of **375 gas**, which will be incurred on every iteration of the loop. It is cheaper to `emit` only [once](https://github.com/ethereum/EIPs/blob/adad5968fd6de29902174e0cb51c8fc3dceb9ab5/EIPS/eip-1155.md?plain=1#L68) after the loop has finished.

*Instances: 3*

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-info Contains emits
 257 |  for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
  :  |
     |      // @audit-issue Save gas by emitting this outside the loop
 261 |      emit BlockCommit(
 262 |          _lastCommittedBatchData.batchNumber,
 263 |          _lastCommittedBatchData.batchHash,
 264 |          _lastCommittedBatchData.commitment
 265 |      );

     |  // @audit-info Contains emits
 289 |  for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
  :  |
     |      // @audit-issue Save gas by emitting this outside the loop
 299 |      emit BlockCommit(
 300 |          _lastCommittedBatchData.batchNumber,
 301 |          _lastCommittedBatchData.batchHash,
 302 |          _lastCommittedBatchData.commitment
 303 |      );

     |  // @audit-info Contains emits
 351 |  for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
  :  |
     |      // @audit-issue Save gas by emitting this outside the loop
 353 |      emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
```
GitHub: [261-265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261-L265), [299-303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L299-L303), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353)


## [G-26] Function names can be optimized to save gas

Function that are `public`/`external` and `public` state variable names can be optimized to save gas.

Method IDs that have two leading zero bytes can save **128 gas** each during deployment, and renaming functions to have lower method IDs will save **22 gas** per call, per sorted position shifted. [Reference](https://blog.emn178.cc/en/post/solidity-gas-optimization-function-name/).

You can use the [Function Name Optimizer Tool](https://emn178.github.io/solidity-optimize-name/) to find new function names.

*Instances: 37*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x8129fc1c: initialize()
     |  // 0xbc187757: tranferTokenToSharedBridge()
     |  // 0xf5f15168: l2TokenAddress()
     |  // 0x933999fb: deposit()
     |  // 0xe8b99b1b: deposit()
     |  // 0x19fa7f62: claimFailedDeposit()
     |  // 0x11a2ccc1: finalizeWithdrawal()
  19 |  contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {
```
GitHub: [19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L19)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0xcd6dc687: initialize()
     |  // 0xc846f6df: transferFundsFromLegacy()
     |  // 0xc2aaf9c4: receiveEth()
     |  // 0xf280efbe: initializeChainGovernance()
     |  // 0x2c4f2a58: bridgehubDepositBaseToken()
     |  // 0xca408c23: bridgehubDeposit()
     |  // 0x8eb7db57: bridgehubConfirmL2Transaction()
     |  // 0xc0991525: claimFailedDeposit()
     |  // 0xc87325f1: finalizeWithdrawal()
     |  // 0x9e6ea417: depositLegacyErc20Bridge()
     |  // 0x7ab08472: finalizeWithdrawalLegacyErc20Bridge()
     |  // 0x8fbb3711: claimFailedDepositLegacyErc20Bridge()
  30 |  contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {
```
GitHub: [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L30)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0xc4d66de8: initialize()
     |  // 0x4dd18bf5: setPendingAdmin()
     |  // 0x0e18b681: acceptAdmin()
     |  // 0xc2570620: getStateTransition()
     |  // 0x74044673: addStateTransitionManager()
     |  // 0xf5ba4232: removeStateTransitionManager()
     |  // 0xd48bfca7: addToken()
     |  // 0xd0bf6fd4: setSharedBridge()
     |  // 0x3f58f5b5: createNewChain()
     |  // 0x99c16d1a: proveL2MessageInclusion()
     |  // 0xe6d9923b: proveL2LogInclusion()
     |  // 0xb292f5f1: proveL1ToL2TransactionStatus()
     |  // 0x71623274: l2TransactionBaseCost()
     |  // 0xd52471c1: requestL2TransactionDirect()
     |  // 0x24fd57fb: requestL2TransactionTwoBridges()
  16 |  contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
```
GitHub: [16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L16)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x31d50750: isOperation()
     |  // 0x584b153e: isOperationPending()
     |  // 0x13bc9f20: isOperationReady()
     |  // 0x2ab0f529: isOperationDone()
     |  // 0x7958004c: getOperationState()
     |  // 0x2c431917: scheduleTransparent()
     |  // 0x6d1d8363: scheduleShadow()
     |  // 0xc4d252f5: cancel()
     |  // 0x74da756b: execute()
     |  // 0x95218ecd: executeInstant()
     |  // 0xc126e860: hashOperation()
     |  // 0x64d62353: updateDelay()
     |  // 0xdbfe3e96: updateSecurityCouncil()
  20 |  contract Governance is IGovernance, Ownable2Step {
```
GitHub: [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L20)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x301e7765: getChainAdmin()
     |  // 0xd9f0e1d6: initialize()
     |  // 0x4dd18bf5: setPendingAdmin()
     |  // 0x0e18b681: acceptAdmin()
     |  // 0x7fb67816: setValidatorTimelock()
     |  // 0x2e3311f8: setInitialCutHash()
     |  // 0x6190f4d8: setNewVersionUpgrade()
     |  // 0x98461504: setUpgradeDiamondCut()
     |  // 0xaccdd16c: freezeChain()
     |  // 0x51d218f7: unfreezeChain()
     |  // 0x53ce2061: revertBatches()
     |  // 0x03208e03: registerAlreadyDeployedStateTransition()
     |  // 0x9366518b: createNewChain()
  27 |  contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {
```
GitHub: [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L27)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x09e14277: setStateTransitionManager()
     |  // 0x4b561753: addValidator()
     |  // 0x6a0cd1f5: removeValidator()
     |  // 0xf34d1868: setExecutionDelay()
     |  // 0xb993549e: getCommittedBatchTimestamp()
     |  // 0x701f58c5: commitBatches()
     |  // 0x6edd4f12: commitBatchesSharedBridge()
     |  // 0x97c09d34: revertBatches()
     |  // 0x0f23da43: revertBatchesSharedBridge()
     |  // 0x7f61885c: proveBatches()
     |  // 0xc37533bb: proveBatchesSharedBridge()
     |  // 0xc3d93e7c: executeBatches()
     |  // 0x6f497ac6: executeBatchesSharedBridge()
  22 |  contract ValidatorTimelock is IExecutor, Ownable2Step {
```
GitHub: [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L22)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0xe4441b98: initialize()
  17 |  contract DiamondInit is ZkSyncStateTransitionBase, IDiamondInit {
```
GitHub: [17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L17)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x4dd18bf5: setPendingAdmin()
     |  // 0x0e18b681: acceptAdmin()
     |  // 0x4623c91d: setValidator()
     |  // 0x1cc5d103: setPorterAvailability()
     |  // 0xbe6f11cf: setPriorityTxMaxGasLimit()
     |  // 0x64bf8d66: changeFeeParams()
     |  // 0x235d9eb5: setTokenMultiplier()
     |  // 0x87c905b7: setValidiumMode()
     |  // 0xfc57565f: upgradeChainFromVersion()
     |  // 0xa9f6d941: executeUpgrade()
     |  // 0x27ae4c16: freezeDiamond()
     |  // 0x17338945: unfreezeDiamond()
  18 |  contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {
```
GitHub: [18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L18)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x701f58c5: commitBatches()
     |  // 0x6edd4f12: commitBatchesSharedBridge()
     |  // 0x6f497ac6: executeBatchesSharedBridge()
     |  // 0xc3d93e7c: executeBatches()
     |  // 0x7f61885c: proveBatches()
     |  // 0xc37533bb: proveBatchesSharedBridge()
     |  // 0x97c09d34: revertBatches()
     |  // 0x0f23da43: revertBatchesSharedBridge()
  22 |  contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {
```
GitHub: [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L22)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x46657fe9: getVerifier()
     |  // 0x6e9960c3: getAdmin()
     |  // 0xd0468156: getPendingAdmin()
     |  // 0x3591c1a0: getBridgehub()
     |  // 0x5518c73b: getStateTransitionManager()
     |  // 0x98acd7a6: getBaseToken()
     |  // 0x086a56f8: getBaseTokenBridge()
     |  // 0xea6c029c: baseTokenGasPriceMultiplierNominator()
     |  // 0x1de72e34: baseTokenGasPriceMultiplierDenominator()
     |  // 0xdb1f0bf9: getTotalBatchesCommitted()
     |  // 0xef3f0bae: getTotalBatchesVerified()
     |  // 0xb8c2f66f: getTotalBatchesExecuted()
     |  // 0xa1954fc5: getTotalPriorityTxs()
     |  // 0x79823c9a: getFirstUnprocessedPriorityTx()
     |  // 0x631f4bac: getPriorityQueueSize()
     |  // 0x56142d7a: priorityQueueFrontOperation()
     |  // 0xfacd743b: isValidator()
     |  // 0x9cd939e4: l2LogsRootHash()
     |  // 0xb22dd78e: storedBatchHash()
     |  // 0xd86970d8: getL2BootloaderBytecodeHash()
     |  // 0xfd791f3c: getL2DefaultAccountBytecodeHash()
     |  // 0x18e3a941: getVerifierParams()
     |  // 0x33ce93fe: getProtocolVersion()
     |  // 0x7b30c8da: getL2SystemContractsUpgradeTxHash()
     |  // 0xe5355c75: getL2SystemContractsUpgradeBatchNumber()
     |  // 0x29b98c67: isDiamondStorageFrozen()
     |  // 0xc3bbd2d7: isFacetFreezable()
     |  // 0x0ec6b0b7: getPriorityTxMaxGasLimit()
     |  // 0xe81e0ba1: isFunctionFreezable()
     |  // 0xbd7c5412: isEthWithdrawalFinalized()
     |  // 0x06d49e5b: getPubdataPricingMode()
     |  // 0x7a0ed627: facets()
     |  // 0xadfca15e: facetFunctionSelectors()
     |  // 0x52ef6b2c: facetAddresses()
     |  // 0xcdffacc6: facetAddress()
     |  // 0xfe26699e: getTotalBlocksCommitted()
     |  // 0xaf6a2dcd: getTotalBlocksVerified()
     |  // 0x39607382: getTotalBlocksExecuted()
     |  // 0x74f4d30d: storedBlockHash()
     |  // 0x9d1b5a81: getL2SystemContractsUpgradeBlockNumber()
  20 |  contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {
```
GitHub: [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L20)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0xc924de35: transferEthToSharedBridge()
     |  // 0x12f43dab: bridgehubRequestL2Transaction()
     |  // 0xe4948f43: proveL2MessageInclusion()
     |  // 0x263b7f8e: proveL2LogInclusion()
     |  // 0x042901c7: proveL1ToL2TransactionStatus()
     |  // 0xb473318e: l2TransactionBaseCost()
     |  // 0x6c0960f9: finalizeEthWithdrawal()
     |  // 0xeb672419: requestL2Transaction()
  30 |  contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {
```
GitHub: [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L30)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x08284e57: upgrade()
  44 |  abstract contract BaseZkSyncUpgrade is ZkSyncStateTransitionBase {
```
GitHub: [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L44)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x08284e57: upgrade()
  17 |  abstract contract BaseZkSyncUpgradeGenesis is BaseZkSyncUpgrade {
```
GitHub: [17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L17)


```solidity
File: code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x08284e57: upgrade()
  10 |  contract DefaultUpgrade is BaseZkSyncUpgrade {
```
GitHub: [10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L10)


```solidity
File: code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x08284e57: upgrade()
  11 |  contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {
```
GitHub: [11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L11)


```solidity
File: code/contracts/ethereum/contracts/state-transition/Verifier.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x9e8945d2: verificationKeyHash()
     |  // 0x87d9d023: verify()
  20 |  contract Verifier is IVerifier {
```
GitHub: [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/Verifier.sol#L20)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_4844.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x08284e57: upgrade()
  12 |  contract Upgrade_4844 is BaseZkSyncUpgrade {
```
GitHub: [12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_4844.sol#L12)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x08284e57: upgrade()
  13 |  contract Upgrade_v1_4_1 is BaseZkSyncUpgrade {
```
GitHub: [13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol#L13)


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x4f1e1be0: storeAccountConstructingCodeHash()
     |  // 0x0d4651aa: storeAccountConstructedCodeHash()
     |  // 0xc2e4ff97: markAccountCodeHashAsConstructed()
     |  // 0x4de2e468: getRawCodeHash()
     |  // 0xe03fe177: getCodeHash()
     |  // 0x1806aa18: getCodeSize()
  22 |  contract AccountCodeStorage is IAccountCodeStorage {
```
GitHub: [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L22)


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0xebe4a3d7: getTransactionHashes()
  16 |  contract BootloaderUtilities is IBootloaderUtilities {
```
GitHub: [16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L16)


```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0xc987336c: upgrade()
  14 |  contract ComplexUpgrader is IComplexUpgrader {
```
GitHub: [14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L14)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0xf5e69a47: publishCompressedBytecode()
     |  // 0x6006d8b5: verifyCompressedStateDiffs()
  22 |  contract Compressor is ICompressor, ISystemContract {
```
GitHub: [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L22)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x7b510fe8: getAccountInfo()
     |  // 0xbb0fd610: extendedAccountVersion()
     |  // 0x57180981: updateAccountVersion()
     |  // 0xec8067c7: updateNonceOrdering()
     |  // 0x84da1fb4: getNewAddressCreate2()
     |  // 0x187598a5: getNewAddressCreate()
     |  // 0x3cda3351: create2()
     |  // 0x9c4d535b: create()
     |  // 0x5d382700: create2Account()
     |  // 0xecf95b8a: createAccount()
     |  // 0xf3385fb6: forceDeployOnAddress()
     |  // 0xe9f18c17: forceDeployOnAddresses()
  23 |  contract ContractDeployer is IContractDeployer, ISystemContract {
```
GitHub: [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L23)


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x202bcce7: validateTransaction()
     |  // 0xdf9c1589: executeTransaction()
     |  // 0xeeb8cb09: executeTransactionFromOutside()
     |  // 0xe2f318e3: payForTransaction()
     |  // 0xa28c1aee: prepareForPaymaster()
  19 |  contract DefaultAccount is IAccount {
```
GitHub: [19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L19)


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x310ab089: getImmutable()
     |  // 0xad7e232e: setImmutables()
  18 |  contract ImmutableSimulator is IImmutableSimulator {
```
GitHub: [18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L18)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0xe516761e: markFactoryDeps()
     |  // 0x79c4f929: markBytecodeAsPublished()
     |  // 0x4c6314f0: getMarker()
  18 |  contract KnownCodesStorage is IKnownCodesStorage, ISystemContract {
```
GitHub: [18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L18)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x56079ac8: sendL2ToL1Log()
     |  // 0x62f84b24: sendToL1()
     |  // 0x39b34c6e: requestBytecodeL1Publication()
     |  // 0x628b636e: publishPubdataAndClearState()
  25 |  contract L1Messenger is IL1Messenger, ISystemContract {
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L25)


```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x579952fc: transferFromTo()
     |  // 0x9cc7f708: balanceOf()
     |  // 0x40c10f19: mint()
     |  // 0x51cff8d9: withdraw()
     |  // 0x84bc3eb0: withdrawWithMessage()
     |  // 0x06fdde03: name()
     |  // 0x95d89b41: symbol()
     |  // 0x313ce567: decimals()
  18 |  contract L2BaseToken is IBaseToken, ISystemContract {
```
GitHub: [18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L18)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x896909dc: getMinNonce()
     |  // 0x5aa9b6b5: getRawNonce()
     |  // 0x38a78092: increaseMinNonce()
     |  // 0x155fd27a: setValueUnderNonce()
     |  // 0x55d35d18: getValueUnderNonce()
     |  // 0xe1239cd8: incrementMinNonceIfEquals()
     |  // 0xfb1a9a57: getDeploymentNonce()
     |  // 0x306395c6: incrementDeploymentNonce()
     |  // 0xcab7e8eb: isNonceUsed()
     |  // 0x6ee1dc20: validateNonceUsage()
  27 |  contract NonceHolder is INonceHolder, ISystemContract {
```
GitHub: [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L27)


```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x2555d2c1: chunkAndPublishPubdata()
  16 |  contract PubdataChunkPublisher is IPubdataChunkPublisher, ISystemContract {
```
GitHub: [16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L16)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0xef0e2ff4: setChainId()
     |  // 0xa851ae78: setTxOrigin()
     |  // 0xbf1fe420: setGasPrice()
     |  // 0xa225efcb: setPubdataInfo()
     |  // 0xc0d5b949: getCurrentPubdataSpent()
     |  // 0x4be99e1d: getCurrentPubdataCost()
     |  // 0x80b41246: getBlockHashEVM()
     |  // 0xddeaa8e6: getBatchHash()
     |  // 0xd0f2c663: getBatchNumberAndTimestamp()
     |  // 0x8e8acf87: getL2BlockNumberAndTimestamp()
     |  // 0x42cbb15c: getBlockNumber()
     |  // 0x796b89b9: getBlockTimestamp()
     |  // 0x06bed036: setL2Block()
     |  // 0x06e7517b: appendTransactionToCurrentL2Block()
     |  // 0x7c9bd1f3: publishTimestampDataToL1()
     |  // 0x02fa5779: setNewBatch()
     |  // 0x29f172ad: unsafeOverrideBatch()
     |  // 0x30e5ccbd: incrementTxNumberInBatch()
     |  // 0x3635f3e6: resetTxNumberInBatch()
     |  // 0xa0803ef7: currentBlockInfo()
     |  // 0xd4a4ca0d: getBlockNumberAndTimestamp()
     |  // 0x85df51fd: blockHash()
  17 |  contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract {
```
GitHub: [17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L17)


```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x41a8596c: gasBoundCall()
  15 |  contract GasBoundCaller {
```
GitHub: [15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L15)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0xa31ee5b0: initialize()
     |  // 0xcfe7af7c: finalizeDeposit()
     |  // 0xd9caed12: withdraw()
     |  // 0xf5f15168: l2TokenAddress()
  23 |  contract L2SharedBridge is IL2SharedBridge, Initializable {
```
GitHub: [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L23)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x95f11a40: bridgeInitialize()
     |  // 0xb71bcf90: reinitializeToken()
     |  // 0x8c2a993e: bridgeMint()
     |  // 0x74f4f547: bridgeBurn()
     |  // 0x06fdde03: name()
     |  // 0x95d89b41: symbol()
     |  // 0x313ce567: decimals()
     |  // 0x95ce3e93: decodeString()
     |  // 0x7ba8be34: decodeUint8()
  15 |  contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {
```
GitHub: [15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L15)


```solidity
File: code/contracts/zksync/contracts/ForceDeployUpgrader.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0xb5a85e9d: forceDeploy()
  10 |  contract ForceDeployUpgrader {
```
GitHub: [10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L10)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x038a24bc: validateAndPayForPaymasterTransaction()
     |  // 0x817b17f0: postTransaction()
  13 |  contract TestnetPaymaster is IPaymaster {
```
GitHub: [13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L13)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

     |  // @audit-issue Can be optimized to two leading zeros:
     |  // 0x0c56efe9: initializeV2()
     |  // 0x8c2a993e: bridgeMint()
     |  // 0x74f4f547: bridgeBurn()
     |  // 0xd0e30db0: deposit()
     |  // 0x2e1a7d4d: withdraw()
     |  // 0xb760faf9: depositTo()
     |  // 0x205c2878: withdrawTo()
  23 |  contract L2WrappedBaseToken is ERC20PermitUpgradeable, IL2WrappedBaseToken, IL2StandardToken {
```
GitHub: [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L23)


## [G-27] Function result should be cached

The instances below show multiple calls to a single function within the same function.

*Instances: 8*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-info Contains multiple external contract reads
 160 |  function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
     |      // @audit-issue Cache this value
 161 |      uint256 balanceBefore = _token.balanceOf(address(sharedBridge));
  :  |
     |      // @audit-issue Cache this value
 163 |      uint256 balanceAfter = _token.balanceOf(address(sharedBridge));
```
GitHub: [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L161), [163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L163)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-info Contains multiple external contract reads
 116 |  function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
  :  |
     |          // @audit-issue Cache this value
 127 |          uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
  :  |
     |          // @audit-issue Cache this value
 131 |          uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

     |  // @audit-info Contains multiple external contract reads
 173 |  function _depositFunds(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
     |      // @audit-issue Cache this value
 174 |      uint256 balanceBefore = _token.balanceOf(address(this));
  :  |
     |      // @audit-issue Cache this value
 176 |      uint256 balanceAfter = _token.balanceOf(address(this));
```
GitHub: [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127), [131](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L174), [176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176)


```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

     |  // @audit-info Contains multiple external contract reads
  35 |  function gasBoundCall(address _to, uint256 _maxTotalGas, bytes calldata _data) external payable {
  :  |
     |      // @audit-issue Cache this value
  51 |      uint256 pubdataPublishedBefore = REAL_SYSTEM_CONTEXT_CONTRACT.getCurrentPubdataSpent();
  :  |
     |      // @audit-issue Cache this value
  59 |      uint256 pubdataPublishedAfter = REAL_SYSTEM_CONTEXT_CONTRACT.getCurrentPubdataSpent();
```
GitHub: [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L51), [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L59)


## [G-28] Functions guaranteed to revert when called by normal users can be marked `payable`

If a function modifier such as `onlyOwner` is used, the function will revert if a normal user tries to pay the function. Marking the function as `payable` will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided. The extra opcodes avoided are 
            `CALLVALUE`(2), `DUP1`(3), `ISZERO`(3), `PUSH2`(3), `JUMPI`(10), `PUSH1`(3), `DUP1`(3), `REVERT`(0), `JUMPDEST`(1), `POP`(2), which costs an average of about **21 gas per call** to the function, in addition to the extra deployment cost.

*Instances: 90*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Consider marking payable to save gas
 116 |  function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 142 |  function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 232 |  function bridgehubConfirmL2Transaction(
 233 |      uint256 _chainId,
 234 |      bytes32 _txDataHash,
 235 |      bytes32 _txHash
 236 |  ) external override onlyBridgehub {

     |  // @audit-issue Consider marking payable to save gas
 615 |  function finalizeWithdrawalLegacyErc20Bridge(
 616 |      uint256 _l2BatchNumber,
 617 |      uint256 _l2MessageIndex,
 618 |      uint16 _l2TxNumberInBatch,
 619 |      bytes calldata _message,
 620 |      bytes32[] calldata _merkleProof
 621 |  ) external override onlyLegacyBridge returns (address l1Receiver, address l1Token, uint256 amount) {

     |  // @audit-issue Consider marking payable to save gas
 644 |  function claimFailedDepositLegacyErc20Bridge(
 645 |      address _depositSender,
 646 |      address _l1Token,
 647 |      uint256 _amount,
 648 |      bytes32 _l2TxHash,
 649 |      uint256 _l2BatchNumber,
 650 |      uint256 _l2MessageIndex,
 651 |      uint16 _l2TxNumberInBatch,
 652 |      bytes32[] calldata _merkleProof
 653 |  ) external override onlyLegacyBridge {
```
GitHub: [116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L116), [142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L142), [232-236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L232-L236), [615-621](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L615-L621), [644-653](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L644-L653)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Consider marking payable to save gas
  51 |  function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

     |  // @audit-issue Consider marking payable to save gas
  82 |  function addStateTransitionManager(address _stateTransitionManager) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
  92 |  function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 101 |  function addToken(address _token) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 108 |  function setSharedBridge(address _sharedBridge) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 114 |  function createNewChain(
 115 |      uint256 _chainId,
 116 |      address _stateTransitionManager,
 117 |      address _baseToken,
 118 |      uint256, //_salt
 119 |      address _admin,
 120 |      bytes calldata _initData
 121 |  ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
```
GitHub: [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L51), [82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L82), [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L92), [101](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L101), [108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108), [114-121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114-L121)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Consider marking payable to save gas
 129 |  function scheduleTransparent(Operation calldata _operation, uint256 _delay) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 142 |  function scheduleShadow(bytes32 _id, uint256 _delay) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 154 |  function cancel(bytes32 _id) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 249 |  function updateDelay(uint256 _newDelay) external onlySelf {

     |  // @audit-issue Consider marking payable to save gas
 256 |  function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
```
GitHub: [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L129), [142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L142), [154](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L154), [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L249), [256](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L256)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Consider marking payable to save gas
 112 |  function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

     |  // @audit-issue Consider marking payable to save gas
 134 |  function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {

     |  // @audit-issue Consider marking payable to save gas
 139 |  function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 144 |  function setNewVersionUpgrade(
 145 |      Diamond.DiamondCutData calldata _cutData,
 146 |      uint256 _oldProtocolVersion,
 147 |      uint256 _newProtocolVersion
 148 |  ) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 154 |  function setUpgradeDiamondCut(
 155 |      Diamond.DiamondCutData calldata _cutData,
 156 |      uint256 _oldProtocolVersion
 157 |  ) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 162 |  function freezeChain(uint256 _chainId) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 167 |  function unfreezeChain(uint256 _chainId) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 172 |  function revertBatches(uint256 _chainId, uint256 _newLastBatch) external onlyOwnerOrAdmin {

     |  // @audit-issue Consider marking payable to save gas
 232 |  function registerAlreadyDeployedStateTransition(
 233 |      uint256 _chainId,
 234 |      address _stateTransitionContract
 235 |  ) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 241 |  function createNewChain(
 242 |      uint256 _chainId,
 243 |      address _baseToken,
 244 |      address _sharedBridge,
 245 |      address _admin,
 246 |      bytes calldata _diamondCut
 247 |  ) external onlyBridgehub {
```
GitHub: [112](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L112), [134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L134), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L139), [144-148](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L144-L148), [154-157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L154-L157), [162](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L162), [167](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L167), [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L172), [232-235](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L232-L235), [241-247](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L241-L247)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Consider marking payable to save gas
  73 |  function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
  78 |  function addValidator(uint256 _chainId, address _newValidator) external onlyChainAdmin(_chainId) {

     |  // @audit-issue Consider marking payable to save gas
  87 |  function removeValidator(uint256 _chainId, address _validator) external onlyChainAdmin(_chainId) {

     |  // @audit-issue Consider marking payable to save gas
  96 |  function setExecutionDelay(uint32 _executionDelay) external onlyOwner {

     |  // @audit-issue Consider marking payable to save gas
 108 |  function commitBatches(
 109 |      StoredBatchInfo calldata,
 110 |      CommitBatchInfo[] calldata _newBatchesData
 111 |  ) external onlyValidator(ERA_CHAIN_ID) {

     |  // @audit-issue Consider marking payable to save gas
 126 |  function commitBatchesSharedBridge(
 127 |      uint256 _chainId,
 128 |      StoredBatchInfo calldata,
 129 |      CommitBatchInfo[] calldata _newBatchesData
 130 |  ) external onlyValidator(_chainId) {

     |  // @audit-issue Consider marking payable to save gas
 146 |  function revertBatches(uint256) external onlyValidator(ERA_CHAIN_ID) {

     |  // @audit-issue Consider marking payable to save gas
 153 |  function revertBatchesSharedBridge(uint256 _chainId, uint256) external onlyValidator(_chainId) {

     |  // @audit-issue Consider marking payable to save gas
 160 |  function proveBatches(
 161 |      StoredBatchInfo calldata,
 162 |      StoredBatchInfo[] calldata,
 163 |      ProofInput calldata
 164 |  ) external onlyValidator(ERA_CHAIN_ID) {

     |  // @audit-issue Consider marking payable to save gas
 171 |  function proveBatchesSharedBridge(
 172 |      uint256 _chainId,
 173 |      StoredBatchInfo calldata,
 174 |      StoredBatchInfo[] calldata,
 175 |      ProofInput calldata
 176 |  ) external onlyValidator(_chainId) {

     |  // @audit-issue Consider marking payable to save gas
 182 |  function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {

     |  // @audit-issue Consider marking payable to save gas
 203 |  function executeBatchesSharedBridge(
 204 |      uint256 _chainId,
 205 |      StoredBatchInfo[] calldata _newBatchesData
 206 |  ) external onlyValidator(_chainId) {
```
GitHub: [73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L73), [78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L78), [87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L87), [96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96), [108-111](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L108-L111), [126-130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L126-L130), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L146), [153](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L153), [160-164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L160-L164), [171-176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L171-L176), [182](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L182), [203-206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L203-L206)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue Consider marking payable to save gas
  23 |  function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {

     |  // @audit-issue Consider marking payable to save gas
  45 |  function setValidator(address _validator, bool _active) external onlyStateTransitionManager {

     |  // @audit-issue Consider marking payable to save gas
  51 |  function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {

     |  // @audit-issue Consider marking payable to save gas
  58 |  function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager {

     |  // @audit-issue Consider marking payable to save gas
  67 |  function changeFeeParams(FeeParams calldata _newFeeParams) external onlyAdminOrStateTransitionManager {

     |  // @audit-issue Consider marking payable to save gas
  79 |  function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {

     |  // @audit-issue Consider marking payable to save gas
  89 |  function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {

     |  // @audit-issue Consider marking payable to save gas
 100 |  function upgradeChainFromVersion(
 101 |      uint256 _oldProtocolVersion,
 102 |      Diamond.DiamondCutData calldata _diamondCut
 103 |  ) external onlyAdminOrStateTransitionManager {

     |  // @audit-issue Consider marking payable to save gas
 123 |  function executeUpgrade(Diamond.DiamondCutData calldata _diamondCut) external onlyStateTransitionManager {

     |  // @audit-issue Consider marking payable to save gas
 133 |  function freezeDiamond() external onlyAdminOrStateTransitionManager {

     |  // @audit-issue Consider marking payable to save gas
 143 |  function unfreezeDiamond() external onlyAdminOrStateTransitionManager {
```
GitHub: [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L23), [45](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L45), [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L51), [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L58), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L67), [79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79), [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L89), [100-103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L100-L103), [123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L123), [133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L133), [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L143)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Consider marking payable to save gas
 199 |  function commitBatches(
 200 |      StoredBatchInfo memory _lastCommittedBatchData,
 201 |      CommitBatchInfo[] calldata _newBatchesData
 202 |  ) external nonReentrant onlyValidator {

     |  // @audit-issue Consider marking payable to save gas
 207 |  function commitBatchesSharedBridge(
 208 |      uint256, // _chainId
 209 |      StoredBatchInfo memory _lastCommittedBatchData,
 210 |      CommitBatchInfo[] calldata _newBatchesData
 211 |  ) external nonReentrant onlyValidator {

     |  // @audit-issue Consider marking payable to save gas
 337 |  function executeBatchesSharedBridge(
 338 |      uint256,
 339 |      StoredBatchInfo[] calldata _batchesData
 340 |  ) external nonReentrant onlyValidator {

     |  // @audit-issue Consider marking payable to save gas
 345 |  function executeBatches(StoredBatchInfo[] calldata _batchesData) external nonReentrant onlyValidator {

     |  // @audit-issue Consider marking payable to save gas
 368 |  function proveBatches(
 369 |      StoredBatchInfo calldata _prevBatch,
 370 |      StoredBatchInfo[] calldata _committedBatches,
 371 |      ProofInput calldata _proof
 372 |  ) external nonReentrant onlyValidator {

     |  // @audit-issue Consider marking payable to save gas
 377 |  function proveBatchesSharedBridge(
 378 |      uint256, // _chainId
 379 |      StoredBatchInfo calldata _prevBatch,
 380 |      StoredBatchInfo[] calldata _committedBatches,
 381 |      ProofInput calldata _proof
 382 |  ) external nonReentrant onlyValidator {

     |  // @audit-issue Consider marking payable to save gas
 472 |  function revertBatches(uint256 _newLastBatch) external nonReentrant onlyValidatorOrStateTransitionManager {

     |  // @audit-issue Consider marking payable to save gas
 477 |  function revertBatchesSharedBridge(uint256, uint256 _newLastBatch) external nonReentrant onlyValidator {
```
GitHub: [199-202](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L199-L202), [207-211](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L207-L211), [337-340](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L337-L340), [345](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L345), [368-372](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L368-L372), [377-382](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L377-L382), [472](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L472), [477](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L477)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Consider marking payable to save gas
  38 |  function transferEthToSharedBridge() external onlyBaseTokenBridge {
```
GitHub: [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L38)


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

     |  // @audit-issue Consider marking payable to save gas
  35 |  function storeAccountConstructingCodeHash(address _address, bytes32 _hash) external override onlyDeployer {

     |  // @audit-issue Consider marking payable to save gas
  46 |  function storeAccountConstructedCodeHash(address _address, bytes32 _hash) external override onlyDeployer {

     |  // @audit-issue Consider marking payable to save gas
  54 |  function markAccountCodeHashAsConstructed(address _address) external override onlyDeployer {
```
GitHub: [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L35), [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L46), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L54)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Consider marking payable to save gas
  65 |  function updateAccountVersion(AccountAbstractionVersion _version) external onlySystemCall {

     |  // @audit-issue Consider marking payable to save gas
  74 |  function updateNonceOrdering(AccountNonceOrdering _nonceOrdering) external onlySystemCall {
```
GitHub: [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L65), [74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L74)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

     |  // @audit-issue Consider marking payable to save gas
  27 |  function markFactoryDeps(bool _shouldSendToL1, bytes32[] calldata _hashes) external onlyCallFromBootloader {

     |  // @audit-issue Consider marking payable to save gas
  39 |  function markBytecodeAsPublished(bytes32 _bytecodeHash) external onlyCompressor {
```
GitHub: [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L27), [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L39)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Consider marking payable to save gas
  70 |  function sendL2ToL1Log(
  71 |      bool _isService,
  72 |      bytes32 _key,
  73 |      bytes32 _value
  74 |  ) external onlyCallFromSystemContract returns (uint256 logIdInMerkleTree) {

     |  // @audit-issue Consider marking payable to save gas
 161 |  function requestBytecodeL1Publication(
 162 |      bytes32 _bytecodeHash
 163 |  ) external override onlyCallFrom(address(KNOWN_CODE_STORAGE_CONTRACT)) {

     |  // @audit-issue Consider marking payable to save gas
 194 |  function publishPubdataAndClearState(
 195 |      bytes calldata _totalL2ToL1PubdataAndStateDiffs
 196 |  ) external onlyCallFromBootloader {
```
GitHub: [70-74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L70-L74), [161-163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L161-L163), [194-196](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L194-L196)


```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

     |  // @audit-issue Consider marking payable to save gas
  64 |  function mint(address _account, uint256 _amount) external override onlyCallFromBootloader {
```
GitHub: [64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L64)


```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

     |  // @audit-issue Consider marking payable to save gas
  47 |  fallback(bytes calldata _data) external onlySystemCall returns (bytes memory) {
```
GitHub: [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L47)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-issue Consider marking payable to save gas
  65 |  function increaseMinNonce(uint256 _value) public onlySystemCall returns (uint256 oldMinNonce) {

     |  // @audit-issue Consider marking payable to save gas
  82 |  function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall {

     |  // @audit-issue Consider marking payable to save gas
 110 |  function incrementMinNonceIfEquals(uint256 _expectedNonce) external onlySystemCall {
```
GitHub: [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L65), [82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L82), [110](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L110)


```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

     |  // @audit-issue Consider marking payable to save gas
  21 |  function chunkAndPublishPubdata(bytes calldata _pubdata) external onlyCallFrom(address(L1_MESSENGER_CONTRACT)) {
```
GitHub: [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L21)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Consider marking payable to save gas
  84 |  function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {

     |  // @audit-issue Consider marking payable to save gas
  99 |  function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {

     |  // @audit-issue Consider marking payable to save gas
 105 |  function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {

     |  // @audit-issue Consider marking payable to save gas
 112 |  function setPubdataInfo(uint256 _gasPerPubdataByte, uint256 _basePubdataSpent) external onlyCallFromBootloader {

     |  // @audit-issue Consider marking payable to save gas
 341 |  function setL2Block(
 342 |      uint128 _l2BlockNumber,
 343 |      uint128 _l2BlockTimestamp,
 344 |      bytes32 _expectedPrevL2BlockHash,
 345 |      bool _isFirstInBatch,
 346 |      uint128 _maxVirtualBlocksToCreate
 347 |  ) external onlyCallFromBootloader {

     |  // @audit-issue Consider marking payable to save gas
 402 |  function appendTransactionToCurrentL2Block(bytes32 _txHash) external onlyCallFromBootloader {

     |  // @audit-issue Consider marking payable to save gas
 408 |  function publishTimestampDataToL1() external onlyCallFromBootloader {

     |  // @audit-issue Consider marking payable to save gas
 444 |  function setNewBatch(
 445 |      bytes32 _prevBatchHash,
 446 |      uint128 _newTimestamp,
 447 |      uint128 _expectedNewNumber,
 448 |      uint256 _baseFee
 449 |  ) external onlyCallFromBootloader {

     |  // @audit-issue Consider marking payable to save gas
 471 |  function unsafeOverrideBatch(
 472 |      uint256 _newTimestamp,
 473 |      uint256 _number,
 474 |      uint256 _baseFee
 475 |  ) external onlyCallFromBootloader {

     |  // @audit-issue Consider marking payable to save gas
 482 |  function incrementTxNumberInBatch() external onlyCallFromBootloader {

     |  // @audit-issue Consider marking payable to save gas
 486 |  function resetTxNumberInBatch() external onlyCallFromBootloader {
```
GitHub: [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L84), [99](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L99), [105](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L105), [112](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L112), [341-347](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L341-L347), [402](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L402), [408](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L408), [444-449](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L444-L449), [471-475](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L471-L475), [482](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L482), [486](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L486)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

     |  // @audit-issue Consider marking payable to save gas
 111 |  function reinitializeToken(
 112 |      ERC20Getters calldata _availableGetters,
 113 |      string memory _newName,
 114 |      string memory _newSymbol,
 115 |      uint8 _version
 116 |  ) external onlyNextVersion(_version) reinitializer(_version) {

     |  // @audit-issue Consider marking payable to save gas
 145 |  function bridgeMint(address _to, uint256 _amount) external override onlyBridge {

     |  // @audit-issue Consider marking payable to save gas
 154 |  function bridgeBurn(address _from, uint256 _amount) external override onlyBridge {
```
GitHub: [111-116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L111-L116), [145](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L145), [154](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L154)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

     |  // @audit-issue Consider marking payable to save gas
  72 |  function bridgeMint(address _to, uint256 _amount) external override onlyBridge {

     |  // @audit-issue Consider marking payable to save gas
  80 |  function bridgeBurn(address _from, uint256 _amount) external override onlyBridge {
```
GitHub: [72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L72), [80](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L80)


## [G-29] Inline `internal` functions that are only called once

Saves 20-40 gas per instance. See https://blog.soliditylang.org/2021/03/02/saving-gas-with-simple-inliner/ for more details.

*Instances: 83*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Inline this function, it's only used once
 160 |  function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```
GitHub: [160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Inline this function, it's only used once
 254 |  function _getERC20Getters(address _token) internal view returns (bytes memory) {

     |  // @audit-issue Inline this function, it's only used once
 458 |  function _checkWithdrawal(
 459 |      uint256 _chainId,
 460 |      MessageParams memory _messageParams,
 461 |      bytes calldata _message,
 462 |      bytes32[] calldata _merkleProof
 463 |  ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {

     |  // @audit-issue Inline this function, it's only used once
 487 |  function _parseL2WithdrawalMessage(
 488 |      uint256 _chainId,
 489 |      bytes memory _l2ToL1message
 490 |  ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
```
GitHub: [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L254), [458-463](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L458-L463), [487-490](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L487-L490)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Inline this function, it's only used once
 179 |  function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
```
GitHub: [179](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L179)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Inline this function, it's only used once
 103 |  function _verifyBatchTimestamp(
 104 |      uint256 _packedBatchAndL2BlockTimestamp,
 105 |      uint256 _expectedBatchTimestamp,
 106 |      uint256 _previousBatchTimestamp
 107 |  ) internal view {

     |  // @audit-issue Inline this function, it's only used once
 130 |  function _processL2Logs(
 131 |      CommitBatchInfo calldata _newBatch,
 132 |      bytes32 _expectedSystemContractUpgradeTxHash
 133 |  ) internal pure returns (LogProcessingOutput memory logOutput) {

     |  // @audit-issue Inline this function, it's only used once
 253 |  function _commitBatchesWithoutSystemContractsUpgrade(
 254 |      StoredBatchInfo memory _lastCommittedBatchData,
 255 |      CommitBatchInfo[] calldata _newBatchesData
 256 |  ) internal {

     |  // @audit-issue Inline this function, it's only used once
 273 |  function _commitBatchesWithSystemContractsUpgrade(
 274 |      StoredBatchInfo memory _lastCommittedBatchData,
 275 |      CommitBatchInfo[] calldata _newBatchesData,
 276 |      bytes32 _systemContractUpgradeTxHash
 277 |  ) internal {

     |  // @audit-issue Inline this function, it's only used once
 308 |  function _collectOperationsFromPriorityQueue(uint256 _nPriorityOps) internal returns (bytes32 concatHash) {

     |  // @audit-issue Inline this function, it's only used once
 321 |  function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {

     |  // @audit-issue Inline this function, it's only used once
 453 |  function _getBatchProofPublicInput(
 454 |      bytes32 _prevBatchCommitment,
 455 |      bytes32 _currentBatchCommitment,
 456 |      VerifierParams memory _verifierParams
 457 |  ) internal pure returns (uint256) {

     |  // @audit-issue Inline this function, it's only used once
 500 |  function _createBatchCommitment(
 501 |      CommitBatchInfo calldata _newBatchData,
 502 |      bytes32 _stateDiffHash,
 503 |      bytes32[] memory _blobCommitments,
 504 |      bytes32[] memory _blobHashes
 505 |  ) internal view returns (bytes32) {

     |  // @audit-issue Inline this function, it's only used once
 515 |  function _batchPassThroughData(CommitBatchInfo calldata _batch) internal pure returns (bytes memory) {

     |  // @audit-issue Inline this function, it's only used once
 525 |  function _batchMetaParameters() internal view returns (bytes memory) {

     |  // @audit-issue Inline this function, it's only used once
 537 |  function _batchAuxiliaryOutput(
 538 |      CommitBatchInfo calldata _batch,
 539 |      bytes32 _stateDiffHash,
 540 |      bytes32[] memory _blobCommitments,
 541 |      bytes32[] memory _blobHashes
 542 |  ) internal pure returns (bytes memory) {

     |  // @audit-issue Inline this function, it's only used once
 561 |  function _encodeBlobAuxilaryOutput(
 562 |      bytes32[] memory _blobCommitments,
 563 |      bytes32[] memory _blobHashes
 564 |  ) internal pure returns (bytes32[] memory blobAuxOutputWords) {

     |  // @audit-issue Inline this function, it's only used once
 592 |  function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

     |  // @audit-issue Inline this function, it's only used once
 597 |  function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {

     |  // @audit-issue Inline this function, it's only used once
 605 |  function _pointEvaluationPrecompile(
 606 |      bytes32 _versionedHash,
 607 |      bytes32 _openingPoint,
 608 |      bytes calldata _openingValueCommitmentProof
 609 |  ) internal view {

     |  // @audit-issue Inline this function, it's only used once
 625 |  function _verifyBlobInformation(
 626 |      bytes calldata _pubdataCommitments,
 627 |      bytes32[] memory _blobHashes
 628 |  ) internal view returns (bytes32[] memory blobCommitments) {
```
GitHub: [103-107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L103-L107), [130-133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L130-L133), [253-256](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L253-L256), [273-277](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L273-L277), [308](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L308), [321](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L321), [453-457](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L453-L457), [500-505](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L500-L505), [515](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515), [525](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525), [537-542](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542), [561-564](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L561-L564), [592](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L592), [597](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597), [605-609](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L605-L609), [625-628](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L625-L628)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Inline this function, it's only used once
 130 |  function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {

     |  // @audit-issue Inline this function, it's only used once
 258 |  function _requestL2Transaction(
 259 |      uint256 _mintValue,
 260 |      WritePriorityOpParams memory _params,
 261 |      bytes memory _calldata,
 262 |      bytes[] memory _factoryDeps
 263 |  ) internal returns (bytes32 canonicalTxHash) {

     |  // @audit-issue Inline this function, it's only used once
 289 |  function _serializeL2Transaction(
 290 |      WritePriorityOpParams memory _priorityOpParams,
 291 |      bytes memory _calldata,
 292 |      bytes[] memory _factoryDeps
 293 |  ) internal pure returns (L2CanonicalTransaction memory transaction) {

     |  // @audit-issue Inline this function, it's only used once
 316 |  function _writePriorityOp(
 317 |      WritePriorityOpParams memory _priorityOpParams,
 318 |      bytes memory _calldata,
 319 |      bytes[] memory _factoryDeps
 320 |  ) internal returns (bytes32 canonicalTxHash) {

     |  // @audit-issue Inline this function, it's only used once
 353 |  function _hashFactoryDeps(bytes[] memory _factoryDeps) internal pure returns (uint256[] memory hashedFactoryDeps) {
```
GitHub: [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L130), [258-263](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L258-L263), [289-293](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L289-L293), [316-320](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L316-L320), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L353)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Inline this function, it's only used once
 163 |  function _upgradeVerifier(address _newVerifier, VerifierParams calldata _verifierParams) internal {

     |  // @audit-issue Inline this function, it's only used once
 171 |  function _setBaseSystemContracts(bytes32 _bootloaderHash, bytes32 _defaultAccountHash) internal {

     |  // @audit-issue Inline this function, it's only used once
 180 |  function _setL2SystemContractUpgrade(
 181 |      L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
 182 |      bytes[] calldata _factoryDeps,
 183 |      uint256 _newProtocolVersion
 184 |  ) internal returns (bytes32) {

     |  // @audit-issue Inline this function, it's only used once
 236 |  function _setNewProtocolVersion(uint256 _newProtocolVersion) internal virtual {

     |  // @audit-issue Inline this function, it's only used once
 263 |  function _upgradeL1Contract(bytes calldata _customCallDataForUpgrade) internal virtual {}

     |  // @audit-issue Inline this function, it's only used once
 269 |  function _postUpgrade(bytes calldata _customCallDataForUpgrade) internal virtual {}
```
GitHub: [163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L163), [171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L171), [180-184](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L180-L184), [236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L236), [263](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L263), [269](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L269)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

     |  // @audit-issue Inline this function, it's only used once
  20 |  function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
```
GitHub: [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

     |  // @audit-issue Inline this function, it's only used once
  49 |  function bytecodeLen(bytes32 _bytecodeHash) internal pure returns (uint256 codeLengthInWords) {
```
GitHub: [49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L49)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

     |  // @audit-issue Inline this function, it's only used once
  69 |  function getMinimalPriorityTransactionGasLimit(
  70 |      uint256 _encodingLength,
  71 |      uint256 _numberOfFactoryDependencies,
  72 |      uint256 _l2GasPricePerPubdata
  73 |  ) internal pure returns (uint256) {

     |  // @audit-issue Inline this function, it's only used once
 109 |  function getTransactionBodyGasLimit(
 110 |      uint256 _totalGasLimit,
 111 |      uint256 _encodingLength
 112 |  ) internal pure returns (uint256 txBodyGasLimit) {

     |  // @audit-issue Inline this function, it's only used once
 128 |  function getOverheadForTransaction(
 129 |      uint256 _encodingLength
 130 |  ) internal pure returns (uint256 batchOverheadForTransaction) {
```
GitHub: [69-73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L69-L73), [109-112](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L109-L112), [128-130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L128-L130)


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

     |  // @audit-issue Inline this function, it's only used once
  44 |  function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {

     |  // @audit-issue Inline this function, it's only used once
 139 |  function encodeEIP2930TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {

     |  // @audit-issue Inline this function, it's only used once
 229 |  function encodeEIP1559TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {
```
GitHub: [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L44), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L139), [229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L229)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue Inline this function, it's only used once
 197 |  function _decodeRawBytecode(
 198 |      bytes calldata _rawCompressedData
 199 |  ) internal pure returns (bytes calldata dictionary, bytes calldata encodedData) {
```
GitHub: [197-199](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L197-L199)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Inline this function, it's only used once
 283 |  function _performDeployOnAddress(
 284 |      bytes32 _bytecodeHash,
 285 |      address _newAddress,
 286 |      AccountAbstractionVersion _aaVersion,
 287 |      bytes calldata _input
 288 |  ) internal {

     |  // @audit-issue Inline this function, it's only used once
 309 |  function _storeConstructingByteCodeHashOnAddress(address _newAddress, bytes32 _bytecodeHash) internal {
```
GitHub: [283-288](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L283-L288), [309](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L309)


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

     |  // @audit-issue Inline this function, it's only used once
  78 |  function _validateTransaction(
  79 |      bytes32 _suggestedSignedHash,
  80 |      Transaction calldata _transaction
  81 |  ) internal returns (bytes4 magic) {

     |  // @audit-issue Inline this function, it's only used once
 131 |  function _execute(Transaction calldata _transaction) internal {

     |  // @audit-issue Inline this function, it's only used once
 159 |  function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {
```
GitHub: [78-81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L78-L81), [131](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L131), [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L159)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

     |  // @audit-issue Inline this function, it's only used once
  74 |  function _validateBytecode(bytes32 _bytecodeHash) internal pure {
```
GitHub: [74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L74)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Inline this function, it's only used once
  61 |  function sha256GasCost(uint256 _length) internal pure returns (uint256) {
```
GitHub: [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L61)


```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

     |  // @audit-issue Inline this function, it's only used once
 112 |  function _getL1WithdrawMessage(address _to, uint256 _amount) internal pure returns (bytes memory) {

     |  // @audit-issue Inline this function, it's only used once
 117 |  function _getExtendedWithdrawMessage(
 118 |      address _to,
 119 |      uint256 _amount,
 120 |      address _sender,
 121 |      bytes memory _additionalData
 122 |  ) internal pure returns (bytes memory) {
```
GitHub: [112](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L112), [117-122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L117-L122)


```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

     |  // @audit-issue Inline this function, it's only used once
  25 |  function _getAbiParams() internal view returns (uint256 value, bool isSystemCall, address to) {
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L25)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Inline this function, it's only used once
 221 |  function _calculateL2BlockHash(
 222 |      uint128 _blockNumber,
 223 |      uint128 _blockTimestamp,
 224 |      bytes32 _prevL2BlockHash,
 225 |      bytes32 _blockTxsRollingHash
 226 |  ) internal pure returns (bytes32) {

     |  // @audit-issue Inline this function, it's only used once
 233 |  function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {

     |  // @audit-issue Inline this function, it's only used once
 241 |  function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {

     |  // @audit-issue Inline this function, it's only used once
 263 |  function _setVirtualBlock(
 264 |      uint128 _l2BlockNumber,
 265 |      uint128 _maxVirtualBlocksToCreate,
 266 |      uint128 _newTimestamp
 267 |  ) internal {

     |  // @audit-issue Inline this function, it's only used once
 427 |  function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {
```
GitHub: [221-226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L221-L226), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L233), [241](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L241), [263-267](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L263-L267), [427](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L427)


```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

     |  // @audit-issue Inline this function, it's only used once
 124 |  function rawCall(
 125 |      uint256 _gas,
 126 |      address _address,
 127 |      uint256 _value,
 128 |      bytes calldata _data,
 129 |      bool _isSystem
 130 |  ) internal returns (bool success) {

     |  // @audit-issue Inline this function, it's only used once
 159 |  function rawStaticCall(uint256 _gas, address _address, bytes calldata _data) internal view returns (bool success) {

     |  // @audit-issue Inline this function, it's only used once
 173 |  function rawDelegateCall(uint256 _gas, address _address, bytes calldata _data) internal returns (bool success) {

     |  // @audit-issue Inline this function, it's only used once
 191 |  function rawMimicCall(
 192 |      uint256 _gas,
 193 |      address _address,
 194 |      bytes calldata _data,
 195 |      address _whoToMimic,
 196 |      bool _isConstructor,
 197 |      bool _isSystem
 198 |  ) internal returns (bool success) {

     |  // @audit-issue Inline this function, it's only used once
 232 |  function propagateRevert() internal pure {
```
GitHub: [124-130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L124-L130), [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L159), [173](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L173), [191-198](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L191-L198), [232](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L232)


```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

     |  // @audit-issue Inline this function, it's only used once
 148 |  function unsafePrecompileCall(
 149 |      uint256 _rawParams,
 150 |      uint32 _gasToBurn,
 151 |      uint32 _pubdataToSpend
 152 |  ) internal view returns (bool success) {

     |  // @audit-issue Inline this function, it's only used once
 203 |  function getZkSyncMetaBytes() internal view returns (uint256 meta) {

     |  // @audit-issue Inline this function, it's only used once
 227 |  function getPubdataPublishedFromMeta(uint256 meta) internal pure returns (uint32 pubdataPublished) {

     |  // @audit-issue Inline this function, it's only used once
 237 |  function getHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 heapSize) {

     |  // @audit-issue Inline this function, it's only used once
 246 |  function getAuxHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 auxHeapSize) {

     |  // @audit-issue Inline this function, it's only used once
 254 |  function getShardIdFromMeta(uint256 meta) internal pure returns (uint8 shardId) {

     |  // @audit-issue Inline this function, it's only used once
 263 |  function getCallerShardIdFromMeta(uint256 meta) internal pure returns (uint8 callerShardId) {

     |  // @audit-issue Inline this function, it's only used once
 272 |  function getCodeShardIdFromMeta(uint256 meta) internal pure returns (uint8 codeShardId) {

     |  // @audit-issue Inline this function, it's only used once
 296 |  function getCallFlags() internal view returns (uint256 callFlags) {
```
GitHub: [148-152](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L148-L152), [203](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L203), [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L227), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L237), [246](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L246), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L254), [263](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L263), [272](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L272), [296](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L296)


```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

     |  // @audit-issue Inline this function, it's only used once
  76 |  function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

     |  // @audit-issue Inline this function, it's only used once
 123 |  function systemCallWithReturndata(
 124 |      uint32 gasLimit,
 125 |      address to,
 126 |      uint128 value,
 127 |      bytes memory data
 128 |  ) internal returns (bool success, bytes memory returnData) {

     |  // @audit-issue Inline this function, it's only used once
 214 |  function getFarCallABI(
 215 |      uint32 dataOffset,
 216 |      uint32 memoryPage,
 217 |      uint32 dataStart,
 218 |      uint32 dataLength,
 219 |      uint32 gasPassed,
 220 |      uint8 shardId,
 221 |      CalldataForwardingMode forwardingMode,
 222 |      bool isConstructorCall,
 223 |      bool isSystemCall
 224 |  ) internal pure returns (uint256 farCallAbi) {

     |  // @audit-issue Inline this function, it's only used once
 250 |  function getFarCallABIWithEmptyFatPointer(
 251 |      uint32 gasPassed,
 252 |      uint8 shardId,
 253 |      CalldataForwardingMode forwardingMode,
 254 |      bool isConstructorCall,
 255 |      bool isSystemCall
 256 |  ) internal pure returns (uint256 farCallAbiWithEmptyFatPtr) {
```
GitHub: [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L76), [123-128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L123-L128), [214-224](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L214-L224), [250-256](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L250-L256)


```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

     |  // @audit-issue Inline this function, it's only used once
  44 |  function bytecodeLenInWords(bytes32 _bytecodeHash) internal pure returns (uint256 codeLengthInWords) {

     |  // @audit-issue Inline this function, it's only used once
  71 |  function constructedBytecodeHash(bytes32 _bytecodeHash) internal pure returns (bytes32) {
```
GitHub: [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L44), [71](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L71)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-issue Inline this function, it's only used once
 109 |  function _deployL2Token(address _l1Token, bytes calldata _data) internal returns (address) {

     |  // @audit-issue Inline this function, it's only used once
 138 |  function _getL1WithdrawMessage(
 139 |      address _to,
 140 |      address _l1Token,
 141 |      uint256 _amount
 142 |  ) internal pure returns (bytes memory) {

     |  // @audit-issue Inline this function, it's only used once
 164 |  function _deployBeaconProxy(bytes32 salt) internal returns (BeaconProxy proxy) {
```
GitHub: [109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L109), [138-142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L138-L142), [164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L164)


```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

     |  // @audit-issue Inline this function, it's only used once
  27 |  function safeCastToU32(uint256 _x) internal pure returns (uint32) {

     |  // @audit-issue Inline this function, it's only used once
  37 |  function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

     |  // @audit-issue Inline this function, it's only used once
  95 |  function getFarCallABI(
  96 |      uint32 dataOffset,
  97 |      uint32 memoryPage,
  98 |      uint32 dataStart,
  99 |      uint32 dataLength,
 100 |      uint32 gasPassed,
 101 |      uint8 shardId,
 102 |      CalldataForwardingMode forwardingMode,
 103 |      bool isConstructorCall,
 104 |      bool isSystemCall
 105 |  ) internal pure returns (uint256 farCallAbi) {

     |  // @audit-issue Inline this function, it's only used once
 121 |  function getFarCallABIWithEmptyFatPointer(
 122 |      uint32 gasPassed,
 123 |      uint8 shardId,
 124 |      CalldataForwardingMode forwardingMode,
 125 |      bool isConstructorCall,
 126 |      bool isSystemCall
 127 |  ) internal pure returns (uint256 farCallAbiWithEmptyFatPtr) {
```
GitHub: [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L27), [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L37), [95-105](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L95-L105), [121-127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L121-L127)


## [G-30] Inline `modifier`s that are only used once, to save gas

Inline `modifier`s that are only used once, to save gas.

*Instances: 25*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-info Contains redundant modifiers
  30 |  contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
 107 |      ) external reentrancyGuardInitializer initializer {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
 153 |      ) external payable virtual onlyBridgehubOrEra(_chainId) {
```
GitHub: [107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L107), [153](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L153)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-info Contains redundant modifiers
  20 |  contract Governance is IGovernance, Ownable2Step {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
 167 |      function execute(Operation calldata _operation) external payable onlyOwnerOrSecurityCouncil {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
 186 |      function executeInstant(Operation calldata _operation) external payable onlySecurityCouncil {
```
GitHub: [167](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L167), [186](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L186)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-info Contains redundant modifiers
  27 |  contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
 247 |      ) external onlyBridgehub {
```
GitHub: [247](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L247)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-info Contains redundant modifiers
  22 |  contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
 472 |      function revertBatches(uint256 _newLastBatch) external nonReentrant onlyValidatorOrStateTransitionManager {
```
GitHub: [472](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L472)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-info Contains redundant modifiers
  30 |  contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
  38 |      function transferEthToSharedBridge() external onlyBaseTokenBridge {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
  49 |      ) external payable onlyBridgehub returns (bytes32 canonicalTxHash) {
```
GitHub: [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L38), [49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L49)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-info Contains redundant modifiers
  22 |  contract Compressor is ICompressor, ISystemContract {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
  47 |      ) external payable onlyCallFromBootloader returns (bytes32 bytecodeHash) {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
 115 |      ) external payable onlyCallFrom(address(L1_MESSENGER_CONTRACT)) returns (bytes32 stateDiffHash) {
```
GitHub: [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L47), [115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L115)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-info Contains redundant modifiers
  23 |  contract ContractDeployer is IContractDeployer, ISystemContract {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
 213 |      function forceDeployOnAddress(ForceDeployment calldata _deployment, address _sender) external payable onlySelf {
```
GitHub: [213](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L213)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

     |  // @audit-info Contains redundant modifiers
  18 |  contract KnownCodesStorage is IKnownCodesStorage, ISystemContract {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
  27 |      function markFactoryDeps(bool _shouldSendToL1, bytes32[] calldata _hashes) external onlyCallFromBootloader {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
  39 |      function markBytecodeAsPublished(bytes32 _bytecodeHash) external onlyCompressor {
```
GitHub: [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L27), [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L39)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-info Contains redundant modifiers
  25 |  contract L1Messenger is IL1Messenger, ISystemContract {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
  74 |      ) external onlyCallFromSystemContract returns (uint256 logIdInMerkleTree) {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
 163 |      ) external override onlyCallFrom(address(KNOWN_CODE_STORAGE_CONTRACT)) {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
 196 |      ) external onlyCallFromBootloader {
```
GitHub: [74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L74), [163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L163), [196](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L196)


```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

     |  // @audit-info Contains redundant modifiers
  18 |  contract L2BaseToken is IBaseToken, ISystemContract {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
  64 |      function mint(address _account, uint256 _amount) external override onlyCallFromBootloader {
```
GitHub: [64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L64)


```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

     |  // @audit-info Contains redundant modifiers
  19 |  contract MsgValueSimulator is ISystemContract {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
  47 |      fallback(bytes calldata _data) external onlySystemCall returns (bytes memory) {
```
GitHub: [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L47)


```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

     |  // @audit-info Contains redundant modifiers
  16 |  contract PubdataChunkPublisher is IPubdataChunkPublisher, ISystemContract {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
  21 |      function chunkAndPublishPubdata(bytes calldata _pubdata) external onlyCallFrom(address(L1_MESSENGER_CONTRACT)) {
```
GitHub: [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L21)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-info Contains redundant modifiers
  17 |  contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
  84 |      function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {
```
GitHub: [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L84)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-info Contains redundant modifiers
  23 |  contract L2SharedBridge is IL2SharedBridge, Initializable {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
  54 |      ) external reinitializer(2) {
```
GitHub: [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L54)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

     |  // @audit-info Contains redundant modifiers
  15 |  contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
  50 |      function bridgeInitialize(address _l1Address, bytes memory _data) external initializer {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
     |      // @audit-issue This is the only invocation of this modifier
 116 |      ) external onlyNextVersion(_version) reinitializer(_version) {
```
GitHub: [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L50), [116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L116), [116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L116)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

     |  // @audit-info Contains redundant modifiers
  23 |  contract L2WrappedBaseToken is ERC20PermitUpgradeable, IL2WrappedBaseToken, IL2StandardToken {
  :  |
     |      // @audit-issue This is the only invocation of this modifier
  49 |      ) external reinitializer(2) {
```
GitHub: [49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L49)


## [G-31] It costs more gas to initialize non-`constant`/non-`immutable` state variables to zero/false than to let the default of zero/false be applied

The default value for variables is zero, so initializing them to zero is superfluous. This will also save gas if the variable is a mutable state variable.

*Instances: 5*

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Initial value is unnecessary
 629 |  uint256 versionedHashIndex = 0;
```
GitHub: [629](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L629)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

     |  // @audit-issue Initial value is unnecessary
  92 |  uint256 costForPubdata = 0;
```
GitHub: [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L92)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue Initial value is unnecessary
 124 |  uint256 numInitialWritesProcessed = 0;
```
GitHub: [124](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L124)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Initial value is unnecessary
 247 |  uint256 sumOfValues = 0;
```
GitHub: [247](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L247)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Initial value is unnecessary
 197 |  uint256 calldataPtr = 0;
```
GitHub: [197](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L197)


## [G-32] Iterating backwards in a `for` statement saves gas

Iterating backwards allows you to specify your loop termination condition using `0`, and comparisons with `0` are more gas efficient than with arbitrary integers.

*Instances: 18*

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Consider looping backwards
 225 |  for (uint256 i = 0; i < _calls.length; ++i) {
```
GitHub: [225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Consider looping backwards
 116 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Consider looping backwards
 135 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Consider looping backwards
 185 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Consider looping backwards
 209 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```
GitHub: [116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185), [209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Consider looping backwards
 580 |  for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

     |  // @audit-issue Consider looping backwards
 667 |  for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
GitHub: [580](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580), [667](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Consider looping backwards
 226 |  for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
GitHub: [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Consider looping backwards
 248 |  for (uint256 i = 0; i < deploymentsLength; ++i) {

     |  // @audit-issue Consider looping backwards
 253 |  for (uint256 i = 0; i < deploymentsLength; ++i) {
```
GitHub: [248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L248), [253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L253)


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

     |  // @audit-issue Consider looping backwards
  38 |  for (uint256 i = 0; i < immutablesLength; ++i) {
```
GitHub: [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L38)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

     |  // @audit-issue Consider looping backwards
  30 |  for (uint256 i = 0; i < hashesLen; ++i) {
```
GitHub: [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L30)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Consider looping backwards
 206 |  for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

     |  // @audit-issue Consider looping backwards
 218 |  for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

     |  // @audit-issue Consider looping backwards
 224 |  for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

     |  // @audit-issue Consider looping backwards
 236 |  for (uint256 i = 0; i < numberOfMessages; ++i) {

     |  // @audit-issue Consider looping backwards
 254 |  for (uint256 i = 0; i < numberOfBytecodes; ++i) {
```
GitHub: [206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L206), [218](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L218), [224](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L224), [236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L236), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L254)


```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

     |  // @audit-issue Consider looping backwards
  36 |  for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
GitHub: [36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)


## [G-33] Mappings are cheaper to use than storage arrays

When using storage arrays, solidity adds an internal lookup of the array's length (a Gcoldsload **2100 gas**) to ensure you don't read past the array's end. You can avoid this lookup by using a `mapping` and storing the number of entries in a separate storage variable. In cases where you have sentinel values (e.g. 'zero' means invalid), you can avoid length checks.

*Instances: 1*

```solidity
File: code/system-contracts/contracts/SystemContext.sol

  70 |  bytes32[MINIBLOCK_HASHES_TO_STORE] internal l2BlockHash;
```
GitHub: [70](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L70)


## [G-34] Merge events to save gas

Consolidating multiple event emissions into a single event in Solidity can result in significant gas savings. Each event emission in Ethereum involves a gas cost, specifically for the topics logged with the event. By merging sequential events into a singular event, you can save on the Glogtopic cost, which is incurred for each topic of each event. This approach can save around 375 gas per additional topic. This strategy is particularly beneficial in functions where multiple related events are emitted in sequence. However, it's crucial to balance gas optimization with the clarity and utility of the event data for off-chain consumers.

*Instances: 8*

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

  60 |  function acceptAdmin() external {
  :  |
  68 |      emit NewPendingAdmin(currentPendingAdmin, address(0));
  69 |      emit NewAdmin(previousAdmin, pendingAdmin);
```
GitHub: [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68), [69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

  41 |  constructor(address _admin, address _securityCouncil, uint256 _minDelay) {
  :  |
  47 |      emit ChangeSecurityCouncil(address(0), _securityCouncil);
  :  |
  50 |      emit ChangeMinDelay(0, _minDelay);
```
GitHub: [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L47), [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L50)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 121 |  function acceptAdmin() external {
  :  |
 129 |      emit NewPendingAdmin(currentPendingAdmin, address(0));
 130 |      emit NewAdmin(previousAdmin, pendingAdmin);
```
GitHub: [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L129), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L130)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

  32 |  function acceptAdmin() external {
  :  |
  40 |      emit NewPendingAdmin(pendingAdmin, address(0));
  41 |      emit NewAdmin(previousAdmin, pendingAdmin);
```
GitHub: [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L41)


## [G-35] Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct`

Saves a storage slot for the mapping. Depending on the circumstances and sizes of types, can avoid a Gsset (20000 gas) per mapping combined. Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Finally, if both fields are accessed in the same function, can save ~42 gas per access due to [not having to recalculate the key's keccak256 hash](https://gist.github.com/IllIllI000/ec23a57daa30a8f8ca8b9681c8ccefb0) (Gkeccak256 - 30 gas) and that calculation's associated stack operations.

*Instances: 13*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Consider whether multiple mappings can be merged into a single struct mapping
  48 |  mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;

     |  // @audit-issue Consider whether multiple mappings can be merged into a single struct mapping
  52 |  mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
  53 |      public
  54 |      override depositHappened;

     |  // @audit-issue Consider whether multiple mappings can be merged into a single struct mapping
  57 |  mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
  58 |      public isWithdrawalFinalized;

     |  // @audit-issue Consider whether multiple mappings can be merged into a single struct mapping
  61 |  mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;

     |  // @audit-issue Consider whether multiple mappings can be merged into a single struct mapping
  65 |  mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;
```
GitHub: [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L48), [52-54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L52-L54), [57-58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57-L58), [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L61), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L65)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Consider whether multiple mappings can be merged into a single struct mapping
  26 |  mapping(uint256 _chainId => address) public stateTransitionManager;

     |  // @audit-issue Consider whether multiple mappings can be merged into a single struct mapping
  29 |  mapping(uint256 _chainId => address) public baseToken;
```
GitHub: [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L26), [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L29)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Consider whether multiple mappings can be merged into a single struct mapping
  47 |  mapping(uint256 => LibMap.Uint32Map) internal committedBatchTimestamp;

     |  // @audit-issue Consider whether multiple mappings can be merged into a single struct mapping
  50 |  mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
GitHub: [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L47), [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

     |  // @audit-issue Consider whether multiple mappings can be merged into a single struct mapping
  86 |  mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;

     |  // @audit-issue Consider whether multiple mappings can be merged into a single struct mapping
  88 |  mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;
```
GitHub: [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L86), [88](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L88)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-issue Consider whether multiple mappings can be merged into a single struct mapping
  36 |  mapping(uint256 account => uint256 packedMinAndDeploymentNonce) internal rawNonces;

     |  // @audit-issue Consider whether multiple mappings can be merged into a single struct mapping
  41 |  mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;
```
GitHub: [36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L36), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L41)


## [G-36] Multiple accesses of a mapping/array should use a local variable cache

The instances below point to multiple accesses of a value inside a mapping/array, within a function. Caching a mapping's value in a local `storage` or `calldata` variable when the value is accessed [multiple times](https://gist.github.com/IllIllI000/ec23a57daa30a8f8ca8b9681c8ccefb0), saves **~42 gas per access** due to not having to recalculate the key's keccak256 hash (Gkeccak256 - **30 gas**) and that calculation's associated stack operations. Caching an array's struct avoids recalculating the array offsets into memory/calldata

*Instances: 35*

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-info Context
 224 |  function _execute(Call[] calldata _calls) internal {
  :  |
     |          // @audit-issue `_calls[i]` usage #1
     |          // @audit-issue `_calls[i]` usage #2
     |          // @audit-issue `_calls[i]` usage #3
 226 |          (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```
GitHub: [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-info Context
 349 |  function _executeBatches(StoredBatchInfo[] calldata _batchesData) internal {
  :  |
     |          // @audit-issue `_batchesData[i]` usage #1
 352 |          _executeOneBatch(_batchesData[i], i);
     |          // @audit-issue `_batchesData[i]` usage #2
     |          // @audit-issue `_batchesData[i]` usage #3
     |          // @audit-issue `_batchesData[i]` usage #4
 353 |          emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

     |  // @audit-info Context
 386 |  function _proveBatches(
 387 |      StoredBatchInfo calldata _prevBatch,
 388 |      StoredBatchInfo[] calldata _committedBatches,
 389 |      ProofInput calldata _proof
 390 |  ) internal {
  :  |
     |              // @audit-issue `_committedBatches[i]` usage #1
 408 |              _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
  :  |
     |          // @audit-issue `_committedBatches[i]` usage #2
 412 |          bytes32 currentBatchCommitment = _committedBatches[i].commitment;
```
GitHub: [352](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L352), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353), [408](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L408), [412](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L412)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-info Context
 163 |  function isFacetFreezable(address _facet) external view returns (bool isFreezable) {
  :  |
     |      // @audit-issue `ds.facetToSelectors[_facet]` usage #1
 168 |      uint256 selectorsArrayLen = ds.facetToSelectors[_facet].selectors.length;
  :  |
     |          // @audit-issue `ds.facetToSelectors[_facet]` usage #2
 170 |          bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];

     |  // @audit-info Context
 181 |  function isFunctionFreezable(bytes4 _selector) external view returns (bool) {
  :  |
     |      // @audit-issue `ds.selectorToFacet[_selector]` usage #1
 183 |      require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");
     |      // @audit-issue `ds.selectorToFacet[_selector]` usage #2
 184 |      return ds.selectorToFacet[_selector].isFreezable;
```
GitHub: [168](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L168), [170](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L170), [183](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183), [184](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L184)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

     |  // @audit-info Context
  96 |  function diamondCut(DiamondCutData memory _diamondCut) internal {
  :  |
     |          // @audit-issue `facetCuts[i]` usage #1
 102 |          Action action = facetCuts[i].action;
     |          // @audit-issue `facetCuts[i]` usage #2
 103 |          address facet = facetCuts[i].facet;
     |          // @audit-issue `facetCuts[i]` usage #3
 104 |          bool isFacetFreezable = facetCuts[i].isFreezable;
     |          // @audit-issue `facetCuts[i]` usage #4
 105 |          bytes4[] memory selectors = facetCuts[i].selectors;

     |  // @audit-info Context
 189 |  function _saveFacetIfNew(address _facet) private {
  :  |
     |      // @audit-issue `ds.facetToSelectors[_facet]` usage #1
 192 |      uint256 selectorsLength = ds.facetToSelectors[_facet].selectors.length;
  :  |
     |          // @audit-issue `ds.facetToSelectors[_facet]` usage #2
 195 |          ds.facetToSelectors[_facet].facetPosition = ds.facets.length.toUint16();

     |  // @audit-info Context
 205 |  function _addOneFunction(address _facet, bytes4 _selector, bool _isSelectorFreezable) private {
  :  |
     |      // @audit-issue `ds.facetToSelectors[_facet]` usage #1
 208 |      uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16();
  :  |
     |          // @audit-issue `ds.facetToSelectors[_facet]` usage #2
 214 |          bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];
  :  |
     |      // @audit-issue `ds.facetToSelectors[_facet]` usage #3
 223 |      ds.facetToSelectors[_facet].selectors.push(_selector);

     |  // @audit-info Context
 228 |  function _removeOneFunction(address _facet, bytes4 _selector) private {
  :  |
     |      // @audit-issue `ds.selectorToFacet[_selector]` usage #1
 232 |      uint256 selectorPosition = ds.selectorToFacet[_selector].selectorPosition;
  :  |
     |      // @audit-issue `ds.selectorToFacet[_selector]` usage #2
 247 |      delete ds.selectorToFacet[_selector];

     |  // @audit-info Context
 228 |  function _removeOneFunction(address _facet, bytes4 _selector) private {
  :  |
     |      // @audit-issue `ds.facetToSelectors[_facet]` usage #1
 233 |      uint256 lastSelectorPosition = ds.facetToSelectors[_facet].selectors.length - 1;
  :  |
     |          // @audit-issue `ds.facetToSelectors[_facet]` usage #2
 237 |          bytes4 lastSelector = ds.facetToSelectors[_facet].selectors[lastSelectorPosition];
  :  |
     |          // @audit-issue `ds.facetToSelectors[_facet]` usage #3
 239 |          ds.facetToSelectors[_facet].selectors[selectorPosition] = lastSelector;
  :  |
     |      // @audit-issue `ds.facetToSelectors[_facet]` usage #4
 244 |      ds.facetToSelectors[_facet].selectors.pop();
```
GitHub: [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L102), [103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L103), [104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L104), [105](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L105), [192](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L192), [195](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L195), [208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L208), [214](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L214), [223](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L223), [232](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L232), [247](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L247), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L233), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L237), [239](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L239), [244](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L244)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

     |  // @audit-info Context
  72 |  function popFront(Queue storage _queue) internal returns (PriorityOperation memory priorityOperation) {
  :  |
     |      // @audit-issue `_queue.data[head]` usage #1
  78 |      priorityOperation = _queue.data[head];
     |      // @audit-issue `_queue.data[head]` usage #2
  79 |      delete _queue.data[head];
```
GitHub: [78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L78), [79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L79)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-info Context
 238 |  function forceDeployOnAddresses(ForceDeployment[] calldata _deployments) external payable {
  :  |
     |          // @audit-issue `_deployments[i]` usage #1
 249 |          sumOfValues += _deployments[i].value;
  :  |
     |          // @audit-issue `_deployments[i]` usage #2
     |          // @audit-issue `_deployments[i]` usage #3
 254 |          this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
```
GitHub: [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L249), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L254), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L254)


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

     |  // @audit-info Context
  34 |  function setImmutables(address _dest, ImmutableData[] calldata _immutables) external override {
  :  |
     |              // @audit-issue `_immutables[i]` usage #1
  39 |              uint256 index = _immutables[i].index;
     |              // @audit-issue `_immutables[i]` usage #2
  40 |              bytes32 value = _immutables[i].value;
```
GitHub: [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L39), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L40)


## [G-37] Nesting `if`-statements is cheaper than using `&&`

Nesting `if`-statements avoids the stack operations of setting up and using an extra `jumpdest`, and saves **6 [gas](https://gist.github.com/IllIllI000/7f3b818abecfadbef93b894481ae7d19)**

*Instances: 12*

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Consider using nested ifs instead of && to save gas
 361 |  if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {
```
GitHub: [361](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L361)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Consider using nested ifs instead of && to save gas
 147 |  if (
 148 |      _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) &&
 149 |      _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) &&
 150 |      _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)
 151 |  ) {
```
GitHub: [147-151](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L147-L151)


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

     |  // @audit-issue Consider using nested ifs instead of && to save gas
 102 |  if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {

     |  // @audit-issue Consider using nested ifs instead of && to save gas
 131 |  if (
 132 |      uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS &&
 133 |      codeHash != 0x00 &&
 134 |      !Utils.isContractConstructing(codeHash)
 135 |  ) {
```
GitHub: [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L102), [131-135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L131-L135)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Consider using nested ifs instead of && to save gas
  47 |  if (
  48 |      _address > address(MAX_SYSTEM_CONTRACT_ADDRESS) &&
  49 |      ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getRawCodeHash(_address) == 0
  50 |  ) {
```
GitHub: [47-50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L47-L50)


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

     |  // @audit-issue Consider using nested ifs instead of && to save gas
 139 |  if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) {
```
GitHub: [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L139)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-issue Consider using nested ifs instead of && to save gas
  88 |  if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {

     |  // @audit-issue Consider using nested ifs instead of && to save gas
 169 |  if (isUsed && !_shouldBeUsed) {

     |  // @audit-issue Consider using nested ifs instead of && to save gas
 171 |  } else if (!isUsed && _shouldBeUsed) {
```
GitHub: [88](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L88), [169](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L169), [171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L171)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Consider using nested ifs instead of && to save gas
 150 |  } else if (
 151 |      _block >= currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block &&
 152 |      currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0
 153 |  ) {

     |  // @audit-issue Consider using nested ifs instead of && to save gas
 277 |  if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {

     |  // @audit-issue Consider using nested ifs instead of && to save gas
 360 |  if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {
```
GitHub: [150-153](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L150-L153), [277](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L277), [360](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L360)


## [G-38] Not using the named return variable is confusing and can waste gas

Consider changing the variable to be an unnamed one, since the variable is never assigned, nor is it returned by name. If the optimizer is not turned on, leaving the code as it is will also waste gas for the stack variable.

*Instances: 4*

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Remove unused variable `chainId` to save gas
 121 |  ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
```
GitHub: [121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L121)


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

     |  // @audit-issue Remove unused variable `txHash` to save gas
  44 |  function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {
```
GitHub: [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L44)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Remove unused variable `info` to save gas
  34 |  function getAccountInfo(address _address) external view returns (AccountInfo memory info) {
```
GitHub: [34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L34)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

     |  // @audit-issue Remove unused variable `context` to save gas
  18 |  ) external payable returns (bytes4 magic, bytes memory context) {
```
GitHub: [18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L18)


## [G-39] Only emit event in setter function if the state variable was changed

Emitting events in setter functions of smart contracts only when state variables change saves gas. This is because emitting events consumes gas, and unnecessary events, where no actual state change occurs, lead to wasteful consumption.

*Instances: 22*

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-info Unvalidated: _newPendingAdmin
  51 |  function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
  :  |
     |      // @audit-issue Potentially redundant emit
  56 |      emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
```
GitHub: [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L56)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-info Unvalidated: _newDelay
 249 |  function updateDelay(uint256 _newDelay) external onlySelf {
     |      // @audit-issue Potentially redundant emit
 250 |      emit ChangeMinDelay(minDelay, _newDelay);

     |  // @audit-info Unvalidated: _newSecurityCouncil
 256 |  function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
     |      // @audit-issue Potentially redundant emit
 257 |      emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```
GitHub: [250](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L250), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L257)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-info Unvalidated: _newPendingAdmin
 112 |  function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
  :  |
     |      // @audit-issue Potentially redundant emit
 117 |      emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
```
GitHub: [117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L117)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-info Unvalidated: _executionDelay
  96 |  function setExecutionDelay(uint32 _executionDelay) external onlyOwner {
  :  |
     |      // @audit-issue Potentially redundant emit
  98 |      emit NewExecutionDelay(_executionDelay);
```
GitHub: [98](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-info Unvalidated: _newPendingAdmin
  23 |  function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {
  :  |
     |      // @audit-issue Potentially redundant emit
  28 |      emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

     |  // @audit-info Unvalidated: _active
  45 |  function setValidator(address _validator, bool _active) external onlyStateTransitionManager {
  :  |
     |      // @audit-issue Potentially redundant emit
  47 |      emit ValidatorStatusUpdate(_validator, _active);

     |  // @audit-info Unvalidated: _zkPorterIsAvailable
  51 |  function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {
  :  |
     |      // @audit-issue Potentially redundant emit
  54 |      emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);

     |  // @audit-info Unvalidated: _newPriorityTxMaxGasLimit
  58 |  function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager {
  :  |
     |      // @audit-issue Potentially redundant emit
  63 |      emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);

     |  // @audit-info Unvalidated: _newFeeParams
  67 |  function changeFeeParams(FeeParams calldata _newFeeParams) external onlyAdminOrStateTransitionManager {
  :  |
     |      // @audit-issue Potentially redundant emit
  75 |      emit NewFeeParams(oldFeeParams, _newFeeParams);

     |  // @audit-info Unvalidated: _nominator, _denominator
  79 |  function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {
  :  |
     |      // @audit-issue Potentially redundant emit
  86 |      emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator);

     |  // @audit-info Unvalidated: _validiumMode
  89 |  function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {
  :  |
     |      // @audit-issue Potentially redundant emit
  92 |      emit ValidiumModeStatusUpdate(_validiumMode);
```
GitHub: [28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L28), [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L47), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L54), [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L63), [75](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L75), [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L86), [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-info Unvalidated: _l2DefaultAccountBytecodeHash
  92 |  function _setL2DefaultAccountBytecodeHash(bytes32 _l2DefaultAccountBytecodeHash) private {
  :  |
     |      // @audit-issue Potentially redundant emit
 104 |      emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);

     |  // @audit-info Unvalidated: _l2BootloaderBytecodeHash
 109 |  function _setL2BootloaderBytecodeHash(bytes32 _l2BootloaderBytecodeHash) private {
  :  |
     |      // @audit-issue Potentially redundant emit
 121 |      emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);

     |  // @audit-info Unvalidated: _newVerifier
 126 |  function _setVerifier(IVerifier _newVerifier) private {
  :  |
     |      // @audit-issue Potentially redundant emit
 137 |      emit NewVerifier(address(oldVerifier), address(_newVerifier));

     |  // @audit-info Unvalidated: _newVerifierParams
 142 |  function _setVerifierParams(VerifierParams calldata _newVerifierParams) private {
  :  |
     |      // @audit-issue Potentially redundant emit
 157 |      emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

     |  // @audit-info Unvalidated: _newProtocolVersion
 236 |  function _setNewProtocolVersion(uint256 _newProtocolVersion) internal virtual {
  :  |
     |      // @audit-issue Potentially redundant emit
 256 |      emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
```
GitHub: [104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L104), [121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L121), [137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L137), [157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L157), [256](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L256)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

     |  // @audit-info Unvalidated: _newProtocolVersion
  20 |  function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
  :  |
     |      // @audit-issue Potentially redundant emit
  40 |      emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
```
GitHub: [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L40)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol

     |  // @audit-info Unvalidated: _newFeeParams
  20 |  function changeFeeParams(FeeParams memory _newFeeParams) private {
  :  |
     |      // @audit-issue Potentially redundant emit
  28 |      emit NewFeeParams(oldFeeParams, _newFeeParams);
```
GitHub: [28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol#L28)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-info Unvalidated: _version
  65 |  function updateAccountVersion(AccountAbstractionVersion _version) external onlySystemCall {
  :  |
     |      // @audit-issue Potentially redundant emit
  68 |      emit AccountVersionUpdated(msg.sender, _version);

     |  // @audit-info Unvalidated: _nonceOrdering
  74 |  function updateNonceOrdering(AccountNonceOrdering _nonceOrdering) external onlySystemCall {
  :  |
     |      // @audit-issue Potentially redundant emit
  86 |      emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);
```
GitHub: [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L68), [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L86)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-info Unvalidated: _value
  82 |  function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall {
  :  |
     |      // @audit-issue Potentially redundant emit
  96 |      emit ValueSetUnderNonce(msg.sender, _key, _value);
```
GitHub: [96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L96)


## [G-40] Operator `>=`/`<=` costs less gas than operator `>`/`<`

The compiler uses opcodes `GT` and `ISZERO` for solidity code that uses `>`, but only requires `LT` for `>=`, [which saves **3 gas**](https://gist.github.com/IllIllI000/3dc79d25acccfa16dee4e83ffdc6ffde). If `<` is being used, the condition can be inverted.

*Instances: 98*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Switch > to >= and < to <=
 121 |  require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");

     |  // @audit-issue Switch > to >= and < to <=
 129 |  require(amount > 0, "ShB: 0 amount to transfer");

     |  // @audit-issue Switch > to >= and < to <=
 327 |  require(_amount > 0, "y1");

     |  // @audit-issue Switch > to >= and < to <=
 375 |  return (_chainId == ERA_CHAIN_ID) && (_l2BatchNumber < eraFirstPostUpgradeBatch);
```
GitHub: [121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L121), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129), [327](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327), [375](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L375)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Switch > to >= and < to <=
 301 |  _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,

     |  // @audit-issue Switch > to >= and < to <=
 329 |  } else if (_refundRecipient.code.length > 0) {
```
GitHub: [301](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L301), [329](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L329)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Switch > to >= and < to <=
 111 |  } else if (timestamp > block.timestamp) {

     |  // @audit-issue Switch > to >= and < to <=
 225 |  for (uint256 i = 0; i < _calls.length; ++i) {
```
GitHub: [111](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L111), [225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Switch > to >= and < to <=
 116 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Switch > to >= and < to <=
 135 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Switch > to >= and < to <=
 185 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Switch > to >= and < to <=
 209 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```
GitHub: [116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185), [209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue Switch > to >= and < to <=
 117 |  s.protocolVersion > _oldProtocolVersion,
```
GitHub: [117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L117)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Switch > to >= and < to <=
 114 |  require(_previousBatchTimestamp < batchTimestamp, "h3");

     |  // @audit-issue Switch > to >= and < to <=
 142 |  for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

     |  // @audit-issue Switch > to >= and < to <=
 257 |  for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

     |  // @audit-issue Switch > to >= and < to <=
 289 |  for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

     |  // @audit-issue Switch > to >= and < to <=
 311 |  for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {

     |  // @audit-issue Switch > to >= and < to <=
 351 |  for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {

     |  // @audit-issue Switch > to >= and < to <=
 405 |  for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {

     |  // @audit-issue Switch > to >= and < to <=
 429 |  if (_proof.serializedProof.length > 0) {

     |  // @audit-issue Switch > to >= and < to <=
 482 |  require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch

     |  // @audit-issue Switch > to >= and < to <=
 485 |  if (_newLastBatch < s.totalBatchesVerified) {

     |  // @audit-issue Switch > to >= and < to <=
 492 |  if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) {

     |  // @audit-issue Switch > to >= and < to <=
 580 |  for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

     |  // @audit-issue Switch > to >= and < to <=
 593 |  return (_bitMap & (1 << _index)) > 0;

     |  // @audit-issue Switch > to >= and < to <=
 631 |  require(_pubdataCommitments.length > 0, "pl");

     |  // @audit-issue Switch > to >= and < to <=
 636 |  for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {

     |  // @audit-issue Switch > to >= and < to <=
 667 |  for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
GitHub: [114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L114), [142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289), [311](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L311), [351](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351), [405](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L405), [429](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L429), [482](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L482), [485](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L485), [492](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L492), [580](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580), [593](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L593), [631](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631), [636](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636), [667](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-issue Switch > to >= and < to <=
 208 |  for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {
```
GitHub: [208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Switch > to >= and < to <=
 158 |  require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

     |  // @audit-issue Switch > to >= and < to <=
 277 |  if (refundRecipient.code.length > 0) {

     |  // @audit-issue Switch > to >= and < to <=
 356 |  for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {
```
GitHub: [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158), [277](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L277), [356](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Switch > to >= and < to <=
 226 |  for (uint256 i = 0; i < _factoryDeps.length; ++i) {

     |  // @audit-issue Switch > to >= and < to <=
 239 |  _newProtocolVersion > previousProtocolVersion,
```
GitHub: [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226), [239](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L239)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

     |  // @audit-issue Switch > to >= and < to <=
  26 |  require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words
```
GitHub: [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L26)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

     |  // @audit-issue Switch > to >= and < to <=
 101 |  for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {

     |  // @audit-issue Switch > to >= and < to <=
 107 |  require(selectors.length > 0, "B"); // no functions for diamond cut

     |  // @audit-issue Switch > to >= and < to <=
 132 |  require(_facet.code.length > 0, "G");

     |  // @audit-issue Switch > to >= and < to <=
 138 |  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

     |  // @audit-issue Switch > to >= and < to <=
 155 |  require(_facet.code.length > 0, "K");

     |  // @audit-issue Switch > to >= and < to <=
 158 |  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

     |  // @audit-issue Switch > to >= and < to <=
 178 |  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
```
GitHub: [101](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101), [107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L138), [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L155), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158), [178](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L178)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

     |  // @audit-issue Switch > to >= and < to <=
  24 |  require(pathLength > 0, "xc");

     |  // @audit-issue Switch > to >= and < to <=
  25 |  require(pathLength < 256, "bt");

     |  // @audit-issue Switch > to >= and < to <=
  26 |  require(_index < (1 << pathLength), "px");

     |  // @audit-issue Switch > to >= and < to <=
  29 |  for (uint256 i; i < pathLength; i = i.uncheckedInc()) {
```
GitHub: [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24), [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L25), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L26), [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L29)


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

     |  // @audit-issue Switch > to >= and < to <=
 102 |  if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {

     |  // @audit-issue Switch > to >= and < to <=
 132 |  uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS &&
```
GitHub: [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L102), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L132)


```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

     |  // @audit-issue Switch > to >= and < to <=
  24 |  require(_delegateTo.code.length > 0, "Delegatee is an EOA");
```
GitHub: [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L24)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue Switch > to >= and < to <=
  61 |  for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {

     |  // @audit-issue Switch > to >= and < to <=
  63 |  require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

     |  // @audit-issue Switch > to >= and < to <=
 127 |  for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

     |  // @audit-issue Switch > to >= and < to <=
 159 |  for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
```
GitHub: [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L63), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L127), [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L159)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Switch > to >= and < to <=
  48 |  _address > address(MAX_SYSTEM_CONTRACT_ADDRESS) &&

     |  // @audit-issue Switch > to >= and < to <=
 248 |  for (uint256 i = 0; i < deploymentsLength; ++i) {

     |  // @audit-issue Switch > to >= and < to <=
 253 |  for (uint256 i = 0; i < deploymentsLength; ++i) {

     |  // @audit-issue Switch > to >= and < to <=
 265 |  require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

     |  // @audit-issue Switch > to >= and < to <=
 303 |  require(knownCodeMarker > 0, "The code hash is not known");

     |  // @audit-issue Switch > to >= and < to <=
 332 |  if (value > 0) {

     |  // @audit-issue Switch > to >= and < to <=
 339 |  if (value > 0) {
```
GitHub: [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L48), [248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L248), [253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L253), [265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L265), [303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L303), [332](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L332), [339](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L339)


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

     |  // @audit-issue Switch > to >= and < to <=
  38 |  for (uint256 i = 0; i < immutablesLength; ++i) {
```
GitHub: [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L38)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

     |  // @audit-issue Switch > to >= and < to <=
  30 |  for (uint256 i = 0; i < hashesLen; ++i) {
```
GitHub: [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L30)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Switch > to >= and < to <=
 206 |  for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

     |  // @audit-issue Switch > to >= and < to <=
 218 |  for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

     |  // @audit-issue Switch > to >= and < to <=
 222 |  while (nodesOnCurrentLevel > 1) {

     |  // @audit-issue Switch > to >= and < to <=
 224 |  for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

     |  // @audit-issue Switch > to >= and < to <=
 236 |  for (uint256 i = 0; i < numberOfMessages; ++i) {

     |  // @audit-issue Switch > to >= and < to <=
 254 |  for (uint256 i = 0; i < numberOfBytecodes; ++i) {
```
GitHub: [206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L206), [218](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L218), [222](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L222), [224](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L224), [236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L236), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L254)


```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

     |  // @audit-issue Switch > to >= and < to <=
  53 |  uint256 userGas = gasInContext > MSG_VALUE_SIMULATOR_STIPEND_GAS
```
GitHub: [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L53)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-issue Switch > to >= and < to <=
 156 |  return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);

     |  // @audit-issue Switch > to >= and < to <=
 156 |  return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);
```
GitHub: [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L156), [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L156)


```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

     |  // @audit-issue Switch > to >= and < to <=
  36 |  for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
GitHub: [36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Switch > to >= and < to <=
 119 |  return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;

     |  // @audit-issue Switch > to >= and < to <=
 144 |  if (blockNumber <= _block || blockNumber - _block > 256) {

     |  // @audit-issue Switch > to >= and < to <=
 146 |  } else if (_block < currentVirtualBlockUpgradeInfo.virtualBlockStartBatch) {

     |  // @audit-issue Switch > to >= and < to <=
 152 |  currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0

     |  // @audit-issue Switch > to >= and < to <=
 245 |  require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

     |  // @audit-issue Switch > to >= and < to <=
 287 |  require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

     |  // @audit-issue Switch > to >= and < to <=
 355 |  require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

     |  // @audit-issue Switch > to >= and < to <=
 387 |  _l2BlockTimestamp > currentL2BlockTimestamp,

     |  // @audit-issue Switch > to >= and < to <=
 413 |  require(currentBatchNumber > 0, "The current batch number must be greater than 0");

     |  // @audit-issue Switch > to >= and < to <=
 430 |  _newTimestamp > currentBlockTimestamp,

     |  // @audit-issue Switch > to >= and < to <=
 451 |  require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");
```
GitHub: [119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L119), [144](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L144), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L146), [152](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L152), [245](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L245), [287](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L287), [355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L355), [387](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L387), [413](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L413), [430](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L430), [451](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L451)


```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

     |  // @audit-issue Switch > to >= and < to <=
  49 |  uint256 pubdataAllowance = _maxTotalGas > expectedForCompute ? _maxTotalGas - expectedForCompute : 0;

     |  // @audit-issue Switch > to >= and < to <=
  63 |  uint256 pubdataSpent = pubdataPublishedAfter > pubdataPublishedBefore
```
GitHub: [49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L49), [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L63)


```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

     |  // @audit-issue Switch > to >= and < to <=
  26 |  if (_val < 128) {

     |  // @audit-issue Switch > to >= and < to <=
  62 |  if (_len < 56) {

     |  // @audit-issue Switch > to >= and < to <=
  86 |  if (_number > type(uint128).max) {

     |  // @audit-issue Switch > to >= and < to <=
  90 |  if (_number > type(uint64).max) {

     |  // @audit-issue Switch > to >= and < to <=
  94 |  if (_number > type(uint32).max) {

     |  // @audit-issue Switch > to >= and < to <=
  98 |  if (_number > type(uint16).max) {

     |  // @audit-issue Switch > to >= and < to <=
 102 |  if (_number > type(uint8).max) {
```
GitHub: [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L26), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L62), [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L86), [90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L90), [94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L94), [98](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L98), [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L102)


```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

     |  // @audit-issue Switch > to >= and < to <=
 319 |  require(index < 10, "There are only 10 accessible registers");
```
GitHub: [319](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319)


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

     |  // @audit-issue Switch > to >= and < to <=
 378 |  if (currentAllowance < minAllowance) {
```
GitHub: [378](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L378)


```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

     |  // @audit-issue Switch > to >= and < to <=
  87 |  require(lengthInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words
```
GitHub: [87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L87)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-issue Switch > to >= and < to <=
 124 |  require(_amount > 0, "Amount cannot be zero");
```
GitHub: [124](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L124)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

     |  // @audit-issue Switch > to >= and < to <=
  40 |  if (amount < requiredETH) {
```
GitHub: [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L40)


## [G-41] Public functions not used internally can be marked as external to save gas

Public functions that aren't used internally in Solidity contracts should be made external to optimize gas usage and improve contract efficiency. External functions can only be called from outside the contract, and their arguments are directly read from the calldata, which is more gas-efficient than loading them into memory, as is the case for public functions. By using external visibility, developers can reduce gas consumption for external calls and ensure that the contract operates more cost-effectively for users. Moreover, setting the appropriate visibility level for functions also enhances code readability and maintainability, promoting a more secure and well-structured contract design. 

*Instances: 19*

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-info Context
  30 |  contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {
  :  |
     |      // @audit-issue Not called internally by this contract
  54 |      function proveL2MessageInclusion(
  55 |          uint256 _batchNumber,
  56 |          uint256 _index,
  57 |          L2Message memory _message,
  58 |          bytes32[] calldata _proof
  59 |      ) public view returns (bool) {
  :  |
     |      // @audit-issue Not called internally by this contract
  74 |      function proveL1ToL2TransactionStatus(
  75 |          bytes32 _l2TxHash,
  76 |          uint256 _l2BatchNumber,
  77 |          uint256 _l2MessageIndex,
  78 |          uint16 _l2TxNumberInBatch,
  79 |          bytes32[] calldata _merkleProof,
  80 |          TxStatus _status
  81 |      ) public view returns (bool) {
  :  |
     |      // @audit-issue Not called internally by this contract
 143 |      function l2TransactionBaseCost(
 144 |          uint256 _gasPrice,
 145 |          uint256 _l2GasLimit,
 146 |          uint256 _l2GasPerPubdataByteLimit
 147 |      ) public view returns (uint256) {
```
GitHub: [54-59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L54-L59), [74-81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L74-L81), [143-147](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L143-L147)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-info Context
  44 |  abstract contract BaseZkSyncUpgrade is ZkSyncStateTransitionBase {
  :  |
     |      // @audit-issue Not called internally by this contract
  67 |      function upgrade(ProposedUpgrade calldata _proposedUpgrade) public virtual returns (bytes32 txHash) {
```
GitHub: [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L67)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

     |  // @audit-info Context
  17 |  abstract contract BaseZkSyncUpgradeGenesis is BaseZkSyncUpgrade {
  :  |
     |      // @audit-issue Not called internally by this contract
  47 |      function upgrade(ProposedUpgrade calldata _proposedUpgrade) public virtual override returns (bytes32) {
```
GitHub: [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L47)


```solidity
File: code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

     |  // @audit-info Context
  10 |  contract DefaultUpgrade is BaseZkSyncUpgrade {
  :  |
     |      // @audit-issue Not called internally by this contract
  13 |      function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```
GitHub: [13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L13)


```solidity
File: code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

     |  // @audit-info Context
  11 |  contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {
  :  |
     |      // @audit-issue Not called internally by this contract
  14 |      function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```
GitHub: [14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L14)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_4844.sol

     |  // @audit-info Context
  12 |  contract Upgrade_4844 is BaseZkSyncUpgrade {
  :  |
     |      // @audit-issue Not called internally by this contract
  15 |      function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```
GitHub: [15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_4844.sol#L15)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol

     |  // @audit-info Context
  13 |  contract Upgrade_v1_4_1 is BaseZkSyncUpgrade {
  :  |
     |      // @audit-issue Not called internally by this contract
  33 |      function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```
GitHub: [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol#L33)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-info Context
  23 |  contract ContractDeployer is IContractDeployer, ISystemContract {
  :  |
     |      // @audit-issue Not called internally by this contract
  40 |      function extendedAccountVersion(address _address) public view returns (AccountAbstractionVersion) {
```
GitHub: [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L40)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-info Context
  27 |  contract NonceHolder is INonceHolder, ISystemContract {
  :  |
     |      // @audit-issue Not called internally by this contract
  57 |      function getRawNonce(address _address) public view returns (uint256) {
  :  |
     |      // @audit-issue Not called internally by this contract
  65 |      function increaseMinNonce(uint256 _value) public onlySystemCall returns (uint256 oldMinNonce) {
  :  |
     |      // @audit-issue Not called internally by this contract
  82 |      function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall {
  :  |
     |      // @audit-issue Not called internally by this contract
 102 |      function getValueUnderNonce(uint256 _key) public view returns (uint256) {
```
GitHub: [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L57), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L65), [82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L82), [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L102)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-info Context
  17 |  contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract {
  :  |
     |      // @audit-issue Not called internally by this contract
 190 |      function getBlockNumber() public view returns (uint128) {
  :  |
     |      // @audit-issue Not called internally by this contract
 198 |      function getBlockTimestamp() public view returns (uint128) {
```
GitHub: [190](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L190), [198](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L198)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

     |  // @audit-info Context
  15 |  contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {
  :  |
     |      // @audit-issue Not called internally by this contract
 159 |      function name() public view override returns (string memory) {
  :  |
     |      // @audit-issue Not called internally by this contract
 165 |      function symbol() public view override returns (string memory) {
  :  |
     |      // @audit-issue Not called internally by this contract
 171 |      function decimals() public view override returns (uint8) {
```
GitHub: [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L159), [165](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L165), [171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L171)


## [G-42] Redundant type conversion

Casting a variable to its own type is redundant and a waste of gas.

*Instances: 17*

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue `uint256(protocolVersion)` is a redundant type cast
 268 |  bytes32(uint256(protocolVersion)),

     |  // @audit-issue `bytes32(storedBatchZero)` is a redundant type cast
 273 |  bytes32(storedBatchZero),
```
GitHub: [268](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L268), [273](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L273)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue `bytes1(_newBatch.pubdataCommitments[0])` is a redundant type cast
  39 |  uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));
```
GitHub: [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L39)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-issue `address(s.bridgehub)` is a redundant type cast
  48 |  return address(s.bridgehub);

     |  // @audit-issue `address(s.stateTransitionManager)` is a redundant type cast
  53 |  return address(s.stateTransitionManager);

     |  // @audit-issue `address(s.baseToken)` is a redundant type cast
  58 |  return address(s.baseToken);

     |  // @audit-issue `address(s.baseTokenBridge)` is a redundant type cast
  63 |  return address(s.baseTokenBridge);
```
GitHub: [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L48), [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L53), [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L58), [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L63)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue `uint256(_priorityOpParams.l2GasPrice)` is a redundant type cast
 300 |  maxFeePerGas: uint256(_priorityOpParams.l2GasPrice),

     |  // @audit-issue `uint256(_priorityOpParams.txId)` is a redundant type cast
 304 |  nonce: uint256(_priorityOpParams.txId),
```
GitHub: [300](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L300), [304](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L304)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

     |  // @audit-issue `uint256(_queue.tail - _queue.head)` is a redundant type cast
  46 |  return uint256(_queue.tail - _queue.head);
```
GitHub: [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L46)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue `bytes1(_compressedStateDiffs[stateDiffPtr])` is a redundant type cast
 143 |  uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

     |  // @audit-issue `bytes1(_compressedStateDiffs[stateDiffPtr])` is a redundant type cast
 174 |  uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
```
GitHub: [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L143), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L174)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue `bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr])` is a redundant type cast
 280 |  uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==

     |  // @audit-issue `bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr])` is a redundant type cast
 289 |  uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));
```
GitHub: [280](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L280), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L289)


```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

     |  // @audit-issue `uint160(MAX_SYSTEM_CONTRACT_ADDRESS)` is a redundant type cast
 339 |  return uint160(_address) <= uint160(MAX_SYSTEM_CONTRACT_ADDRESS);
```
GitHub: [339](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L339)


```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

     |  // @audit-issue `uint32(Utils.safeCastToU32(data.length))` is a redundant type cast
  83 |  uint32 dataLength = uint32(Utils.safeCastToU32(data.length));
```
GitHub: [83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L83)


```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

     |  // @audit-issue `uint32(Utils.safeCastToU32(data.length))` is a redundant type cast
  44 |  uint32 dataLength = uint32(Utils.safeCastToU32(data.length));
```
GitHub: [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L44)


## [G-43] Refactor modifiers to call a local function

Modifiers code is copied in all instances where it's used, increasing bytecode size. If deployment gas costs are a concern for this contract, refactoring modifiers into functions can reduce bytecode size significantly at the cost of one JUMP.

*Instances: 33*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Refactor to a function to save gas
  68 |  modifier onlyBridgehub() {

     |  // @audit-issue Refactor to a function to save gas
  74 |  modifier onlyBridgehubOrEra(uint256 _chainId) {

     |  // @audit-issue Refactor to a function to save gas
  83 |  modifier onlyLegacyBridge() {
```
GitHub: [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L68), [74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L74), [83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L83)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Refactor to a function to save gas
  45 |  modifier onlyOwnerOrAdmin() {
```
GitHub: [45](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L45)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Refactor to a function to save gas
  58 |  modifier onlySelf() {

     |  // @audit-issue Refactor to a function to save gas
  64 |  modifier onlySecurityCouncil() {

     |  // @audit-issue Refactor to a function to save gas
  70 |  modifier onlyOwnerOrSecurityCouncil() {
```
GitHub: [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L58), [64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L64), [70](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L70)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Refactor to a function to save gas
  65 |  modifier onlyBridgehub() {

     |  // @audit-issue Refactor to a function to save gas
  71 |  modifier onlyOwnerOrAdmin() {
```
GitHub: [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L65), [71](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L71)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Refactor to a function to save gas
  61 |  modifier onlyChainAdmin(uint256 _chainId) {

     |  // @audit-issue Refactor to a function to save gas
  67 |  modifier onlyValidator(uint256 _chainId) {
```
GitHub: [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L61), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L67)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

     |  // @audit-issue Refactor to a function to save gas
  15 |  modifier onlyAdmin() {

     |  // @audit-issue Refactor to a function to save gas
  21 |  modifier onlyValidator() {

     |  // @audit-issue Refactor to a function to save gas
  26 |  modifier onlyStateTransitionManager() {

     |  // @audit-issue Refactor to a function to save gas
  31 |  modifier onlyBridgehub() {

     |  // @audit-issue Refactor to a function to save gas
  36 |  modifier onlyAdminOrStateTransitionManager() {

     |  // @audit-issue Refactor to a function to save gas
  44 |  modifier onlyValidatorOrStateTransitionManager() {

     |  // @audit-issue Refactor to a function to save gas
  52 |  modifier onlyBaseTokenBridge() {
```
GitHub: [15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L15), [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L21), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L26), [31](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L31), [36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L36), [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L44), [52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L52)


```solidity
File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

     |  // @audit-issue Refactor to a function to save gas
  41 |  modifier reentrancyGuardInitializer() {

     |  // @audit-issue Refactor to a function to save gas
  68 |  modifier nonReentrant() {
```
GitHub: [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L41), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L68)


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

     |  // @audit-issue Refactor to a function to save gas
  25 |  modifier onlyDeployer() {
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L25)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Refactor to a function to save gas
  28 |  modifier onlySelf() {
```
GitHub: [28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L28)


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

     |  // @audit-issue Refactor to a function to save gas
  28 |  modifier ignoreNonBootloader() {

     |  // @audit-issue Refactor to a function to save gas
  45 |  modifier ignoreInDelegateCall() {
```
GitHub: [28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L28), [45](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L45)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

     |  // @audit-issue Refactor to a function to save gas
  19 |  modifier onlyCompressor() {
```
GitHub: [19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L19)


```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

     |  // @audit-issue Refactor to a function to save gas
  20 |  modifier onlySystemCall() {

     |  // @audit-issue Refactor to a function to save gas
  30 |  modifier onlyCallFromSystemContract() {

     |  // @audit-issue Refactor to a function to save gas
  40 |  modifier onlyCallFrom(address caller) {

     |  // @audit-issue Refactor to a function to save gas
  47 |  modifier onlyCallFromBootloader() {

     |  // @audit-issue Refactor to a function to save gas
  54 |  modifier onlyCallFromForceDeployer() {
```
GitHub: [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L20), [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L30), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L40), [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L47), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L54)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

     |  // @audit-issue Refactor to a function to save gas
 129 |  modifier onlyBridge() {

     |  // @audit-issue Refactor to a function to save gas
 134 |  modifier onlyNextVersion(uint8 _version) {
```
GitHub: [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L129), [134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L134)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

     |  // @audit-issue Refactor to a function to save gas
  64 |  modifier onlyBridge() {
```
GitHub: [64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L64)


## [G-44] Remove empty functions to save gas

Empty function body in solidity is not recommended, removing it can not only save deployment gas but save execution gas in the function selector code by shifting other functions up.

*Instances: 7*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Consider removing this empty function
  60 |  function initialize() external reentrancyGuardInitializer {}
```
GitHub: [60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L60)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Consider removing this empty function
  38 |  constructor() reentrancyGuardInitializer {}
```
GitHub: [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

     |  // @audit-issue Consider removing this empty function
  19 |  constructor() reentrancyGuardInitializer {}
```
GitHub: [19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Consider removing this empty function
 263 |  function _upgradeL1Contract(bytes calldata _customCallDataForUpgrade) internal virtual {}

     |  // @audit-issue Consider removing this empty function
 269 |  function _postUpgrade(bytes calldata _customCallDataForUpgrade) internal virtual {}
```
GitHub: [263](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L263), [269](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L269)


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

     |  // @audit-issue Consider removing this empty function
 125 |  function executeTransactionFromOutside(Transaction calldata _transaction) external payable override {
 126 |      // Behave the same as for fallback/receive, just execute nothing, returns nothing
 127 |  }
```
GitHub: [125-127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L125-L127)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

     |  // @audit-issue Consider removing this empty function
  70 |  function postTransaction(
  71 |      bytes calldata _context,
  72 |      Transaction calldata _transaction,
  73 |      bytes32,
  74 |      bytes32,
  75 |      ExecutionResult _txResult,
  76 |      uint256 _maxRefundedGas
  77 |  ) external payable override {
  78 |      // Refunds are not supported yet.
  79 |  }
```
GitHub: [70-79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L70-L79)


## [G-45] Replace OpenZeppelin components with Solady equivalents to save gas

The following OpenZeppelin imports have a [Solady](https://github.com/Vectorized/solady/tree/main) equivalent, as such they can be used to save GAS as Solady modules have been specifically designed to be as GAS efficient as possible.

*Instances: 4*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Consider using the Solady implementation
   5 |  import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L5)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Consider using the Solady implementation
   9 |  import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";
```
GitHub: [9](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L9)


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

     |  // @audit-issue Consider using the Solady implementation
   5 |  import "../openzeppelin/token/ERC20/IERC20.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L5)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

     |  // @audit-issue Consider using the Solady implementation
   5 |  import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L5)


## [G-46] Same cast is done multiple times

It's cheaper to do it once, and store the result to a variable.

*Instances: 50*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-info Contains redundant type conversions
  63 |  function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
  64 |      require(msg.sender == address(sharedBridge), "Not shared bridge");
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
  67 |      IERC20(_token).safeTransfer(address(sharedBridge), amount);
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
  65 |      uint256 amount = IERC20(_token).balanceOf(address(this));
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
  67 |      IERC20(_token).safeTransfer(address(sharedBridge), amount);

     |  // @audit-info Contains redundant type conversions
 160 |  function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 161 |      uint256 balanceBefore = _token.balanceOf(address(sharedBridge));
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 162 |      _token.safeTransferFrom(_from, address(sharedBridge), _amount);
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 163 |      uint256 balanceAfter = _token.balanceOf(address(sharedBridge));
```
GitHub: [64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L161), [162](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L162), [163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L163)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-info Contains redundant type conversions
 116 |  function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 127 |          uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 128 |          uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 131 |          uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

     |  // @audit-info Contains redundant type conversions
 487 |  function _parseL2WithdrawalMessage(
 488 |      uint256 _chainId,
 489 |      bytes memory _l2ToL1message
 490 |  ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 504 |      if (bytes4(functionSignature) == IMailbox.finalizeEthWithdrawal.selector) {
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 509 |      } else if (bytes4(functionSignature) == IL1ERC20Bridge.finalizeWithdrawal.selector) {
```
GitHub: [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127), [128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L128), [131](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131), [504](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L504), [509](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L509)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-info Contains redundant type conversions
 114 |  function createNewChain(
 115 |      uint256 _chainId,
 116 |      address _stateTransitionManager,
 117 |      address _baseToken,
 118 |      uint256, //_salt
 119 |      address _admin,
 120 |      bytes calldata _initData
 121 |  ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 130 |      require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 140 |          address(sharedBridge),

     |  // @audit-info Contains redundant type conversions
 262 |  function requestL2TransactionTwoBridges(
 263 |      L2TransactionRequestTwoBridgesOuter calldata _request
 264 |  ) external payable override nonReentrant returns (bytes32 canonicalTxHash) {
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 288 |      L2TransactionRequestTwoBridgesInner memory outputRequest = IL1SharedBridge(_request.secondBridgeAddress)
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 318 |      IL1SharedBridge(_request.secondBridgeAddress).bridgehubConfirmL2Transaction(
```
GitHub: [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130), [140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L140), [288](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L288), [318](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L318)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-info Contains redundant type conversions
 130 |  function _processL2Logs(
 131 |      CommitBatchInfo calldata _newBatch,
 132 |      bytes32 _expectedSystemContractUpgradeTxHash
 133 |  ) internal pure returns (LogProcessingOutput memory logOutput) {
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 149 |          require(!_checkBit(processedLogs, uint8(logKey)), "kp");
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 150 |          processedLogs = _setBit(processedLogs, uint8(logKey));
  :  |
     |              // @audit-issue Cache this type conversion result that is used in multiple locations
 164 |              logOutput.packedBatchAndL2BlockTimestamp = uint256(logValue);
  :  |
     |              // @audit-issue Cache this type conversion result that is used in multiple locations
 173 |              logOutput.numberOfLayer1Txs = uint256(logValue);
```
GitHub: [149](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L149), [150](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L150), [164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L164), [173](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L173)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-info Contains redundant type conversions
 110 |  function verifyCompressedStateDiffs(
 111 |      uint256 _numberOfStateDiffs,
 112 |      uint256 _enumerationIndexSize,
 113 |      bytes calldata _stateDiffs,
 114 |      bytes calldata _compressedStateDiffs
 115 |  ) external payable onlyCallFrom(address(L1_MESSENGER_CONTRACT)) returns (bytes32 stateDiffHash) {
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 143 |          uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 174 |          uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 143 |          uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 174 |          uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
```
GitHub: [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L143), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L174), [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L143), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L174)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-info Contains redundant type conversions
 258 |  function _nonSystemDeployOnAddress(
 259 |      bytes32 _bytecodeHash,
 260 |      address _newAddress,
 261 |      AccountAbstractionVersion _aaVersion,
 262 |      bytes calldata _input
 263 |  ) internal {
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 265 |      require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 269 |          ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0,
```
GitHub: [265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L265), [269](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L269)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-info Contains redundant type conversions
 194 |  function publishPubdataAndClearState(
 195 |      bytes calldata _totalL2ToL1PubdataAndStateDiffs
 196 |  ) external onlyCallFromBootloader {
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 200 |      uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 233 |      uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 237 |          uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 251 |      uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 300 |      uint32 numberOfStateDiffs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 200 |      uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 233 |      uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 237 |          uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 251 |      uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
  :  |
     |              // @audit-issue Cache this type conversion result that is used in multiple locations
 256 |              bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 300 |      uint32 numberOfStateDiffs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 280 |          uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 289 |      uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 280 |          uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 289 |      uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));
```
GitHub: [200](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L200), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L233), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L237), [251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L251), [300](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L300), [200](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L200), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L233), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L237), [251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L251), [256](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L256), [300](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L300), [280](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L280), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L289), [280](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L280), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L289)


```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

     |  // @audit-info Contains redundant type conversions
  60 |  function _encodeLength(uint64 _len, uint256 _offset) private pure returns (bytes memory encoded) {
  :  |
     |              // @audit-issue Cache this type conversion result that is used in multiple locations
  66 |              uint256 hbs = _highestByteSet(uint256(_len));
  :  |
     |              // @audit-issue Cache this type conversion result that is used in multiple locations
  72 |              uint256 shiftedVal = uint256(_len) << (lbs * 8);
```
GitHub: [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L66), [72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L72)


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

     |  // @audit-info Contains redundant type conversions
 362 |  function processPaymasterInput(Transaction calldata _transaction) internal {
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
 377 |          uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);
  :  |
     |              // @audit-issue Cache this type conversion result that is used in multiple locations
 382 |              IERC20(token).safeApprove(paymaster, 0);
     |              // @audit-issue Cache this type conversion result that is used in multiple locations
 383 |              IERC20(token).safeApprove(paymaster, minAllowance);
```
GitHub: [377](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377), [382](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L382), [383](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L383)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-info Contains redundant type conversions
 109 |  function _deployL2Token(address _l1Token, bytes calldata _data) internal returns (address) {
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 113 |      L2StandardERC20(address(l2Token)).bridgeInitialize(_l1Token, _data);
  :  |
     |      // @audit-issue Cache this type conversion result that is used in multiple locations
 115 |      return address(l2Token);
```
GitHub: [113](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L113), [115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L115)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

     |  // @audit-info Contains redundant type conversions
  14 |  function validateAndPayForPaymasterTransaction(
  15 |      bytes32,
  16 |      bytes32,
  17 |      Transaction calldata _transaction
  18 |  ) external payable returns (bytes4 magic, bytes memory context) {
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
  35 |          uint256 providedAllowance = IERC20(token).allowance(userAddress, thisAddress);
  :  |
     |          // @audit-issue Cache this type conversion result that is used in multiple locations
  50 |          try IERC20(token).transferFrom(userAddress, thisAddress, amount) {} catch (bytes memory revertReason) {
```
GitHub: [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L35), [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L50)


## [G-47] Simple checks for zero can be done using assembly to save gas

Using assembly for simple zero checks on unsigned integers can save gas due to lower-level, optimized operations. 

*Instances: 67*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 141 |  require(_amount != 0, "0T"); // empty deposit

 186 |  require(amount != 0, "2T"); // empty deposit
```
GitHub: [141](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141), [186](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 158 |  require(msg.value == 0, "ShB m.v > 0 b d.it");

 200 |  require(_depositAmount == 0, "ShB wrong withdraw amount");

 202 |  require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");

 208 |  require(amount != 0, "6T"); // empty deposit amount
```
GitHub: [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L158), [200](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L200), [202](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202), [208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L208)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 122 |  require(_chainId != 0, "Bridgehub: chainId cannot be 0");

 225 |  require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");
```
GitHub: [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L122), [225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

 107 |  if (timestamp == 0) {
```
GitHub: [107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L107)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

  25 |  require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

  90 |  require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed
```
GitHub: [90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 237 |  if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {

 284 |  require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");

 291 |  bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);

 361 |  if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {

 633 |  require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");
```
GitHub: [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L237), [284](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L284), [291](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L291), [361](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L361), [633](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L633)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

 169 |  if (selectorsArrayLen != 0) {
```
GitHub: [169](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L169)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 186 |  if (_l2ProtocolUpgradeTx.txType == 0) {

 251 |  s.l2SystemContractsUpgradeBatchNumber == 0,
```
GitHub: [186](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L186), [251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L251)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

  35 |  s.l2SystemContractsUpgradeBatchNumber == 0,
```
GitHub: [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L35)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

  23 |  require(_bytecode.length % 32 == 0, "pq");
```
GitHub: [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 194 |  if (selectorsLength == 0) {

 213 |  if (selectorPosition != 0) {

 250 |  if (lastSelectorPosition == 0) {

 280 |  require(_calldata.length == 0, "H"); // Non-empty calldata for zero address
```
GitHub: [194](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L194), [213](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L213), [250](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L250), [280](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L280)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

  30 |  currentHash = (_index % 2 == 0)
```
GitHub: [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L30)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

  50 |  require(_transaction.paymaster == 0, "uc");

  51 |  require(_transaction.value == 0, "ud");

  52 |  require(_transaction.maxFeePerGas == 0, "uq");

  53 |  require(_transaction.maxPriorityFeePerGas == 0, "ux");

  54 |  require(_transaction.reserved[0] == 0, "ue");

  56 |  require(_transaction.reserved[2] == 0, "ug");

  57 |  require(_transaction.reserved[3] == 0, "uo");

  58 |  require(_transaction.signature.length == 0, "uh");

  59 |  require(_transaction.paymasterInput.length == 0, "ul1");

  60 |  require(_transaction.reservedDynamic.length == 0, "um");
```
GitHub: [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L50), [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L51), [52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L52), [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L53), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L54), [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L56), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L57), [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L58), [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L59), [60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L60)


```solidity
File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

  58 |  require(lockSlotOldValue == 0, "1B");
```
GitHub: [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L58)


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

  96 |  if (_transaction.reserved[0] != 0) {
```
GitHub: [96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L96)


```solidity
File: code/system-contracts/contracts/Compressor.sol

 130 |  if (enumIndex != 0) {

 146 |  uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

 162 |  if (enumIndex == 0) {

 177 |  uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

 229 |  if (_operation == 0 || _operation == 3) {
```
GitHub: [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L130), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L146), [162](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L162), [177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L177), [229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L229)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

 273 |  require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied");

 350 |  require(value == 0, "The value must be zero if we do not call the constructor");
```
GitHub: [273](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L273), [350](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L350)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

  47 |  if (getMarker(_bytecodeHash) == 0) {
```
GitHub: [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L47)


```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

  30 |  isSystemCall = (mask & MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT) != 0;

  62 |  if (value != 0) {
```
GitHub: [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L30), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L62)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

  85 |  require(_value != 0, "Nonce value cannot be set to 0");

  88 |  if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {
```
GitHub: [85](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L85), [88](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L88)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

 268 |  if (virtualBlockUpgradeInfo.virtualBlockFinishL2Block != 0) {

 277 |  if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {

 277 |  if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {

 289 |  } else if (_maxVirtualBlocksToCreate == 0) {

 360 |  if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {

 360 |  if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {

 373 |  require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");
```
GitHub: [268](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L268), [277](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L277), [277](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L277), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L289), [360](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L360), [360](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L360), [373](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L373)


```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

  73 |  if (pubdataCost != 0) {
```
GitHub: [73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L73)


```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

 131 |  if (_value == 0) {
```
GitHub: [131](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L131)


```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

  29 |  encoded[0] = (_val == 0) ? bytes1(uint8(128)) : bytes1(uint8(_val));
```
GitHub: [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L29)


```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

 332 |  return (callFlags & 2) != 0;
```
GitHub: [332](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L332)


```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

  98 |  if (value == 0) {
```
GitHub: [98](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L98)


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

  95 |  return _addr == uint256(uint160(address(BASE_TOKEN_SYSTEM_CONTRACT))) || _addr == 0;

 184 |  if (_transaction.reserved[0] != 0) {
```
GitHub: [95](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L95), [184](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L184)


```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

  84 |  require(_bytecode.length % 32 == 0, "po");
```
GitHub: [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L84)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

  92 |  require(msg.value == 0, "Value should be 0 for ERC20 bridge");
```
GitHub: [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92)


```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

  59 |  if (value == 0) {
```
GitHub: [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L59)


## [G-48] Splitting `require()` statements that use `&&` saves gas

See [this issue](https://github.com/code-423n4/2022-01-xdefi-findings/issues/128) which describes the fact that there is a larger deployment gas cost, but with enough runtime calls, the change ends up being cheaper by **3 gas**.

*Instances: 5*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

  75 |  require(
  76 |      msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
  77 |      "L1SharedBridge: not bridgehub or era chain"
  78 |  );
```
GitHub: [75-78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75-L78)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 668 |  require(
 669 |      (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
 670 |          (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
 671 |      "bh"
 672 |  );
```
GitHub: [668-672](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L668-L672)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

  41 |  require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash
```
GitHub: [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L41)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

  77 |  require(
  78 |      _nonceOrdering == AccountNonceOrdering.Arbitrary &&
  79 |          currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
  80 |      "It is only possible to change from sequential to arbitrary ordering"
  81 |  );
```
GitHub: [77-81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L77-L81)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

  76 |  require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
```
GitHub: [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L76)


## [G-49] Stack variable is only used once

If the variable is only accessed once, it's cheaper to use the assigned value directly that one time, and save the **3 gas** the extra stack assignment would spend.

*Instances: 96*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Used once: request
 187 |  ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
  :  |
     |          // @audit-issue Used once: l2TxCalldata
 217 |          bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, amount);

     |  // @audit-issue Used once: gettersData
 249 |  bytes memory gettersData = _getERC20Getters(_l1Token);

     |      // @audit-issue Used once: name
 256 |      bytes memory name = bytes("Ether");
     |      // @audit-issue Used once: symbol
 257 |      bytes memory symbol = bytes("ETH");
     |      // @audit-issue Used once: decimals
 258 |      bytes memory decimals = abi.encode(uint8(18));
  :  |
     |  // @audit-issue Used once: data1
 262 |  (, bytes memory data1) = _token.staticcall(abi.encodeCall(IERC20Metadata.name, ()));
     |  // @audit-issue Used once: data2
 263 |  (, bytes memory data2) = _token.staticcall(abi.encodeCall(IERC20Metadata.symbol, ()));
     |  // @audit-issue Used once: data3
 264 |  (, bytes memory data3) = _token.staticcall(abi.encodeCall(IERC20Metadata.decimals, ()));

     |  // @audit-issue Used once: messageParams
 430 |  MessageParams memory messageParams = MessageParams({

     |  // @audit-issue Used once: l2TxCalldata
 571 |  bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);
  :  |
     |      // @audit-issue Used once: request
 584 |      L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
```
GitHub: [187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L187), [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L217), [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L249), [256](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L256), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L257), [258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L258), [262](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L262), [263](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L263), [264](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L264), [430](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L430), [571](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L571), [584](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L584)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Used once: _log
 168 |  L2Log memory _log,
```
GitHub: [168](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L168)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Used once: batchZero
  92 |  IExecutor.StoredBatchInfo memory batchZero = IExecutor.StoredBatchInfo(

     |  // @audit-issue Used once: systemContextCalldata
 180 |  bytes memory systemContextCalldata = abi.encodeCall(ISystemContext.setChainId, (_chainId));
     |  // @audit-issue Used once: uintEmptyArray
 181 |  uint256[] memory uintEmptyArray;
     |  // @audit-issue Used once: bytesEmptyArray
 182 |  bytes[] memory bytesEmptyArray;
  :  |
     |  // @audit-issue Used once: proposedUpgrade
 204 |  ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
  :  |
     |  // @audit-issue Used once: emptyArray
 221 |  Diamond.FacetCut[] memory emptyArray;
     |  // @audit-issue Used once: cutData
 222 |  Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({
```
GitHub: [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L92), [180](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L180), [181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L181), [182](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L182), [204](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L204), [221](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L221), [222](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L222)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

     |  // @audit-issue Used once: _diamondCut
  11 |  constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
```
GitHub: [11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue Used once: oldFeeParams
  72 |  FeeParams memory oldFeeParams = s.feeParams;
```
GitHub: [72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L72)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Used once: _lastCommittedBatchData
 200 |  StoredBatchInfo memory _lastCommittedBatchData,

     |  // @audit-issue Used once: _lastCommittedBatchData
 209 |  StoredBatchInfo memory _lastCommittedBatchData,

     |  // @audit-issue Used once: priorityOp
 312 |  PriorityOperation memory priorityOp = s.priorityQueue.popFront();

     |  // @audit-issue Used once: verifierParams
 396 |  VerifierParams memory verifierParams = s.verifierParams;

     |  // @audit-issue Used once: _blobCommitments
 503 |  bytes32[] memory _blobCommitments,
     |  // @audit-issue Used once: _blobHashes
 504 |  bytes32[] memory _blobHashes

     |  // @audit-issue Used once: _blobCommitments
 540 |  bytes32[] memory _blobCommitments,
     |  // @audit-issue Used once: _blobHashes
 541 |  bytes32[] memory _blobHashes

     |  // @audit-issue Used once: _storedBatchInfo
 587 |  function _hashStoredBatchInfo(StoredBatchInfo memory _storedBatchInfo) internal pure returns (bytes32) {

     |  // @audit-issue Used once: precompileInput
 610 |  bytes memory precompileInput = abi.encodePacked(_versionedHash, _openingPoint, _openingValueCommitmentProof);
  :  |
     |  // @audit-issue Used once: data
 612 |  (bool success, bytes memory data) = POINT_EVALUATION_PRECOMPILE_ADDR.staticcall(precompileInput);

     |  // @audit-issue Used once: data
 680 |  (bool success, bytes memory data) = s.blobVersionedHashRetriever.staticcall(abi.encode(_index));
```
GitHub: [200](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L200), [209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L209), [312](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L312), [396](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L396), [503](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L503), [504](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L504), [540](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L540), [541](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L541), [587](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L587), [610](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L610), [612](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L612), [680](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L680)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-issue Used once: facetToSelectors
 210 |  Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];
```
GitHub: [210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L210)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Used once: _request
  48 |  BridgehubL2TransactionRequest memory _request

     |  // @audit-issue Used once: _message
  57 |  L2Message memory _message,

     |  // @audit-issue Used once: _log
  67 |  L2Log memory _log,

     |  // @audit-issue Used once: l2Log
  92 |  L2Log memory l2Log = L2Log({

     |  // @audit-issue Used once: _calldata
 261 |  bytes memory _calldata,

     |      // @audit-issue Used once: _calldata
 291 |      bytes memory _calldata,
     |      // @audit-issue Used once: _factoryDeps
 292 |      bytes[] memory _factoryDeps
     |  // @audit-issue Used once: transaction
 293 |  ) internal pure returns (L2CanonicalTransaction memory transaction) {

     |  // @audit-issue Used once: _calldata
 318 |  bytes memory _calldata,

     |  // @audit-issue Used once: hashedFactoryDeps
 353 |  function _hashFactoryDeps(bytes[] memory _factoryDeps) internal pure returns (uint256[] memory hashedFactoryDeps) {
```
GitHub: [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L48), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L57), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L67), [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L92), [261](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L261), [291](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L291), [292](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L292), [293](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L293), [318](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L318), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L353)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Used once: oldVerifierParams
 155 |  VerifierParams memory oldVerifierParams = s.verifierParams;
```
GitHub: [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L155)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

     |  // @audit-issue Used once: oldFacet
 140 |  SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
```
GitHub: [140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L140)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

     |  // @audit-issue Used once: _operation
  55 |  function pushBack(Queue storage _queue, PriorityOperation memory _operation) internal {

     |  // @audit-issue Used once: priorityOperation
  72 |  function popFront(Queue storage _queue) internal returns (PriorityOperation memory priorityOperation) {
```
GitHub: [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L55), [72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L72)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol

     |  // @audit-issue Used once: oldFeeParams
  25 |  FeeParams memory oldFeeParams = s.feeParams;
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol#L25)


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

     |  // @audit-issue Used once: encodedGasPrice
  56 |  bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);
     |  // @audit-issue Used once: encodedGasLimit
  57 |  bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

     |  // @audit-issue Used once: encodedChainId
 143 |  bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);
     |  // @audit-issue Used once: encodedNonce
 144 |  bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);
     |  // @audit-issue Used once: encodedGasPrice
 145 |  bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);
     |  // @audit-issue Used once: encodedGasLimit
 146 |  bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);
     |  // @audit-issue Used once: encodedTo
 147 |  bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
     |  // @audit-issue Used once: encodedValue
 148 |  bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);

     |  // @audit-issue Used once: encodedChainId
 236 |  bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);
     |  // @audit-issue Used once: encodedNonce
 237 |  bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);
     |  // @audit-issue Used once: encodedMaxPriorityFeePerGas
 238 |  bytes memory encodedMaxPriorityFeePerGas = RLPEncoder.encodeUint256(_transaction.maxPriorityFeePerGas);
     |  // @audit-issue Used once: encodedMaxFeePerGas
 239 |  bytes memory encodedMaxFeePerGas = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);
     |  // @audit-issue Used once: encodedGasLimit
 240 |  bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);
     |  // @audit-issue Used once: encodedTo
 241 |  bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
     |  // @audit-issue Used once: encodedValue
 242 |  bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);
```
GitHub: [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L56), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L57), [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L143), [144](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L144), [145](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L145), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L146), [147](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L147), [148](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L148), [236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L236), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L237), [238](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L238), [239](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L239), [240](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L240), [241](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L241), [242](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L242)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Used once: _newInfo
  58 |  function _storeAccountInfo(address _address, AccountInfo memory _newInfo) internal {

     |  // @audit-issue Used once: returnData
 343 |  bytes memory returnData = EfficientCall.mimicCall(gasleft(), _newAddress, _input, _sender, true, _isSystem);
  :  |
     |  // @audit-issue Used once: immutables
 347 |  ImmutableData[] memory immutables = abi.decode(returnData, (ImmutableData[]));
```
GitHub: [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L58), [343](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L343), [347](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L347)


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

     |  // @audit-issue Used once: _signature
 159 |  function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {
```
GitHub: [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L159)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Used once: l2ToL1Log
  75 |  L2ToL1Log memory l2ToL1Log = L2ToL1Log({

     |  // @audit-issue Used once: l2ToL1Log
 125 |  L2ToL1Log memory l2ToL1Log = L2ToL1Log({
```
GitHub: [75](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L75), [125](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L125)


```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

     |  // @audit-issue Used once: message
  76 |  bytes memory message = _getL1WithdrawMessage(_l1Receiver, amount);

     |  // @audit-issue Used once: message
  89 |  bytes memory message = _getExtendedWithdrawMessage(_l1Receiver, amount, msg.sender, _additionalData);

     |  // @audit-issue Used once: _additionalData
 121 |  bytes memory _additionalData
```
GitHub: [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L76), [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L89), [121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L121)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-issue Used once: accountInfo
  83 |  IContractDeployer.AccountInfo memory accountInfo = DEPLOYER_SYSTEM_CONTRACT.getAccountInfo(msg.sender);
```
GitHub: [83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L83)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Used once: newBlockInfo
 459 |  BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp});

     |  // @audit-issue Used once: newBlockInfo
 476 |  BlockInfo memory newBlockInfo = BlockInfo({number: uint128(_number), timestamp: uint128(_newTimestamp)});
```
GitHub: [459](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L459), [476](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L476)


```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

     |  // @audit-issue Used once: returnData
  64 |  ) internal returns (bytes memory returnData) {

     |  // @audit-issue Used once: returnData
  78 |  ) internal view returns (bytes memory returnData) {

     |  // @audit-issue Used once: returnData
  92 |  ) internal returns (bytes memory returnData) {

     |  // @audit-issue Used once: returnData
 112 |  ) internal returns (bytes memory returnData) {

     |  // @audit-issue Used once: returnData
 215 |  function _verifyCallResult(bool _success) private pure returns (bytes memory returnData) {
```
GitHub: [64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L64), [78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L78), [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L92), [112](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L112), [215](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L215)


```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

     |  // @audit-issue Used once: encoded
  11 |  function encodeAddress(address _val) internal pure returns (bytes memory encoded) {
```
GitHub: [11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L11)


```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

     |  // @audit-issue Used once: data
  76 |  function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

     |      // @audit-issue Used once: data
 127 |      bytes memory data
     |  // @audit-issue Used once: returnData
 128 |  ) internal returns (bool success, bytes memory returnData) {

     |      // @audit-issue Used once: data
 154 |      bytes memory data
     |  // @audit-issue Used once: returnData
 155 |  ) internal returns (bytes memory returnData) {
```
GitHub: [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L76), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L127), [128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L128), [154](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L154), [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L155)


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

     |  // @audit-issue Used once: encodedGasPrice
 159 |  bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);
     |  // @audit-issue Used once: encodedGasLimit
 160 |  bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);

     |  // @audit-issue Used once: encodedChainId
 228 |  bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);
     |  // @audit-issue Used once: encodedNonce
 229 |  bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);
     |  // @audit-issue Used once: encodedGasPrice
 230 |  bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);
     |  // @audit-issue Used once: encodedGasLimit
 231 |  bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);
     |  // @audit-issue Used once: encodedTo
 232 |  bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
     |  // @audit-issue Used once: encodedValue
 233 |  bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);
```
GitHub: [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L159), [160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L160), [228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L228), [229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L229), [230](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L230), [231](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L231), [232](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L232), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L233)


## [G-50] Structs can be packed into fewer storage slots

Each slot saved can avoid an extra Gsset (20000 gas) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings

*Instances: 9*

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol
Struct ZkSyncStateTransitionStorage

     |  // @audit-issue Can improve from 44 to 47 slots:
     |  // slot[0] = baseTokenGasPriceMultiplierDenominator (uint128/16 bytes), baseTokenGasPriceMultiplierNominator (uint128/16 bytes)
     |  // slot[1] = zkPorterIsAvailable (bool/1 bytes), baseTokenBridge (address/20 bytes)
     |  // slot[2] = baseToken (address/20 bytes)
     |  // slot[3] = stateTransitionManager (address/20 bytes)
     |  // slot[4] = bridgehub (address/20 bytes)
     |  // slot[5] = blobVersionedHashRetriever (address/20 bytes)
     |  // slot[6] = pendingAdmin (address/20 bytes)
     |  // slot[7] = admin (address/20 bytes)
     |  // slot[8] = __DEPRECATED_allowList (address/20 bytes)
     |  // slot[9] = verifier (contract/20 bytes)
     |  // slot[10] = __DEPRECATED_pendingGovernor (address/20 bytes)
     |  // slot[11] = __DEPRECATED_governor (address/20 bytes)
     |  // slot[12] = chainId (uint256/32 bytes)
     |  // slot[13] = l2SystemContractsUpgradeBatchNumber (uint256/32 bytes)
     |  // slot[14] = l2SystemContractsUpgradeTxHash (bytes32/32 bytes)
     |  // slot[15] = protocolVersion (uint256/32 bytes)
     |  // slot[16] = __DEPRECATED_totalDepositedAmountPerUser (mapping/32 bytes)
     |  // slot[17] = __DEPRECATED_withdrawnAmountInWindow (uint256/32 bytes)
     |  // slot[18] = __DEPRECATED_lastWithdrawalLimitReset (uint256/32 bytes)
     |  // slot[19] = isEthWithdrawalFinalized (mapping/32 bytes)
     |  // slot[20] = priorityTxMaxGasLimit (uint256/32 bytes)
     |  // slot[21] = l2DefaultAccountBytecodeHash (bytes32/32 bytes)
     |  // slot[22] = l2BootloaderBytecodeHash (bytes32/32 bytes)
     |  // slot[23] = l2LogsRootHashes (mapping/32 bytes)
     |  // slot[24] = storedBatchHashes (mapping/32 bytes)
     |  // slot[25] = totalBatchesCommitted (uint256/32 bytes)
     |  // slot[26] = totalBatchesVerified (uint256/32 bytes)
     |  // slot[27] = totalBatchesExecuted (uint256/32 bytes)
     |  // slot[28] = feeParams (struct/64 bytes)
     |  // slot[29] = feeParams (struct/64 bytes)
     |  // slot[30] = __DEPRECATED_upgrades (struct/96 bytes)
     |  // slot[31] = __DEPRECATED_upgrades (struct/96 bytes)
     |  // slot[32] = __DEPRECATED_upgrades (struct/96 bytes)
     |  // slot[33] = verifierParams (struct/96 bytes)
     |  // slot[34] = verifierParams (struct/96 bytes)
     |  // slot[35] = verifierParams (struct/96 bytes)
     |  // slot[36] = priorityQueue (struct/96 bytes)
     |  // slot[37] = priorityQueue (struct/96 bytes)
     |  // slot[38] = priorityQueue (struct/96 bytes)
     |  // slot[39] = __DEPRECATED_diamondCutStorage (32[7]/224 bytes)
     |  // slot[40] = __DEPRECATED_diamondCutStorage (32[7]/224 bytes)
     |  // slot[41] = __DEPRECATED_diamondCutStorage (32[7]/224 bytes)
     |  // slot[42] = __DEPRECATED_diamondCutStorage (32[7]/224 bytes)
     |  // slot[43] = __DEPRECATED_diamondCutStorage (32[7]/224 bytes)
     |  // slot[44] = __DEPRECATED_diamondCutStorage (32[7]/224 bytes)
     |  // slot[45] = __DEPRECATED_diamondCutStorage (32[7]/224 bytes)
     |  // slot[46] = validators (mapping/32 bytes)
  66 |  struct ZkSyncStateTransitionStorage {
  67 |      /// @dev Storage of variables needed for deprecated diamond cut facet
  68 |      uint256[7] __DEPRECATED_diamondCutStorage;
  69 |      /// @notice Address which will exercise critical changes to the Diamond Proxy (upgrades, freezing & unfreezing). Replaced by STM
  70 |      address __DEPRECATED_governor;
  71 |      /// @notice Address that the governor proposed as one that will replace it
  72 |      address __DEPRECATED_pendingGovernor;
  73 |      /// @notice List of permitted validators
  74 |      mapping(address validatorAddress => bool isValidator) validators;
  75 |      /// @dev Verifier contract. Used to verify aggregated proof for batches
  76 |      IVerifier verifier;
  77 |      /// @notice Total number of executed batches i.e. batches[totalBatchesExecuted] points at the latest executed batch
  78 |      /// (batch 0 is genesis)
  79 |      uint256 totalBatchesExecuted;
  80 |      /// @notice Total number of proved batches i.e. batches[totalBatchesProved] points at the latest proved batch
  81 |      uint256 totalBatchesVerified;
  82 |      /// @notice Total number of committed batches i.e. batches[totalBatchesCommitted] points at the latest committed
  83 |      /// batch
  84 |      uint256 totalBatchesCommitted;
  85 |      /// @dev Stored hashed StoredBatch for batch number
  86 |      mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
  87 |      /// @dev Stored root hashes of L2 -> L1 logs
  88 |      mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;
  89 |      /// @dev Container that stores transactions requested from L1
  90 |      PriorityQueue.Queue priorityQueue;
  91 |      /// @dev The smart contract that manages the list with permission to call contract functions
  92 |      address __DEPRECATED_allowList;
  93 |      /// @notice Part of the configuration parameters of ZKP circuits. Used as an input for the verifier smart contract
  94 |      VerifierParams verifierParams;
  95 |      /// @notice Bytecode hash of bootloader program.
  96 |      /// @dev Used as an input to zkp-circuit.
  97 |      bytes32 l2BootloaderBytecodeHash;
  98 |      /// @notice Bytecode hash of default account (bytecode for EOA).
  99 |      /// @dev Used as an input to zkp-circuit.
 100 |      bytes32 l2DefaultAccountBytecodeHash;
 101 |      /// @dev Indicates that the porter may be touched on L2 transactions.
 102 |      /// @dev Used as an input to zkp-circuit.
 103 |      bool zkPorterIsAvailable;
 104 |      /// @dev The maximum number of the L2 gas that a user can request for L1 -> L2 transactions
 105 |      /// @dev This is the maximum number of L2 gas that is available for the "body" of the transaction, i.e.
 106 |      /// without overhead for proving the batch.
 107 |      uint256 priorityTxMaxGasLimit;
 108 |      /// @dev Storage of variables needed for upgrade facet
 109 |      UpgradeStorage __DEPRECATED_upgrades;
 110 |      /// @dev A mapping L2 batch number => message number => flag.
 111 |      /// @dev The L2 -> L1 log is sent for every withdrawal, so this mapping is serving as
 112 |      /// a flag to indicate that the message was already processed.
 113 |      /// @dev Used to indicate that eth withdrawal was already processed
 114 |      mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;
 115 |      /// @dev The most recent withdrawal time and amount reset
 116 |      uint256 __DEPRECATED_lastWithdrawalLimitReset;
 117 |      /// @dev The accumulated withdrawn amount during the withdrawal limit window
 118 |      uint256 __DEPRECATED_withdrawnAmountInWindow;
 119 |      /// @dev A mapping user address => the total deposited amount by the user
 120 |      mapping(address => uint256) __DEPRECATED_totalDepositedAmountPerUser;
 121 |      /// @dev Stores the protocol version. Note, that the protocol version may not only encompass changes to the
 122 |      /// smart contracts, but also to the node behavior.
 123 |      uint256 protocolVersion;
 124 |      /// @dev Hash of the system contract upgrade transaction. If 0, then no upgrade transaction needs to be done.
 125 |      bytes32 l2SystemContractsUpgradeTxHash;
 126 |      /// @dev Batch number where the upgrade transaction has happened. If 0, then no upgrade transaction has happened
 127 |      /// yet.
 128 |      uint256 l2SystemContractsUpgradeBatchNumber;
 129 |      /// @dev Address which will exercise non-critical changes to the Diamond Proxy (changing validator set & unfreezing)
 130 |      address admin;
 131 |      /// @notice Address that the admin proposed as one that will replace admin role
 132 |      address pendingAdmin;
 133 |      /// @dev Fee params used to derive gasPrice for the L1->L2 transactions. For L2 transactions,
 134 |      /// the bootloader gives enough freedom to the operator.
 135 |      FeeParams feeParams;
 136 |      /// @dev Address of the blob versioned hash getter smart contract used for EIP-4844 versioned hashes.
 137 |      address blobVersionedHashRetriever;
 138 |      /// new fields
 139 |      /// @dev The chainId of the chain
 140 |      uint256 chainId;
 141 |      /// @dev The address of the bridgehub
 142 |      address bridgehub;
 143 |      /// @dev The address of the StateTransitionManager
 144 |      address stateTransitionManager;
 145 |      /// @dev The address of the baseToken contract. Eth is address(1)
 146 |      address baseToken;
 147 |      /// @dev The address of the baseTokenbridge. Eth also uses the shared bridge
 148 |      address baseTokenBridge;
 149 |      /// @notice gasPriceMultiplier for each baseToken, so that each L1->L2 transaction pays for its transaction on the destination
 150 |      /// we multiply by the nominator, and divide by the denominator
 151 |      uint128 baseTokenGasPriceMultiplierNominator;
 152 |      uint128 baseTokenGasPriceMultiplierDenominator;
 153 |  }
```
GitHub: [66-153](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L66-L153)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
Struct ProposedUpgrade

     |  // @audit-issue Can improve from 29 to 30 slots:
     |  // slot[0] = verifier (address/20 bytes)
     |  // slot[1] = newProtocolVersion (uint256/32 bytes)
     |  // slot[2] = upgradeTimestamp (uint256/32 bytes)
     |  // slot[3] = postUpgradeCalldata (bytes/32 bytes)
     |  // slot[4] = l1ContractsUpgradeCalldata (bytes/32 bytes)
     |  // slot[5] = defaultAccountHash (bytes32/32 bytes)
     |  // slot[6] = bootloaderHash (bytes32/32 bytes)
     |  // slot[7] = verifierParams (struct/96 bytes)
     |  // slot[8] = verifierParams (struct/96 bytes)
     |  // slot[9] = verifierParams (struct/96 bytes)
     |  // slot[10] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[11] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[12] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[13] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[14] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[15] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[16] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[17] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[18] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[19] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[20] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[21] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[22] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[23] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[24] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[25] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[26] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[27] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[28] = l2ProtocolUpgradeTx (struct/608 bytes)
     |  // slot[29] = factoryDeps ([]/32 bytes)
  28 |  struct ProposedUpgrade {
  29 |      L2CanonicalTransaction l2ProtocolUpgradeTx;
  30 |      bytes[] factoryDeps;
  31 |      bytes32 bootloaderHash;
  32 |      bytes32 defaultAccountHash;
  33 |      address verifier;
  34 |      VerifierParams verifierParams;
  35 |      bytes l1ContractsUpgradeCalldata;
  36 |      bytes postUpgradeCalldata;
  37 |      uint256 upgradeTimestamp;
  38 |      uint256 newProtocolVersion;
  39 |  }
```
GitHub: [28-39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L28-L39)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
Struct FacetCut

     |  // @audit-issue Can improve from 4 to 3 slots:
     |  // slot[0] = isFreezable (bool/1 bytes), facet (address/20 bytes)
     |  // slot[1] = selectors ([]/32 bytes)
     |  // slot[2] = action (enum/32 bytes)
  62 |  struct FacetCut {
  63 |      address facet;
  64 |      Action action;
  65 |      bool isFreezable;
  66 |      bytes4[] selectors;
  67 |  }
```
GitHub: [62-67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L62-L67)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol
Struct InitializeData

     |  // @audit-issue Can improve from 17 to 19 slots:
     |  // slot[0] = blobVersionedHashRetriever (address/20 bytes)
     |  // slot[1] = verifier (contract/20 bytes)
     |  // slot[2] = baseTokenBridge (address/20 bytes)
     |  // slot[3] = baseToken (address/20 bytes)
     |  // slot[4] = validatorTimelock (address/20 bytes)
     |  // slot[5] = admin (address/20 bytes)
     |  // slot[6] = stateTransitionManager (address/20 bytes)
     |  // slot[7] = bridgehub (address/20 bytes)
     |  // slot[8] = priorityTxMaxGasLimit (uint256/32 bytes)
     |  // slot[9] = l2DefaultAccountBytecodeHash (bytes32/32 bytes)
     |  // slot[10] = l2BootloaderBytecodeHash (bytes32/32 bytes)
     |  // slot[11] = storedBatchZero (bytes32/32 bytes)
     |  // slot[12] = protocolVersion (uint256/32 bytes)
     |  // slot[13] = feeParams (struct/64 bytes)
     |  // slot[14] = feeParams (struct/64 bytes)
     |  // slot[15] = verifierParams (struct/96 bytes)
     |  // slot[16] = verifierParams (struct/96 bytes)
     |  // slot[17] = verifierParams (struct/96 bytes)
     |  // slot[18] = chainId (uint256/32 bytes)
  25 |  struct InitializeData {
  26 |      uint256 chainId;
  27 |      address bridgehub;
  28 |      address stateTransitionManager;
  29 |      uint256 protocolVersion;
  30 |      address admin;
  31 |      address validatorTimelock;
  32 |      address baseToken;
  33 |      address baseTokenBridge;
  34 |      bytes32 storedBatchZero;
  35 |      IVerifier verifier;
  36 |      VerifierParams verifierParams;
  37 |      bytes32 l2BootloaderBytecodeHash;
  38 |      bytes32 l2DefaultAccountBytecodeHash;
  39 |      uint256 priorityTxMaxGasLimit;
  40 |      FeeParams feeParams;
  41 |      address blobVersionedHashRetriever;
  42 |  }
```
GitHub: [25-42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L25-L42)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol
Struct InitializeDataNewChain

     |  // @audit-issue Can improve from 8 to 10 slots:
     |  // slot[0] = blobVersionedHashRetriever (address/20 bytes)
     |  // slot[1] = verifier (contract/20 bytes)
     |  // slot[2] = priorityTxMaxGasLimit (uint256/32 bytes)
     |  // slot[3] = l2DefaultAccountBytecodeHash (bytes32/32 bytes)
     |  // slot[4] = feeParams (struct/64 bytes)
     |  // slot[5] = feeParams (struct/64 bytes)
     |  // slot[6] = verifierParams (struct/96 bytes)
     |  // slot[7] = verifierParams (struct/96 bytes)
     |  // slot[8] = verifierParams (struct/96 bytes)
     |  // slot[9] = l2BootloaderBytecodeHash (bytes32/32 bytes)
  51 |  struct InitializeDataNewChain {
  52 |      IVerifier verifier;
  53 |      VerifierParams verifierParams;
  54 |      bytes32 l2BootloaderBytecodeHash;
  55 |      bytes32 l2DefaultAccountBytecodeHash;
  56 |      uint256 priorityTxMaxGasLimit;
  57 |      FeeParams feeParams;
  58 |      address blobVersionedHashRetriever;
  59 |  }
```
GitHub: [51-59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L51-L59)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol
Struct StoredBatchInfo

     |  // @audit-issue Can improve from 8 to 7 slots:
     |  // slot[0] = indexRepeatedStorageChanges (uint64/8 bytes), batchNumber (uint64/8 bytes)
     |  // slot[1] = commitment (bytes32/32 bytes)
     |  // slot[2] = timestamp (uint256/32 bytes)
     |  // slot[3] = l2LogsTreeRoot (bytes32/32 bytes)
     |  // slot[4] = priorityOperationsHash (bytes32/32 bytes)
     |  // slot[5] = numberOfLayer1Txs (uint256/32 bytes)
     |  // slot[6] = batchHash (bytes32/32 bytes)
  83 |  struct StoredBatchInfo {
  84 |      uint64 batchNumber;
  85 |      bytes32 batchHash;
  86 |      uint64 indexRepeatedStorageChanges;
  87 |      uint256 numberOfLayer1Txs;
  88 |      bytes32 priorityOperationsHash;
  89 |      bytes32 l2LogsTreeRoot;
  90 |      uint256 timestamp;
  91 |      bytes32 commitment;
  92 |  }
```
GitHub: [83-92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L83-L92)


```solidity
File: code/contracts/ethereum/contracts/common/Messaging.sol
Struct L2CanonicalTransaction

     |  // @audit-issue Can improve from 18 to 19 slots:
     |  // slot[0] = reservedDynamic (bytes/32 bytes)
     |  // slot[1] = paymasterInput (bytes/32 bytes)
     |  // slot[2] = factoryDeps ([]/32 bytes)
     |  // slot[3] = signature (bytes/32 bytes)
     |  // slot[4] = data (bytes/32 bytes)
     |  // slot[5] = value (uint256/32 bytes)
     |  // slot[6] = nonce (uint256/32 bytes)
     |  // slot[7] = paymaster (uint256/32 bytes)
     |  // slot[8] = maxPriorityFeePerGas (uint256/32 bytes)
     |  // slot[9] = maxFeePerGas (uint256/32 bytes)
     |  // slot[10] = gasPerPubdataByteLimit (uint256/32 bytes)
     |  // slot[11] = gasLimit (uint256/32 bytes)
     |  // slot[12] = to (uint256/32 bytes)
     |  // slot[13] = from (uint256/32 bytes)
     |  // slot[14] = reserved (32[4]/128 bytes)
     |  // slot[15] = reserved (32[4]/128 bytes)
     |  // slot[16] = reserved (32[4]/128 bytes)
     |  // slot[17] = reserved (32[4]/128 bytes)
     |  // slot[18] = txType (uint256/32 bytes)
  98 |  struct L2CanonicalTransaction {
  99 |      uint256 txType;
 100 |      uint256 from;
 101 |      uint256 to;
 102 |      uint256 gasLimit;
 103 |      uint256 gasPerPubdataByteLimit;
 104 |      uint256 maxFeePerGas;
 105 |      uint256 maxPriorityFeePerGas;
 106 |      uint256 paymaster;
 107 |      uint256 nonce;
 108 |      uint256 value;
 109 |      // In the future, we might want to add some
 110 |      // new fields to the struct. The `txData` struct
 111 |      // is to be passed to account and any changes to its structure
 112 |      // would mean a breaking change to these accounts. To prevent this,
 113 |      // we should keep some fields as "reserved"
 114 |      // It is also recommended that their length is fixed, since
 115 |      // it would allow easier proof integration (in case we will need
 116 |      // some special circuit for preprocessing transactions)
 117 |      uint256[4] reserved;
 118 |      bytes data;
 119 |      bytes signature;
 120 |      uint256[] factoryDeps;
 121 |      bytes paymasterInput;
 122 |      // Reserved dynamic type for the future use-case. Using it should be avoided,
 123 |      // But it is still here, just in case we want to enable some additional functionality
 124 |      bytes reservedDynamic;
 125 |  }
```
GitHub: [98-125](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L98-L125)


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol
Struct Transaction

     |  // @audit-issue Can improve from 18 to 19 slots:
     |  // slot[0] = reservedDynamic (bytes/32 bytes)
     |  // slot[1] = paymasterInput (bytes/32 bytes)
     |  // slot[2] = factoryDeps ([]/32 bytes)
     |  // slot[3] = signature (bytes/32 bytes)
     |  // slot[4] = data (bytes/32 bytes)
     |  // slot[5] = value (uint256/32 bytes)
     |  // slot[6] = nonce (uint256/32 bytes)
     |  // slot[7] = paymaster (uint256/32 bytes)
     |  // slot[8] = maxPriorityFeePerGas (uint256/32 bytes)
     |  // slot[9] = maxFeePerGas (uint256/32 bytes)
     |  // slot[10] = gasPerPubdataByteLimit (uint256/32 bytes)
     |  // slot[11] = gasLimit (uint256/32 bytes)
     |  // slot[12] = to (uint256/32 bytes)
     |  // slot[13] = from (uint256/32 bytes)
     |  // slot[14] = reserved (32[4]/128 bytes)
     |  // slot[15] = reserved (32[4]/128 bytes)
     |  // slot[16] = reserved (32[4]/128 bytes)
     |  // slot[17] = reserved (32[4]/128 bytes)
     |  // slot[18] = txType (uint256/32 bytes)
  25 |  struct Transaction {
  26 |      // The type of the transaction.
  27 |      uint256 txType;
  28 |      // The caller.
  29 |      uint256 from;
  30 |      // The callee.
  31 |      uint256 to;
  32 |      // The gasLimit to pass with the transaction.
  33 |      // It has the same meaning as Ethereum's gasLimit.
  34 |      uint256 gasLimit;
  35 |      // The maximum amount of gas the user is willing to pay for a byte of pubdata.
  36 |      uint256 gasPerPubdataByteLimit;
  37 |      // The maximum fee per gas that the user is willing to pay.
  38 |      // It is akin to EIP1559's maxFeePerGas.
  39 |      uint256 maxFeePerGas;
  40 |      // The maximum priority fee per gas that the user is willing to pay.
  41 |      // It is akin to EIP1559's maxPriorityFeePerGas.
  42 |      uint256 maxPriorityFeePerGas;
  43 |      // The transaction's paymaster. If there is no paymaster, it is equal to 0.
  44 |      uint256 paymaster;
  45 |      // The nonce of the transaction.
  46 |      uint256 nonce;
  47 |      // The value to pass with the transaction.
  48 |      uint256 value;
  49 |      // In the future, we might want to add some
  50 |      // new fields to the struct. The `txData` struct
  51 |      // is to be passed to account and any changes to its structure
  52 |      // would mean a breaking change to these accounts. In order to prevent this,
  53 |      // we should keep some fields as "reserved".
  54 |      // It is also recommended that their length is fixed, since
  55 |      // it would allow easier proof integration (in case we will need
  56 |      // some special circuit for preprocessing transactions).
  57 |      uint256[4] reserved;
  58 |      // The transaction's calldata.
  59 |      bytes data;
  60 |      // The signature of the transaction.
  61 |      bytes signature;
  62 |      // The properly formatted hashes of bytecodes that must be published on L1
  63 |      // with the inclusion of this transaction. Note, that a bytecode has been published
  64 |      // before, the user won't pay fees for its republishing.
  65 |      bytes32[] factoryDeps;
  66 |      // The input to the paymaster.
  67 |      bytes paymasterInput;
  68 |      // Reserved dynamic type for the future use-case. Using it should be avoided,
  69 |      // But it is still here, just in case we want to enable some additional functionality.
  70 |      bytes reservedDynamic;
  71 |  }
```
GitHub: [25-71](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L25-L71)


```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol
Struct Transaction

     |  // @audit-issue Can improve from 18 to 19 slots:
     |  // slot[0] = reservedDynamic (bytes/32 bytes)
     |  // slot[1] = paymasterInput (bytes/32 bytes)
     |  // slot[2] = factoryDeps ([]/32 bytes)
     |  // slot[3] = signature (bytes/32 bytes)
     |  // slot[4] = data (bytes/32 bytes)
     |  // slot[5] = value (uint256/32 bytes)
     |  // slot[6] = nonce (uint256/32 bytes)
     |  // slot[7] = paymaster (uint256/32 bytes)
     |  // slot[8] = maxPriorityFeePerGas (uint256/32 bytes)
     |  // slot[9] = maxFeePerGas (uint256/32 bytes)
     |  // slot[10] = gasPerPubdataByteLimit (uint256/32 bytes)
     |  // slot[11] = gasLimit (uint256/32 bytes)
     |  // slot[12] = to (uint256/32 bytes)
     |  // slot[13] = from (uint256/32 bytes)
     |  // slot[14] = reserved (32[4]/128 bytes)
     |  // slot[15] = reserved (32[4]/128 bytes)
     |  // slot[16] = reserved (32[4]/128 bytes)
     |  // slot[17] = reserved (32[4]/128 bytes)
     |  // slot[18] = txType (uint256/32 bytes)
 117 |  struct Transaction {
 118 |      // The type of the transaction.
 119 |      uint256 txType;
 120 |      // The caller.
 121 |      uint256 from;
 122 |      // The callee.
 123 |      uint256 to;
 124 |      // The gasLimit to pass with the transaction.
 125 |      // It has the same meaning as Ethereum's gasLimit.
 126 |      uint256 gasLimit;
 127 |      // The maximum amount of gas the user is willing to pay for a byte of pubdata.
 128 |      uint256 gasPerPubdataByteLimit;
 129 |      // The maximum fee per gas that the user is willing to pay.
 130 |      // It is akin to EIP1559's maxFeePerGas.
 131 |      uint256 maxFeePerGas;
 132 |      // The maximum priority fee per gas that the user is willing to pay.
 133 |      // It is akin to EIP1559's maxPriorityFeePerGas.
 134 |      uint256 maxPriorityFeePerGas;
 135 |      // The transaction's paymaster. If there is no paymaster, it is equal to 0.
 136 |      uint256 paymaster;
 137 |      // The nonce of the transaction.
 138 |      uint256 nonce;
 139 |      // The value to pass with the transaction.
 140 |      uint256 value;
 141 |      // In the future, we might want to add some
 142 |      // new fields to the struct. The `txData` struct
 143 |      // is to be passed to account and any changes to its structure
 144 |      // would mean a breaking change to these accounts. In order to prevent this,
 145 |      // we should keep some fields as "reserved".
 146 |      // It is also recommended that their length is fixed, since
 147 |      // it would allow easier proof integration (in case we will need
 148 |      // some special circuit for preprocessing transactions).
 149 |      uint256[4] reserved;
 150 |      // The transaction's calldata.
 151 |      bytes data;
 152 |      // The signature of the transaction.
 153 |      bytes signature;
 154 |      // The properly formatted hashes of bytecodes that must be published on L1
 155 |      // with the inclusion of this transaction. Note, that a bytecode has been published
 156 |      // before, the user won't pay fees for its republishing.
 157 |      bytes32[] factoryDeps;
 158 |      // The input to the paymaster.
 159 |      bytes paymasterInput;
 160 |      // Reserved dynamic type for the future use-case. Using it should be avoided,
 161 |      // But it is still here, just in case we want to enable some additional functionality.
 162 |      bytes reservedDynamic;
 163 |  }
```
GitHub: [117-163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L117-L163)


## [G-51] Subtraction can potentially be marked `unchecked` to save gas

In Solidity 0.8.x and above, arithmetic operations like subtraction automatically check for underflows and overflows, and revert the transaction if such a condition is met. This built-in safety feature provides a layer of security against potential numerical errors. However, these automatic checks also come with additional gas costs.

In some situations, you may already have a guard condition, like a require() statement or an if statement, that ensures the safety of the arithmetic operation. In such cases, the automatic check becomes redundant and leads to unnecessary gas expenditure.

For example, you may have a function that subtracts a smaller number from a larger one, and you may have already verified that the smaller number is indeed smaller. In this case, you're already sure that the subtraction operation won't underflow, so there's no need for the automatic check.

In these situations, you can use the unchecked { } block around the subtraction operation to skip the automatic check. This will reduce gas costs and make your contract more efficient, without sacrificing security. However, it's critical to use unchecked { } only when you're absolutely sure that the operation is safe.

*Instances: 69*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 165 |  return balanceAfter - balanceBefore;
```
GitHub: [165](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L165)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 123 |  chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
 124 |  balanceAfter -
 125 |  balanceBefore;

     |  // @audit-issue Use unchecked to save gas, if possible
 132 |  require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");

     |  // @audit-issue Use unchecked to save gas, if possible
 178 |  return balanceAfter - balanceBefore;
```
GitHub: [123-125](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L123-L125), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132), [178](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L178)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  63 |  keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),

     |  // @audit-issue Use unchecked to save gas, if possible
  68 |  _newBatch.pubdataCommitments[_newBatch.pubdataCommitments.length - 32:_newBatch

     |  // @audit-issue Use unchecked to save gas, if possible
 122 |  require(block.timestamp - COMMIT_TIMESTAMP_NOT_OLDER <= batchTimestamp, "h1"); // New batch timestamp is too small
```
GitHub: [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L63), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L68), [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L122)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 172 |  uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata;
```
GitHub: [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L172)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 243 |  _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
```
GitHub: [243](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L243)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  28 |  _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
```
GitHub: [28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L28)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 233 |  uint256 lastSelectorPosition = ds.facetToSelectors[_facet].selectors.length - 1;

     |  // @audit-issue Use unchecked to save gas, if possible
 262 |  uint256 lastFacetPosition = ds.facets.length - 1;
```
GitHub: [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L233), [262](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L262)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  46 |  return uint256(_queue.tail - _queue.head);
```
GitHub: [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L46)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 118 |  txBodyGasLimit = _totalGasLimit - overhead;
```
GitHub: [118](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L118)


```solidity
File: code/contracts/ethereum/contracts/common/Config.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 114 |  bytes32 constant TWO_BRIDGES_MAGIC_VALUE = bytes32(uint256(keccak256("TWO_BRIDGES_MAGIC_VALUE")) - 1);
```
GitHub: [114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L114)


```solidity
File: code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  40 |  l1Address = address(uint160(l2Address) - offset);
```
GitHub: [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L40)


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 193 |  vEncoded = RLPEncoder.encodeUint256(vInt - 27);

     |  // @audit-issue Use unchecked to save gas, if possible
 288 |  vEncoded = RLPEncoder.encodeUint256(vInt - 27);
```
GitHub: [193](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L193), [288](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L288)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 238 |  _initialValue - convertedValue == _finalValue,

     |  // @audit-issue Use unchecked to save gas, if possible
 253 |  number >>= (256 - (_calldataSlice.length * 8));
```
GitHub: [238](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L238), [253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L253)


```solidity
File: code/system-contracts/contracts/Constants.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  94 |  uint256 constant MAX_MSG_VALUE = 2 ** 128 - 1;
```
GitHub: [94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Constants.sol#L94)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 119 |  uint256 gasSpentOnMessageHashing = gasBeforeMessageHashing - gasleft();
```
GitHub: [119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L119)


```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  43 |  balance[_from] = fromBalance - _amount;
```
GitHub: [43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L43)


```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  54 |  ? gasInContext - MSG_VALUE_SIMULATOR_STIPEND_GAS
```
GitHub: [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L54)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  89 |  require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");
```
GitHub: [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L89)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 119 |  return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;

     |  // @audit-issue Use unchecked to save gas, if possible
 144 |  if (blockNumber <= _block || blockNumber - _block > 256) {

     |  // @audit-issue Use unchecked to save gas, if possible
 248 |  bytes32 correctPrevBlockHash = _calculateLegacyL2BlockHash(_l2BlockNumber - 1);

     |  // @audit-issue Use unchecked to save gas, if possible
 255 |  _setL2BlockHash(_l2BlockNumber - 1, correctPrevBlockHash);

     |  // @audit-issue Use unchecked to save gas, if possible
 319 |  _setL2BlockHash(_l2BlockNumber - 1, _prevL2BlockHash);

     |  // @audit-issue Use unchecked to save gas, if possible
 370 |  _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),

     |  // @audit-issue Use unchecked to save gas, if possible
 376 |  bytes32 prevL2BlockHash = _getLatest257L2blockHash(currentL2BlockNumber - 1);
```
GitHub: [119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L119), [144](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L144), [248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L248), [255](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L255), [319](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L319), [370](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L370), [376](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L376)


```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  49 |  uint256 pubdataAllowance = _maxTotalGas > expectedForCompute ? _maxTotalGas - expectedForCompute : 0;

     |  // @audit-issue Use unchecked to save gas, if possible
  64 |  ? pubdataPublishedAfter - pubdataPublishedBefore
```
GitHub: [49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L49), [64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L64)


```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 261 |  uint32 shrinkTo = uint32(msg.data.length - (_data.length + dataOffset));
```
GitHub: [261](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L261)


```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  36 |  uint256 lbs = 31 - hbs;

     |  // @audit-issue Use unchecked to save gas, if possible
  71 |  uint256 lbs = 31 - hbs;
```
GitHub: [36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L36), [71](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L71)


```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

     |  // @audit-issue Use unchecked to save gas, if possible
 217 |  uint256 shifted = (meta << (256 - size - offset));

     |  // @audit-issue Use unchecked to save gas, if possible
 217 |  uint256 shifted = (meta << (256 - size - offset));

     |  // @audit-issue Use unchecked to save gas, if possible
 219 |  result = (shifted >> (256 - size));
```
GitHub: [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L217), [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L217), [219](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L219)


```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  12 |  address constant TO_L1_CALL_ADDRESS = address((1 << 16) - 1);

     |  // @audit-issue Use unchecked to save gas, if possible
  13 |  address constant CODE_ADDRESS_CALL_ADDRESS = address((1 << 16) - 2);

     |  // @audit-issue Use unchecked to save gas, if possible
  14 |  address constant PRECOMPILE_CALL_ADDRESS = address((1 << 16) - 3);

     |  // @audit-issue Use unchecked to save gas, if possible
  15 |  address constant META_CALL_ADDRESS = address((1 << 16) - 4);

     |  // @audit-issue Use unchecked to save gas, if possible
  16 |  address constant MIMIC_CALL_CALL_ADDRESS = address((1 << 16) - 5);

     |  // @audit-issue Use unchecked to save gas, if possible
  17 |  address constant SYSTEM_MIMIC_CALL_CALL_ADDRESS = address((1 << 16) - 6);

     |  // @audit-issue Use unchecked to save gas, if possible
  18 |  address constant MIMIC_CALL_BY_REF_CALL_ADDRESS = address((1 << 16) - 7);

     |  // @audit-issue Use unchecked to save gas, if possible
  19 |  address constant SYSTEM_MIMIC_CALL_BY_REF_CALL_ADDRESS = address((1 << 16) - 8);

     |  // @audit-issue Use unchecked to save gas, if possible
  20 |  address constant RAW_FAR_CALL_CALL_ADDRESS = address((1 << 16) - 9);

     |  // @audit-issue Use unchecked to save gas, if possible
  21 |  address constant RAW_FAR_CALL_BY_REF_CALL_ADDRESS = address((1 << 16) - 10);

     |  // @audit-issue Use unchecked to save gas, if possible
  22 |  address constant SYSTEM_CALL_CALL_ADDRESS = address((1 << 16) - 11);

     |  // @audit-issue Use unchecked to save gas, if possible
  23 |  address constant SYSTEM_CALL_BY_REF_CALL_ADDRESS = address((1 << 16) - 12);

     |  // @audit-issue Use unchecked to save gas, if possible
  24 |  address constant SET_CONTEXT_VALUE_CALL_ADDRESS = address((1 << 16) - 13);

     |  // @audit-issue Use unchecked to save gas, if possible
  25 |  address constant SET_PUBDATA_PRICE_CALL_ADDRESS = address((1 << 16) - 14);

     |  // @audit-issue Use unchecked to save gas, if possible
  26 |  address constant INCREMENT_TX_COUNTER_CALL_ADDRESS = address((1 << 16) - 15);

     |  // @audit-issue Use unchecked to save gas, if possible
  27 |  address constant PTR_CALLDATA_CALL_ADDRESS = address((1 << 16) - 16);

     |  // @audit-issue Use unchecked to save gas, if possible
  28 |  address constant CALLFLAGS_CALL_ADDRESS = address((1 << 16) - 17);

     |  // @audit-issue Use unchecked to save gas, if possible
  29 |  address constant PTR_RETURNDATA_CALL_ADDRESS = address((1 << 16) - 18);

     |  // @audit-issue Use unchecked to save gas, if possible
  30 |  address constant EVENT_INITIALIZE_ADDRESS = address((1 << 16) - 19);

     |  // @audit-issue Use unchecked to save gas, if possible
  31 |  address constant EVENT_WRITE_ADDRESS = address((1 << 16) - 20);

     |  // @audit-issue Use unchecked to save gas, if possible
  32 |  address constant LOAD_CALLDATA_INTO_ACTIVE_PTR_CALL_ADDRESS = address((1 << 16) - 21);

     |  // @audit-issue Use unchecked to save gas, if possible
  33 |  address constant LOAD_LATEST_RETURNDATA_INTO_ACTIVE_PTR_CALL_ADDRESS = address((1 << 16) - 22);

     |  // @audit-issue Use unchecked to save gas, if possible
  34 |  address constant PTR_ADD_INTO_ACTIVE_CALL_ADDRESS = address((1 << 16) - 23);

     |  // @audit-issue Use unchecked to save gas, if possible
  35 |  address constant PTR_SHRINK_INTO_ACTIVE_CALL_ADDRESS = address((1 << 16) - 24);

     |  // @audit-issue Use unchecked to save gas, if possible
  36 |  address constant PTR_PACK_INTO_ACTIVE_CALL_ADDRESS = address((1 << 16) - 25);

     |  // @audit-issue Use unchecked to save gas, if possible
  37 |  address constant MULTIPLICATION_HIGH_ADDRESS = address((1 << 16) - 26);

     |  // @audit-issue Use unchecked to save gas, if possible
  38 |  address constant GET_EXTRA_ABI_DATA_ADDRESS = address((1 << 16) - 27);
```
GitHub: [12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L12), [13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L13), [14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L14), [15](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L15), [16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L16), [17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L17), [18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L18), [19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L19), [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L20), [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L21), [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L22), [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L23), [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L24), [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L25), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L26), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L27), [28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L28), [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L29), [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L30), [31](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L31), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L32), [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L33), [34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L34), [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L35), [36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L36), [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L37), [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L38)


```solidity
File: code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol

     |  // @audit-issue Use unchecked to save gas, if possible
  40 |  l1Address = address(uint160(l2Address) - offset);
```
GitHub: [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L40)


```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

     |  // @audit-issue Use unchecked to save gas, if possible
   7 |  address constant SYSTEM_CALL_CALL_ADDRESS = address((1 << 16) - 11);
```
GitHub: [7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L7)


## [G-52] The result of function calls should be cached rather than re-calling the function

The instances below point to the second+ call of the function within a single function.

*Instances: 55*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Called 2 times in _depositFundsToSharedBridge()
 161 |  uint256 balanceBefore = _token.balanceOf(address(sharedBridge));

     |  // @audit-issue Called 2 times in _depositFundsToSharedBridge()
 163 |  uint256 balanceAfter = _token.balanceOf(address(sharedBridge));
```
GitHub: [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L161), [163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L163)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Called 2 times in transferFundsFromLegacy()
 127 |  uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

     |  // @audit-issue Called 2 times in transferFundsFromLegacy()
 131 |  uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

     |  // @audit-issue Called 2 times in _depositFunds()
 174 |  uint256 balanceBefore = _token.balanceOf(address(this));

     |  // @audit-issue Called 2 times in _depositFunds()
 176 |  uint256 balanceAfter = _token.balanceOf(address(this));

     |  // @audit-issue Called 3 times in _parseL2WithdrawalMessage()
 506 |  (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);

     |  // @audit-issue Called 2 times in _parseL2WithdrawalMessage()
 507 |  (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);

     |  // @audit-issue Called 3 times in _parseL2WithdrawalMessage()
 518 |  (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);

     |  // @audit-issue Called 3 times in _parseL2WithdrawalMessage()
 519 |  (l1Token, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);

     |  // @audit-issue Called 2 times in _parseL2WithdrawalMessage()
 520 |  (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);
```
GitHub: [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127), [131](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L174), [176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176), [506](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L506), [507](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L507), [518](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L518), [519](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L519), [520](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L520)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Called 2 times in execute()
 172 |  require(isOperationReady(id), "Operation must be ready before execution");

     |  // @audit-issue Called 2 times in execute()
 177 |  require(isOperationReady(id), "Operation must be ready after execution");

     |  // @audit-issue Called 2 times in executeInstant()
 191 |  require(isOperationPending(id), "Operation must be pending before execution");

     |  // @audit-issue Called 2 times in executeInstant()
 196 |  require(isOperationPending(id), "Operation must be pending after execution");
```
GitHub: [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L172), [177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L177), [191](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L191), [196](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L196)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Called 5 times in _setChainIdUpgrade()
 198 |  signature: new bytes(0),

     |  // @audit-issue Called 5 times in _setChainIdUpgrade()
 200 |  paymasterInput: new bytes(0),

     |  // @audit-issue Called 5 times in _setChainIdUpgrade()
 201 |  reservedDynamic: new bytes(0)

     |  // @audit-issue Called 5 times in _setChainIdUpgrade()
 215 |  l1ContractsUpgradeCalldata: new bytes(0),

     |  // @audit-issue Called 5 times in _setChainIdUpgrade()
 216 |  postUpgradeCalldata: new bytes(0),
```
GitHub: [198](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L198), [200](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L200), [201](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L201), [215](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L215), [216](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L216)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Called 2 times in _commitOneBatch()
  46 |  bytes32[] memory blobCommitments = new bytes32[](MAX_NUMBER_OF_BLOBS);

     |  // @audit-issue Called 2 times in _commitOneBatch()
  47 |  bytes32[] memory blobHashes = new bytes32[](MAX_NUMBER_OF_BLOBS);

     |  // @audit-issue Called 2 times in _proveBatches()
 430 |  _verifyProof(proofPublicInput, _proof);

     |  // @audit-issue Called 2 times in _proveBatches()
 433 |  _verifyProof(proofPublicInput, _proof);

     |  // @audit-issue Called 2 times in _verifyBlobInformation()
 637 |  bytes32 blobVersionedHash = _getBlobVersionedHash(versionedHashIndex);

     |  // @audit-issue Called 2 times in _verifyBlobInformation()
 662 |  bytes32 versionedHash = _getBlobVersionedHash(versionedHashIndex);
```
GitHub: [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L46), [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L47), [430](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L430), [433](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L433), [637](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L637), [662](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L662)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Called 3 times in _serializeL2Transaction()
 308 |  signature: new bytes(0),

     |  // @audit-issue Called 3 times in _serializeL2Transaction()
 310 |  paymasterInput: new bytes(0),

     |  // @audit-issue Called 3 times in _serializeL2Transaction()
 311 |  reservedDynamic: new bytes(0)
```
GitHub: [308](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L308), [310](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L310), [311](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L311)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

     |  // @audit-issue Called 2 times in validateUpgradeTransaction()
  49 |  require(_transaction.to <= type(uint160).max, "ub");

     |  // @audit-issue Called 2 times in validateUpgradeTransaction()
  55 |  require(_transaction.reserved[1] <= type(uint160).max, "uf");
```
GitHub: [49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L49), [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue Called 2 times in verifyCompressedStateDiffs()
 129 |  uint64 enumIndex = stateDiff.readUint64(84);

     |  // @audit-issue Called 2 times in verifyCompressedStateDiffs()
 138 |  uint256 initValue = stateDiff.readUint256(92);

     |  // @audit-issue Called 2 times in verifyCompressedStateDiffs()
 139 |  uint256 finalValue = stateDiff.readUint256(124);

     |  // @audit-issue Called 2 times in verifyCompressedStateDiffs()
 147 |  _verifyValueCompression(
 148 |      initValue,
 149 |      finalValue,
 150 |      operation,
 151 |      _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
 152 |  );

     |  // @audit-issue Called 2 times in verifyCompressedStateDiffs()
 161 |  uint64 enumIndex = stateDiff.readUint64(84);

     |  // @audit-issue Called 2 times in verifyCompressedStateDiffs()
 166 |  uint256 initValue = stateDiff.readUint256(92);

     |  // @audit-issue Called 2 times in verifyCompressedStateDiffs()
 167 |  uint256 finalValue = stateDiff.readUint256(124);

     |  // @audit-issue Called 2 times in verifyCompressedStateDiffs()
 178 |  _verifyValueCompression(
 179 |      initValue,
 180 |      finalValue,
 181 |      operation,
 182 |      _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
 183 |  );
```
GitHub: [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L129), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L138), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L139), [147-152](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L147-L152), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L161), [166](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L166), [167](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L167), [178-183](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L178-L183)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Called 2 times in sendL2ToL1Log()
  89 |  uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) + 2 * keccakGasCost(64);

     |  // @audit-issue Called 3 times in sendL2ToL1Log()
  89 |  uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) + 2 * keccakGasCost(64);

     |  // @audit-issue Called 2 times in sendToL1()
 117 |  uint256 gasBeforeMessageHashing = gasleft();

     |  // @audit-issue Called 2 times in sendToL1()
 119 |  uint256 gasSpentOnMessageHashing = gasBeforeMessageHashing - gasleft();

     |  // @audit-issue Called 2 times in sendToL1()
 148 |  uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) +

     |  // @audit-issue Called 4 times in sendToL1()
 150 |  keccakGasCost(64) +
```
GitHub: [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L89), [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L89), [117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L117), [119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L119), [148](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L148), [150](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L150)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Called 2 times in setL2Block()
 365 |  _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);

     |  // @audit-issue Called 2 times in setL2Block()
 392 |  _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);
```
GitHub: [365](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L365), [392](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L392)


```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

     |  // @audit-issue Called 5 times in gasBoundCall()
  40 |  uint256 expectedForCompute = gasleft() + CALL_ENTRY_OVERHEAD;

     |  // @audit-issue Called 5 times in gasBoundCall()
  46 |  require(_maxTotalGas >= gasleft(), "Gas limit is too low");

     |  // @audit-issue Called 2 times in gasBoundCall()
  51 |  uint256 pubdataPublishedBefore = REAL_SYSTEM_CONTEXT_CONTRACT.getCurrentPubdataSpent();

     |  // @audit-issue Called 5 times in gasBoundCall()
  57 |  bytes memory returnData = EfficientCall.call(gasleft(), _to, msg.value, _data, false);

     |  // @audit-issue Called 2 times in gasBoundCall()
  59 |  uint256 pubdataPublishedAfter = REAL_SYSTEM_CONTEXT_CONTRACT.getCurrentPubdataSpent();

     |  // @audit-issue Called 5 times in gasBoundCall()
  76 |  require(pubdataAllowance + gasleft() >= pubdataCost + CALL_RETURN_OVERHEAD, "Not enough gas for pubdata");
```
GitHub: [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L40), [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L46), [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L51), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L59), [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L76)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-issue Called 2 times in finalizeDeposit()
  88 |  AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||

     |  // @audit-issue Called 2 times in finalizeDeposit()
  89 |  AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
```
GitHub: [88](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L88), [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L89)


## [G-53] Time-related state variables can use smaller integer data types to save gas

Storage optimization in Solidity contracts is vital for reducing gas costs, especially when storing time-related state variables. Using `uint40`, or `int44`, for storing time values like timestamps is often sufficient, given it can represent dates up to the year 11421. By truncating larger default integer types to `uint40` or `int44`, you significantly save on storage space and consequently on gas costs for deployment and state modifications. However, ensure that the truncation does not lead to overflow issues and that the variable's size is adequate for the application's expected lifespan and precision requirements. Adopting this optimization practice contributes to more efficient and cost-effective smart contract development.

*Instances: 1*

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

  22 |  uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1);
```
GitHub: [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L22)


## [G-54] Usage of non-`uint256`/`int256` types uses more gas

When using a smaller int/uint type it first needs to be converted to it's 256 bit counterpart to be operated upon, this increases the gas cost and thus should be avoided. However it does make sense to use smaller int/uint values within structs provided you pack the struct properly. 

*Instances: 99*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Consider u/int256
 182 |  uint16 _l2TxNumberInBatch,

     |  // @audit-issue Consider u/int256
 211 |  uint16 _l2TxNumberInBatch,
```
GitHub: [182](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L182), [211](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L211)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Consider u/int256
 285 |  uint16 _l2TxNumberInBatch,

     |  // @audit-issue Consider u/int256
 312 |  uint16 _l2TxNumberInBatch,

     |  // @audit-issue Consider u/int256
 389 |  uint16 _l2TxNumberInBatch,

     |  // @audit-issue Consider u/int256
 404 |  uint16 l2TxNumberInBatch;

     |  // @audit-issue Consider u/int256
 413 |  uint16 _l2TxNumberInBatch,

     |  // @audit-issue Consider u/int256
 503 |  (uint32 functionSignature, uint256 offset) = UnsafeBytes.readUint32(_l2ToL1message, 0);

     |  // @audit-issue Consider u/int256
 618 |  uint16 _l2TxNumberInBatch,

     |  // @audit-issue Consider u/int256
 651 |  uint16 _l2TxNumberInBatch,
```
GitHub: [285](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L285), [312](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L312), [389](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L389), [404](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L404), [413](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L413), [503](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L503), [618](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L618), [651](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L651)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Consider u/int256
 181 |  uint16 _l2TxNumberInBatch,
```
GitHub: [181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L181)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Consider u/int256
  53 |  uint32 public executionDelay;

     |  // @audit-issue Consider u/int256
  55 |  constructor(address _initialOwner, uint32 _executionDelay) {

     |  // @audit-issue Consider u/int256
  96 |  function setExecutionDelay(uint32 _executionDelay) external onlyOwner {

     |  // @audit-issue Consider u/int256
 115 |  uint32 timestamp = uint32(block.timestamp);

     |  // @audit-issue Consider u/int256
 134 |  uint32 timestamp = uint32(block.timestamp);
```
GitHub: [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L53), [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55), [96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96), [115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L115), [134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L134)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

     |  // @audit-issue Consider u/int256
  32 |  uint40 proposedUpgradeTimestamp;

     |  // @audit-issue Consider u/int256
  33 |  uint40 currentProposalId;

     |  // @audit-issue Consider u/int256
  54 |  uint32 batchOverheadL1Gas;

     |  // @audit-issue Consider u/int256
  55 |  uint32 maxPubdataPerBatch;

     |  // @audit-issue Consider u/int256
  56 |  uint32 maxL2GasPerBatch;

     |  // @audit-issue Consider u/int256
  57 |  uint32 priorityTxMaxPubdata;

     |  // @audit-issue Consider u/int256
  58 |  uint64 minimalL2GasPrice;

     |  // @audit-issue Consider u/int256
 151 |  uint128 baseTokenGasPriceMultiplierNominator;

     |  // @audit-issue Consider u/int256
 152 |  uint128 baseTokenGasPriceMultiplierDenominator;
```
GitHub: [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L32), [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L33), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L54), [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L55), [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L56), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L57), [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L58), [151](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L151), [152](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L152)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue Consider u/int256
  79 |  function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {

     |  // @audit-issue Consider u/int256
  79 |  function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {

     |  // @audit-issue Consider u/int256
  80 |  uint128 oldNominator = s.baseTokenGasPriceMultiplierNominator;

     |  // @audit-issue Consider u/int256
  81 |  uint128 oldDenominator = s.baseTokenGasPriceMultiplierDenominator;
```
GitHub: [79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79), [79](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79), [80](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L80), [81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L81)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Consider u/int256
  39 |  uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));

     |  // @audit-issue Consider u/int256
 592 |  function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

     |  // @audit-issue Consider u/int256
 597 |  function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {
```
GitHub: [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L39), [592](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L592), [597](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-issue Consider u/int256
  67 |  function baseTokenGasPriceMultiplierNominator() external view returns (uint128) {

     |  // @audit-issue Consider u/int256
  72 |  function baseTokenGasPriceMultiplierDenominator() external view returns (uint128) {
```
GitHub: [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L67), [72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L72)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Consider u/int256
  78 |  uint16 _l2TxNumberInBatch,

     |  // @audit-issue Consider u/int256
 181 |  uint16 _l2TxNumberInBatch,
```
GitHub: [78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L78), [181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L181)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

     |  // @audit-issue Consider u/int256
  40 |  uint8 version = uint8(_bytecodeHash[0]);
```
GitHub: [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L40)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol

     |  // @audit-issue Consider u/int256
  19 |  function readUint32(bytes memory _bytes, uint256 _start) internal pure returns (uint32 result, uint256 offset) {
```
GitHub: [19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L19)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

     |  // @audit-issue Consider u/int256
  32 |  uint16 selectorPosition;

     |  // @audit-issue Consider u/int256
  41 |  uint16 facetPosition;

     |  // @audit-issue Consider u/int256
 208 |  uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16();
```
GitHub: [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L32), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L41), [208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L208)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

     |  // @audit-issue Consider u/int256
  18 |  function get(Uint32Map storage _map, uint256 _index) internal view returns (uint32 result) {

     |  // @audit-issue Consider u/int256
  38 |  function set(Uint32Map storage _map, uint256 _index, uint32 _value) internal {

     |  // @audit-issue Consider u/int256
  54 |  uint32 oldValue = uint32(mapValue >> bitOffset);
```
GitHub: [18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L18), [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L38), [54](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L54)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

     |  // @audit-issue Consider u/int256
  12 |  uint64 expirationTimestamp;

     |  // @audit-issue Consider u/int256
  13 |  uint192 layer2Tip;
```
GitHub: [12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L12), [13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L13)


```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

     |  // @audit-issue Consider u/int256
  49 |  uint16 _l2TxNumberInBatch,

     |  // @audit-issue Consider u/int256
  56 |  uint16 _l2TxNumberInBatch,
```
GitHub: [49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L49), [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L56)


```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

     |  // @audit-issue Consider u/int256
  81 |  uint16 _l2TxNumberInBatch,

     |  // @audit-issue Consider u/int256
  93 |  uint16 _l2TxNumberInBatch,

     |  // @audit-issue Consider u/int256
 100 |  uint16 _l2TxNumberInBatch,

     |  // @audit-issue Consider u/int256
 109 |  uint16 _l2TxNumberInBatch,
```
GitHub: [81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L81), [93](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L93), [100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L100), [109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L109)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol

     |  // @audit-issue Consider u/int256
  94 |  uint16 _l2TxNumberInBatch,
```
GitHub: [94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L94)


```solidity
File: code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

     |  // @audit-issue Consider u/int256
  20 |  uint64 genesisIndexRepeatedStorageChanges;
```
GitHub: [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L20)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol

     |  // @audit-issue Consider u/int256
  40 |  function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external;

     |  // @audit-issue Consider u/int256
  40 |  function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external;

     |  // @audit-issue Consider u/int256
  84 |  uint128 oldNominator,

     |  // @audit-issue Consider u/int256
  85 |  uint128 oldDenominator,

     |  // @audit-issue Consider u/int256
  86 |  uint128 newNominator,

     |  // @audit-issue Consider u/int256
  87 |  uint128 newDenominator
```
GitHub: [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L40), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L40), [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L84), [85](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L85), [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L86), [87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L87)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

     |  // @audit-issue Consider u/int256
  84 |  uint64 batchNumber;

     |  // @audit-issue Consider u/int256
  86 |  uint64 indexRepeatedStorageChanges;

     |  // @audit-issue Consider u/int256
 113 |  uint64 batchNumber;

     |  // @audit-issue Consider u/int256
 114 |  uint64 timestamp;

     |  // @audit-issue Consider u/int256
 115 |  uint64 indexRepeatedStorageChanges;
```
GitHub: [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L84), [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L86), [113](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L113), [114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L114), [115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L115)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol

     |  // @audit-issue Consider u/int256
 112 |  function baseTokenGasPriceMultiplierNominator() external view returns (uint128);

     |  // @audit-issue Consider u/int256
 115 |  function baseTokenGasPriceMultiplierDenominator() external view returns (uint128);
```
GitHub: [112](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L112), [115](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L115)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

     |  // @audit-issue Consider u/int256
  51 |  uint16 _l2TxNumberInBatch,

     |  // @audit-issue Consider u/int256
  65 |  uint16 _l2TxNumberInBatch,

     |  // @audit-issue Consider u/int256
 126 |  uint64 expirationTimestamp,
```
GitHub: [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L51), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L65), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L126)


```solidity
File: code/contracts/ethereum/contracts/common/Messaging.sol

     |  // @audit-issue Consider u/int256
  24 |  uint8 l2ShardId;

     |  // @audit-issue Consider u/int256
  26 |  uint16 txNumberInBatch;

     |  // @audit-issue Consider u/int256
  38 |  uint16 txNumberInBatch;

     |  // @audit-issue Consider u/int256
  60 |  uint64 expirationTimestamp;
```
GitHub: [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L24), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L26), [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L38), [60](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L60)


```solidity
File: code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

     |  // @audit-issue Consider u/int256
  22 |  uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
```
GitHub: [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L22)


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

     |  // @audit-issue Consider u/int256
  68 |  uint64 txDataLen = uint64(_transaction.data.length);

     |  // @audit-issue Consider u/int256
 164 |  uint64 txDataLen = uint64(_transaction.data.length);

     |  // @audit-issue Consider u/int256
 259 |  uint64 txDataLen = uint64(_transaction.data.length);
```
GitHub: [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L68), [164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L164), [259](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L259)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue Consider u/int256
  65 |  uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);

     |  // @audit-issue Consider u/int256
  66 |  uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

     |  // @audit-issue Consider u/int256
 129 |  uint64 enumIndex = stateDiff.readUint64(84);

     |  // @audit-issue Consider u/int256
 143 |  uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

     |  // @audit-issue Consider u/int256
 145 |  uint8 operation = metadata & OPERATION_BITMASK;

     |  // @audit-issue Consider u/int256
 146 |  uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

     |  // @audit-issue Consider u/int256
 161 |  uint64 enumIndex = stateDiff.readUint64(84);

     |  // @audit-issue Consider u/int256
 174 |  uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

     |  // @audit-issue Consider u/int256
 176 |  uint8 operation = metadata & OPERATION_BITMASK;

     |  // @audit-issue Consider u/int256
 177 |  uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
```
GitHub: [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L65), [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L66), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L129), [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L143), [145](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L145), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L146), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L161), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L174), [176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L176), [177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L177)


```solidity
File: code/system-contracts/contracts/Constants.sol

     |  // @audit-issue Consider u/int256
  20 |  uint160 constant SYSTEM_CONTRACTS_OFFSET = 0x8000;

     |  // @audit-issue Consider u/int256
  25 |  uint160 constant REAL_SYSTEM_CONTRACTS_OFFSET = 0x8000;

     |  // @audit-issue Consider u/int256
  29 |  uint160 constant MAX_SYSTEM_CONTRACT_ADDRESS = 0xffff; // 2^16 - 1
```
GitHub: [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Constants.sol#L20), [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Constants.sol#L25), [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Constants.sol#L29)


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

     |  // @audit-issue Consider u/int256
 133 |  uint128 value = Utils.safeCastToU128(_transaction.value);

     |  // @audit-issue Consider u/int256
 135 |  uint32 gas = Utils.safeCastToU32(gasleft());

     |  // @audit-issue Consider u/int256
 161 |  uint8 v;
```
GitHub: [133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L133), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L135), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L161)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

     |  // @audit-issue Consider u/int256
  75 |  uint8 version = uint8(_bytecodeHash[0]);
```
GitHub: [75](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L75)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Consider u/int256
 200 |  uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

     |  // @audit-issue Consider u/int256
 233 |  uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

     |  // @audit-issue Consider u/int256
 237 |  uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

     |  // @audit-issue Consider u/int256
 251 |  uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
```
GitHub: [200](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L200), [233](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L233), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L237), [251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L251)


## [G-55] Use != 0 instead of > 0

If possible, i.e. the range of the variable precludes negative values, consider using `!= 0` to save gas.

*Instances: 24*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 129 |  require(amount > 0, "ShB: 0 amount to transfer");

 327 |  require(_amount > 0, "y1");
```
GitHub: [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129), [327](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 329 |  } else if (_refundRecipient.code.length > 0) {
```
GitHub: [329](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L329)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 429 |  if (_proof.serializedProof.length > 0) {

 593 |  return (_bitMap & (1 << _index)) > 0;

 631 |  require(_pubdataCommitments.length > 0, "pl");
```
GitHub: [429](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L429), [593](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L593), [631](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

 158 |  require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

 277 |  if (refundRecipient.code.length > 0) {
```
GitHub: [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158), [277](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L277)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 107 |  require(selectors.length > 0, "B"); // no functions for diamond cut

 132 |  require(_facet.code.length > 0, "G");

 155 |  require(_facet.code.length > 0, "K");
```
GitHub: [107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132), [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L155)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

  24 |  require(pathLength > 0, "xc");
```
GitHub: [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24)


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

 102 |  if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {
```
GitHub: [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L102)


```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

  24 |  require(_delegateTo.code.length > 0, "Delegatee is an EOA");
```
GitHub: [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L24)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

 303 |  require(knownCodeMarker > 0, "The code hash is not known");

 332 |  if (value > 0) {

 339 |  if (value > 0) {
```
GitHub: [303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L303), [332](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L332), [339](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L339)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

 156 |  return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);
```
GitHub: [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L156)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

 152 |  currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0

 245 |  require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

 287 |  require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

 355 |  require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

 413 |  require(currentBatchNumber > 0, "The current batch number must be greater than 0");
```
GitHub: [152](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L152), [245](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L245), [287](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L287), [355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L355), [413](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L413)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

 124 |  require(_amount > 0, "Amount cannot be zero");
```
GitHub: [124](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L124)


## [G-56] Use Solady library where possible to save gas

Utilizing gas-optimized math functions from libraries like [Solady](https://github.com/Vectorized/solady/blob/main/src/utils/FixedPointMathLib.sol) can lead to more efficient smart contracts.
This is particularly beneficial in contracts where these operations are frequently used.

For example, `(x * WAD) / y` can be replaced with Solady's `divWad()`.


*Instances: 11*

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Consider using the Solady library for this arithmetic
 580 |  for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
 581 |      blobAuxOutputWords[i * 2] = _blobHashes[i];
 582 |      blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
 583 |  }
```
GitHub: [580-583](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580-L583)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Consider using the Solady library for this arithmetic
 159 |  uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
 160 |      s.baseTokenGasPriceMultiplierDenominator;
```
GitHub: [159-160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L159-L160)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

     |  // @audit-issue Consider using the Solady library for this arithmetic
  98 |  costForPubdata += _numberOfFactoryDependencies * L1_TX_DELTA_FACTORY_DEPS_PUBDATA * _l2GasPricePerPubdata;
```
GitHub: [98](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L98)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue Consider using the Solady library for this arithmetic
  56 |  require(
  57 |      dictionary.length / 8 <= encodedData.length / 2,
  58 |      "Dictionary should have at most the same number of entries as the encoded data"
  59 |  );

     |  // @audit-issue Consider using the Solady library for this arithmetic
  61 |              for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
  62 |                  uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
  63 |                  require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");
  65 |                  uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);
  66 |                  uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);
  68 |                  require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");
  69 |              }
```
GitHub: [56-59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L56-L59), [61-69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L61-L69)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Consider using the Solady library for this arithmetic
  51 |  return KECCAK_ROUND_GAS_COST * (_length / KECCAK_ROUND_NUMBER_OF_BYTES + 1);

     |  // @audit-issue Consider using the Solady library for this arithmetic
  62 |  return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1);

     |  // @audit-issue Consider using the Solady library for this arithmetic
 148 |  uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) +
 149 |      3 *
 150 |      keccakGasCost(64) +
 151 |      gasSpentOnMessageHashing +
 152 |      COMPUTATIONAL_PRICE_FOR_PUBDATA *
 153 |      pubdataLen;

     |  // @audit-issue Consider using the Solady library for this arithmetic
 222 |  while (nodesOnCurrentLevel > 1) {
 223 |      nodesOnCurrentLevel /= 2;
 224 |      for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {
 225 |          l2ToL1LogsTreeArray[i] = keccak256(
 226 |              abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
 227 |          );
 228 |      }
 229 |  }

     |  // @audit-issue Consider using the Solady library for this arithmetic
 224 |  for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {
 225 |      l2ToL1LogsTreeArray[i] = keccak256(
 226 |          abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
 227 |      );
 228 |  }

     |  // @audit-issue Consider using the Solady library for this arithmetic
 225 |  l2ToL1LogsTreeArray[i] = keccak256(
 226 |      abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
 227 |  );
```
GitHub: [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L51), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L62), [148-153](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L148-L153), [222-229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L222-L229), [224-228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L224-L228), [225-227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L225-L227)


## [G-57] Use `<<` to efficiently multiple by powers of `2`

Multiplication by a power of `2` can be accomplished more efficiently using a left bit shift.

*Instances: 31*

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Use `<<` to multiply because `32` is a power of 2
 108 |  assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);

     |  // @audit-issue Use `<<` to multiply because `2` is a power of 2
 108 |  assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
```
GitHub: [108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L108), [108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L108)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

     |  // @audit-issue Use `<<` to multiply because `32` is a power of 2
  51 |  assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);

     |  // @audit-issue Use `<<` to multiply because `2` is a power of 2
  51 |  assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
```
GitHub: [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L51), [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L51)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Use `<<` to multiply because `2` is a power of 2
 578 |  blobAuxOutputWords = new bytes32[](2 * TOTAL_BLOBS_IN_COMMITMENT);

     |  // @audit-issue Use `<<` to multiply because `2` is a power of 2
 581 |  blobAuxOutputWords[i * 2] = _blobHashes[i];

     |  // @audit-issue Use `<<` to multiply because `2` is a power of 2
 582 |  blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
```
GitHub: [578](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L578), [581](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L581), [582](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L582)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

     |  // @audit-issue Use `<<` to multiply because `256` is a power of 2
  50 |  codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));
```
GitHub: [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L50)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

     |  // @audit-issue Use `<<` to multiply because `32` is a power of 2
  27 |  uint256 bitOffset = (_index & 7) * 32;

     |  // @audit-issue Use `<<` to multiply because `32` is a power of 2
  48 |  uint256 bitOffset = (_index & 7) * 32;
```
GitHub: [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L27), [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L48)


```solidity
File: code/contracts/ethereum/contracts/common/Config.sol

     |  // @audit-issue Use `<<` to multiply because `512` is a power of 2
  16 |  uint256 constant MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES = 4 + L2_TO_L1_LOG_SERIALIZE_SIZE * 512;
```
GitHub: [16](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L16)


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

     |  // @audit-issue Use `<<` to multiply because `2` is a power of 2
  97 |  vInt += 8 + block.chainid * 2;
```
GitHub: [97](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L97)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue Use `<<` to multiply because `4` is a power of 2
  52 |  encodedData.length * 4 == _bytecode.length,

     |  // @audit-issue Use `<<` to multiply because `8` is a power of 2
  62 |  uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;

     |  // @audit-issue Use `<<` to multiply because `4` is a power of 2
  66 |  uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

     |  // @audit-issue Use `<<` to multiply because `8` is a power of 2
 203 |  dictionary = _rawCompressedData[2:2 + dictionaryLen * 8];

     |  // @audit-issue Use `<<` to multiply because `8` is a power of 2
 204 |  encodedData = _rawCompressedData[2 + dictionaryLen * 8:];

     |  // @audit-issue Use `<<` to multiply because `8` is a power of 2
 253 |  number >>= (256 - (_calldataSlice.length * 8));
```
GitHub: [52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L52), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L62), [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L66), [203](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L203), [204](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L204), [253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L253)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Use `<<` to multiply because `2` is a power of 2
  89 |  uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) + 2 * keccakGasCost(64);

     |  // @audit-issue Use `<<` to multiply because `2` is a power of 2
 226 |  abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])

     |  // @audit-issue Use `<<` to multiply because `2` is a power of 2
 226 |  abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
```
GitHub: [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L89), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L226), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L226)


```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

     |  // @audit-issue Use `<<` to multiply because `8` is a power of 2
  37 |  uint256 shiftedVal = _val << (lbs * 8);

     |  // @audit-issue Use `<<` to multiply because `8` is a power of 2
  72 |  uint256 shiftedVal = uint256(_len) << (lbs * 8);
```
GitHub: [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L37), [72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L72)


```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

     |  // @audit-issue Use `<<` to multiply because `8` is a power of 2
  41 |  uint256 constant META_GAS_PER_PUBDATA_BYTE_OFFSET = 0 * 8;

     |  // @audit-issue Use `<<` to multiply because `8` is a power of 2
  42 |  uint256 constant META_HEAP_SIZE_OFFSET = 8 * 8;

     |  // @audit-issue Use `<<` to multiply because `8` is a power of 2
  42 |  uint256 constant META_HEAP_SIZE_OFFSET = 8 * 8;

     |  // @audit-issue Use `<<` to multiply because `8` is a power of 2
  43 |  uint256 constant META_AUX_HEAP_SIZE_OFFSET = 12 * 8;

     |  // @audit-issue Use `<<` to multiply because `8` is a power of 2
  44 |  uint256 constant META_SHARD_ID_OFFSET = 28 * 8;

     |  // @audit-issue Use `<<` to multiply because `8` is a power of 2
  45 |  uint256 constant META_CALLER_SHARD_ID_OFFSET = 29 * 8;

     |  // @audit-issue Use `<<` to multiply because `8` is a power of 2
  46 |  uint256 constant META_CODE_SHARD_ID_OFFSET = 30 * 8;
```
GitHub: [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L41), [42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L42), [42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L42), [43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L43), [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L44), [45](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L45), [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L46)


```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

     |  // @audit-issue Use `<<` to multiply because `256` is a power of 2
  46 |  codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));
```
GitHub: [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L46)


## [G-58] Use `>>` to efficiently divide by powers of `2`

Division by a power of `2` can be accomplished more efficiently using a right bit shift.

*Instances: 6*

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

     |  // @audit-issue Use `>>` to divide because `32` is a power of 2
  25 |  uint256 bytecodeLenInWords = _bytecode.length / 32;
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

     |  // @audit-issue Use `>>` to divide because `8` is a power of 2
  23 |  uint256 mapValue = _map.map[_index / 8];

     |  // @audit-issue Use `>>` to divide because `8` is a power of 2
  43 |  uint256 mapIndex = _index / 8;
```
GitHub: [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L23), [43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L43)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue Use `>>` to divide because `8` is a power of 2
  57 |  dictionary.length / 8 <= encodedData.length / 2,

     |  // @audit-issue Use `>>` to divide because `2` is a power of 2
  57 |  dictionary.length / 8 <= encodedData.length / 2,
```
GitHub: [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L57), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L57)


```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

     |  // @audit-issue Use `>>` to divide because `32` is a power of 2
  86 |  uint256 lengthInWords = _bytecode.length / 32;
```
GitHub: [86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L86)


## [G-59] Use `Array.unsafeAccess()` to avoid repeated array length checks

When using storage arrays, solidity adds an internal lookup of the array's length (a Gcoldsload **2100 gas**) to ensure you don't read past the array's end. You can avoid this lookup by using [`Array.unsafeAccess()`](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/94697be8a3f0dfcd95dfb13ffbd39b5973f5c65d/contracts/utils/Arrays.sol#L57) in cases where the length has already been checked, as is the case with the instances below.

*Instances: 10*

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

 226 |  (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```
GitHub: [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 117 |  committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);

 136 |  committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);

 187 |  _newBatchesData[i].batchNumber

 210 |  uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
```
GitHub: [117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L117), [136](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L136), [187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L187), [210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L210)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 258 |  _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));

 294 |  _newBatchesData[i],
```
GitHub: [258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L258), [294](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L294)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 228 |  L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
```
GitHub: [228](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L228)


## [G-60] Use `calldata` instead of `memory` for function arguments that are read only

When a function with a `memory` array is called externally, the `abi.decode()` step has to use a for-loop to copy each index of the `calldata` to the `memory` index. Each iteration of this for-loop costs at least 60 gas (i.e. 60 * `<mem_array>.length`). Using calldata directly, removes the need for such a loop in the contract code and runtime execution.  
                    
If the array is passed to an `internal` function which passes the array to another `internal` function where the array is modified and therefore `memory` is used in the `external` call, it's still more gas-efficient to use `calldata` when the external function uses modifiers, since the modifiers may prevent the `internal` functions from being called. `Structs` have the same overhead as an array of length one.

*Instances: 45*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Consider switching `_messageParams` param to `calldata`
 460 |  MessageParams memory _messageParams,
```
GitHub: [460](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L460)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Consider switching `_log` param to `calldata`
 168 |  L2Log memory _log,
```
GitHub: [168](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L168)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

     |  // @audit-issue Consider switching `_diamondCut` param to `calldata`
  11 |  constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
```
GitHub: [11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Consider switching `_previousBatch` param to `calldata`
  33 |  StoredBatchInfo memory _previousBatch,

     |  // @audit-issue Consider switching `_lastCommittedBatchData` param to `calldata`
 200 |  StoredBatchInfo memory _lastCommittedBatchData,

     |  // @audit-issue Consider switching `_lastCommittedBatchData` param to `calldata`
 209 |  StoredBatchInfo memory _lastCommittedBatchData,

     |  // @audit-issue Consider switching `_lastCommittedBatchData` param to `calldata`
 216 |  StoredBatchInfo memory _lastCommittedBatchData,

     |  // @audit-issue Consider switching `_lastCommittedBatchData` param to `calldata`
 254 |  StoredBatchInfo memory _lastCommittedBatchData,

     |  // @audit-issue Consider switching `_lastCommittedBatchData` param to `calldata`
 274 |  StoredBatchInfo memory _lastCommittedBatchData,

     |  // @audit-issue Consider switching `_storedBatch` param to `calldata`
 321 |  function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {

     |  // @audit-issue Consider switching `proofPublicInput` param to `calldata`
 440 |  function _verifyProof(uint256[] memory proofPublicInput, ProofInput calldata _proof) internal view {

     |  // @audit-issue Consider switching `_verifierParams` param to `calldata`
 456 |  VerifierParams memory _verifierParams

     |  // @audit-issue Consider switching `_blobCommitments` param to `calldata`
 503 |  bytes32[] memory _blobCommitments,
     |  // @audit-issue Consider switching `_blobHashes` param to `calldata`
 504 |  bytes32[] memory _blobHashes

     |  // @audit-issue Consider switching `_blobCommitments` param to `calldata`
 540 |  bytes32[] memory _blobCommitments,
     |  // @audit-issue Consider switching `_blobHashes` param to `calldata`
 541 |  bytes32[] memory _blobHashes

     |  // @audit-issue Consider switching `_blobCommitments` param to `calldata`
 562 |  bytes32[] memory _blobCommitments,
     |  // @audit-issue Consider switching `_blobHashes` param to `calldata`
 563 |  bytes32[] memory _blobHashes

     |  // @audit-issue Consider switching `_storedBatchInfo` param to `calldata`
 587 |  function _hashStoredBatchInfo(StoredBatchInfo memory _storedBatchInfo) internal pure returns (bytes32) {

     |  // @audit-issue Consider switching `_blobHashes` param to `calldata`
 627 |  bytes32[] memory _blobHashes
```
GitHub: [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L33), [200](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L200), [209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L209), [216](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L216), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L254), [274](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L274), [321](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L321), [440](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L440), [456](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L456), [503](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L503), [504](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L504), [540](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L540), [541](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L541), [562](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L562), [563](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L563), [587](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L587), [627](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L627)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Consider switching `_request` param to `calldata`
  48 |  BridgehubL2TransactionRequest memory _request

     |  // @audit-issue Consider switching `_message` param to `calldata`
  57 |  L2Message memory _message,

     |  // @audit-issue Consider switching `_log` param to `calldata`
  67 |  L2Log memory _log,

     |  // @audit-issue Consider switching `_log` param to `calldata`
 107 |  L2Log memory _log,

     |  // @audit-issue Consider switching `_message` param to `calldata`
 130 |  function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {

     |  // @audit-issue Consider switching `_request` param to `calldata`
 229 |  BridgehubL2TransactionRequest memory _request

     |  // @audit-issue Consider switching `_params` param to `calldata`
 260 |  WritePriorityOpParams memory _params,
  :  |
     |  // @audit-issue Consider switching `_factoryDeps` param to `calldata`
 262 |  bytes[] memory _factoryDeps

     |  // @audit-issue Consider switching `_priorityOpParams` param to `calldata`
 290 |  WritePriorityOpParams memory _priorityOpParams,
  :  |
     |  // @audit-issue Consider switching `_factoryDeps` param to `calldata`
 292 |  bytes[] memory _factoryDeps

     |  // @audit-issue Consider switching `_priorityOpParams` param to `calldata`
 317 |  WritePriorityOpParams memory _priorityOpParams,
  :  |
     |  // @audit-issue Consider switching `_factoryDeps` param to `calldata`
 319 |  bytes[] memory _factoryDeps

     |  // @audit-issue Consider switching `_factoryDeps` param to `calldata`
 353 |  function _hashFactoryDeps(bytes[] memory _factoryDeps) internal pure returns (uint256[] memory hashedFactoryDeps) {
```
GitHub: [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L48), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L57), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L67), [107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L107), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L130), [229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L229), [260](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L260), [262](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L262), [290](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L290), [292](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L292), [317](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L317), [319](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L319), [353](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L353)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

     |  // @audit-issue Consider switching `_diamondCut` param to `calldata`
  96 |  function diamondCut(DiamondCutData memory _diamondCut) internal {

     |  // @audit-issue Consider switching `_selectors` param to `calldata`
 126 |  function _addFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {

     |  // @audit-issue Consider switching `_selectors` param to `calldata`
 149 |  function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {

     |  // @audit-issue Consider switching `_selectors` param to `calldata`
 172 |  function _removeFunctions(address _facet, bytes4[] memory _selectors) private {
```
GitHub: [96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L96), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L126), [149](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L149), [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L172)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

     |  // @audit-issue Consider switching `_operation` param to `calldata`
  55 |  function pushBack(Queue storage _queue, PriorityOperation memory _operation) internal {
```
GitHub: [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L55)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

     |  // @audit-issue Consider switching `_transaction` param to `calldata`
  20 |  L2CanonicalTransaction memory _transaction,

     |  // @audit-issue Consider switching `_transaction` param to `calldata`
  46 |  function validateUpgradeTransaction(L2CanonicalTransaction memory _transaction) internal pure {
```
GitHub: [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L20), [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L46)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol

     |  // @audit-issue Consider switching `_log` param to `calldata`
  85 |  L2Log memory _log,
```
GitHub: [85](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L85)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

     |  // @audit-issue Consider switching `_log` param to `calldata`
  34 |  L2Log memory _log,
```
GitHub: [34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L34)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol

     |  // @audit-issue Consider switching `_newFeeParams` param to `calldata`
  20 |  function changeFeeParams(FeeParams memory _newFeeParams) private {
```
GitHub: [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol#L20)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Consider switching `_newInfo` param to `calldata`
  58 |  function _storeAccountInfo(address _address, AccountInfo memory _newInfo) internal {
```
GitHub: [58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L58)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Consider switching `_l2ToL1Log` param to `calldata`
  94 |  function _processL2ToL1Log(L2ToL1Log memory _l2ToL1Log) internal returns (uint256 logIdInMerkleTree) {
```
GitHub: [94](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L94)


## [G-61] Use `private` rather than `public` for constants

If needed, the values can be read from the verified contract source code, or if there are multiple values there can be a single getter function that [returns a tuple](https://github.com/code-423n4/2022-08-frax/blob/90f55a9ce4e25bceed3a74290b854341d8de6afa/src/contracts/FraxlendPair.sol#L156-L178) of the values of all currently-public constants. Saves **3406-3606 gas** in deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it's used, and not adding another entry to the method ID table.

*Instances: 5*

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Switch visibility to private
  26 |  string public constant override getName = "ValidatorTimelock";
```
GitHub: [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue Switch visibility to private
  20 |  string public constant override getName = "AdminFacet";
```
GitHub: [20](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Switch visibility to private
  27 |  string public constant override getName = "ExecutorFacet";
```
GitHub: [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-issue Switch visibility to private
  25 |  string public constant override getName = "GettersFacet";
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Switch visibility to private
  35 |  string public constant override getName = "MailboxFacet";
```
GitHub: [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35)


## [G-62] Use `uint256(1)`/`uint256(2)` instead of `true`/`false` to save gas for changes

Avoids a Gsset (**20000 gas**) when changing from `false` to `true`, after having been `true` in the past. Since most of the bools aren't changed twice in one transaction, I've counted the amount of gas as half of the full amount, for each variable.

*Instances: 6*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

  27 |  mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
  28 |      public isWithdrawalFinalized;
```
GitHub: [27-28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27-L28)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

  57 |  mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
  58 |      public isWithdrawalFinalized;

  61 |  mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;
```
GitHub: [57-58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57-L58), [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L61)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

  21 |  mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;

  23 |  mapping(address _token => bool) public tokenIsRegistered;
```
GitHub: [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21), [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L23)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

  50 |  mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
GitHub: [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50)


## [G-63] Use assembly to calculate hashes

If the arguments to the encode call can fit into the scratch space (two words or fewer), then it's more efficient to use assembly to generate the hash (**80 gas**):
                    
```solidity
    keccak256(abi.encodePacked(a, b)); }
```

to

```solidity 
    assembly {
        mstore(0x00, a)
        mstore(0x20, b)
        let result := keccak256(0x00, 0x40)
    }
```

*Instances: 61*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Use assembly to calcuate hashes
  76 |  bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
```
GitHub: [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Use assembly to calcuate hashes
 210 |  bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));

     |  // @audit-issue Use assembly to calcuate hashes
 341 |  bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));

     |  // @audit-issue Use assembly to calcuate hashes
 598 |  bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
```
GitHub: [210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L210), [341](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L341), [598](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L598)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Use assembly to calcuate hashes
 205 |  return keccak256(abi.encode(_operation));
```
GitHub: [205](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L205)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Use assembly to calcuate hashes
 102 |  storedBatchZero = keccak256(abi.encode(batchZero));

     |  // @audit-issue Use assembly to calcuate hashes
 104 |  initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

     |  // @audit-issue Use assembly to calcuate hashes
 140 |  initialCutHash = keccak256(abi.encode(_diamondCut));

     |  // @audit-issue Use assembly to calcuate hashes
 149 |  upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

     |  // @audit-issue Use assembly to calcuate hashes
 158 |  upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

     |  // @audit-issue Use assembly to calcuate hashes
 257 |  bytes32 cutHashInput = keccak256(_diamondCut);
```
GitHub: [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102), [104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L104), [140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L140), [149](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L149), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L158), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L257)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue Use assembly to calcuate hashes
 104 |  bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
```
GitHub: [104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Use assembly to calcuate hashes
  63 |  keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),

     |  // @audit-issue Use assembly to calcuate hashes
 313 |  concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));

     |  // @audit-issue Use assembly to calcuate hashes
 460 |  keccak256(
 461 |      abi.encodePacked(
 462 |          _prevBatchCommitment,
 463 |          _currentBatchCommitment,
 464 |          _verifierParams.recursionNodeLevelVkHash,
 465 |          _verifierParams.recursionLeafLevelVkHash
 466 |      )
 467 |  )

     |  // @audit-issue Use assembly to calcuate hashes
 506 |  bytes32 passThroughDataHash = keccak256(_batchPassThroughData(_newBatchData));

     |  // @audit-issue Use assembly to calcuate hashes
 507 |  bytes32 metadataHash = keccak256(_batchMetaParameters());

     |  // @audit-issue Use assembly to calcuate hashes
 508 |  bytes32 auxiliaryOutputHash = keccak256(
 509 |      _batchAuxiliaryOutput(_newBatchData, _stateDiffHash, _blobCommitments, _blobHashes)
 510 |  );

     |  // @audit-issue Use assembly to calcuate hashes
 512 |  return keccak256(abi.encode(passThroughDataHash, metadataHash, auxiliaryOutputHash));

     |  // @audit-issue Use assembly to calcuate hashes
 545 |  bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs);

     |  // @audit-issue Use assembly to calcuate hashes
 588 |  return keccak256(abi.encode(_storedBatchInfo));

     |  // @audit-issue Use assembly to calcuate hashes
 654 |  blobCommitments[versionedHashIndex] = keccak256(
 655 |      abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
 656 |  );
```
GitHub: [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L63), [313](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313), [460-467](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L460-L467), [506](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L506), [507](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L507), [508-510](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L508-L510), [512](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L512), [545](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L545), [588](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L588), [654-656](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L654-L656)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Use assembly to calcuate hashes
 112 |  bytes32 hashedLog = keccak256(
 113 |      abi.encodePacked(_log.l2ShardId, _log.isService, _log.txNumberInBatch, _log.sender, _log.key, _log.value)
 114 |  );

     |  // @audit-issue Use assembly to calcuate hashes
 138 |  value: keccak256(_message.data)

     |  // @audit-issue Use assembly to calcuate hashes
 332 |  canonicalTxHash = keccak256(transactionEncoding);
```
GitHub: [112-114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L112-L114), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L138), [332](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L332)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Use assembly to calcuate hashes
 212 |  bytes32 l2ProtocolUpgradeTxHash = keccak256(encodedTransaction);
```
GitHub: [212](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L212)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

     |  // @audit-issue Use assembly to calcuate hashes
  12 |  bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");

     |  // @audit-issue Use assembly to calcuate hashes
  67 |  bytes32 data = keccak256(
  68 |      bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
  69 |  );
```
GitHub: [12](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L12), [67-69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L67-L69)


```solidity
File: code/contracts/ethereum/contracts/common/Config.sol

     |  // @audit-issue Use assembly to calcuate hashes
 114 |  bytes32 constant TWO_BRIDGES_MAGIC_VALUE = bytes32(uint256(keccak256("TWO_BRIDGES_MAGIC_VALUE")) - 1);
```
GitHub: [114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L114)


```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

     |  // @audit-issue Use assembly to calcuate hashes
  29 |  txHash = keccak256(bytes.concat(signedTxHash, EfficientCall.keccak(_transaction.signature)));

     |  // @audit-issue Use assembly to calcuate hashes
 120 |  keccak256(
 121 |      bytes.concat(
 122 |          encodedListLength,
 123 |          encodedNonce,
 124 |          encodedGasParam,
 125 |          encodedTo,
 126 |          encodedValue,
 127 |          encodedDataLength,
 128 |          _transaction.data,
 129 |          vEncoded,
 130 |          rEncoded,
 131 |          sEncoded
 132 |      )
 133 |  );

     |  // @audit-issue Use assembly to calcuate hashes
 211 |  keccak256(
 212 |      bytes.concat(
 213 |          "\x01",
 214 |          encodedListLength,
 215 |          encodedFixedLengthParams,
 216 |          encodedDataLength,
 217 |          _transaction.data,
 218 |          encodedAccessListLength,
 219 |          vEncoded,
 220 |          rEncoded,
 221 |          sEncoded
 222 |      )
 223 |  );

     |  // @audit-issue Use assembly to calcuate hashes
 306 |  keccak256(
 307 |      bytes.concat(
 308 |          "\x02",
 309 |          encodedListLength,
 310 |          encodedFixedLengthParams,
 311 |          encodedDataLength,
 312 |          _transaction.data,
 313 |          encodedAccessListLength,
 314 |          vEncoded,
 315 |          rEncoded,
 316 |          sEncoded
 317 |      )
 318 |  );
```
GitHub: [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L29), [120-133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L120-L133), [211-223](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L211-L223), [306-318](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L306-L318)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Use assembly to calcuate hashes
 105 |  bytes32 hash = keccak256(
 106 |      bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, constructorInputHash)
 107 |  );

     |  // @audit-issue Use assembly to calcuate hashes
 121 |  bytes32 hash = keccak256(
 122 |      bytes.concat(CREATE_PREFIX, bytes32(uint256(uint160(_sender))), bytes32(_senderNonce))
 123 |  );
```
GitHub: [105-107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L105-L107), [121-123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L121-L123)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Use assembly to calcuate hashes
  95 |  bytes32 hashedLog = keccak256(
  96 |      abi.encodePacked(
  97 |          _l2ToL1Log.l2ShardId,
  98 |          _l2ToL1Log.isService,
  99 |          _l2ToL1Log.txNumberInBlock,
 100 |          _l2ToL1Log.sender,
 101 |          _l2ToL1Log.key,
 102 |          _l2ToL1Log.value
 103 |      )
 104 |  );

     |  // @audit-issue Use assembly to calcuate hashes
 106 |  chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

     |  // @audit-issue Use assembly to calcuate hashes
 122 |  chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

     |  // @audit-issue Use assembly to calcuate hashes
 164 |  chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

     |  // @audit-issue Use assembly to calcuate hashes
 212 |  reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));

     |  // @audit-issue Use assembly to calcuate hashes
 225 |  l2ToL1LogsTreeArray[i] = keccak256(
 226 |      abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
 227 |  );

     |  // @audit-issue Use assembly to calcuate hashes
 243 |  reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));

     |  // @audit-issue Use assembly to calcuate hashes
 259 |  reconstructedChainedL1BytecodesRevealDataHash = keccak256(
 260 |      abi.encode(
 261 |          reconstructedChainedL1BytecodesRevealDataHash,
 262 |          Utils.hashL2Bytecode(
 263 |              _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
 264 |          )
 265 |      )
 266 |  );
```
GitHub: [95-104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L95-L104), [106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L106), [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L122), [164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L164), [212](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L212), [225-227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L225-L227), [243](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L243), [259-266](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L259-L266)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Use assembly to calcuate hashes
 159 |  hash = keccak256(abi.encode(_block));

     |  // @audit-issue Use assembly to calcuate hashes
 227 |  return keccak256(abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash));

     |  // @audit-issue Use assembly to calcuate hashes
 234 |  return keccak256(abi.encodePacked(uint32(_blockNumber)));

     |  // @audit-issue Use assembly to calcuate hashes
 403 |  currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));
```
GitHub: [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L159), [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L227), [234](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L234), [403](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L403)


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

     |  // @audit-issue Use assembly to calcuate hashes
  82 |  bytes32 constant EIP712_DOMAIN_TYPEHASH = keccak256("EIP712Domain(string name,string version,uint256 chainId)");

     |  // @audit-issue Use assembly to calcuate hashes
  85 |  keccak256(
  86 |      "Transaction(uint256 txType,uint256 from,uint256 to,uint256 gasLimit,uint256 gasPerPubdataByteLimit,uint256 maxFeePerGas,uint256 maxPriorityFeePerGas,uint256 paymaster,uint256 nonce,uint256 value,bytes data,bytes32[] factoryDeps,bytes paymasterInput)"
  87 |  );

     |  // @audit-issue Use assembly to calcuate hashes
 119 |  bytes32 structHash = keccak256(
 120 |      abi.encode(
 121 |          EIP712_TRANSACTION_TYPE_HASH,
 122 |          _transaction.txType,
 123 |          _transaction.from,
 124 |          _transaction.to,
 125 |          _transaction.gasLimit,
 126 |          _transaction.gasPerPubdataByteLimit,
 127 |          _transaction.maxFeePerGas,
 128 |          _transaction.maxPriorityFeePerGas,
 129 |          _transaction.paymaster,
 130 |          _transaction.nonce,
 131 |          _transaction.value,
 132 |          EfficientCall.keccak(_transaction.data),
 133 |          keccak256(abi.encodePacked(_transaction.factoryDeps)),
 134 |          EfficientCall.keccak(_transaction.paymasterInput)
 135 |      )
 136 |  );

     |  // @audit-issue Use assembly to calcuate hashes
 133 |  keccak256(abi.encodePacked(_transaction.factoryDeps)),

     |  // @audit-issue Use assembly to calcuate hashes
 138 |  bytes32 domainSeparator = keccak256(
 139 |      abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
 140 |  );

     |  // @audit-issue Use assembly to calcuate hashes
 139 |  abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

     |  // @audit-issue Use assembly to calcuate hashes
 139 |  abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

     |  // @audit-issue Use assembly to calcuate hashes
 142 |  return keccak256(abi.encodePacked("\x19\x01", domainSeparator, structHash));

     |  // @audit-issue Use assembly to calcuate hashes
 203 |  keccak256(
 204 |      bytes.concat(
 205 |          encodedListLength,
 206 |          encodedNonce,
 207 |          encodedGasParam,
 208 |          encodedTo,
 209 |          encodedValue,
 210 |          encodedDataLength,
 211 |          _transaction.data,
 212 |          encodedChainId
 213 |      )
 214 |  );

     |  // @audit-issue Use assembly to calcuate hashes
 275 |  keccak256(
 276 |      bytes.concat(
 277 |          "\x01",
 278 |          encodedListLength,
 279 |          encodedFixedLengthParams,
 280 |          encodedDataLength,
 281 |          _transaction.data,
 282 |          encodedAccessListLength
 283 |      )
 284 |  );

     |  // @audit-issue Use assembly to calcuate hashes
 347 |  keccak256(
 348 |      bytes.concat(
 349 |          "\x02",
 350 |          encodedListLength,
 351 |          encodedFixedLengthParams,
 352 |          encodedDataLength,
 353 |          _transaction.data,
 354 |          encodedAccessListLength
 355 |      )
 356 |  );
```
GitHub: [82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L82), [85-87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L85-L87), [119-136](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L119-L136), [133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L133), [138-140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L138-L140), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139), [142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L142), [203-214](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L203-L214), [275-284](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L275-L284), [347-356](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L347-L356)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-issue Use assembly to calcuate hashes
 150 |  bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""));
```
GitHub: [150](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150)


```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

     |  // @audit-issue Use assembly to calcuate hashes
  85 |  bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");

     |  // @audit-issue Use assembly to calcuate hashes
 108 |  bytes32 data = keccak256(
 109 |      bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
 110 |  );
```
GitHub: [85](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L85), [108-110](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L108-L110)


## [G-64] Use assembly to perform external calls, in order to save gas

Using Solidity's assembly scratch space for constructing calldata in external calls with one or two arguments can be a gas-efficient approach. This method leverages the designated memory area (the first 64 bytes of memory) for temporary data storage during assembly operations. By directly writing arguments into this scratch space, it eliminates the need for additional memory allocation typically required for calldata preparation. This technique can lead to notable gas savings, especially in high-frequency or gas-sensitive operations. However, it requires careful implementation to avoid data corruption and should be used with a thorough understanding of low-level EVM operations and memory handling. Proper testing and validation are crucial when employing such optimizations.

*Instances: 13*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Save gas by call this in assembly
  65 |  uint256 amount = IERC20(_token).balanceOf(address(this));

     |  // @audit-issue Save gas by call this in assembly
  67 |  IERC20(_token).safeTransfer(address(sharedBridge), amount);

     |  // @audit-issue Save gas by call this in assembly
 161 |  uint256 balanceBefore = _token.balanceOf(address(sharedBridge));

     |  // @audit-issue Save gas by call this in assembly
 163 |  uint256 balanceAfter = _token.balanceOf(address(sharedBridge));
```
GitHub: [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L161), [163](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L163)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Save gas by call this in assembly
 119 |  IMailbox(_target).transferEthToSharedBridge();

     |  // @audit-issue Save gas by call this in assembly
 127 |  uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

     |  // @audit-issue Save gas by call this in assembly
 128 |  uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));

     |  // @audit-issue Save gas by call this in assembly
 130 |  IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);

     |  // @audit-issue Save gas by call this in assembly
 131 |  uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

     |  // @audit-issue Save gas by call this in assembly
 138 |  require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");

     |  // @audit-issue Save gas by call this in assembly
 174 |  uint256 balanceBefore = _token.balanceOf(address(this));

     |  // @audit-issue Save gas by call this in assembly
 176 |  uint256 balanceAfter = _token.balanceOf(address(this));

     |  // @audit-issue Save gas by call this in assembly
 195 |  require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");
```
GitHub: [119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L119), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127), [128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L128), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L130), [131](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138), [174](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L174), [176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176), [195](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195)


## [G-65] Use assembly to write storage values

Instead of:
                    
```solidity
owner = _newOwner
```

write:

```solidity
assembly { sstore(owner.slot, _newOwner) }
```


*Instances: 99*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Use assembly `sstore` to save gas
  56 |  sharedBridge = _sharedBridge;

     |  // @audit-issue Use assembly `sstore` to save gas
 154 |  depositAmount[msg.sender][_l1Token][l2TxHash] = _amount;
```
GitHub: [56](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L56), [154](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L154)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Use assembly `sstore` to save gas
  96 |  l1WethAddress = _l1WethAddress;

     |  // @audit-issue Use assembly `sstore` to save gas
  97 |  bridgehub = _bridgehub;

     |  // @audit-issue Use assembly `sstore` to save gas
  98 |  legacyBridge = _legacyBridge;

     |  // @audit-issue Use assembly `sstore` to save gas
 111 |  eraFirstPostUpgradeBatch = _eraFirstPostUpgradeBatch;

     |  // @audit-issue Use assembly `sstore` to save gas
 112 |  l2BridgeAddress[ERA_CHAIN_ID] = ERA_ERC20_BRIDGE_ADDRESS;

     |  // @audit-issue Use assembly `sstore` to save gas
 122 |  chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
 123 |      chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
 124 |      balanceAfter -
 125 |      balanceBefore;

     |  // @audit-issue Use assembly `sstore` to save gas
 133 |  chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;

     |  // @audit-issue Use assembly `sstore` to save gas
 143 |  l2BridgeAddress[_chainId] = _l2BridgeAddress;

     |  // @audit-issue Use assembly `sstore` to save gas
 165 |  chainBalance[_chainId][_l1Token] += _amount;

     |  // @audit-issue Use assembly `sstore` to save gas
 212 |  chainBalance[_chainId][_l1Token] += amount;

     |  // @audit-issue Use assembly `sstore` to save gas
 238 |  depositHappened[_chainId][_txHash] = _txDataHash;

     |  // @audit-issue Use assembly `sstore` to save gas
 350 |  chainBalance[_chainId][_l1Token] -= _amount;

     |  // @audit-issue Use assembly `sstore` to save gas
 418 |  isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true;

     |  // @audit-issue Use assembly `sstore` to save gas
 440 |  chainBalance[_chainId][l1Token] -= amount;

     |  // @audit-issue Use assembly `sstore` to save gas
 568 |  chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;

     |  // @audit-issue Use assembly `sstore` to save gas
 600 |  depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;
```
GitHub: [96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L96), [97](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L97), [98](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L98), [111](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L111), [112](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L112), [122-125](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L122-L125), [133](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133), [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L143), [165](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L165), [212](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L212), [238](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L238), [350](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L350), [418](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L418), [440](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L440), [568](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L568), [600](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L600)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Use assembly `sstore` to save gas
  55 |  pendingAdmin = _newPendingAdmin;

     |  // @audit-issue Use assembly `sstore` to save gas
  65 |  admin = currentPendingAdmin;

     |  // @audit-issue Use assembly `sstore` to save gas
  87 |  stateTransitionManagerIsRegistered[_stateTransitionManager] = true;

     |  // @audit-issue Use assembly `sstore` to save gas
  97 |  stateTransitionManagerIsRegistered[_stateTransitionManager] = false;

     |  // @audit-issue Use assembly `sstore` to save gas
 103 |  tokenIsRegistered[_token] = true;

     |  // @audit-issue Use assembly `sstore` to save gas
 109 |  sharedBridge = IL1SharedBridge(_sharedBridge);

     |  // @audit-issue Use assembly `sstore` to save gas
 134 |  stateTransitionManager[_chainId] = _stateTransitionManager;

     |  // @audit-issue Use assembly `sstore` to save gas
 135 |  baseToken[_chainId] = _baseToken;
```
GitHub: [55](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L65), [87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L87), [97](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L97), [103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L103), [109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L109), [134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L135)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Use assembly `sstore` to save gas
  46 |  securityCouncil = _securityCouncil;

     |  // @audit-issue Use assembly `sstore` to save gas
  49 |  minDelay = _minDelay;

     |  // @audit-issue Use assembly `sstore` to save gas
 179 |  timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP;

     |  // @audit-issue Use assembly `sstore` to save gas
 198 |  timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP;

     |  // @audit-issue Use assembly `sstore` to save gas
 219 |  timestamps[_id] = block.timestamp + _delay;

     |  // @audit-issue Use assembly `sstore` to save gas
 251 |  minDelay = _newDelay;

     |  // @audit-issue Use assembly `sstore` to save gas
 258 |  securityCouncil = _newSecurityCouncil;
```
GitHub: [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L46), [49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L49), [179](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L179), [198](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L198), [219](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L219), [251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L251), [258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L258)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Use assembly `sstore` to save gas
  61 |  bridgehub = _bridgehub;

     |  // @audit-issue Use assembly `sstore` to save gas
  87 |  genesisUpgrade = _initializeData.genesisUpgrade;

     |  // @audit-issue Use assembly `sstore` to save gas
  88 |  protocolVersion = _initializeData.protocolVersion;

     |  // @audit-issue Use assembly `sstore` to save gas
  89 |  validatorTimelock = _initializeData.validatorTimelock;

     |  // @audit-issue Use assembly `sstore` to save gas
 102 |  storedBatchZero = keccak256(abi.encode(batchZero));

     |  // @audit-issue Use assembly `sstore` to save gas
 104 |  initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

     |  // @audit-issue Use assembly `sstore` to save gas
 116 |  pendingAdmin = _newPendingAdmin;

     |  // @audit-issue Use assembly `sstore` to save gas
 126 |  admin = currentPendingAdmin;

     |  // @audit-issue Use assembly `sstore` to save gas
 135 |  validatorTimelock = _validatorTimelock;

     |  // @audit-issue Use assembly `sstore` to save gas
 140 |  initialCutHash = keccak256(abi.encode(_diamondCut));

     |  // @audit-issue Use assembly `sstore` to save gas
 149 |  upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

     |  // @audit-issue Use assembly `sstore` to save gas
 150 |  protocolVersion = _newProtocolVersion;

     |  // @audit-issue Use assembly `sstore` to save gas
 158 |  upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

     |  // @audit-issue Use assembly `sstore` to save gas
 236 |  stateTransition[_chainId] = _stateTransitionContract;

     |  // @audit-issue Use assembly `sstore` to save gas
 284 |  stateTransition[_chainId] = stateTransitionAddress;
```
GitHub: [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L61), [87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L87), [88](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L88), [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L89), [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102), [104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L104), [116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L116), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L126), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L135), [140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L140), [149](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L149), [150](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L150), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L158), [236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L236), [284](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L284)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Use assembly `sstore` to save gas
  57 |  executionDelay = _executionDelay;

     |  // @audit-issue Use assembly `sstore` to save gas
  74 |  stateTransitionManager = _stateTransitionManager;

     |  // @audit-issue Use assembly `sstore` to save gas
  82 |  validators[_chainId][_newValidator] = true;

     |  // @audit-issue Use assembly `sstore` to save gas
  91 |  validators[_chainId][_validator] = false;

     |  // @audit-issue Use assembly `sstore` to save gas
  97 |  executionDelay = _executionDelay;
```
GitHub: [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57), [74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L74), [82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L82), [91](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L91), [97](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L97)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

     |  // @audit-issue Use assembly `sstore` to save gas
  30 |  s.chainId = _initializeData.chainId;

     |  // @audit-issue Use assembly `sstore` to save gas
  31 |  s.bridgehub = _initializeData.bridgehub;

     |  // @audit-issue Use assembly `sstore` to save gas
  32 |  s.stateTransitionManager = _initializeData.stateTransitionManager;

     |  // @audit-issue Use assembly `sstore` to save gas
  33 |  s.baseToken = _initializeData.baseToken;

     |  // @audit-issue Use assembly `sstore` to save gas
  34 |  s.baseTokenBridge = _initializeData.baseTokenBridge;

     |  // @audit-issue Use assembly `sstore` to save gas
  35 |  s.protocolVersion = _initializeData.protocolVersion;

     |  // @audit-issue Use assembly `sstore` to save gas
  37 |  s.verifier = _initializeData.verifier;

     |  // @audit-issue Use assembly `sstore` to save gas
  38 |  s.admin = _initializeData.admin;

     |  // @audit-issue Use assembly `sstore` to save gas
  39 |  s.validators[_initializeData.validatorTimelock] = true;

     |  // @audit-issue Use assembly `sstore` to save gas
  41 |  s.storedBatchHashes[0] = _initializeData.storedBatchZero;

     |  // @audit-issue Use assembly `sstore` to save gas
  42 |  s.verifierParams = _initializeData.verifierParams;

     |  // @audit-issue Use assembly `sstore` to save gas
  43 |  s.l2BootloaderBytecodeHash = _initializeData.l2BootloaderBytecodeHash;

     |  // @audit-issue Use assembly `sstore` to save gas
  44 |  s.l2DefaultAccountBytecodeHash = _initializeData.l2DefaultAccountBytecodeHash;

     |  // @audit-issue Use assembly `sstore` to save gas
  45 |  s.priorityTxMaxGasLimit = _initializeData.priorityTxMaxGasLimit;

     |  // @audit-issue Use assembly `sstore` to save gas
  46 |  s.feeParams = _initializeData.feeParams;

     |  // @audit-issue Use assembly `sstore` to save gas
  47 |  s.blobVersionedHashRetriever = _initializeData.blobVersionedHashRetriever;
```
GitHub: [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L30), [31](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L31), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L32), [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L33), [34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L34), [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L35), [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L37), [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L38), [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L39), [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L41), [42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L42), [43](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L43), [44](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L44), [45](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L45), [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L46), [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L47)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue Use assembly `sstore` to save gas
  27 |  s.pendingAdmin = _newPendingAdmin;

     |  // @audit-issue Use assembly `sstore` to save gas
  37 |  s.admin = pendingAdmin;

     |  // @audit-issue Use assembly `sstore` to save gas
  46 |  s.validators[_validator] = _active;

     |  // @audit-issue Use assembly `sstore` to save gas
  53 |  s.zkPorterIsAvailable = _zkPorterIsAvailable;

     |  // @audit-issue Use assembly `sstore` to save gas
  62 |  s.priorityTxMaxGasLimit = _newPriorityTxMaxGasLimit;

     |  // @audit-issue Use assembly `sstore` to save gas
  73 |  s.feeParams = _newFeeParams;

     |  // @audit-issue Use assembly `sstore` to save gas
  83 |  s.baseTokenGasPriceMultiplierNominator = _nominator;

     |  // @audit-issue Use assembly `sstore` to save gas
  84 |  s.baseTokenGasPriceMultiplierDenominator = _denominator;

     |  // @audit-issue Use assembly `sstore` to save gas
  91 |  s.feeParams.pubdataPricingMode = _validiumMode;
```
GitHub: [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L27), [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L37), [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L46), [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L53), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L62), [73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L73), [83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L83), [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L84), [91](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L91)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Use assembly `sstore` to save gas
 247 |  s.totalBatchesCommitted = s.totalBatchesCommitted + _newBatchesData.length;

     |  // @audit-issue Use assembly `sstore` to save gas
 260 |  s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);

     |  // @audit-issue Use assembly `sstore` to save gas
 287 |  s.l2SystemContractsUpgradeBatchNumber = _newBatchesData[0].batchNumber;

     |  // @audit-issue Use assembly `sstore` to save gas
 298 |  s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);

     |  // @audit-issue Use assembly `sstore` to save gas
 333 |  s.l2LogsRootHashes[currentBatchNumber] = _storedBatch.l2LogsTreeRoot;

     |  // @audit-issue Use assembly `sstore` to save gas
 357 |  s.totalBatchesExecuted = newTotalBatchesExecuted;

     |  // @audit-issue Use assembly `sstore` to save gas
 437 |  s.totalBatchesVerified = currentTotalBatchesVerified;

     |  // @audit-issue Use assembly `sstore` to save gas
 486 |  s.totalBatchesVerified = _newLastBatch;

     |  // @audit-issue Use assembly `sstore` to save gas
 488 |  s.totalBatchesCommitted = _newLastBatch;
```
GitHub: [247](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L247), [260](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L260), [287](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L287), [298](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L298), [333](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L333), [357](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L357), [437](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L437), [486](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L486), [488](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L488)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Use assembly `sstore` to save gas
 103 |  s.l2DefaultAccountBytecodeHash = _l2DefaultAccountBytecodeHash;

     |  // @audit-issue Use assembly `sstore` to save gas
 120 |  s.l2BootloaderBytecodeHash = _l2BootloaderBytecodeHash;

     |  // @audit-issue Use assembly `sstore` to save gas
 136 |  s.verifier = _newVerifier;

     |  // @audit-issue Use assembly `sstore` to save gas
 156 |  s.verifierParams = _newVerifierParams;

     |  // @audit-issue Use assembly `sstore` to save gas
 214 |  s.l2SystemContractsUpgradeTxHash = l2ProtocolUpgradeTxHash;

     |  // @audit-issue Use assembly `sstore` to save gas
 255 |  s.protocolVersion = _newProtocolVersion;
```
GitHub: [103](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L103), [120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L120), [136](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L136), [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L156), [214](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L214), [255](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L255)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

     |  // @audit-issue Use assembly `sstore` to save gas
  39 |  s.protocolVersion = _newProtocolVersion;
```
GitHub: [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L39)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_4844.sol

     |  // @audit-issue Use assembly `sstore` to save gas
  19 |  s.blobVersionedHashRetriever = 0x0000000000000000000000000000000000001337;
```
GitHub: [19](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_4844.sol#L19)


```solidity
File: code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol

     |  // @audit-issue Use assembly `sstore` to save gas
  26 |  s.feeParams = _newFeeParams;
```
GitHub: [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/Upgrade_v1_4_1.sol#L26)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Use assembly `sstore` to save gas
  59 |  accountInfo[_address] = _newInfo;

     |  // @audit-issue Use assembly `sstore` to save gas
  66 |  accountInfo[msg.sender].supportedAAVersion = _version;
```
GitHub: [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L59), [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L66)


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

     |  // @audit-issue Use assembly `sstore` to save gas
  41 |  immutableDataStorage[uint256(uint160(_dest))][index] = value;
```
GitHub: [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L41)


## [G-66] Use custom errors rather than `revert()`/`require()` strings to save gas

Custom errors are available from solidity version 0.8.4. Custom errors save [**~50 gas**](https://gist.github.com/IllIllI000/ad1bd0d29a0101b25e57c293b4b0c746) each time they're hit by [avoiding having to allocate and store the revert string](https://blog.soliditylang.org/2021/04/21/custom-errors/#errors-in-depth). Not defining the strings also save deployment gas.

*Instances: 99*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Use custom errors
  64 |  require(msg.sender == address(sharedBridge), "Not shared bridge");

     |  // @audit-issue Use custom errors
  66 |  require(amount == _amount, "Incorrect amount");

     |  // @audit-issue Use custom errors
 141 |  require(_amount != 0, "0T"); // empty deposit

     |  // @audit-issue Use custom errors
 143 |  require(amount == _amount, "3T"); // The token has non-standard transfer logic

     |  // @audit-issue Use custom errors
 186 |  require(amount != 0, "2T"); // empty deposit

     |  // @audit-issue Use custom errors
 215 |  require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw");
```
GitHub: [64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64), [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L66), [141](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141), [143](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L143), [186](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186), [215](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L215)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Use custom errors
  69 |  require(msg.sender == address(bridgehub), "ShB not BH");

     |  // @audit-issue Use custom errors
  75 |  require(
  76 |      msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
  77 |      "L1SharedBridge: not bridgehub or era chain"
  78 |  );

     |  // @audit-issue Use custom errors
  84 |  require(msg.sender == address(legacyBridge), "ShB not legacy bridge");

     |  // @audit-issue Use custom errors
 108 |  require(_owner != address(0), "ShB owner 0");

     |  // @audit-issue Use custom errors
 121 |  require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");

     |  // @audit-issue Use custom errors
 129 |  require(amount > 0, "ShB: 0 amount to transfer");

     |  // @audit-issue Use custom errors
 132 |  require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");

     |  // @audit-issue Use custom errors
 138 |  require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");

     |  // @audit-issue Use custom errors
 155 |  require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");

     |  // @audit-issue Use custom errors
 158 |  require(msg.value == 0, "ShB m.v > 0 b d.it");

     |  // @audit-issue Use custom errors
 161 |  require(amount == _amount, "3T"); // The token has non-standard transfer logic

     |  // @audit-issue Use custom errors
 188 |  require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

     |  // @audit-issue Use custom errors
 194 |  require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");

     |  // @audit-issue Use custom errors
 195 |  require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

     |  // @audit-issue Use custom errors
 200 |  require(_depositAmount == 0, "ShB wrong withdraw amount");

     |  // @audit-issue Use custom errors
 202 |  require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");

     |  // @audit-issue Use custom errors
 206 |  require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic

     |  // @audit-issue Use custom errors
 208 |  require(amount != 0, "6T"); // empty deposit amount

     |  // @audit-issue Use custom errors
 237 |  require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");

     |  // @audit-issue Use custom errors
 325 |  require(proofValid, "yn");

     |  // @audit-issue Use custom errors
 327 |  require(_amount > 0, "y1");

     |  // @audit-issue Use custom errors
 342 |  require(dataHash == txDataHash, "ShB: d.it not hap");

     |  // @audit-issue Use custom errors
 349 |  require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");

     |  // @audit-issue Use custom errors
 360 |  require(callSuccess, "ShB: claimFailedDeposit failed");

     |  // @audit-issue Use custom errors
 396 |  require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");

     |  // @audit-issue Use custom errors
 417 |  require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");

     |  // @audit-issue Use custom errors
 427 |  require(!alreadyFinalized, "Withdrawal is already finalized 2");

     |  // @audit-issue Use custom errors
 439 |  require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds

     |  // @audit-issue Use custom errors
 449 |  require(callSuccess, "ShB: withdraw failed");

     |  // @audit-issue Use custom errors
 484 |  require(success, "ShB withd w proof"); // withdrawal wrong proof

     |  // @audit-issue Use custom errors
 501 |  require(_l2ToL1message.length >= 56, "ShB wrong msg len"); // wrong messsage length

     |  // @audit-issue Use custom errors
 517 |  require(_l2ToL1message.length == 76, "ShB wrong msg len 2");

     |  // @audit-issue Use custom errors
 563 |  require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

     |  // @audit-issue Use custom errors
 564 |  require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");

     |  // @audit-issue Use custom errors
 522 |  revert("ShB Incorrect message function selector");
```
GitHub: [69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69), [75-78](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75-L78), [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L84), [108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L108), [121](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L121), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138), [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L155), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L158), [161](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L161), [188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188), [194](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L194), [195](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195), [200](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L200), [202](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202), [206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L206), [208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L208), [237](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L237), [325](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L325), [327](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327), [342](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L342), [349](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L349), [360](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L360), [396](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L396), [417](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L417), [427](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L427), [439](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L439), [449](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L449), [484](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L484), [501](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L501), [517](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L517), [563](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563), [564](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564), [522](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L522)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Use custom errors
  46 |  require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

     |  // @audit-issue Use custom errors
  62 |  require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

     |  // @audit-issue Use custom errors
  83 |  require(
  84 |      !stateTransitionManagerIsRegistered[_stateTransitionManager],
  85 |      "Bridgehub: state transition already registered"
  86 |  );

     |  // @audit-issue Use custom errors
  93 |  require(
  94 |      stateTransitionManagerIsRegistered[_stateTransitionManager],
  95 |      "Bridgehub: state transition not registered yet"
  96 |  );

     |  // @audit-issue Use custom errors
 102 |  require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

     |  // @audit-issue Use custom errors
 122 |  require(_chainId != 0, "Bridgehub: chainId cannot be 0");

     |  // @audit-issue Use custom errors
 123 |  require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");

     |  // @audit-issue Use custom errors
 125 |  require(
 126 |      stateTransitionManagerIsRegistered[_stateTransitionManager],
 127 |      "Bridgehub: state transition not registered"
 128 |  );

     |  // @audit-issue Use custom errors
 129 |  require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");

     |  // @audit-issue Use custom errors
 130 |  require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

     |  // @audit-issue Use custom errors
 132 |  require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

     |  // @audit-issue Use custom errors
 223 |  require(msg.value == _request.mintValue, "Bridgehub: msg.value mismatch 1");

     |  // @audit-issue Use custom errors
 225 |  require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");

     |  // @audit-issue Use custom errors
 269 |  require(
 270 |      msg.value == _request.mintValue + _request.secondBridgeValue,
 271 |      "Bridgehub: msg.value mismatch 2"
 272 |  );

     |  // @audit-issue Use custom errors
 275 |  require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3");

     |  // @audit-issue Use custom errors
 296 |  require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch");

     |  // @audit-issue Use custom errors
 300 |  require(
 301 |      _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
 302 |      "Bridgehub: second bridge address too low"
 303 |  ); // to avoid calls to precompiles
```
GitHub: [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62), [83-86](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83-L86), [93-96](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L93-L96), [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102), [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L122), [123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123), [125-128](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L125-L128), [129](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L129), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132), [223](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L223), [225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225), [269-272](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L269-L272), [275](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L275), [296](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L296), [300-303](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L300-L303)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Use custom errors
  42 |  require(_admin != address(0), "Admin should be non zero address");

     |  // @audit-issue Use custom errors
  59 |  require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

     |  // @audit-issue Use custom errors
  65 |  require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

     |  // @audit-issue Use custom errors
  71 |  require(
  72 |      msg.sender == owner() || msg.sender == securityCouncil,
  73 |      "Only the owner and security council are allowed to call this function"
  74 |  );

     |  // @audit-issue Use custom errors
 155 |  require(isOperationPending(_id), "Operation must be pending");

     |  // @audit-issue Use custom errors
 172 |  require(isOperationReady(id), "Operation must be ready before execution");

     |  // @audit-issue Use custom errors
 177 |  require(isOperationReady(id), "Operation must be ready after execution");

     |  // @audit-issue Use custom errors
 191 |  require(isOperationPending(id), "Operation must be pending before execution");

     |  // @audit-issue Use custom errors
 196 |  require(isOperationPending(id), "Operation must be pending after execution");

     |  // @audit-issue Use custom errors
 216 |  require(!isOperation(_id), "Operation with this proposal id already exists");

     |  // @audit-issue Use custom errors
 217 |  require(_delay >= minDelay, "Proposed delay is less than minimum delay");

     |  // @audit-issue Use custom errors
 240 |  require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");
```
GitHub: [42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L42), [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L59), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L65), [71-74](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L71-L74), [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L155), [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L172), [177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L177), [191](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L191), [196](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L196), [216](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L216), [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L217), [240](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L240)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Use custom errors
  66 |  require(msg.sender == bridgehub, "StateTransition: only bridgehub");

     |  // @audit-issue Use custom errors
  72 |  require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

     |  // @audit-issue Use custom errors
  84 |  require(_initializeData.governor != address(0), "StateTransition: governor zero");

     |  // @audit-issue Use custom errors
 123 |  require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

     |  // @audit-issue Use custom errors
 258 |  require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");
```
GitHub: [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L66), [72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L72), [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L84), [123](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L123), [258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L258)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Use custom errors
  62 |  require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

     |  // @audit-issue Use custom errors
  68 |  require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");

     |  // @audit-issue Use custom errors
 195 |  require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

     |  // @audit-issue Use custom errors
 217 |  require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
```
GitHub: [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68), [195](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195), [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L217)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

     |  // @audit-issue Use custom errors
  25 |  require(address(_initializeData.verifier) != address(0), "vt");

     |  // @audit-issue Use custom errors
  26 |  require(_initializeData.admin != address(0), "vy");

     |  // @audit-issue Use custom errors
  27 |  require(_initializeData.validatorTimelock != address(0), "hc");

     |  // @audit-issue Use custom errors
  28 |  require(_initializeData.priorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "vu");
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25), [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L26), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27), [28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L28)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

     |  // @audit-issue Use custom errors
  14 |  require(_chainId == block.chainid, "pr");

     |  // @audit-issue Use custom errors
  25 |  require(msg.data.length >= 4 || msg.data.length == 0, "Ut");

     |  // @audit-issue Use custom errors
  30 |  require(facetAddress != address(0), "F"); // Proxy has no facet for this selector

     |  // @audit-issue Use custom errors
  31 |  require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen
```
GitHub: [14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L14), [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25), [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30), [31](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L31)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue Use custom errors
  34 |  require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights

     |  // @audit-issue Use custom errors
  59 |  require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");

     |  // @audit-issue Use custom errors
  70 |  require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");

     |  // @audit-issue Use custom errors
  90 |  require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed

     |  // @audit-issue Use custom errors
 105 |  require(
 106 |      cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
 107 |      "StateTransition: cutHash mismatch"
 108 |  );

     |  // @audit-issue Use custom errors
 110 |  require(
 111 |      s.protocolVersion == _oldProtocolVersion,
 112 |      "StateTransition: protocolVersion mismatch in STC when upgrading"
 113 |  );

     |  // @audit-issue Use custom errors
 116 |  require(
 117 |      s.protocolVersion > _oldProtocolVersion,
 118 |      "StateTransition: protocolVersion mismatch in STC after upgrading"
 119 |  );

     |  // @audit-issue Use custom errors
 136 |  require(!diamondStorage.isFrozen, "a9"); // diamond proxy is frozen already

     |  // @audit-issue Use custom errors
 146 |  require(diamondStorage.isFrozen, "a7"); // diamond proxy is not frozen
```
GitHub: [34](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34), [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L59), [70](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L70), [90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90), [105-108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L105-L108), [110-113](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L110-L113), [116-119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L116-L119), [136](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L136), [146](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L146)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Use custom errors
  37 |  require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f"); // only commit next batch

     |  // @audit-issue Use custom errors
  40 |  require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us");

     |  // @audit-issue Use custom errors
  50 |  require(logOutput.pubdataHash == 0x00, "v0h");
```
GitHub: [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L37), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L40), [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L50)


## [G-67] Use local variables for emitting

Using a state variable will incur a `Gwarmaccess`. It is unlikely that a variable would be emitted in an `event` unless used in the enclosing `function`/`modifier` scope. Therefore, use a local stack variable copy of the state variable when emitting the event. If the state variable hasn't been used, reconsider whether it makes sense to include it in the event.

*Instances: 12*

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue `pendingAdmin` is a state variable
  69 |  emit NewAdmin(previousAdmin, pendingAdmin);
```
GitHub: [69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue `minDelay` is a state variable
 250 |  emit ChangeMinDelay(minDelay, _newDelay);

     |  // @audit-issue `securityCouncil` is a state variable
 257 |  emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```
GitHub: [250](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L250), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L257)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue `pendingAdmin` is a state variable
 130 |  emit NewAdmin(previousAdmin, pendingAdmin);

     |  // @audit-issue `protocolVersion` is a state variable
 229 |  emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
```
GitHub: [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L130), [229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L229)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue `s` is a state variable
 436 |  emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

     |  // @audit-issue `s` is a state variable
     |  // @audit-issue `s` is a state variable
     |  // @audit-issue `s` is a state variable
 496 |  emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
```
GitHub: [436](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436), [496](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496), [496](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496), [496](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

     |  // @audit-issue `decimals_` is a state variable
 101 |  emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);

     |  // @audit-issue `l1Address` is a state variable
     |  // @audit-issue `decimals_` is a state variable
 126 |  emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);
```
GitHub: [101](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L101), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126), [126](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126)


## [G-68] Use more recent OpenZeppelin version for gas boost

OpenZeppelin version 4.9.0+ provides many small gas optimizations, see [here](https://github.com/OpenZeppelin/openzeppelin-contracts/releases/tag/v4.9.0) for more info.

*Instances: 25*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (token/ERC20/IERC20.sol)"
   5 |  import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";

     |  // @audit-issue OpenZeppelin 4.9.3 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.3) (token/ERC20/utils/SafeERC20.sol)"
   6 |  import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L5), [6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L6)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (proxy/utils/Initializable.sol)"
   5 |  import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (access/Ownable2Step.sol)"
   6 |  import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (token/ERC20/IERC20.sol)"
   9 |  import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";

     |  // @audit-issue OpenZeppelin 4.9.3 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.3) (token/ERC20/utils/SafeERC20.sol)"
  10 |  import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L5), [6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L6), [9](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L9), [10](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L10)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (access/Ownable2Step.sol)"
   5 |  import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L5)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (access/Ownable2Step.sol)"
   5 |  import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L5)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (access/Ownable2Step.sol)"
  18 |  import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```
GitHub: [18](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L18)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (access/Ownable2Step.sol)"
   5 |  import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L5)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (utils/math/Math.sol)"
   5 |  import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L5)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

     |  // @audit-issue OpenZeppelin 4.8.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.8.0) (utils/math/SafeCast.sol)"
   5 |  import {SafeCast} from "@openzeppelin/contracts/utils/math/SafeCast.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L5)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (utils/math/Math.sol)"
   5 |  import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L5)


```solidity
File: code/contracts/ethereum/contracts/common/Dependencies.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (proxy/transparent/TransparentUpgradeableProxy.sol)"
   5 |  import "@openzeppelin/contracts/proxy/transparent/TransparentUpgradeableProxy.sol";

     |  // @audit-issue OpenZeppelin 4.8.3 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.8.3) (proxy/transparent/ProxyAdmin.sol)"
   6 |  import "@openzeppelin/contracts/proxy/transparent/ProxyAdmin.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Dependencies.sol#L5), [6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Dependencies.sol#L6)


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

     |  // @audit-issue OpenZeppelin 4.6.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.6.0) (token/ERC20/IERC20.sol)"
   5 |  import "../openzeppelin/token/ERC20/IERC20.sol";

     |  // @audit-issue OpenZeppelin 4.8.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.8.0) (token/ERC20/utils/SafeERC20.sol)"
   6 |  import "../openzeppelin/token/ERC20/utils/SafeERC20.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L5), [6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L6)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (proxy/utils/Initializable.sol)"
   5 |  import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";

     |  // @audit-issue OpenZeppelin 4.7.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.7.0) (proxy/beacon/BeaconProxy.sol)"
   6 |  import {BeaconProxy} from "@openzeppelin/contracts/proxy/beacon/BeaconProxy.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L5), [6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L6)


```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (token/ERC20/extensions/draft-ERC20Permit.sol)"
   5 |  import {ERC20PermitUpgradeable} from "@openzeppelin/contracts-upgradeable/token/ERC20/extensions/draft-ERC20PermitUpgradeable.sol";

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (proxy/ERC1967/ERC1967Upgrade.sol)"
   7 |  import {ERC1967Upgrade} from "@openzeppelin/contracts/proxy/ERC1967/ERC1967Upgrade.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L5), [7](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L7)


```solidity
File: code/contracts/zksync/contracts/Dependencies.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (proxy/transparent/TransparentUpgradeableProxy.sol)"
   5 |  import "@openzeppelin/contracts/proxy/transparent/TransparentUpgradeableProxy.sol";

     |  // @audit-issue OpenZeppelin 4.8.3 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.8.3) (proxy/transparent/ProxyAdmin.sol)"
   6 |  import "@openzeppelin/contracts/proxy/transparent/ProxyAdmin.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/Dependencies.sol#L5), [6](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/Dependencies.sol#L6)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (token/ERC20/IERC20.sol)"
   5 |  import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L5)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

     |  // @audit-issue OpenZeppelin 4.9.0 can be updated to 4.9.5
     |  // "// OpenZeppelin Contracts (last updated v4.9.0) (token/ERC20/extensions/draft-ERC20Permit.sol)"
   5 |  import {ERC20PermitUpgradeable} from "@openzeppelin/contracts-upgradeable/token/ERC20/extensions/draft-ERC20PermitUpgradeable.sol";
```
GitHub: [5](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L5)


## [G-69] Use named `return` parameters

Using named return values instead of explicitly calling `return` saves ~13 execution gas per call and >1000 deployment gas per instance.

*Instances: 99*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Provide names for all return parameters
  75 |  function l2TokenAddress(address _l1Token) external view returns (address) {

     |  // @audit-issue Provide names for all return parameters
 160 |  function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```
GitHub: [75](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L75), [160](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Provide names for all return parameters
 173 |  function _depositFunds(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
 243 |  function _getDepositL2Calldata(
 244 |      address _l1Sender,
 245 |      address _l2Receiver,
 246 |      address _l1Token,
 247 |      uint256 _amount
 248 |  ) internal view returns (bytes memory) {

     |  // @audit-issue Provide names for all return parameters
 254 |  function _getERC20Getters(address _token) internal view returns (bytes memory) {

     |  // @audit-issue Provide names for all return parameters
 374 |  function _isEraLegacyWithdrawal(uint256 _chainId, uint256 _l2BatchNumber) internal view returns (bool) {
```
GitHub: [173](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L173), [243-248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L243-L248), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L254), [374](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L374)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue Provide names for all return parameters
  75 |  function getStateTransition(uint256 _chainId) public view returns (address) {

     |  // @audit-issue Provide names for all return parameters
 152 |  function proveL2MessageInclusion(
 153 |      uint256 _chainId,
 154 |      uint256 _batchNumber,
 155 |      uint256 _index,
 156 |      L2Message calldata _message,
 157 |      bytes32[] calldata _proof
 158 |  ) external view override returns (bool) {

     |  // @audit-issue Provide names for all return parameters
 164 |  function proveL2LogInclusion(
 165 |      uint256 _chainId,
 166 |      uint256 _batchNumber,
 167 |      uint256 _index,
 168 |      L2Log memory _log,
 169 |      bytes32[] calldata _proof
 170 |  ) external view override returns (bool) {

     |  // @audit-issue Provide names for all return parameters
 176 |  function proveL1ToL2TransactionStatus(
 177 |      uint256 _chainId,
 178 |      bytes32 _l2TxHash,
 179 |      uint256 _l2BatchNumber,
 180 |      uint256 _l2MessageIndex,
 181 |      uint16 _l2TxNumberInBatch,
 182 |      bytes32[] calldata _merkleProof,
 183 |      TxStatus _status
 184 |  ) external view override returns (bool) {

     |  // @audit-issue Provide names for all return parameters
 198 |  function l2TransactionBaseCost(
 199 |      uint256 _chainId,
 200 |      uint256 _gasPrice,
 201 |      uint256 _l2GasLimit,
 202 |      uint256 _l2GasPerPubdataByteLimit
 203 |  ) external view returns (uint256) {
```
GitHub: [75](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L75), [152-158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L152-L158), [164-170](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L164-L170), [176-184](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L176-L184), [198-203](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L198-L203)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Provide names for all return parameters
  84 |  function isOperation(bytes32 _id) public view returns (bool) {

     |  // @audit-issue Provide names for all return parameters
  89 |  function isOperationPending(bytes32 _id) public view returns (bool) {

     |  // @audit-issue Provide names for all return parameters
  95 |  function isOperationReady(bytes32 _id) public view returns (bool) {

     |  // @audit-issue Provide names for all return parameters
 100 |  function isOperationDone(bytes32 _id) public view returns (bool) {

     |  // @audit-issue Provide names for all return parameters
 105 |  function getOperationState(bytes32 _id) public view returns (OperationState) {

     |  // @audit-issue Provide names for all return parameters
 204 |  function hashOperation(Operation calldata _operation) public pure returns (bytes32) {
```
GitHub: [84](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L84), [89](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L89), [95](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L95), [100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L100), [105](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L105), [204](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L204)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Provide names for all return parameters
  76 |  function getChainAdmin(uint256 _chainId) external view override returns (address) {
```
GitHub: [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L76)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Provide names for all return parameters
 102 |  function getCommittedBatchTimestamp(uint256 _chainId, uint256 _l2BatchNumber) external view returns (uint256) {
```
GitHub: [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L102)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

     |  // @audit-issue Provide names for all return parameters
  24 |  function initialize(InitializeData calldata _initializeData) external reentrancyGuardInitializer returns (bytes32) {
```
GitHub: [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L24)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Provide names for all return parameters
  32 |  function _commitOneBatch(
  33 |      StoredBatchInfo memory _previousBatch,
  34 |      CommitBatchInfo calldata _newBatch,
  35 |      bytes32 _expectedSystemContractUpgradeTxHash
  36 |  ) internal view returns (StoredBatchInfo memory) {

     |  // @audit-issue Provide names for all return parameters
 453 |  function _getBatchProofPublicInput(
 454 |      bytes32 _prevBatchCommitment,
 455 |      bytes32 _currentBatchCommitment,
 456 |      VerifierParams memory _verifierParams
 457 |  ) internal pure returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
 500 |  function _createBatchCommitment(
 501 |      CommitBatchInfo calldata _newBatchData,
 502 |      bytes32 _stateDiffHash,
 503 |      bytes32[] memory _blobCommitments,
 504 |      bytes32[] memory _blobHashes
 505 |  ) internal view returns (bytes32) {

     |  // @audit-issue Provide names for all return parameters
 515 |  function _batchPassThroughData(CommitBatchInfo calldata _batch) internal pure returns (bytes memory) {

     |  // @audit-issue Provide names for all return parameters
 525 |  function _batchMetaParameters() internal view returns (bytes memory) {

     |  // @audit-issue Provide names for all return parameters
 537 |  function _batchAuxiliaryOutput(
 538 |      CommitBatchInfo calldata _batch,
 539 |      bytes32 _stateDiffHash,
 540 |      bytes32[] memory _blobCommitments,
 541 |      bytes32[] memory _blobHashes
 542 |  ) internal pure returns (bytes memory) {

     |  // @audit-issue Provide names for all return parameters
 587 |  function _hashStoredBatchInfo(StoredBatchInfo memory _storedBatchInfo) internal pure returns (bytes32) {

     |  // @audit-issue Provide names for all return parameters
 592 |  function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

     |  // @audit-issue Provide names for all return parameters
 597 |  function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {
```
GitHub: [32-36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L32-L36), [453-457](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L453-L457), [500-505](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L500-L505), [515](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515), [525](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525), [537-542](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542), [587](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L587), [592](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L592), [597](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-issue Provide names for all return parameters
  32 |  function getVerifier() external view returns (address) {

     |  // @audit-issue Provide names for all return parameters
  37 |  function getAdmin() external view returns (address) {

     |  // @audit-issue Provide names for all return parameters
  42 |  function getPendingAdmin() external view returns (address) {

     |  // @audit-issue Provide names for all return parameters
  47 |  function getBridgehub() external view returns (address) {

     |  // @audit-issue Provide names for all return parameters
  52 |  function getStateTransitionManager() external view returns (address) {

     |  // @audit-issue Provide names for all return parameters
  57 |  function getBaseToken() external view returns (address) {

     |  // @audit-issue Provide names for all return parameters
  62 |  function getBaseTokenBridge() external view returns (address) {

     |  // @audit-issue Provide names for all return parameters
  67 |  function baseTokenGasPriceMultiplierNominator() external view returns (uint128) {

     |  // @audit-issue Provide names for all return parameters
  72 |  function baseTokenGasPriceMultiplierDenominator() external view returns (uint128) {

     |  // @audit-issue Provide names for all return parameters
  77 |  function getTotalBatchesCommitted() external view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
  82 |  function getTotalBatchesVerified() external view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
  87 |  function getTotalBatchesExecuted() external view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
  92 |  function getTotalPriorityTxs() external view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
  97 |  function getFirstUnprocessedPriorityTx() external view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
 102 |  function getPriorityQueueSize() external view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
 107 |  function priorityQueueFrontOperation() external view returns (PriorityOperation memory) {

     |  // @audit-issue Provide names for all return parameters
 112 |  function isValidator(address _address) external view returns (bool) {

     |  // @audit-issue Provide names for all return parameters
 117 |  function l2LogsRootHash(uint256 _batchNumber) external view returns (bytes32) {

     |  // @audit-issue Provide names for all return parameters
 122 |  function storedBatchHash(uint256 _batchNumber) external view returns (bytes32) {

     |  // @audit-issue Provide names for all return parameters
 127 |  function getL2BootloaderBytecodeHash() external view returns (bytes32) {

     |  // @audit-issue Provide names for all return parameters
 132 |  function getL2DefaultAccountBytecodeHash() external view returns (bytes32) {

     |  // @audit-issue Provide names for all return parameters
 137 |  function getVerifierParams() external view returns (VerifierParams memory) {

     |  // @audit-issue Provide names for all return parameters
 142 |  function getProtocolVersion() external view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
 147 |  function getL2SystemContractsUpgradeTxHash() external view returns (bytes32) {

     |  // @audit-issue Provide names for all return parameters
 152 |  function getL2SystemContractsUpgradeBatchNumber() external view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
 157 |  function isDiamondStorageFrozen() external view returns (bool) {

     |  // @audit-issue Provide names for all return parameters
 176 |  function getPriorityTxMaxGasLimit() external view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
 181 |  function isFunctionFreezable(bytes4 _selector) external view returns (bool) {

     |  // @audit-issue Provide names for all return parameters
 188 |  function isEthWithdrawalFinalized(uint256 _l2BatchNumber, uint256 _l2MessageIndex) external view returns (bool) {

     |  // @audit-issue Provide names for all return parameters
 193 |  function getPubdataPricingMode() external view returns (PubdataPricingMode) {

     |  // @audit-issue Provide names for all return parameters
 217 |  function facetFunctionSelectors(address _facet) external view returns (bytes4[] memory) {

     |  // @audit-issue Provide names for all return parameters
 223 |  function facetAddresses() external view returns (address[] memory) {

     |  // @audit-issue Provide names for all return parameters
 229 |  function facetAddress(bytes4 _selector) external view returns (address) {

     |  // @audit-issue Provide names for all return parameters
 239 |  function getTotalBlocksCommitted() external view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
 244 |  function getTotalBlocksVerified() external view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
 249 |  function getTotalBlocksExecuted() external view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
 254 |  function storedBlockHash(uint256 _batchNumber) external view returns (bytes32) {

     |  // @audit-issue Provide names for all return parameters
 259 |  function getL2SystemContractsUpgradeBlockNumber() external view returns (uint256) {
```
GitHub: [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L32), [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L37), [42](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L42), [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L47), [52](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L52), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L57), [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L62), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L67), [72](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L72), [77](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L77), [82](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L82), [87](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L87), [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L92), [97](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L97), [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L102), [107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L107), [112](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L112), [117](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L117), [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L122), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L127), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L132), [137](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L137), [142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L142), [147](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L147), [152](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L152), [157](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L157), [176](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L176), [181](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L181), [188](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L188), [193](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L193), [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L217), [223](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L223), [229](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L229), [239](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L239), [244](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L244), [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L249), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L254), [259](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L259)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Provide names for all return parameters
  54 |  function proveL2MessageInclusion(
  55 |      uint256 _batchNumber,
  56 |      uint256 _index,
  57 |      L2Message memory _message,
  58 |      bytes32[] calldata _proof
  59 |  ) public view returns (bool) {

     |  // @audit-issue Provide names for all return parameters
  64 |  function proveL2LogInclusion(
  65 |      uint256 _batchNumber,
  66 |      uint256 _index,
  67 |      L2Log memory _log,
  68 |      bytes32[] calldata _proof
  69 |  ) external view returns (bool) {

     |  // @audit-issue Provide names for all return parameters
  74 |  function proveL1ToL2TransactionStatus(
  75 |      bytes32 _l2TxHash,
  76 |      uint256 _l2BatchNumber,
  77 |      uint256 _l2MessageIndex,
  78 |      uint16 _l2TxNumberInBatch,
  79 |      bytes32[] calldata _merkleProof,
  80 |      TxStatus _status
  81 |  ) public view returns (bool) {

     |  // @audit-issue Provide names for all return parameters
 104 |  function _proveL2LogInclusion(
 105 |      uint256 _batchNumber,
 106 |      uint256 _index,
 107 |      L2Log memory _log,
 108 |      bytes32[] calldata _proof
 109 |  ) internal view returns (bool) {

     |  // @audit-issue Provide names for all return parameters
 130 |  function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {

     |  // @audit-issue Provide names for all return parameters
 143 |  function l2TransactionBaseCost(
 144 |      uint256 _gasPrice,
 145 |      uint256 _l2GasLimit,
 146 |      uint256 _l2GasPerPubdataByteLimit
 147 |  ) public view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
 156 |  function _deriveL2GasPrice(uint256 _l1GasPrice, uint256 _gasPerPubdata) internal view returns (uint256) {
```
GitHub: [54-59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L54-L59), [64-69](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L64-L69), [74-81](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L74-L81), [104-109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L104-L109), [130](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L130), [143-147](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L143-L147), [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L156)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Provide names for all return parameters
 180 |  function _setL2SystemContractUpgrade(
 181 |      L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
 182 |      bytes[] calldata _factoryDeps,
 183 |      uint256 _newProtocolVersion
 184 |  ) internal returns (bytes32) {
```
GitHub: [180-184](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L180-L184)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

     |  // @audit-issue Provide names for all return parameters
  47 |  function upgrade(ProposedUpgrade calldata _proposedUpgrade) public virtual override returns (bytes32) {
```
GitHub: [47](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L47)


```solidity
File: code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

     |  // @audit-issue Provide names for all return parameters
  13 |  function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```
GitHub: [13](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L13)


```solidity
File: code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

     |  // @audit-issue Provide names for all return parameters
  14 |  function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```
GitHub: [14](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L14)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

     |  // @audit-issue Provide names for all return parameters
  60 |  function computeCreate2Address(
  61 |      address _sender,
  62 |      bytes32 _salt,
  63 |      bytes32 _bytecodeHash,
  64 |      bytes32 _constructorInputHash
  65 |  ) internal pure returns (address) {
```
GitHub: [60-65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L60-L65)


```solidity
File: code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol

     |  // @audit-issue Provide names for all return parameters
  11 |  function uncheckedInc(uint256 _number) internal pure returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
  17 |  function uncheckedAdd(uint256 _lhs, uint256 _rhs) internal pure returns (uint256) {
```
GitHub: [11](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L11), [17](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L17)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

     |  // @audit-issue Provide names for all return parameters
  18 |  function calculateRoot(
  19 |      bytes32[] calldata _path,
  20 |      uint256 _index,
  21 |      bytes32 _itemHash
  22 |  ) internal pure returns (bytes32) {
```
GitHub: [18-22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L18-L22)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

     |  // @audit-issue Provide names for all return parameters
  35 |  function getFirstUnprocessedPriorityTx(Queue storage _queue) internal view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
  40 |  function getTotalPriorityTxs(Queue storage _queue) internal view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
  45 |  function getSize(Queue storage _queue) internal view returns (uint256) {

     |  // @audit-issue Provide names for all return parameters
  50 |  function isEmpty(Queue storage _queue) internal view returns (bool) {

     |  // @audit-issue Provide names for all return parameters
  64 |  function front(Queue storage _queue) internal view returns (PriorityOperation memory) {
```
GitHub: [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L35), [40](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L40), [45](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L45), [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L50), [64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L64)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

     |  // @audit-issue Provide names for all return parameters
  69 |  function getMinimalPriorityTransactionGasLimit(
  70 |      uint256 _encodingLength,
  71 |      uint256 _numberOfFactoryDependencies,
  72 |      uint256 _l2GasPricePerPubdata
  73 |  ) internal pure returns (uint256) {
```
GitHub: [69-73](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L69-L73)


```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

     |  // @audit-issue Provide names for all return parameters
  24 |  function isWithdrawalFinalized(uint256 _l2BatchNumber, uint256 _l2MessageIndex) external view returns (bool);

     |  // @audit-issue Provide names for all return parameters
  61 |  function l2TokenAddress(address _l1Token) external view returns (address);

     |  // @audit-issue Provide names for all return parameters
  63 |  function sharedBridge() external view returns (IL1SharedBridge);

     |  // @audit-issue Provide names for all return parameters
  65 |  function l2TokenBeacon() external view returns (address);

     |  // @audit-issue Provide names for all return parameters
  67 |  function l2Bridge() external view returns (address);
```
GitHub: [24](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L24), [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L67)


```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

     |  // @audit-issue Provide names for all return parameters
  58 |  function isWithdrawalFinalized(
  59 |      uint256 _chainId,
  60 |      uint256 _l2BatchNumber,
  61 |      uint256 _l2MessageIndex
  62 |  ) external view returns (bool);

     |  // @audit-issue Provide names for all return parameters
 114 |  function l1WethAddress() external view returns (address);

     |  // @audit-issue Provide names for all return parameters
 116 |  function bridgehub() external view returns (IBridgehub);

     |  // @audit-issue Provide names for all return parameters
 118 |  function legacyBridge() external view returns (IL1ERC20Bridge);

     |  // @audit-issue Provide names for all return parameters
 120 |  function l2BridgeAddress(uint256 _chainId) external view returns (address);

     |  // @audit-issue Provide names for all return parameters
 122 |  function depositHappened(uint256 _chainId, bytes32 _l2TxHash) external view returns (bytes32);
```
GitHub: [58-62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L58-L62), [114](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L114), [116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L116), [118](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L118), [120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L120), [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L122)


## [G-70] Use nested `if`s instead of `&&`

Optimization of condition checks in your smart contract is a crucial aspect in ensuring gas efficiency. Specifically, substituting multiple `&&` checks with nested `if` statements can lead to substantial gas savings.

When evaluating multiple conditions within a single `if` statement using the `&&` operator, each condition will consume gas even if a preceding condition fails. However, if these checks are broken down into nested `if` statements, execution halts as soon as a condition fails, saving the gas that would have been consumed by subsequent checks.

This practice is especially beneficial in scenarios where the `if` statement isn't followed by an `else` statement. The reason being, when an `else` statement is present, all conditions must be checked regardless to determine the correct branch of execution.

By reworking your code to utilize nested `if` statements, you can optimize gas usage, reduce execution cost, and enhance your contract's performance.

*Instances: 7*

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Save gas by using nested `if`
 361 |  if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {
```
GitHub: [361](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L361)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Save gas by using nested `if`
 148 |  _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) &&
 149 |  _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) &&
 150 |  _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)
```
GitHub: [148-150](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L148-L150)


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

     |  // @audit-issue Save gas by using nested `if`
 132 |  uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS &&
 133 |  codeHash != 0x00 &&
 134 |  !Utils.isContractConstructing(codeHash)
```
GitHub: [132-134](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L132-L134)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Save gas by using nested `if`
  48 |  _address > address(MAX_SYSTEM_CONTRACT_ADDRESS) &&
  49 |  ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getRawCodeHash(_address) == 0
```
GitHub: [48-49](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L48-L49)


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

     |  // @audit-issue Save gas by using nested `if`
 139 |  if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) {
```
GitHub: [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L139)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-issue Save gas by using nested `if`
  88 |  if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {

     |  // @audit-issue Save gas by using nested `if`
 171 |  } else if (!isUsed && _shouldBeUsed) {
```
GitHub: [88](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L88), [171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L171)


## [G-71] Use of low-level `call()` can be optimized with assembly

Low-level calls, when optimized with assembly, can save gas by avoiding unnecessary operations related to unused returndata. In a typical `.call`, Solidity automatically allocates memory and handles returndata even if it's not used, incurring extra gas costs. By using assembly, a developer can precisely control the execution, selectively ignoring or handling returndata, thereby optimizing gas usage. This specific control over the EVM allows for more efficient execution of calls by eliminating unnecessary memory operations, providing a more gas-efficient method when unused returndata is a concern. However, such optimization should be handled with care, as improper use of assembly might lead to vulnerabilities.

*Instances: 7*

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Consider using call in assembly for gas savings
 226 |  (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```
GitHub: [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

     |  // @audit-issue Consider using call in assembly for gas savings
 283 |  (bool success, bytes memory data) = _init.delegatecall(_calldata);
```
GitHub: [283](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L283)


```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

     |  // @audit-issue Consider using call in assembly for gas savings
  25 |  (bool success, bytes memory returnData) = _delegateTo.delegatecall(_calldata);
```
GitHub: [25](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L25)


```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

     |  // @audit-issue Consider using call in assembly for gas savings
  63 |  (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call(
  64 |      abi.encodeCall(REAL_BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo, (msg.sender, to, value))
  65 |  );
```
GitHub: [63-65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L63-L65)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

     |  // @audit-issue Consider using call in assembly for gas savings
  63 |  (bool success, ) = payable(BOOTLOADER_ADDRESS).call{value: requiredETH}("");
```
GitHub: [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L63)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

     |  // @audit-issue Consider using call in assembly for gas savings
  83 |  (bool success, ) = msg.sender.call{value: _amount}("");

     |  // @audit-issue Consider using call in assembly for gas savings
 108 |  (bool success, ) = _to.call{value: _amount}("");
```
GitHub: [83](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L83), [108](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L108)


## [G-72] Using `bool`s for storage incurs overhead

```solidity
    // Booleans are more expensive than uint256 or any type that takes up a full
    // word because each write operation emits an extra SLOAD to first read the
    // slot's contents, replace the bits taken up by the boolean, and then write
    // back. This is the compiler's defense against contract upgrades and
    // pointer aliasing, and it cannot be disabled.
```
https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27
Use `uint256(0)` and `uint256(1)` for true/false to avoid a Gwarmaccess (**[100 gas](https://gist.github.com/IllIllI000/1b70014db712f8572a72378321250058)**) for the extra SLOAD

*Instances: 6*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

  27 |  mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
  28 |      public isWithdrawalFinalized;
```
GitHub: [27-28](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27-L28)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

  57 |  mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
  58 |      public isWithdrawalFinalized;

  61 |  mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;
```
GitHub: [57-58](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57-L58), [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L61)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

  21 |  mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;

  23 |  mapping(address _token => bool) public tokenIsRegistered;
```
GitHub: [21](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21), [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L23)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

  50 |  mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
GitHub: [50](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50)


## [G-73] Using `storage` instead of `memory` for structs/arrays saves gas

When fetching data from a storage location, assigning the data to a `memory` variable causes all fields of the struct/array to be read from storage, which incurs a Gcoldsload (**2100 gas**) for *each* field of the struct/array. If the fields are read from the new memory variable, they incur an additional `MLOAD` rather than a cheap stack read. Instead of declearing the variable with the `memory` keyword, declaring the variable with the `storage` keyword and caching any fields that need to be re-read in stack variables, will be much cheaper, only incuring the Gcoldsload for the fields actually read. The only time it makes sense to read the whole struct/array into a `memory` variable, is if the full struct/array is being returned by the function, is being passed to a function that requires `memory`, or if the array/struct is being read from another `memory` array/struct.

*Instances: 2*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 219 |  request = L2TransactionRequestTwoBridgesInner({
 220 |      magicValue: TWO_BRIDGES_MAGIC_VALUE,
 221 |      l2Contract: l2BridgeAddress[_chainId],
 222 |      l2Calldata: l2TxCalldata,
 223 |      factoryDeps: new bytes[](0),
 224 |      txDataHash: txDataHash
 225 |  });
```
GitHub: [219-225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L219-L225)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

 265 |  _params.txId = s.priorityQueue.getTotalPriorityTxs();
```
GitHub: [265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L265)


## [G-74] Using assembly's `selfbalance()` is cheaper than `address(this).balance`

Saves 159 gas per instance:
```solidity
    assembly {
        mstore(0x00, selfbalance())
        return(0x00, 0x20)
    }
```

*Instances: 4*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Use assembly selfbalance()
 118 |  uint256 balanceBefore = address(this).balance;

     |  // @audit-issue Use assembly selfbalance()
 120 |  uint256 balanceAfter = address(this).balance;
```
GitHub: [118](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118), [120](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Use assembly selfbalance()
  41 |  uint256 amount = address(this).balance;
```
GitHub: [41](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41)


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

     |  // @audit-issue Use assembly selfbalance()
 100 |  require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");
```
GitHub: [100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L100)


## [G-75] `++i` costs less gas than `i++`, especially when it's used in `for`-loops (`--i`/`i--` too)

Try pre-increment (`++i`) or pre-decrement (`--i`).

*Instances: 8*

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Switch to the pre-increment/decrement form
 580 |  for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

     |  // @audit-issue Switch to the pre-increment/decrement form
 667 |  for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
GitHub: [580](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580), [667](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue Switch to the pre-increment/decrement form
 135 |  numInitialWritesProcessed++;

     |  // @audit-issue Switch to the pre-increment/decrement form
 144 |  stateDiffPtr++;
```
GitHub: [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L135), [144](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L144)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Switch to the pre-increment/decrement form
 109 |  numberOfLogsToProcess++;

     |  // @audit-issue Switch to the pre-increment/decrement form
 284 |  calldataPtr++;

     |  // @audit-issue Switch to the pre-increment/decrement form
 290 |  calldataPtr++;
```
GitHub: [109](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L109), [284](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L284), [290](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L290)


```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

     |  // @audit-issue Switch to the pre-increment/decrement form
  36 |  for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
GitHub: [36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)


## [G-76] `++i`/`i++` should be `unchecked{++i}`/`unchecked{i++}` when it is not possible for them to overflow, as is the case when used in `for`- and `while`-loops

The `unchecked` keyword is new in solidity version 0.8.0, so this only applies to that version or higher, which these instances are. This saves **30-40 gas [per loop](https://gist.github.com/hrkrshnn/ee8fabd532058307229d65dcd5836ddc#the-increment-in-for-loop-post-condition-can-be-made-unchecked)**

*Instances: 18*

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 225 |  for (uint256 i = 0; i < _calls.length; ++i) {
```
GitHub: [225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 116 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 135 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 185 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 209 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```
GitHub: [116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185), [209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 580 |  for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 667 |  for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
GitHub: [580](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580), [667](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 226 |  for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
GitHub: [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 248 |  for (uint256 i = 0; i < deploymentsLength; ++i) {

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 253 |  for (uint256 i = 0; i < deploymentsLength; ++i) {
```
GitHub: [248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L248), [253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L253)


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
  38 |  for (uint256 i = 0; i < immutablesLength; ++i) {
```
GitHub: [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L38)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
  30 |  for (uint256 i = 0; i < hashesLen; ++i) {
```
GitHub: [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L30)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 206 |  for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 218 |  for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 224 |  for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 236 |  for (uint256 i = 0; i < numberOfMessages; ++i) {

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
 254 |  for (uint256 i = 0; i < numberOfBytecodes; ++i) {
```
GitHub: [206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L206), [218](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L218), [224](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L224), [236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L236), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L254)


```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

     |  // @audit-issue Consider incrementing loop variable in an `unchecked` block
  36 |  for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
GitHub: [36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)


## [G-77] `<array>.length` should not be looked up in every loop of a `for`-loop

The overheads outlined below are _PER LOOP_, excluding the first loop:

* storage arrays incur a Gwarmaccess (**100 gas**)
* memory arrays use `MLOAD` (**3 gas**)
* calldata arrays use `CALLDATALOAD` (**3 gas**)

Caching the length changes each of these to a `DUP<N>` (**3 gas**), and gets rid of the extra `DUP<N>` needed to store the stack offset

*Instances: 8*

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Cache .length outside the loop expression
 225 |  for (uint256 i = 0; i < _calls.length; ++i) {
```
GitHub: [225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Cache .length outside the loop expression
 116 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Cache .length outside the loop expression
 135 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Cache .length outside the loop expression
 185 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Cache .length outside the loop expression
 209 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```
GitHub: [116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185), [209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Cache .length outside the loop expression
 257 |  for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

     |  // @audit-issue Cache .length outside the loop expression
 289 |  for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
```
GitHub: [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Cache .length outside the loop expression
 226 |  for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
GitHub: [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226)


## [G-78] `<x> += <y>` costs more gas than `<x> = <x> + <y>` for state variables

Using the addition operator instead of plus-equals saves **[113 gas](https://gist.github.com/IllIllI000/cbbfb267425b898e5be734d4008d4fe8)**

*Instances: 11*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Switch to <x> + <y> and <x> - <y>
 165 |  chainBalance[_chainId][_l1Token] += _amount;

     |  // @audit-issue Switch to <x> + <y> and <x> - <y>
 212 |  chainBalance[_chainId][_l1Token] += amount;

     |  // @audit-issue Switch to <x> + <y> and <x> - <y>
 350 |  chainBalance[_chainId][_l1Token] -= _amount;

     |  // @audit-issue Switch to <x> + <y> and <x> - <y>
 440 |  chainBalance[_chainId][l1Token] -= amount;

     |  // @audit-issue Switch to <x> + <y> and <x> - <y>
 568 |  chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
```
GitHub: [165](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L165), [212](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L212), [350](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L350), [440](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L440), [568](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L568)


```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

     |  // @audit-issue Switch to <x> + <y> and <x> - <y>
  46 |  balance[_to] += _amount;

     |  // @audit-issue Switch to <x> + <y> and <x> - <y>
  65 |  totalSupply += _amount;

     |  // @audit-issue Switch to <x> + <y> and <x> - <y>
  66 |  balance[_account] += _amount;

     |  // @audit-issue Switch to <x> + <y> and <x> - <y>
 106 |  balance[address(this)] -= amount;

     |  // @audit-issue Switch to <x> + <y> and <x> - <y>
 107 |  totalSupply -= amount;
```
GitHub: [46](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L46), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L65), [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L66), [106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L106), [107](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L107)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Switch to <x> + <y> and <x> - <y>
 483 |  txNumberInBlock += 1;
```
GitHub: [483](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L483)


## [G-79] `abi.encode()` is less efficient than `abi.encodepacked()` for non-address arguments

See for more information: https://github.com/ConnorBlockchain/Solidity-Encode-Gas-Comparison

*Instances: 34*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

     |  // @audit-issue Consider `abi.encodePacked()`
  76 |  bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
```
GitHub: [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76)


```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue Consider `abi.encodePacked()`
 210 |  bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));

     |  // @audit-issue Consider `abi.encodePacked()`
 258 |  bytes memory decimals = abi.encode(uint8(18));

     |  // @audit-issue Consider `abi.encodePacked()`
 259 |  return abi.encode(name, symbol, decimals); // when depositing eth to a non-eth based chain it is an ERC20

     |  // @audit-issue Consider `abi.encodePacked()`
 265 |  return abi.encode(data1, data2, data3);

     |  // @audit-issue Consider `abi.encodePacked()`
 341 |  bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));

     |  // @audit-issue Consider `abi.encodePacked()`
 598 |  bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
```
GitHub: [210](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L210), [258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L258), [259](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L259), [265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L265), [341](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L341), [598](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L598)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Consider `abi.encodePacked()`
 205 |  return keccak256(abi.encode(_operation));
```
GitHub: [205](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L205)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue Consider `abi.encodePacked()`
 102 |  storedBatchZero = keccak256(abi.encode(batchZero));

     |  // @audit-issue Consider `abi.encodePacked()`
 104 |  initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

     |  // @audit-issue Consider `abi.encodePacked()`
 140 |  initialCutHash = keccak256(abi.encode(_diamondCut));

     |  // @audit-issue Consider `abi.encodePacked()`
 149 |  upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

     |  // @audit-issue Consider `abi.encodePacked()`
 158 |  upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
```
GitHub: [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102), [104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L104), [140](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L140), [149](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L149), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L158)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue Consider `abi.encodePacked()`
 104 |  bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
```
GitHub: [104](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Consider `abi.encodePacked()`
 313 |  concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));

     |  // @audit-issue Consider `abi.encodePacked()`
 512 |  return keccak256(abi.encode(passThroughDataHash, metadataHash, auxiliaryOutputHash));

     |  // @audit-issue Consider `abi.encodePacked()`
 588 |  return keccak256(abi.encode(_storedBatchInfo));

     |  // @audit-issue Consider `abi.encodePacked()`
 680 |  (bool success, bytes memory data) = s.blobVersionedHashRetriever.staticcall(abi.encode(_index));
```
GitHub: [313](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313), [512](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L512), [588](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L588), [680](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L680)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Consider `abi.encodePacked()`
 323 |  bytes memory transactionEncoding = abi.encode(transaction);
```
GitHub: [323](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L323)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Consider `abi.encodePacked()`
 192 |  bytes memory encodedTransaction = abi.encode(_l2ProtocolUpgradeTx);
```
GitHub: [192](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L192)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Consider `abi.encodePacked()`
 106 |  chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

     |  // @audit-issue Consider `abi.encodePacked()`
 122 |  chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

     |  // @audit-issue Consider `abi.encodePacked()`
 164 |  chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

     |  // @audit-issue Consider `abi.encodePacked()`
 212 |  reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));

     |  // @audit-issue Consider `abi.encodePacked()`
 226 |  abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])

     |  // @audit-issue Consider `abi.encodePacked()`
 243 |  reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));

     |  // @audit-issue Consider `abi.encodePacked()`
 260 |  abi.encode(
 261 |      reconstructedChainedL1BytecodesRevealDataHash,
 262 |      Utils.hashL2Bytecode(
 263 |          _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
 264 |      )
 265 |  )
```
GitHub: [106](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L106), [122](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L122), [164](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L164), [212](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L212), [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L226), [243](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L243), [260-265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L260-L265)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue Consider `abi.encodePacked()`
 159 |  hash = keccak256(abi.encode(_block));

     |  // @audit-issue Consider `abi.encodePacked()`
 227 |  return keccak256(abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash));

     |  // @audit-issue Consider `abi.encodePacked()`
 403 |  currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));
```
GitHub: [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L159), [227](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L227), [403](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L403)


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

     |  // @audit-issue Consider `abi.encodePacked()`
 120 |  abi.encode(
 121 |      EIP712_TRANSACTION_TYPE_HASH,
 122 |      _transaction.txType,
 123 |      _transaction.from,
 124 |      _transaction.to,
 125 |      _transaction.gasLimit,
 126 |      _transaction.gasPerPubdataByteLimit,
 127 |      _transaction.maxFeePerGas,
 128 |      _transaction.maxPriorityFeePerGas,
 129 |      _transaction.paymaster,
 130 |      _transaction.nonce,
 131 |      _transaction.value,
 132 |      EfficientCall.keccak(_transaction.data),
 133 |      keccak256(abi.encodePacked(_transaction.factoryDeps)),
 134 |      EfficientCall.keccak(_transaction.paymasterInput)
 135 |  )

     |  // @audit-issue Consider `abi.encodePacked()`
 139 |  abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
```
GitHub: [120-135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L120-L135), [139](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-issue Consider `abi.encodePacked()`
 150 |  bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""));

     |  // @audit-issue Consider `abi.encodePacked()`
 171 |  (salt, l2TokenProxyBytecodeHash, abi.encode(address(l2TokenBeacon), ""))
```
GitHub: [150](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150), [171](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L171)


## [G-80] `do`-`while` is cheaper than `for`-loops when the initial check can be skipped

A `do while` loop will cost less gas if the condition does not need to be checked in the first iteration:

```solidity
for (uint256 i; i < len; ++i) { ... } // when 'len' is known to be > 0
```
  
could be written as:

```solidity
do { ...; ++i } while (i < len);
```


*Instances: 35*

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue Save gas by switching to a do-while loop
 225 |  for (uint256 i = 0; i < _calls.length; ++i) {
```
GitHub: [225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue Save gas by switching to a do-while loop
 116 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Save gas by switching to a do-while loop
 135 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Save gas by switching to a do-while loop
 185 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

     |  // @audit-issue Save gas by switching to a do-while loop
 209 |  for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```
GitHub: [116](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116), [135](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185), [209](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue Save gas by switching to a do-while loop
 142 |  for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

     |  // @audit-issue Save gas by switching to a do-while loop
 257 |  for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

     |  // @audit-issue Save gas by switching to a do-while loop
 289 |  for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

     |  // @audit-issue Save gas by switching to a do-while loop
 311 |  for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {

     |  // @audit-issue Save gas by switching to a do-while loop
 351 |  for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {

     |  // @audit-issue Save gas by switching to a do-while loop
 405 |  for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {

     |  // @audit-issue Save gas by switching to a do-while loop
 580 |  for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

     |  // @audit-issue Save gas by switching to a do-while loop
 636 |  for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {

     |  // @audit-issue Save gas by switching to a do-while loop
 667 |  for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
GitHub: [142](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142), [257](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257), [289](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289), [311](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L311), [351](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351), [405](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L405), [580](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580), [636](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636), [667](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

     |  // @audit-issue Save gas by switching to a do-while loop
 208 |  for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {
```
GitHub: [208](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue Save gas by switching to a do-while loop
 356 |  for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {
```
GitHub: [356](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue Save gas by switching to a do-while loop
 226 |  for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
GitHub: [226](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

     |  // @audit-issue Save gas by switching to a do-while loop
 101 |  for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {

     |  // @audit-issue Save gas by switching to a do-while loop
 138 |  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

     |  // @audit-issue Save gas by switching to a do-while loop
 158 |  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

     |  // @audit-issue Save gas by switching to a do-while loop
 178 |  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
```
GitHub: [101](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101), [138](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L138), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158), [178](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L178)


```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

     |  // @audit-issue Save gas by switching to a do-while loop
  29 |  for (uint256 i; i < pathLength; i = i.uncheckedInc()) {
```
GitHub: [29](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L29)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue Save gas by switching to a do-while loop
  61 |  for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {

     |  // @audit-issue Save gas by switching to a do-while loop
 127 |  for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

     |  // @audit-issue Save gas by switching to a do-while loop
 159 |  for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
```
GitHub: [61](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L61), [127](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L127), [159](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L159)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue Save gas by switching to a do-while loop
 248 |  for (uint256 i = 0; i < deploymentsLength; ++i) {

     |  // @audit-issue Save gas by switching to a do-while loop
 253 |  for (uint256 i = 0; i < deploymentsLength; ++i) {
```
GitHub: [248](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L248), [253](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L253)


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

     |  // @audit-issue Save gas by switching to a do-while loop
  38 |  for (uint256 i = 0; i < immutablesLength; ++i) {
```
GitHub: [38](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L38)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

     |  // @audit-issue Save gas by switching to a do-while loop
  30 |  for (uint256 i = 0; i < hashesLen; ++i) {
```
GitHub: [30](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L30)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue Save gas by switching to a do-while loop
 206 |  for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

     |  // @audit-issue Save gas by switching to a do-while loop
 218 |  for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

     |  // @audit-issue Save gas by switching to a do-while loop
 224 |  for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

     |  // @audit-issue Save gas by switching to a do-while loop
 236 |  for (uint256 i = 0; i < numberOfMessages; ++i) {

     |  // @audit-issue Save gas by switching to a do-while loop
 254 |  for (uint256 i = 0; i < numberOfBytecodes; ++i) {
```
GitHub: [206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L206), [218](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L218), [224](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L224), [236](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L236), [254](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L254)


```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

     |  // @audit-issue Save gas by switching to a do-while loop
  36 |  for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
GitHub: [36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)


## [G-81] require()`/`revert()` strings longer than 32 bytes cost extra gas

Each extra memory word of bytes past the original 32 [incurs an MSTORE](https://gist.github.com/hrkrshnn/ee8fabd532058307229d65dcd5836ddc#consider-having-short-revert-strings) which costs **3 gas**

*Instances: 70*

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 155 |  require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 195 |  require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 427 |  require(!alreadyFinalized, "Withdrawal is already finalized 2");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 564 |  require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
```
GitHub: [155](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L155), [195](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195), [427](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L427), [564](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564)


```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 102 |  require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 132 |  require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 225 |  require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");
```
GitHub: [102](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102), [132](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132), [225](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225)


```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  59 |  require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  65 |  require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 172 |  require(isOperationReady(id), "Operation must be ready before execution");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 177 |  require(isOperationReady(id), "Operation must be ready after execution");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 191 |  require(isOperationPending(id), "Operation must be pending before execution");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 196 |  require(isOperationPending(id), "Operation must be pending after execution");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 216 |  require(!isOperation(_id), "Operation with this proposal id already exists");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 217 |  require(_delay >= minDelay, "Proposed delay is less than minimum delay");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 240 |  require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");
```
GitHub: [59](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L59), [65](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L65), [172](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L172), [177](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L177), [191](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L191), [196](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L196), [216](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L216), [217](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L217), [240](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L240)


```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 258 |  require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");
```
GitHub: [258](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L258)


```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  62 |  require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  68 |  require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
```
GitHub: [62](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  90 |  require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed
```
GitHub: [90](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 616 |  require(success, "failed to call point evaluation precompile");
```
GitHub: [616](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  39 |  require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 158 |  require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 185 |  require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 206 |  require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");
```
GitHub: [39](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39), [158](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158), [185](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L185), [206](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L206)


```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  22 |  require(s.validators[msg.sender], "StateTransition Chain: not validator");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  27 |  require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  32 |  require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  53 |  require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
```
GitHub: [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22), [27](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27), [32](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32), [53](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 190 |  require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 249 |  require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
```
GitHub: [190](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L190), [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L249)


```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  33 |  require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
```
GitHub: [33](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33)


```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  26 |  require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  37 |  require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  48 |  require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  57 |  require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");
```
GitHub: [26](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L26), [37](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L37), [48](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L48), [57](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L57)


```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  22 |  require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");
```
GitHub: [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L22)


```solidity
File: code/system-contracts/contracts/Compressor.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  63 |  require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  68 |  require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 119 |  require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 156 |  require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 187 |  require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 230 |  require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");
```
GitHub: [63](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L63), [68](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L68), [119](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L119), [156](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L156), [187](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L187), [230](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L230)


```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

     |  // @audit-issue @audit-issue Literal string here uses 2 additional words(s)
 251 |  require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 265 |  require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 350 |  require(value == 0, "The value must be zero if we do not call the constructor");
```
GitHub: [251](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L251), [265](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L265), [350](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L350)


```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 100 |  require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 202 |  require(success, "Failed to pay the fee to the operator");
```
GitHub: [100](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L100), [202](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L202)


```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  35 |  require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
GitHub: [35](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L35)


```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  76 |  require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
```
GitHub: [76](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L76)


```solidity
File: code/system-contracts/contracts/L1Messenger.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 315 |  require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");
```
GitHub: [315](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L315)


```solidity
File: code/system-contracts/contracts/NonceHolder.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  66 |  require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");
```
GitHub: [66](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L66)


```solidity
File: code/system-contracts/contracts/SystemContext.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 242 |  require(_isFirstInBatch, "Upgrade transaction must be first");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 245 |  require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 249 |  require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 355 |  require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 367 |  require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 368 |  require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 373 |  require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 385 |  require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 413 |  require(currentBatchNumber > 0, "The current batch number must be greater than 0");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 452 |  require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
```
GitHub: [242](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L242), [245](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L245), [249](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L249), [355](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L355), [367](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L367), [368](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L368), [373](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L373), [385](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L385), [413](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L413), [452](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L452)


```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 319 |  require(index < 10, "There are only 10 accessible registers");
```
GitHub: [319](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319)


```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
 363 |  require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");
```
GitHub: [363](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L363)


```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  92 |  require(msg.value == 0, "Value should be 0 for ERC20 bridge");
```
GitHub: [92](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92)


```solidity
File: code/contracts/zksync/contracts/TestnetPaymaster.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  22 |  require(msg.sender == BOOTLOADER_ADDRESS, "Only bootloader can call this contract");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  23 |  require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  36 |  require(providedAllowance >= amount, "The user did not provide enough allowance");

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  64 |  require(success, "Failed to transfer funds to the bootloader");
```
GitHub: [22](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L22), [23](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L23), [36](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L36), [64](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/TestnetPaymaster.sol#L64)


```solidity
File: code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

     |  // @audit-issue @audit-issue Literal string here uses 1 additional words(s)
  51 |  require(_l1Address != address(0), "L1 WETH token address cannot be zero");
```
GitHub: [51](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L51)
