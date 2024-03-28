# Gas Optimizations

<details>
  <summary>DISCLAIMER</summary>

---

While we've tried our best to maintain readability for brevity and focus, we have selectively truncated the code snippets to spotlight relevant sections. Certain excerpts may be abbreviated, and some references are provided via search commands due to the extensive nature of the project and time constraints.

---

We urge developers to proceed with caution when implementing recommended changes to ensure no new vulnerabilities are introduced. Although we have pre-tested a fair amount of suggested optimizations logically, the onus of comprehensive validation remains with the development team. Rigorous code review and further testing are imperative to mitigate potential risks during the refactoring process.

---

Finally, it's important to mention that a previous audit conducted [a few months back by Code4rena](https://github.com/code-423n4/2023-10-zksync) on an [older commit](https://github.com/code-423n4/2024-03-zksync/compare/2023-10-zksync...main) of the contracts in scope, this contest had a bot race and as such yielded a [bot report](https://raw.githubusercontent.com/code-423n4/2023-10-zksync/main/bot-report.md) with multiple gas optimization findings in `1014` instances. Our quick review on the optimizations revealed that only few of thosse suggestions have been acted upon. We recommend that, alongside this report, the team also revisits the [bot report](https://raw.githubusercontent.com/code-423n4/2023-10-zksync/main/bot-report.md) to explore further opportunities for gas savings, this is cause we've deliberately tried our best in not duplicating points from that previous analysis in this report.

---

</details>

## Table of Contents

| Issue ID                                                                                                                                                                                                                   | Description                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [G-01](#g-01-multiple-instances-in-scope-where-re-ordering-and-packing-could-save-multiple-storage-slots-in-scope)                                                                                                         | Multiple instances in scope where re-ordering and packing could save multiple storage slots in scope                                                                                                        |
| [G-02](<#g-02-consider-removing-unnecessary-variables-_(one-time-usage)_-in-different-files-in-scope-being-cached-during-executions>)                                                                                      | Consider removing unnecessary variables _(one time usage)_ in different files in scope being cached during executions                                                                                       |
| [G-03](#g-03-consider-using-storage-instead-of-memory-for-structs-or-arrays-inorder-to-save-gas)                                                                                                                           | Consider using storage instead of memory for structs or arrays inorder to save gas                                                                                                                          |
| [G-04](#g-04-we-can-avoid-multiple-sstores-in-case-of-reverts)                                                                                                                                                             | We can avoid multiple SSTOREs in case of reverts                                                                                                                                                            |
| [G-05](#g-05-non-gas-efficient-lookup-of-mappings-in-diamond.sol-&-l1erc20bridge.sol)                                                                                                                                      | Non-gas efficient lookup of mappings in `Diamond.sol` & `L1ERC20Bridge.sol`                                                                                                                                 |
| [G-06](#g-06-do-not-update-storage-when-the-value-hasnt-changed)                                                                                                                                                           | Do not update storage when the value hasn't changed                                                                                                                                                         |
| [G-07](#g-07-more-than-one-address/id-mappings-can-be-combined-into-a-single-mapping-of-an-address/id-to-a-struct-where-appropriate)                                                                                       | More than one address/ID mappings can be combined into a single mapping of an address/ID to a struct, where appropriate                                                                                     |
| [G-08](#g-08-some-events-in-admin.sol-should-be-emmitted-one-step-above)                                                                                                                                                   | Some events in `Admin.sol` should be emmitted one step above                                                                                                                                                |
| [G-09](<#g-09-l1sharedbridgedeposit()s-current-implementation-would-cost-users-unnecessary-gas-while-depositing>)                                                                                                          | `L1SharedBridge::deposit()'`s current implementation would cost users unnecessary gas while depositing                                                                                                      |
| [G-10](#g-10-initializing-uint256-variable-to-default-value-of-0-can-be-omitted)                                                                                                                                           | Initializing `uint256` variable to default value of 0 can be omitted                                                                                                                                        |
| [G-11](#g-11-diamond.sol-non-gas-efficient-expansion-of-memory)                                                                                                                                                            | `Diamond.sol:` Non-gas efficient expansion of memory                                                                                                                                                        |
| [G-12](#g-12-remove-the-addition-if-we-are-always-adding-0)                                                                                                                                                                | Remove the addition if we are always adding `0`                                                                                                                                                             |
| [G-13](#g-13-consider-utilizing-uint256-for-boolean-state-management-in-order-to-save-gas)                                                                                                                                 | Consider utilizing `uint256` for Boolean state management in order to save gas                                                                                                                              |
| [G-14](#g-14-use-assembly-to-revert-with-an-error-message-to-save-gas)                                                                                                                                                     | Use assembly to revert with an error message to save gas                                                                                                                                                    |
| [G-15](<#g-15-make-finalizedeposit()-more-efficient>)                                                                                                                                                                      | Make `finalizeDeposit()` more efficient                                                                                                                                                                     |
| [G-16](#g-16-consider-not-using-the-nonreentrant-modifier-for-admin-functions)                                                                                                                                             | Consider not using the `nonReentrant` modifier for Admin functions                                                                                                                                          |
| [G-17](<#g-17--_commitbatches()-should-be-made-more-efficient-_(2-modifications)_>)                                                                                                                                        | ` _commitBatches()` should be made more efficient _(2 modifications)_                                                                                                                                       |
| [G-18](#g-18-chosing-internal-functions-over-modifiers)                                                                                                                                                                    | Chosing internal functions over modifiers                                                                                                                                                                   |
| [G-19](#g-19-protocol-does-not-consider-eip-4844-and-still-assumes-more-than-one-batch-can-be-commited)                                                                                                                    | Protocol does not consider EIP-4844 and still assumes more than one batch can be commited                                                                                                                   |
| [G-20](#g-20-diamondproxy.sols-fallback-could-be-made-more-efficient)                                                                                                                                                      | `DiamondProxy.sol`'s fallback could be made more efficient                                                                                                                                                  |
| [G-21](#g-21-consider-using-assembly-for-loops)                                                                                                                                                                            | Consider using assembly for loops                                                                                                                                                                           |
| [G-22](#g-22-use-assembly-to-write-address-storage-values)                                                                                                                                                                 | Use assembly to write address storage values                                                                                                                                                                |
| [G-23](#g-23-executions-we-are-sure-would-never-underflow/overrflow-should-be-wrapped-in-an-unchecked)                                                                                                                     | Executions we are sure would never underflow/overrflow should be wrapped in an unchecked                                                                                                                    |
| [G-24](#g-24-remove-instances-of-unnecessary-casting)                                                                                                                                                                      | Remove instances of unnecessary casting                                                                                                                                                                     |
| [G-25](#g-25-it-is-cheaper-to-use-vanity-addresses-with-leading-zeros)                                                                                                                                                     | It is cheaper to use vanity addresses with leading zeros                                                                                                                                                    |
| [G-26](#g-26-in-some-instances-we-can-make-the-variables-outside-the-loop-so-as-to-save-gas)                                                                                                                               | In some instances we can make the variables outside the `loop` so as to save gas                                                                                                                            |
| [G-27](#g-27-always-use-unsafe-increment-for-for-loops-if-possible-when-being-used-as-terneries)                                                                                                                           | Always use unsafe increment for `for` loops if possible when being used as terneries                                                                                                                        |
| [G-28](#g-28-consider-inverting-if-else-statements-that-have-a-negation-and-also-reducing-negations-when-possible)                                                                                                         | Consider inverting `if-else` statements that have a negation and also reducing negations when possible                                                                                                      |
| [G-29](#g-29-usage-of-ternary-operators-in-scope-could-be-better-optimized)                                                                                                                                                | Usage of ternary operators in scope could be better optimized                                                                                                                                               |
| [G-30](#g-30-replace-variable-+-1-with-value++)                                                                                                                                                                            | Replace `variable + 1` with `value++`                                                                                                                                                                       |
| [G-31](#g-31-consider-caching-bytecode.length-than-querying-it-twice)                                                                                                                                                      | Consider caching `bytecode.length` than querying it twice                                                                                                                                                   |
| [G-32](#g-32-remove-the-last-offset-from-the-sharedbridge.sols-and-other-contracts-query-to-unsafebytes.readaddress)                                                                                                       | Remove the last offset from the SharedBridge.sol's and other contract's query to `UnsafeBytes.readAddress`                                                                                                  |
| [G-33](#g-33-removing-code-for-testing-before-final-production)                                                                                                                                                            | Removing code for testing before final production                                                                                                                                                           |
| [G-34](#g-34-private-functions-used-once-can-be-inlined)                                                                                                                                                                   | Private functions used once can be inlined                                                                                                                                                                  |
| [G-35](#g-35-unnecessary-duplication-of-checks-should-be-removed)                                                                                                                                                          | Unnecessary duplication of checks should be removed                                                                                                                                                         |
| [G-36](<#g-36-no-need-of-require(s.l2systemcontractsupgradebatchnumber-==-0-"ik");-while-commiting-batches-with-system-upgrades>)                                                                                          | No need of `require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");` while commiting batches with system upgrades                                                                                        |
| [G-37](#g-37-consider-importing-gas-optimised-libmap)                                                                                                                                                                      | Consider importing gas optimised `Libmap`                                                                                                                                                                   |
| [G-38](#g-38-instead-of-arrays-we-can-use-mappings)                                                                                                                                                                        | Instead of arrays we can use mappings                                                                                                                                                                       |
| [G-39](#g-39-caching-global-variables-is-more-expensive-than-using-the-actual-variable)                                                                                                                                    | Caching global variables is more expensive than using the actual variable                                                                                                                                   |
| [G-40](#g-40-divisions-by-the-powers-of-two-should-use-bit-shifting)                                                                                                                                                       | Divisions by the powers of two should use bit shifting                                                                                                                                                      |
| [G-41](#g-41-import-libraries-only-when-multiple-functions-are-going-to-be-implemented)                                                                                                                                    | Import libraries only when multiple functions are going to be implemented                                                                                                                                   |
| [G-42](#g-42-sequential-for-loops-should-be-merged)                                                                                                                                                                        | Sequential for loops should be merged                                                                                                                                                                       |
| [G-43](#g-43-consider-using-the-expectedbool-==-1-syntax-for-booleans)                                                                                                                                                     | Consider using the `expectedBool == 1` syntax for booleans                                                                                                                                                  |
| [G-44](#g-44-shift-left-instead-of-multiplication-saves-gas)                                                                                                                                                               | Shift Left instead of multiplication saves gas                                                                                                                                                              |
| [G-45](#g-45-memory-should-be-used-of-instead-state-variables-while-emiting-events)                                                                                                                                        | `memory` should be used of instead state variables while emiting events                                                                                                                                     |
| [G-46](#g-46-"--"-is-cheaper-than new-bytes(0))                                                                                                                                                                            | " `` " is cheaper than new bytes(0)                                                                                                                                                                         |
| [G-47](#g-47-always-use-named-returns-for-more-efficiency)                                                                                                                                                                 | Always use named returns for more efficiency                                                                                                                                                                |
| [G-48](#g-48-check-the-last-bit-of-a-number-to-know-if-its-even/odd-instead-of-the-modulo-operator)                                                                                                                        | Check the last bit of a number to know if it's even/odd instead of the modulo operator                                                                                                                      |
| [G-49](#g-49-remove-unused-mapping-and-import-variables)                                                                                                                                                                   | Remove unused `mapping` and `import variables`                                                                                                                                                              |
| [G-50](#g-50-assembly-checks-for address(0)-are-more-gas-efficient)                                                                                                                                                        | Assembly checks for `address(0)` are more gas efficient                                                                                                                                                     |
| [G-51](#g-51-to-extract-calldata-values-more-efficiently-we-schould-use-assembly-instead-of-abi.decode)                                                                                                                    | To extract calldata values more efficiently we schould use assembly instead of `abi.decode`                                                                                                                 |
| [G-52](#g-52-use-modifiers-instead-of-functions-to-save-gas)                                                                                                                                                               | Use modifiers instead of functions to save gas                                                                                                                                                              |
| [G-53](#g-53-it-is-sometimes-cheaper-to-cache-calldata)                                                                                                                                                                    | It is sometimes cheaper to cache calldata                                                                                                                                                                   |
| [G-54](#g-54-admin-functions-can-be-made-payable)                                                                                                                                                                          | Admin functions can be made payable                                                                                                                                                                         |
| [G-55](#g-55-in-some-cases-using-bytes32-instead-of-string-saves-gas)                                                                                                                                                      | In some cases using bytes32 instead of string saves gas                                                                                                                                                     |
| [G-56](#g-56-redundant-check-in-defaultaccount.sol)                                                                                                                                                                        | Redundant check in DefaultAccount.sol                                                                                                                                                                       |
| [G-57](#g-57-chunking-the-pubdata-should-be-made-more-efficient)                                                                                                                                                           | Chunking the pubdata should be made more efficient                                                                                                                                                          |
| [G-58](<#g-58-transactionhelperisethtoken()-is-not-used-anywhere-so-it-should-be-removed>)                                                                                                                                 | `TransactionHelper::isEthToken()` is not used anywhere so it should be removed                                                                                                                              |
| [G-59](#g-59-count-up-instead-of-counting-down-in-for-statements)                                                                                                                                                          | Count up instead of counting down in `for` statements                                                                                                                                                       |
| [G-60](#g-60-simplifying-conditional-checks-with-bitwise-operators)                                                                                                                                                        | Simplifying conditional checks with Bitwise Operators                                                                                                                                                       |
| [G-61](#g-61-consider-writing-gas-optimal-for-loops)                                                                                                                                                                       | Consider writing gas-optimal for-loops                                                                                                                                                                      |
| [G-62](<#g-62-[unsafebytes.sol](https//github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/unsafebytes.sol)-could-be-better-optimized-while-parsing-bytes-for-transactions>) | [UnsafeBytes.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol) could be better optimized while parsing bytes for transactions |
| [G-63](#g-63-do-while-loops-are-cheaper-than-for-loops-and-should-be-considered)                                                                                                                                           | Do-while loops are cheaper than for loops and should be considered                                                                                                                                          |
| [G-64](#g-64-consider-short-circuit-booleans)                                                                                                                                                                              | Consider Short-circuit booleans                                                                                                                                                                             |
| [G-65](#g-65-shortening-an-array-rather-than-copying-to-a-new-one-saves-gas)                                                                                                                                               | Shortening an array rather than copying to a new one saves gas                                                                                                                                              |
| [G-66](#g-66-use-assembly-to-perform-efficient-back-to-back-calls)                                                                                                                                                         | Use assembly to perform efficient back-to-back calls                                                                                                                                                        |
| [G-67](#g-67-using-assembly-to-validate-msg.sender-is-more-gas-efficient)                                                                                                                                                  | Using assembly to validate `msg.sender` is more gas efficient                                                                                                                                               |
| [G-68](<#g-68-proof-verification-is-performed-twice-in-provebatches()-causing-double-expenditure-of-gas>)                                                                                                                  | Proof verification is performed twice in `proveBatches()` causing double expenditure of gas                                                                                                                 |
| [G-69](#g-69-use-assembly-to-hash-instead-of-solidity)                                                                                                                                                                     | Use assembly to hash instead of solidity                                                                                                                                                                    |
| [G-70](#g-70-openzeppelins-safecast-is-not-gas-optimized-consider-using-soladys-safecast-library)                                                                                                                          | Openzeppelin's SafeCast is not gas optimized, consider using Solady's safeCast library                                                                                                                      |

## G-01 Multiple instances in scope where re-ordering and packing could save multiple storage slots in scope

### Proof of Concept

#### G-01-01

We can see that via re-ordering state variables (in this case the `zkPorterIsAvailable` bool) an extra storage slot can be saved also if we are to pack both `totalBatchesVerified` and `totalBatchesCommitted` together, we save another extra storage slot

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L66-L88

```diff

struct ZkSyncStateTransitionStorage {
    /// @dev Storage of variables needed for deprecated diamond cut facet
    uint256[7] __DEPRECATED_diamondCutStorage;
    /// @notice Address which will exercise critical changes to the Diamond Proxy (upgrades, freezing & unfreezing). Replaced by STM
    address __DEPRECATED_governor;
+   bool zkPorterIsAvailable; // @audit reordered here
    /// @notice Address that the governor proposed as one that will replace it
    address __DEPRECATED_pendingGovernor;
    /// @notice List of permitted validators
    mapping(address validatorAddress => bool isValidator) validators;
    /// @dev Verifier contract. Used to verify aggregated proof for batches
    IVerifier verifier;
    /// @notice Total number of executed batches i.e. batches[totalBatchesExecuted] points at the latest executed batch
    /// (batch 0 is genesis)
-    uint256 totalBatchesExecuted;
    /// @notice Total number of proved batches i.e. batches[totalBatchesProved] points at the latest proved batch
-    uint256 totalBatchesVerified;

+   uint256 totalBatchesExecuted;
+   uint256 totalBatchesVerified;
    /// @notice Total number of committed batches i.e. batches[totalBatchesCommitted] points at the latest committed
    /// batch
    uint256 totalBatchesCommitted;
    /// @dev Stored hashed StoredBatch for batch number
    mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
    /// @dev Stored root hashes of L2 -> L1 logs
    mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;

    //..snip
-    uint256 protocolVersion;
+    uint96 protocolVersion;
+    uint256 l2SystemContractsUpgradeBatchNumber;

    /// @dev Hash of the system contract upgrade transaction. If 0, then no upgrade transaction needs to be done.
    bytes32 l2SystemContractsUpgradeTxHash;
    /// @dev Batch number where the upgrade transaction has happened. If 0, then no upgrade transaction has happened
    /// yet.
-    uint256 l2SystemContractsUpgradeBatchNumber;
    //..snip

```

> Consider reordering the `bool` and packing the variables.

`protocolVersion` value is increased by one, so the next version number is always one greater than the current version number. This means the value shoukd not in no case exceed the maximum range of `uint96`, thid is a very large number, and it is unlikely that any protocol would ever need to be upgraded more than this many times.

Also `l2SystemContractsUpgradeBatchNumber` is the batch number of the latest upgrade transaction. If its value is 0, it signifies that no upgrade transactions have occurred, this should also fit with no problems to a `uint96`.

#### G-01-02

- Another instance to be considered https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L83-L93

```diff
    struct StoredBatchInfo {
        uint64 batchNumber;
+        uint64 indexRepeatedStorageChanges;
        bytes32 batchHash;
-        uint64 indexRepeatedStorageChanges;
        uint256 numberOfLayer1Txs;
        bytes32 priorityOperationsHash;
        bytes32 l2LogsTreeRoot;
        uint256 timestamp;
        bytes32 commitment;
    }
```

#### G-01-03

- Also for https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L55-L66 we can reduce the ` txId``uint64 ` to reduce a slot

```diff
struct WritePriorityOpParams {
    address sender;
+    uint64 txId;
-    uint256 txId;
    uint256 l2Value;
    address contractAddressL2;
    uint64 expirationTimestamp;
    uint256 l2GasLimit;
    uint256 l2GasPrice;
    uint256 l2GasPricePerPubdata;
    uint256 valueToMint;
    address refundRecipient;
}
```

#### G-01-04

```diff
contract Governance is IGovernance, Ownable2Step {
    /// @notice A constant representing the timestamp for completed operations.
    uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1);

    /// @notice The address of the security council.
    /// @dev It is supposed to be multisig contract.
    address public securityCouncil;
+    uint64 public minDelay;


    /// @notice A mapping to store timestamps when each operation will be ready for execution.
    /// @dev - 0 means the operation is not created.
    /// @dev - 1 (EXECUTED_PROPOSAL_TIMESTAMP) means the operation is already executed.
    /// @dev - any other value means timestamp in seconds when the operation will be ready for execution.
    mapping(bytes32 operationId => uint256 executionTimestamp) public timestamps;

    /// @notice The minimum delay in seconds for operations to be ready for execution.
-    uint256 public minDelay;
    ..//snip

```

### G-01-05

Re-ordering a struct's variable makes it to be packed more efficiently

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L15-L24

```diff
struct StateTransitionManagerInitializeData {
    address governor;
    address validatorTimelock;
+    uint64 genesisIndexRepeatedStorageChanges;
    address genesisUpgrade;
    bytes32 genesisBatchHash;
-    uint64 genesisIndexRepeatedStorageChanges;
    bytes32 genesisBatchCommitment;
    Diamond.DiamondCutData diamondCut;
    uint256 protocolVersion;
}

```

As seen `genesisIndexRepeatedStorageChanges` consumes 8 bytes, so moving it up an extra storage slot can be saved

### Recommended Mitigation Steps

Apply suggested diff changes and rearrange where possible to even optimise more gas

## G-02 Consider removing unnecessary variables _(one time usage)_ in different files in scope being cached during executions

### Proof of Concept

Multiple instances

#### `Mailbox.sol`https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

- First instance

```solidity
    /// @inheritdoc IMailbox
    function l2TransactionBaseCost(
        uint256 _gasPrice,
        uint256 _l2GasLimit,
        uint256 _l2GasPerPubdataByteLimit
    ) public view returns (uint256) {
        uint256 l2GasPrice = _deriveL2GasPrice(_gasPrice, _l2GasPerPubdataByteLimit);
        return l2GasPrice * _l2GasLimit;
    }
```

Consider applying these changes since `l2GasPrice ` is used only once.

```diff
    /// @inheritdoc IMailbox
    function l2TransactionBaseCost(
        uint256 _gasPrice,
        uint256 _l2GasLimit,
        uint256 _l2GasPerPubdataByteLimit
    ) public view returns (uint256) {
-        uint256 l2GasPrice = _deriveL2GasPrice(_gasPrice, _l2GasPerPubdataByteLimit);
-        return l2GasPrice * _l2GasLimit;
+        return _deriveL2GasPrice(_gasPrice, _l2GasPerPubdataByteLimit) * _l2GasLimit;
    }
```

- Second instance:

```solidity
    function _deriveL2GasPrice(uint256 _l1GasPrice, uint256 _gasPerPubdata) internal view returns (uint256) {
        FeeParams memory feeParams = s.feeParams;
        require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");
        uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
            s.baseTokenGasPriceMultiplierDenominator;
        uint256 pubdataPriceBaseToken;
        if (feeParams.pubdataPricingMode == PubdataPricingMode.Rollup) {
            pubdataPriceBaseToken = L1_GAS_PER_PUBDATA_BYTE * l1GasPriceConverted;
        }

        uint256 batchOverheadBaseToken = uint256(feeParams.batchOverheadL1Gas) * l1GasPriceConverted;
        uint256 fullPubdataPriceBaseToken = pubdataPriceBaseToken +
            batchOverheadBaseToken /
            uint256(feeParams.maxPubdataPerBatch);

        uint256 l2GasPrice = feeParams.minimalL2GasPrice + batchOverheadBaseToken / uint256(feeParams.maxL2GasPerBatch);
        uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata;

        return Math.max(l2GasPrice, minL2GasPriceBaseToken);
    }
```

Here we have `pubdataPriceBaseToken` and `minL2GasPriceBaseToken` which are used only once so we don't need to declare them.

#### Secondly, take a look at `L1ERC20Bridge.sol` https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L158C1-L167C1

```solidity

    /// @dev Transfers tokens from the depositor address to the shared bridge address.
    /// @return The difference between the contract balance before and after the transferring of funds.
    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
        uint256 balanceBefore = _token.balanceOf(address(sharedBridge));
        _token.safeTransferFrom(_from, address(sharedBridge), _amount);
        uint256 balanceAfter = _token.balanceOf(address(sharedBridge));

        return balanceAfter - balanceBefore;
    }

```

Here we can see that `balanceAfter` is only used once, so there is no need for us to cache it, we can just `return _token.balanceOf(address(sharedBridge)) - balanceBefore` as the last step

- Another one in this contract is here

```solidity

    function l2TokenAddress(address _l1Token) external view returns (address) {
        bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
        bytes32 salt = bytes32(uint256(uint160(_l1Token)));

        return L2ContractHelper.computeCreate2Address(l2Bridge, salt, l2TokenProxyBytecodeHash, constructorInputHash);
    }
```

`constructorInputHash` and `salt` are used only once, so they don't need to be declared at all, consider just changing the function implementation to only include this line: ` return L2ContractHelper.computeCreate2Address(l2Bridge, bytes32(uint256(uint160(_l1Token))), l2TokenProxyBytecodeHash, keccak256(abi.encode(address(l2TokenBeacon), "")));`

#### Now consider the `L1SharedBridge.sol` contract https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity

316             bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
                _chainId,
                _l2TxHash,
                _l2BatchNumber,
                _l2MessageIndex,
                _l2TxNumberInBatch,
                _merkleProof,
                TxStatus.Failure
            );
            require(proofValid, "yn");
```

Here we can just pass the whole call into the (require) instead of dividing it into two steps, since `proofValid ` is used only once, so it doesn't need to be declared

- Another one in this contract is

```solidity

        bool success = bridgehub.proveL2MessageInclusion(
            _chainId,
            _messageParams.l2BatchNumber,
            _messageParams.l2MessageIndex,
            l2ToL1Message,
            _merkleProof
        );
        require(success, "ShB withd w proof"); // withdrawal wrong proof
```

Here we can also just pass the whole call into the (require) instead of dividing it into two steps, since `success ` is used only once, so it doesn't need to be declared.

#### Now consider the `BaseZkSyncUpgrade.sol` contract https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L222C1-L232C6

```solidity
    function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure {
        require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");
        require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");

        for (uint256 i = 0; i < _factoryDeps.length; ++i) {
            require(
                L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
                "Wrong factory dep hash"
            );
        }
    }
```

Here `_factoryDeps.length;` is being queried, 3 times.

#### See `TransactionValidator.sol` contract, https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

```solidity
    function getOverheadForTransaction(
        uint256 _encodingLength
    ) internal pure returns (uint256 batchOverheadForTransaction) {
        // The overhead from taking up the transaction's slot
        batchOverheadForTransaction = TX_SLOT_OVERHEAD_L2_GAS;

        // The overhead for occupying the bootloader memory can be derived from encoded_len
        uint256 overheadForLength = MEMORY_OVERHEAD_GAS * _encodingLength;
        batchOverheadForTransaction = Math.max(batchOverheadForTransaction, overheadForLength);
    }
```

Here `batchOverheadForTransaction` and `overheadForLength` are only used once so they don't need to be declared, we can just have the function be one line of `  batchOverheadForTransaction = Math.max(TX_SLOT_OVERHEAD_L2_GAS, (MEMORY_OVERHEAD_GAS * _encodingLength))`

#### Consider the `LibMap.sol` contract https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

- For [functions `get`](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L18-L32), we can see that ariables `mapValue` and `bitOffset` are used only once, so they don't need to be declared at all.

- Also for [functions `set`](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L38-L64) the variables `oldValue` & `nexValueXorOldValue` are only used once too, they also should not be declared.

#### Consider `Getters.sol`https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

```solidity

    function isFacetFreezable(address _facet) external view returns (bool isFreezable) {
        Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();

        // There is no direct way to get whether the facet address is freezable,
        // so we get it from one of the selectors that are associated with the facet.
        uint256 selectorsArrayLen = ds.facetToSelectors[_facet].selectors.length;
        if (selectorsArrayLen != 0) {
            bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];
            isFreezable = ds.selectorToFacet[selector0].isFreezable;
        }
    }
```

Here `selectorsArrayLen` and `selector0` are used only once, so we shouldn't declare them.

#### `Diamond.sol` https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#

```solidity
   function _saveFacetIfNew(address _facet) private {
        DiamondStorage storage ds = getDiamondStorage();

        uint256 selectorsLength = ds.facetToSelectors[_facet].selectors.length;
        // If there are no selectors associated with facet then save facet as new one
        if (selectorsLength == 0) {
            ds.facetToSelectors[_facet].facetPosition = ds.facets.length.toUint16();
            ds.facets.push(_facet);
        }
    }
```

Here `selectorsLength` is used only once.

Also in the same contract,

```solidity

    function diamondCut(DiamondCutData memory _diamondCut) internal {
        FacetCut[] memory facetCuts = _diamondCut.facetCuts;
        address initAddress = _diamondCut.initAddress;
        bytes memory initCalldata = _diamondCut.initCalldata;
        uint256 facetCutsLength = facetCuts.length;
        for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {
            Action action = facetCuts[i].action;
            address facet = facetCuts[i].facet;
            bool isFacetFreezable = facetCuts[i].isFreezable;
            bytes4[] memory selectors = facetCuts[i].selectors;

            require(selectors.length > 0, "B"); // no functions for diamond cut

            if (action == Action.Add) {
                _addFunctions(facet, selectors, isFacetFreezable);
            } else if (action == Action.Replace) {
                _replaceFunctions(facet, selectors, isFacetFreezable);
            } else if (action == Action.Remove) {
                _removeFunctions(facet, selectors);
            } else {
                revert("C"); // undefined diamond cut action
            }
        }

        _initializeDiamondCut(initAddress, initCalldata);
        emit DiamondCut(facetCuts, initAddress, initCalldata);
    }
```

Here `facet` and `isFacetFreezable` are used only once and should not be declared.

- Another instance would be in the `addOneFunction` https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L213-L215 where `selector0`is being used only once

- Another instance here would be ttps://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L85-L92

```solidity

function getDiamondStorage() internal pure returns (DiamondStorage storage diamondStorage) {
        bytes32 position = DIAMOND_STORAGE_POSITION;
        assembly {
            diamondStorage.slot := position
        }
    }

```

```diff

  function getDiamondStorage() internal pure returns (DiamondStorage storage diamondStorage) {
-        bytes32 position = DIAMOND_STORAGE_POSITION;
        assembly {
-            diamondStorage.slot := position
+            diamondStorage.slot := DIAMOND_STORAGE_POSITION
        }
    }

```

#### `ValidatorTimelock.sol` https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity

    function _propagateToZkSyncStateTransition(uint256 _chainId) internal {
        address contractAddress = stateTransitionManager.stateTransition(_chainId);
        assembly {
            // Copy function signature and arguments from calldata at zero position into memory at pointer position
            calldatacopy(0, 0, calldatasize())
            // Call method of the hyperchain diamond contract returns 0 on error
            let result := call(gas(), contractAddress, 0, 0, calldatasize(), 0, 0)
            // Get the size of the last return data
            let size := returndatasize()
            // Copy the size length of bytes from return data at zero position to pointer position
            returndatacopy(0, 0, size)
            // Depending on the result value
            switch result
            case 0 {
                // End execution and revert state changes
                revert(0, size)
            }
            default {
                // Return data with length of size at pointers position
                return(0, size)
            }
        }
    }

```

```diff
   function _propagateToZkSyncStateTransition(uint256 _chainId) internal {
-        address contractAddress = stateTransitionManager.stateTransition(_chainId);
       assembly {
           // Copy function signature and arguments from calldata at zero position into memory at pointer position
           calldatacopy(0, 0, calldatasize())
           // Call method of the hyperchain diamond contract returns 0 on error
-            let result := call(gas(), contractAddress, 0, 0, calldatasize(), 0, 0)
+            let result := call(gas(), stateTransitionManager.stateTransition(_chainId), 0, 0, calldatasize(), 0, 0)
           // Get the size of the last return data
           let size := returndatasize()
           // Copy the size length of bytes from return data at zero position to pointer position
           returndatacopy(0, 0, size)
           // Depending on the result value
           switch result
           case 0 {
               // End execution and revert state changes
               revert(0, size)
           }
           default {
               // Return data with length of size at pointers position
               return(0, size)
           }
       }
   }
```

#### `SystemContext.sol` https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol

```solidity
            uint128 currentBatchTimestamp = currentBatchInfo.timestamp;
            require(
                _l2BlockTimestamp >= currentBatchTimestamp,
                "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
            );
```

```diff
-            uint128 currentBatchTimestamp = currentBatchInfo.timestamp;
            require(
-                _l2BlockTimestamp >= currentBatchTimestamp,
+                _l2BlockTimestamp >= currentBatchInfo.timestamp,
                "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
            );
```

- Here again https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L428-L431

```solidity
        uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp;
        require(
            _newTimestamp > currentBlockTimestamp,
            "The timestamp of the batch must be greater than the timestamp of the previous block"
```

```diff
-        uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp;
        require(
-            _newTimestamp > currentBlockTimestamp,
+            _newTimestamp > currentL2BlockInfo.timestamp,
            "The timestamp of the batch must be greater than the timestamp of the previous block"
```

#### Recommended Mitigation Steps

Consider applying suggested diff changes and not declaring variables if they are only used once

## G-03 Consider using storage instead of memory for structs or arrays inorder to save gas

When accessing data from storage, assigning this data to a variable in memory triggers the entire struct or array to be read from storage. This operation costs a significant amount of gas (2100 gas per field in the struct or array). Accessing these fields from the memory variable later adds extra cost due to the need for an MLOAD operation, as opposed to a less expensive stack read.

- Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity


246        WritePriorityOpParams memory params;

321        L2CanonicalTransaction memory transaction = _serializeL2Transaction(_priorityOpParams, _calldata, _factoryDeps);

```

- Another instance here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity

396        VerifierParams memory verifierParams = s.verifierParams;

339924        uint256[] memory proofPublicInput = new uint256[](committedBatchesLength);

```

- Another instance https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L27

```solidity

27        Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];
```

- Another instance https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L155

```solidity

136        VerifierParams memory oldVerifierParams = s.verifierParams;
```

- Another instance https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity

97        FacetCut[] memory facetCuts = _diamondCut.facetCuts;

105            bytes4[] memory selectors = facetCuts[i].selectors;

```

To dive deeper, still in this same contract we can see the excessive calls on `SelectorToFacet memory oldFacet = ds.selectorToFacet[selector]`, i.e take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L124-L185

```soldity

    function _addFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {
        DiamondStorage storage ds = getDiamondStorage();


        // Facet with no code cannot be added.
        // This check also verifies that the facet does not have zero address, since it is the
        // address with which 0x00000000 selector is associated.
        require(_facet.code.length > 0, "G");


        // Add facet to the list of facets if the facet address is new one
        _saveFacetIfNew(_facet);


        uint256 selectorsLength = _selectors.length;
        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
            bytes4 selector = _selectors[i];
            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
            require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists


            _addOneFunction(_facet, selector, _isFacetFreezable);
        }
    }

    function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {
        DiamondStorage storage ds = getDiamondStorage();


        // Facet with no code cannot be added.
        // This check also verifies that the facet does not have zero address, since it is the
        // address with which 0x00000000 selector is associated.
        require(_facet.code.length > 0, "K");


        uint256 selectorsLength = _selectors.length;
        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
            bytes4 selector = _selectors[i];
            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
            require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address


            _removeOneFunction(oldFacet.facetAddress, selector);
            // Add facet to the list of facets if the facet address is a new one
            _saveFacetIfNew(_facet);
            _addOneFunction(_facet, selector, _isFacetFreezable);
        }
    }

    function _removeFunctions(address _facet, bytes4[] memory _selectors) private {
        DiamondStorage storage ds = getDiamondStorage();


        require(_facet == address(0), "a1"); // facet address must be zero


        uint256 selectorsLength = _selectors.length;
        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
            bytes4 selector = _selectors[i];
            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
            require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet


            _removeOneFunction(oldFacet.facetAddress, selector);
        }
    }
```

These three functions are used to manage the facets and the functions associated with them, case is that in all three functions `SelectorToFacet memory oldFacet = ds.selectorToFacet[selector]` is first queried and then checked to checked to be the old facet, issue is that these instances each copy a complete struct to the memory and then only uses one of its attributes, keep in mind that this is done in a for-loop making it even more expensive.

### Recommended Mitigation Steps

Since it's more gas-efficient to declare the variable as storage and use stack variables to cache any frequently accessed fields this should then be done, cause this approach minimizes gas consumption to only those fields that are actually accessed.

To suggest a fix for the instances of `SelectorToFacet memory oldFacet = ds.selectorToFacet[selector]`,then instead pass it directly in the required check, i.e changes in all three functions should be like this:

```diff
-       SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
-       require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists
+       require(ds.selectorToFacet[selector].facetAddress == address(0), "J"); // @audit attach the necessary error message for each function
```

## G-04 We can avoid multiple SSTOREs in case of reverts

### G-04-01

#### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
    function _executeBatches(StoredBatchInfo[] calldata _batchesData) internal {
        uint256 nBatches = _batchesData.length;
        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
            _executeOneBatch(_batchesData[i], i);
            emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
        }

        uint256 newTotalBatchesExecuted = s.totalBatchesExecuted + nBatches;
        //@audit
        s.totalBatchesExecuted = newTotalBatchesExecuted;
        require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.

        uint256 batchWhenUpgradeHappened = s.l2SystemContractsUpgradeBatchNumber;
        if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {
            delete s.l2SystemContractsUpgradeTxHash;
            delete s.l2SystemContractsUpgradeBatchNumber;
        }
    }

```

Consider this instance too https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L402

```solidity
    function _proveBatches(
        StoredBatchInfo calldata _prevBatch,
        StoredBatchInfo[] calldata _committedBatches,
        ProofInput calldata _proof
    ) internal {
        // Save the variables into the stack to save gas on reading them later
        uint256 currentTotalBatchesVerified = s.totalBatchesVerified;
        uint256 committedBatchesLength = _committedBatches.length;

        // Save the variable from the storage to memory to save gas
        VerifierParams memory verifierParams = s.verifierParams;

        // Initialize the array, that will be used as public input to the ZKP
        uint256[] memory proofPublicInput = new uint256[](committedBatchesLength);

        // Check that the batch passed by the validator is indeed the first unverified batch
        //@audit
        require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");

```

### G-04-02

Consider this instance in scope https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L402

```solidity

        // Save the variables into the stack to save gas on reading them later
        uint256 currentTotalBatchesVerified = s.totalBatchesVerified;
        uint256 committedBatchesLength = _committedBatches.length;

        // Save the variable from the storage to memory to save gas
        VerifierParams memory verifierParams = s.verifierParams;

        // Initialize the array, that will be used as public input to the ZKP
        uint256[] memory proofPublicInput = new uint256[](committedBatchesLength);

        // Check that the batch passed by the validator is indeed the first unverified batch
        require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");

```

```diff

        // Save the variables into the stack to save gas on reading them later
        uint256 currentTotalBatchesVerified = s.totalBatchesVerified;
+
+        require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");
+
        uint256 committedBatchesLength = _committedBatches.length;

        // Save the variable from the storage to memory to save gas
        VerifierParams memory verifierParams = s.verifierParams;

        // Initialize the array, that will be used as public input to the ZKP
        uint256[] memory proofPublicInput = new uint256[](committedBatchesLength);

        // Check that the batch passed by the validator is indeed the first unverified batch
-        require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");

```

### Recommended Mitigation Steps

For the first case, we can save an SSTORE here for whenever this attemot reverts, if we move apply these changes

```diff
    function _executeBatches(StoredBatchInfo[] calldata _batchesData) internal {
        uint256 nBatches = _batchesData.length;
        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
            _executeOneBatch(_batchesData[i], i);
            emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
        }

        uint256 newTotalBatchesExecuted = s.totalBatchesExecuted + nBatches;
        //@audit
+        require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.
        s.totalBatchesExecuted = newTotalBatchesExecuted;
-        require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.

        uint256 batchWhenUpgradeHappened = s.l2SystemContractsUpgradeBatchNumber;
        if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {
            delete s.l2SystemContractsUpgradeTxHash;
            delete s.l2SystemContractsUpgradeBatchNumber;
        }
    }
```

```diff
    function _proveBatches(
        StoredBatchInfo calldata _prevBatch,
        StoredBatchInfo[] calldata _committedBatches,
        ProofInput calldata _proof
    ) internal {
        // Save the variables into the stack to save gas on reading them later
        uint256 currentTotalBatchesVerified = s.totalBatchesVerified;
+        // Check that the batch passed by the validator is indeed the first unverified batch
+        require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");
+
        uint256 committedBatchesLength = _committedBatches.length;

        // Save the variable from the storage to memory to save gas
        VerifierParams memory verifierParams = s.verifierParams;

        // Initialize the array, that will be used as public input to the ZKP
        uint256[] memory proofPublicInput = new uint256[](committedBatchesLength);

        // Check that the batch passed by the validator is indeed the first unverified batch
-        // Check that the batch passed by the validator is indeed the first unverified batch
-        require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");

```

For the second cae, apply the suggested `diff` change in the report.

## G-05 Non-gas efficient lookup of mappings in `Diamond.sol` & `L1ERC20Bridge.sol`

Multiple instances within the `Diamond.sol` contract https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
208        uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16();

214             bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];

223         ds.facetToSelectors[_facet].selectors.push(_selector);

233         uint256 lastSelectorPosition = ds.facetToSelectors[_facet].selectors.length - 1;

237             bytes4 lastSelector = ds.facetToSelectors[_facet].selectors[lastSelectorPosition];

244         ds.facetToSelectors[_facet].selectors.pop();

245             ds.selectorToFacet[lastSelector].selectorPosition = selectorPosition.toUint16();
```

All the above in their instances will re-calculate the `keccak256` hash of the `facetToSelectors` and `selectorToFacet` mapping slots multiple times and not being optimized.

Now within the `L1ERC20Bridge`https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L215

```solidity
215        require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw");
```

### Recommended Mitigation Steps

Though the compiler does optimize `keccak256` claculations of the same value consecutively, the referenced code snippets are not performed in sequence and could benefit from an optimization where the `mapping` lookup is being cached in a local variable.

## G-06 Do not update storage when the value hasn't changed

### Proof of Concept

Multiple instances, consider:

- Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L154

```solidity

154    depositAmount[msg.sender][_l1Token][l2TxHash] = _amount;
```

- Also https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L59

```solidity

59       _queue.data[tail] = _operation;
```

### Recommended Mitigation Steps

If the old value is equal to the new value, not re-storing the value will avoid a Gsreset (2900 gas), potentially at the expense of a Gcoldsload (2100 gas) or a Gwarmaccess (100 gas)

## G-07 More than one address/ID mappings can be combined into a single mapping of an address/ID to a struct, where appropriate

### Proof of Concept

This saves a storage slot for the mapping. Depending on the circumstances and sizes of types, here we avoid a Gsset (20000 gas) per mapping combined.

Note that reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Finally, if both fields are accessed in the same function, can save ~42 gas per access due to [ not recalculaing the key's keccak256 hash](https://gist.github.com/IllIllI000/ec23a57daa30a8f8ca8b9681c8ccefb0) (Gkeccak256 - 30 gas) and that calculation's associated stack operations.

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L45-L51

```solidity
    mapping(address => uint256) public __DEPRECATED_lastWithdrawalLimitReset;

    /// @dev A mapping L1 token address => the accumulated withdrawn amount during the withdrawal limit window
    mapping(address => uint256) public __DEPRECATED_withdrawnAmountInWindow;

    /// @dev The accumulated deposited amount per user.
    /// @dev A mapping L1 token address => user address => the total deposited amount by the user
    mapping(address => mapping(address => uint256)) public __DEPRECATED_totalDepositedAmountPerUser;
```

## G-08 Some events in `Admin.sol` should be emmitted one step above

### Proof of Concept

Some instacs of setting some variables in `Adminsol` could make use of the change of having the event get emmited one step earlier so as to save for one memory's gas cost.

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#

```diff
function setPendingAdmin(address _newPendingAdmin) external onlyGovernorOrAdmin {
        // Save previous value into the stack to put it into the event later
-       address oldPendingAdmin = s.pendingAdmin;
+       emit NewPendingGovernor(s.pendingAdmin, _newPendingAdmin);
        // Change pending admin
        s.pendingAdmin = _newPendingAdmin;
-       emit NewPendingGovernor(oldPendingAdmin, _newPendingAdmin);
    }
```

```diff
function acceptAdmin() external {
        address pendingAdmin = s.pendingAdmin;
        require(msg.sender == pendingAdmin, "n4");

-       address previousAdmin = s.admin;
+       emit NewAdmin(s.admin, pendingAdmin);
        s.admin = pendingAdmin;
        delete s.pendingAdmin;

        emit NewPendingAdmin(pendingAdmin, address(0));
-       emit NewAdmin(previousAdmin, pendingAdmin);
```

```diff
-       uint256 oldPriorityTxMaxGasLimit = s.priorityTxMaxGasLimit;
+       emit NewPriorityTxMaxGasLimit(s.priorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);
        s.priorityTxMaxGasLimit = _newPriorityTxMaxGasLimit;
-       emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);
```

### Recommended Mitigation Steps

Apply suggested diff changes

## G-09 `L1SharedBridge::deposit()'`s current implementation would cost users unnecessary gas while depositing

### Proof of Concept

Take a look at the whole shared bridge contract(both L1 and L2): https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol & https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol, most especially the depositing logic

The current implementation follows these steps:

1. **Deposit and Lock:** A user initiates a deposit by locking tokens on the L1 bridge (`L1SharedBridge.sol`).
2. **Finalize Deposit** When finalizing the deposit on the L2 bridge, the code checks if an L2 token exists for the deposited ERC20 token, source (https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L80-L103).
   - If no L2 token exists, the `_deployL2Token` function deploys a new L2 token using the provided data. This data includes the token name, symbol, and decimals, source: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L97-L101
   - If an L2 token already exists, the code verifies that it corresponds to the deposited ERC20 token, source https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L102.
3. **Data Parsing:** The `_deployL2Token` function parses the provided data to extract the token name, symbol, and decimals, source https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L110-L117
4. **Redundant Token Information Calls:** Regardless of whether the information has already been fetched, the bridge attempts to retrieve the name, symbol, and decimals directly from the ERC20 token contract using the `_getERC20Getters` function, source https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L254
5. **Appending Data to Transaction:** The retrieved ( re-fetched) token name, symbol, and decimals are then appended to the transaction calldata when requesting the L2 transaction, source https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L249
6. **Gas Cost Impact:** Users pay transaction fees based on the gas consumed during the transaction. The redundant token information retrieval adds unnecessary data to the transaction, increasing gas costs.

- Now say each redundant token information fetch might cost ~0.0001 ETH, assuming only 30,000 users and an average of 20 deposits per user, this inefficiency could lead to a total overpayment of 60 ETH in transaction fees `(600,000 transactions * 0.0001 ETH)`... _(current value of that is `~220,000` USD)_

### Impact

The `deposit` function in `L1ERC20Bridge.sol` incurs unnecessary gas costs by fetching the ERC20 token's name, symbol, and decimals on every deposit transaction, even when this information has already been retrieved for the same token in previous deposits. This repetitive fetching wastes gas and increases transaction fees for users.

### Recommended Mitigation Steps

Try only querying the ERC20 token for its name, symbol, and decimals during the first successful deposit for a particular token. Subsequent deposits for the same token can reuse the cached information, eliminating redundant calls and reducing transaction fees for users.

## G-10 Initializing `uint256` variable to default value of 0 can be omitted

### Proof of Concept

Multiple instances of this in scope, from `uint256` variables, to `bool` variables being implemented as `0`.

We can see this from a suggested search command [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+%3D+0+NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON+NOT+language%3ADotenv+NOT+language%3ARust+NOT+language%3ATOML&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+%3D+0+NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON+NOT+language%3ADotenv+NOT+language%3ARust+NOT+language%3ATOML&type=code) (we need to heavily pinpoint this swearch comand though)

A direct ecample could be this in [Config.sol]()

`    uint256 constant PRIORITY_EXPIRATION = 0 days;`

### Recommended Mitigation Steps

We can see that there is no need to initialize variables to their default values during declaration, since they are any way initialized to default value once declared.

## G-11 `Diamond.sol:` Non-gas efficient expansion of memory

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L102C1-L105C64

```solidity
            Action action = facetCuts[i].action;
            address facet = facetCuts[i].facet;
            bool isFacetFreezable = facetCuts[i].isFreezable;
            bytes4[] memory selectors = facetCuts[i].selectors;
```

These referenced variables are declared locally within the `for` loop of `Diamond::diamondCut` even though they are already present in `memory` as the function's argument.

### Recommended Mitigation Steps

Consider utilizing a single local variable within the `for` loop, i.e a `FacetCut memory` variable whose members are accessed wherever the previous declarations were.

This optimization will result in an observable amount of decrease of per iteration, with optimizations turned on for a `FacetCut` payload with `3` selectors. The optimizations will scale with the number of `selectors` present in a cut.

## G-12 Remove the addition if we are always adding `0`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L283

```solidity
uint64 expirationTimestamp = uint64(block.timestamp + PRIORITY_EXPIRATION); // Safe to cast
```

Note that `PRIORITY_EXPIRATION` is defined in `ethereum/contracts/zksync/Config.sol` as:

```
/// NOTE: The constant is set to zero for the Alpha release period
uint256 constant PRIORITY_EXPIRATION = 0 days;
```

The above makes this addition redundant (since we're adding 0).

### Recommended Mitigation Steps

Since `PRIORITY_EXPIRATION` is a constant value, known during compiling time, then `block.timestamp + PRIORITY_EXPIRATION` will never overflow. The max value of `uint64` converted into timestamp is in the year `2554`, so we can either remove the additon of have it unchecked.

## G-13 Consider utilizing `uint256` for Boolean state management in order to save gas

Quoting this article: https://detectors.auditbase.com/int-instead-of-bool-gas-optimization

" If you don't use boolean for storage, you can avoid Gwarmaccess 100 gas. In addition, state changes from true to false can cost up to ~20000 gas, whereas using uint256(2) to represent false and uint256(1) for `true` would cost significantly less."

Now if we are to transition to a convention where `uint256(1)` represents 'true' and `uint256(2)` signifies 'false' then we can actually have substantial gas savings. Cause this method avoids the `Gwarmaccess` cost of 100 gas and circumvents the 20,000 gas expense associated with `Gsset` when switching a boolean from 'false' back to 'true', particularly beneficial if the initial state was 'true'.

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L31

```solidity
31 bool approvedBySecurityCouncil;
74  mapping(address validatorAddress => bool isValidator) validators;
103 bool zkPorterIsAvailable;
114 mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;
```

Other instances to be considered https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
33 bool isFreezable;
54 bool isFrozen;
65 bool isFreezable;
```

### Recommended Mitigation Steps

[Consider this gist](https://gist.github.com/Bauchibred/9d8aaa0ec3187ec4eb40e464c2f5d3b2) to see how to input this idea in scope to achieve more efficient gas usage, particularly in operations involving frequent state toggles between true and false values.

## G-14 Use assembly to revert with an error message to save gas

### Proof of Concept

When reverting in solidity code, and there is a use of require or revert statement to revert execution with an error message, then we can in most cases further optimize the code by using assembly to revert with the error message.
Consider an example:

```
/// calling restrictedAction(2) with a non-owner address: 24042
contract SolidityRevert {
    address owner;
    uint256 specialNumber = 1;

    constructor() {
        owner = msg.sender;
    }

    function restrictedAction(uint256 num)  external {
        require(owner == msg.sender, "caller is not owner");
        specialNumber = num;
    }
}

/// calling restrictedAction(2) with a non-owner address: 23734
contract AssemblyRevert {
    address owner;
    uint256 specialNumber = 1;

    constructor() {
        owner = msg.sender;
    }

    function restrictedAction(uint256 num)  external {
        assembly {
            if sub(caller(), sload(owner.slot)) {
                mstore(0x00, 0x20) // store offset to where length of revert message is stored
                mstore(0x20, 0x13) // store length (19)
                mstore(0x40, 0x63616c6c6572206973206e6f74206f776e657200000000000000000000000000) // store hex representation of message
                revert(0x00, 0x60) // revert with data
            }
        }
        specialNumber = num;
    }
}

```

Deploying this on remix, we can see that we get a gas saving in the hundreds (~300 gas) when reverting wth the same error message with assembly against doing so in solidity. This gas savings come from the memory expansion costs and extra type checks the solidity compiler does under the hood.

### Recommended Mitigation Steps

Consider using assembly to revert with an error message when possible.

## G-15 Make `finalizeDeposit()` more efficient

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L80-L107

```solidity
    function finalizeDeposit(
        address _l1Sender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        bytes calldata _data
    ) external payable override {
        // Only the L1 bridge counterpart can initiate and finalize the deposit.
        require(
            AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
                AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
            "mq"
        );
        require(msg.value == 0, "Value should be 0 for ERC20 bridge");

        address expectedL2Token = l2TokenAddress(_l1Token);
        address currentL1Token = l1TokenAddress[expectedL2Token];
        if (currentL1Token == address(0)) {
            address deployedToken = _deployL2Token(_l1Token, _data);
            require(deployedToken == expectedL2Token, "mt");
            l1TokenAddress[expectedL2Token] = _l1Token;
        } else {
            require(currentL1Token == _l1Token, "gg"); // Double check that the expected value equal to real one
        }

        IL2StandardToken(expectedL2Token).bridgeMint(_l2Receiver, _amount);
        emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);
    }
```

This function is used to finalize deposits, but it's been marked as `payable` and then goes ahead to attach this check ` require(msg.value == 0, "Value should be 0 for ERC20 bridge")` leading to an unnecessary check, cause not having the `payable` attached would mean that the native check of ensuring that no msg.value was passed to the function would be applied, but this implementation forgoes that and then attaches an error message making it more costly than the native check

### Impact

More gas spent whenever `finalizeDeposit()` is called, due to forgoing the native implementation and having a custom one with an error

### Recommended Mitigation Steps

Consider applying these changes:

```diff
    function finalizeDeposit(
        address _l1Sender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        bytes calldata _data
-    ) external payable override {
+    ) external  override {
        // Only the L1 bridge counterpart can initiate and finalize the deposit.
        require(
            AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
                AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
            "mq"
        );
-        require(msg.value == 0, "Value should be 0 for ERC20 bridge");

        address expectedL2Token = l2TokenAddress(_l1Token);
        address currentL1Token = l1TokenAddress[expectedL2Token];
        if (currentL1Token == address(0)) {
            address deployedToken = _deployL2Token(_l1Token, _data);
            require(deployedToken == expectedL2Token, "mt");
            l1TokenAddress[expectedL2Token] = _l1Token;
        } else {
            require(currentL1Token == _l1Token, "gg"); // Double check that the expected value equal to real one
        }

        IL2StandardToken(expectedL2Token).bridgeMint(_l2Receiver, _amount);
        emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);
    }
```

## G-16 Consider not using the `nonReentrant` modifier for Admin functions

In most instances admin functions are trusted there is no use of nonReentrant modifier to save significant amount of Gas.

### Proof of Concept

Multiple instances in code, could be grepped by considering functions restricted to admins, this search command can help prepoint these modifiers: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++modifier+only+NOT+language%3AYul+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++modifier+only+NOT+language%3AYul+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code) then the functions where most of these modifiers are used can then remove the `nonReentrant` keep in mind that some other instances exist where not modifiers are used to restrict calls to only admins but ` require msg.sender == expectedAdmin` checks are made so this should be checked too.

### Recommended Mitigation Steps

Consider not using the `nonReentrant` modifier for Admin functions, but keep in mind the level of trust for the admin, if protocol plans on making such entry points decentralised in the future then they return them back to being `nonReentrant` protected at that ti,e

## G-17 ` _commitBatches()` should be made more efficient _(2 modifications)_

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L215-L249

```solidity
    function _commitBatches(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData
    ) internal {
        // check that we have the right protocol version
        // three comments:
        // 1. A chain has to keep their protocol version up to date, as processing a block requires the latest or previous protocol version
        // to solve this we will need to add the feature to create batches with only the protocol upgrade tx, without any other txs.
        // 2. A chain might become out of sync if it launches while we are in the middle of a protocol upgrade. This would mean they cannot process their genesis upgrade
        // as thier protocolversion would be outdated, and they also cannot process the protocol upgrade tx as they have a pending upgrade.
        // 3. The protocol upgrade is increased in the BaseZkSyncUpgrade, in the executor only the systemContractsUpgradeTxHash is checked
        require(
            IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
            "Executor facet: wrong protocol version"
        );
        // With the new changes for EIP-4844, namely the restriction on number of blobs per block, we only allow for a single batch to be committed at a time.
        require(_newBatchesData.length == 1, "e4");
        // Check that we commit batches after last committed batch
        //@audit
        require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data

        bytes32 systemContractsUpgradeTxHash = s.l2SystemContractsUpgradeTxHash;
        // Upgrades are rarely done so we optimize a case with no active system contracts upgrade.
        if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {
            _commitBatchesWithoutSystemContractsUpgrade(_lastCommittedBatchData, _newBatchesData);
        } else {
            _commitBatchesWithSystemContractsUpgrade(
                _lastCommittedBatchData,
                _newBatchesData,
                systemContractsUpgradeTxHash
            );
        }
    //@audit
        s.totalBatchesCommitted = s.totalBatchesCommitted + _newBatchesData.length;
    }
```

Keep in mind that with the current implementation of EIP-4844 `_newBatchesData.length` is always going to be `1`, also we can see that `totalBatchesCommitted` is actually read twice leading to more gas expenditure due to the double `SLOADs`.

### Recommended Mitigation Steps

Reimplement the function, i.e try storing the first storage access in a local variable, and then consider applying these changes

```diff
//..snip
+        s.totalBatchesCommitted = s.totalBatchesCommitted + 1;
-        s.totalBatchesCommitted = s.totalBatchesCommitted + _newBatchesData.length;
    }
```

## G-18 Chosing internal functions over modifiers

### Proof of Concept

Modifiers inject their implementation bytecode where it is used while internal functions jump to the location in the runtime code where the its implementation is. This brings certain trade-offs to both options.

In short, using modifiers "more than once" means repetitiveness and increase in size of the runtime code but reduces gas cost because of the absence of jumping to the internal function execution offset and jumping back to continue. So if we want to consider runtime gas cost on a primary basis, then modifiers should be our choice but if deployment gas cost and/or reducing the size of the creation code is most important to you then using internal functions will be best.

This can be proven by the test in this [gist](https://gist.github.com/Bauchibred/73b1b2ed213f54db66e063615fc47c9f), where around 35k gas is saved from using modifiers in just 3 functions.

### Recommended Mitigation Steps

Consider implementong this where possible, but keep in mind that
modifiers have the tradeoff that they can only be executed at the start or end of a functon. This means executing it at the middle of a function wouldn’t be directly possible.

## G-19 Protocol does not consider EIP-4844 and still assumes more than one batch can be commited

### G-19-01 Note

There are two instances of this, i.e both in `_commitBatchesWithoutSystemContractsUpgrade()` and `_commitBatchesWithSystemContractsUpgrade()`.

#### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L215-L306

```solidity
    function _commitBatches(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData
    ) internal {
        //omitted for brevity
        //@audit
        // With the new changes for EIP-4844, namely the restriction on number of blobs per block, we only allow for a single batch to be committed at a time.
        require(_newBatchesData.length == 1, "e4");
        // Check that we commit batches after last committed batch
        require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data

        bytes32 systemContractsUpgradeTxHash = s.l2SystemContractsUpgradeTxHash;
        // Upgrades are rarely done so we optimize a case with no active system contracts upgrade.
        if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {
            _commitBatchesWithoutSystemContractsUpgrade(_lastCommittedBatchData, _newBatchesData);
        } else {
            _commitBatchesWithSystemContractsUpgrade(
                _lastCommittedBatchData,
                _newBatchesData,
                systemContractsUpgradeTxHash
            );
        }

        s.totalBatchesCommitted = s.totalBatchesCommitted + _newBatchesData.length;
    }


    function _commitBatchesWithoutSystemContractsUpgrade(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData
    ) internal {
        //omitted for brevity
        //@audit
        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
            _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));

            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
            emit BlockCommit(
                _lastCommittedBatchData.batchNumber,
                _lastCommittedBatchData.batchHash,
                _lastCommittedBatchData.commitment
            );
        }
    }


    function _commitBatchesWithSystemContractsUpgrade(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData,
        bytes32 _systemContractUpgradeTxHash
    ) internal {
        //omitted for brevity
        //@audit
        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
            // The upgrade transaction must only be included in the first batch.
            bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
            _lastCommittedBatchData = _commitOneBatch(
                _lastCommittedBatchData,
                _newBatchesData[i],
                expectedUpgradeTxHash
            );

            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
            emit BlockCommit(
                _lastCommittedBatchData.batchNumber,
                _lastCommittedBatchData.batchHash,
                _lastCommittedBatchData.commitment
            );
        }
    }

```

Now these functions are called whenever batches are to be committed, now post the EIP-4844 implementation, due to the restriction on number of blobs per block, protocol can only allow for a single batch to be committed at a time, which is clearly noted in `_commitBatches()`, but navigating to both `_commitBatchesWithoutSystemContractsUpgrade()` and `_commitBatchesWithSystemContractsUpgrade()`, we can still see an unnecessary attempt to loop through the `newBatchesData.length` which is already hardcoded and can only be `1`.

#### Recommended Mitigation Steps

Remove the unnecessary for loops in both the `_commitBatchesWithoutSystemContractsUpgrade()` and `_commitBatchesWithSystemContractsUpgrade()` functions.

#### Additional Note

This bug is also present in this instance below: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L107-L142

```solidity

    function commitBatches(
        StoredBatchInfo calldata,
        CommitBatchInfo[] calldata _newBatchesData
    ) external onlyValidator(ERA_CHAIN_ID) {
        unchecked {
            // This contract is only a temporary solution, that hopefully will be disabled until 2106 year, so...
            // It is safe to cast.
            uint32 timestamp = uint32(block.timestamp);
            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);
            }
        }

        _propagateToZkSyncStateTransition(ERA_CHAIN_ID);
    }

    /// @dev Records the timestamp for all provided committed batches and make
    /// a call to the hyperchain diamond contract with the same calldata.
    function commitBatchesSharedBridge(
        uint256 _chainId,
        StoredBatchInfo calldata,
        CommitBatchInfo[] calldata _newBatchesData
    ) external onlyValidator(_chainId) {
        unchecked {
            // This contract is only a temporary solution, that hopefully will be disabled until 2106 year, so...
            // It is safe to cast.
            uint32 timestamp = uint32(block.timestamp);
            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);
            }
        }

        _propagateToZkSyncStateTransition(_chainId);
    }

```

And https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L180-L222

```solidity
    /// @dev Check that batches were committed at least X time ago and
    /// make a call to the hyperchain diamond contract with the same calldata.
    function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {
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

                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
            }
        }
        _propagateToZkSyncStateTransition(ERA_CHAIN_ID);
    }

    /// @dev Check that batches were committed at least X time ago and
    /// make a call to the hyperchain diamond contract with the same calldata.
    function executeBatchesSharedBridge(
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

                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
            }
        }
        _propagateToZkSyncStateTransition(_chainId);
    }

```

### G-19-02 Executor.sol: new batches would always be `1`

#### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L215-L249

```solidity
    function _commitBatches(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData
    ) internal {
        // check that we have the right protocol version
        // three comments:
        // 1. A chain has to keep their protocol version up to date, as processing a block requires the latest or previous protocol version
        // to solve this we will need to add the feature to create batches with only the protocol upgrade tx, without any other txs.
        // 2. A chain might become out of sync if it launches while we are in the middle of a protocol upgrade. This would mean they cannot process their genesis upgrade
        // as thier protocolversion would be outdated, and they also cannot process the protocol upgrade tx as they have a pending upgrade.
        // 3. The protocol upgrade is increased in the BaseZkSyncUpgrade, in the executor only the systemContractsUpgradeTxHash is checked
        require(
            IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
            "Executor facet: wrong protocol version"
        );
        // With the new changes for EIP-4844, namely the restriction on number of blobs per block, we only allow for a single batch to be committed at a time.
        //@audit
        require(_newBatchesData.length == 1, "e4");
        // Check that we commit batches after last committed batch
        require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data

        bytes32 systemContractsUpgradeTxHash = s.l2SystemContractsUpgradeTxHash;
        // Upgrades are rarely done so we optimize a case with no active system contracts upgrade.
        if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {
            _commitBatchesWithoutSystemContractsUpgrade(_lastCommittedBatchData, _newBatchesData);
        } else {
            _commitBatchesWithSystemContractsUpgrade(
                _lastCommittedBatchData,
                _newBatchesData,
                systemContractsUpgradeTxHash
            );
        }

        //@audit

        s.totalBatchesCommitted = s.totalBatchesCommitted + _newBatchesData.length;
    }

```

This function, is used to commit batches, but the last step queries ` _newBatchesData.length` , but this line `require(_newBatchesData.length == 1, "e4");` exists which means that `_newBatchesData` would always be `1`, so it's unnecessary to query the length

#### Recommended Mitigation Steps

Apply these changes:

```diff
    function _commitBatches(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData
    ) internal {
        // check that we have the right protocol version
        // three comments:
        // 1. A chain has to keep their protocol version up to date, as processing a block requires the latest or previous protocol version
        // to solve this we will need to add the feature to create batches with only the protocol upgrade tx, without any other txs.
        // 2. A chain might become out of sync if it launches while we are in the middle of a protocol upgrade. This would mean they cannot process their genesis upgrade
        // as thier protocolversion would be outdated, and they also cannot process the protocol upgrade tx as they have a pending upgrade.
        // 3. The protocol upgrade is increased in the BaseZkSyncUpgrade, in the executor only the systemContractsUpgradeTxHash is checked
        require(
            IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
            "Executor facet: wrong protocol version"
        );
        // With the new changes for EIP-4844, namely the restriction on number of blobs per block, we only allow for a single batch to be committed at a time.
        require(_newBatchesData.length == 1, "e4");
        // Check that we commit batches after last committed batch
        require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data

        bytes32 systemContractsUpgradeTxHash = s.l2SystemContractsUpgradeTxHash;
        // Upgrades are rarely done so we optimize a case with no active system contracts upgrade.
        if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {
            _commitBatchesWithoutSystemContractsUpgrade(_lastCommittedBatchData, _newBatchesData);
        } else {
            _commitBatchesWithSystemContractsUpgrade(
                _lastCommittedBatchData,
                _newBatchesData,
                systemContractsUpgradeTxHash
            );
        }

-        s.totalBatchesCommitted = s.totalBatchesCommitted + _newBatchesData.length;
+        s.totalBatchesCommitted = s.totalBatchesCommitted + 1;
    }

```

## G-20 `DiamondProxy.sol`'s fallback could be made more efficient

> NB A similar logic can be applied to Mailbox's `_proveL2LogInclusion()` snippet attached

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L20C1-L28C51

```solidity
    fallback() external payable {
        Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
        // Check whether the data contains a "full" selector or it is empty.
        // Required because Diamond proxy finds a facet by function signature,
        // which is not defined for data length in range [1, 3].
        require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
        // Get facet from function selector
        Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];
        address facetAddress = facet.facetAddress;
```

The fallback function should validate `msg.data.length` first which could help avoid making a state load

- Here is the snippet to a similar https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L104-L127

```solidity
    function _proveL2LogInclusion(
        uint256 _batchNumber,
        uint256 _index,
        L2Log memory _log,
        bytes32[] calldata _proof
    ) internal view returns (bool) {
        require(_batchNumber <= s.totalBatchesExecuted, "xx");


        bytes32 hashedLog = keccak256(
            abi.encodePacked(_log.l2ShardId, _log.isService, _log.txNumberInBatch, _log.sender, _log.key, _log.value)
        );
        // Check that hashed log is not the default one,
        // otherwise it means that the value is out of range of sent L2 -> L1 logs
        require(hashedLog != L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH, "tw");


        // It is ok to not check length of `_proof` array, as length
        // of leaf preimage (which is `L2_TO_L1_LOG_SERIALIZE_SIZE`) is not
        // equal to the length of other nodes preimages (which are `2 * 32`)


        bytes32 calculatedRootHash = Merkle.calculateRoot(_proof, _index, hashedLog);
        bytes32 actualRootHash = s.l2LogsRootHashes[_batchNumber];


        return actualRootHash == calculatedRootHash;
    }

```

Consider moving the `require(_batchNumber <= s.totalBatchesExecuted, "xx");` way lower in the function's execution to save gas not sstoring in case another check reverts.

### Recommended Mitigation Steps

In order to optimize code we shouldn't load storage if we might revert on another check, validate msg.data first before reading from storage

```diff
    fallback() external payable {
+        require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
        Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
        // Check whether the data contains a "full" selector or it is empty.
        // Required because Diamond proxy finds a facet by function signature,
        // which is not defined for data length in range [1, 3].
-        require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
        // Get facet from function selector
        Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];
        address facetAddress = facet.facetAddress;
```

## G-21 Consider using assembly for loops

In Solidity, assembly for loops save gas by avoiding the overhead of stack operations, that's because in solidity the compiler generates assembly code that includes stack operations to store and retrieve variables. This can lead to high gas costs, especially if the for loop is iterating over a large number of elements, which is why using assembly is more gas efficient since we avoid this unnecessary overhead.

Using this [simple contract](https://gist.github.com/sathishpic22/34b6972901f825a475753e44d39f0faf) in Remix IDE we can see how it saves gas in the hundreds per iteration. The gas savings may high based on the complexity.

Multiple instances, we can see that by using this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+for+%28+NOT+language%3AMarkdown+NOT+language%3ATypeScript+NOT+language%3AYul+NOT+language%3ARust&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+for+%28+NOT+language%3AMarkdown+NOT+language%3ATypeScript+NOT+language%3AYul+NOT+language%3ARust&type=code)

### Recommended Mitigation Steps

Consider swapping the normal for loop for assembly implemented ones, or atleast in instances where the logic is simple and mistakes would be hard to be made.

## G-22 Use assembly to write address storage values

### Proof of Concept

An instance can be seen in [ValidatorTimelock.sol]()

```solidity


  validator = _validator;

  validator = _newValidator;

```

### Recommended Mitigation Steps

Consider using assembly to write address storage values to save gas

## G-23 Executions we are sure would never underflow/overrflow should be wrapped in an unchecked

### Underflow

Take a look at L1ERC20Bridge.sol https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L158C1-L167C1

```solidity

    /// @dev Transfers tokens from the depositor address to the shared bridge address.
    /// @return The difference between the contract balance before and after the transferring of funds.
    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
        uint256 balanceBefore = _token.balanceOf(address(sharedBridge));
        _token.safeTransferFrom(_from, address(sharedBridge), _amount);
        uint256 balanceAfter = _token.balanceOf(address(sharedBridge));

        return balanceAfter - balanceBefore;
    }

```

Here we are very certain that in no instance is `balanceAfter < balanceBefore` ever going to be true, since protocol does not support "funny" tokens so we can wrap this deduction in an unchecked block

### Overrflow

Take a look at [Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.so)

```
require(block.timestamp - COMMIT_TIMESTAMP_NOT_OLDER <= batchTimestamp, "h1"); // New batch timestamp is too small
require(lastL2BlockTimestamp <= block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA, "h2"); // The last L2 block timestamp is too big
```

Note that `COMMIT_TIMESTAMP_NOT_OLDER` and `COMMIT_TIMESTAMP_APPROXIMATION_DELTA` are constant values, which are known before compilation time, in our case from here [https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L44] we can see that `COMMIT_TIMESTAMP_APPROXIMATION_DELTA` is just `1 hour` so `block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA` won't overflow, so we can uncheck the two lines can be

### Recommended Mitigation Steps

Consider wrapping the mathematical operations in an unchecked block.

## G-24 Remove instances of unnecessary casting

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L45

```solidity

    /// @return The total number of unprocessed priority operations in a priority queue
    function getSize(Queue storage _queue) internal view returns (uint256) {
        return uint256(_queue.tail - _queue.head);
    }

```

But from [here ](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L45) we can see that both `_queue.tail ` & `_queue.head` are of `unit256` already so there's no need for this casting.

### Recommended Mitigation Steps

Remove the unnecessary casting

## G-25 It is cheaper to use vanity addresses with leading zeros

First take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L22

```solidity
   uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
```

Now consider OpenSea Seaport contract with this address: `0x00000000000000ADc04C56Bf30aC9d3c0aAF14dC`, now keep in mind that this will not save gas when calling the address directly. But, if that contract’s address is used as an argument to a function, that function call will cost way less gas due to having more zeros in the calldata.

### Recommended Mitigation Steps

Consider implementing vanity addresses, just be aware that there have been hacks from generating vanity addresses for wallets with insufficiently random private keys, but this is not a concern for smart contracts vanity addresses created with finding a salt for create2, because smart contracts do not have private keys.

## G-26 In some instances we can make the variables outside the `loop` so as to save gas

When we declare a variable inside a loop, Solidity creates a new instance of the variable for each iteration of the loop. This can lead to unnecessary gas costs, especially in the case where the loop is executed frequently or iterates over a large number of elements. By declaring the variable outside the loop, you can avoid the creation of multiple instances of the variable and reduce the gas cost of your contract.

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L224-L234

```solidity

  function _execute(Call[] calldata _calls) internal {
        for (uint256 i = 0; i < _calls.length; ++i) {
            (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
            if (!success) {
                // Propage an error if the call fails.
                assembly {
                    revert(add(returnData, 0x20), mload(returnData))
                }
            }
        }
    }

```

```diff
File : contracts/ethereum/contracts/governance/Governance.sol

  function _execute(Call[] calldata _calls) internal {
+
+     bool success;
+     bytes memory returnData;
+
        for (uint256 i = 0; i < _calls.length; ++i) {
-            (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
+            (success, returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
            if (!success) {
                // Propage an error if the call fails.
                assembly {
                    revert(add(returnData, 0x20), mload(returnData))
                }
            }
        }
    }

```

- Another instance https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L141-L148

```solidity



        // linear traversal of the logs
        for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
            // Extract the values to be compared to/used such as the log sender, key, and value
            (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
            (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
            (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);

```

```diff

+
+      address logSender;
+      uint256 logKey;
+      bytes32 logValue;
        // linear traversal of the logs
        for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
            // Extract the values to be compared to/used such as the log sender, key, and value
-            (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
+            (logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
-            (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
+            (logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
-            (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);
+            (logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);

```

The same file, https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L307-L315

```solidity

    function _collectOperationsFromPriorityQueue(uint256 _nPriorityOps) internal returns (bytes32 concatHash) {
        concatHash = EMPTY_STRING_KECCAK;


        for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {
            PriorityOperation memory priorityOp = s.priorityQueue.popFront();
            concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));
        }
    }
```

```diff


+        PriorityOperation memory priorityOp;
        for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {
-            PriorityOperation memory priorityOp = s.priorityQueue.popFront();
+            priorityOp = s.priorityQueue.popFront();

```

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L405-L412

```solidity

       bytes32 prevBatchCommitment = _prevBatch.commitment;
        for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {
            currentTotalBatchesVerified = currentTotalBatchesVerified.uncheckedInc();
            require(
                _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
                "o1"
            );

            bytes32 currentBatchCommitment = _committedBatches[i].commitment;

```

```diff

       bytes32 prevBatchCommitment = _prevBatch.commitment;
+       bytes32 currentBatchCommitment;
        for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {
            currentTotalBatchesVerified = currentTotalBatchesVerified.uncheckedInc();
            require(
                _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
                "o1"
            );

-            bytes32 currentBatchCommitment = _committedBatches[i].commitment;
+            currentBatchCommitment = _committedBatches[i].commitment;

```

Another contract https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L207-L213

```solidity

   for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {
            address facetAddr = ds.facets[i];
            Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];

            result[i] = Facet(facetAddr, facetToSelectors.selectors);
        }

```

```diff

+  address facetAddr;
+  Diamond.FacetToSelectors memory facetToSelectors;
   for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {
-            address facetAddr = ds.facets[i];
+            facetAddr = ds.facets[i];
-            Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];
+            facetToSelectors = ds.facetToSelectors[facetAddr];

            result[i] = Facet(facetAddr, facetToSelectors.selectors);
        }

```

Another contract https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L354-L358

```solidity


  uint256 factoryDepsLen = _factoryDeps.length;
        hashedFactoryDeps = new uint256[](factoryDepsLen);
        for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {
            bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);

```

```diff
File : contracts/ethereum/contracts/zksync/facets/Mailbox.sol


        uint256 factoryDepsLen = _factoryDeps.length;
        hashedFactoryDeps = new uint256[](factoryDepsLen);
+       bytes32 hashedBytecode;
        for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {
-            bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);
+            hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);

```

### Recommended Mitigation Steps

Apply the diff changes

## G-27 Always use unsafe increment for `for` loops if possible when being used as terneries

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226C8-L226C58, unlike most instances of for loops in the codebase, this one does not use an unchecked method to increment `i`
`         for (uint256 i = 0; i < _factoryDeps.length; ++i) {`

Another instance can be seen in https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225
`          for (uint256 i = 0; i < _calls.length; ++i) {`

Other instances in scope, can be pinpointed, by using this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+length%3B+%2B%2Bi+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+length%3B+%2B%2Bi+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code)

### Recommended Mitigation Steps

Consider having the increment statement be performed unsafely, optimizing the code's gas cost.

## G-28 Consider inverting `if-else` statements that have a negation and also reducing negations when possible

### Proof of Concept

Multiple instances in code, use this search command to pinpoint interesting areas: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+if+%28%21+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+if+%28%21+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code)

Use the code snippet below as an example, the second function avoids an unnecessary negation. where as the extra `!` increases the computational cost. one should benchmark both methods because the compiler can sometimes optimize this.

```solidity
function condition() public {
    if (!condition) {
        action1();
    }
    else {
        action2();
    }
}
function condition() public {
    if (condition) {
        action2();
    }
    else {
        action1();
    }
}
```

#### _Not really related to the previous, but still on negation so attached as one_

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L31

```
require(!diamondStorage.isFrozen || !facet.isFreezable, "q1");
```

Here we can save one negation by rewriting the statement to:

```
require(!(diamondStorage.isFrozen && facet.isFreezable)), "q1");
```

### Recommended Mitigation Steps

Consider inverting, while not over-complicating code.

## G-29 Usage of ternary operators in scope could be better optimized

### Proof of Concept

For example consider this instance in the state-tramsition facet, https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L291

```solidity
bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0)
```

It's been implemented in the `Executor::_commitBatchesWithSystemContractsUpgrade` where it executes a special logic for the first batch of the total batches being committed inefficiently within the `for` loop.

### Recommended Mitigation Steps

Consider making the system upgrade batch to be executed outside the `for` loop and then the `for` loop body could be identical to the `Executor::_commitBatchesWIthoutSystemContractsUpgrade` but here start the iterator at `1` instead of `0`.

## G-30 Replace `variable + 1` with `value++`

### Proof of Concept

> NB: In some instances `uncheck{ value++ }` will be preferable

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L323

```diff
require(currentBatchNumber == s.totalBatchesExecuted + _executedBatchIdx + 1, "k");
```

- Also https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L37

```diff
-  require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f");

+  require(_newBatch.batchNumber == _previousBatch.batchNumber++, "f");
```

### Recommended Mitigation Steps

Apply the diff changes

## G-31 Consider caching `bytecode.length` than querying it twice

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L21C1-L33C6

```solidity
    function hashL2Bytecode(bytes memory _bytecode) internal pure returns (bytes32 hashedBytecode) {
        // Note that the length of the bytecode must be provided in 32-byte words.
        require(_bytecode.length % 32 == 0, "pq");

        uint256 bytecodeLenInWords = _bytecode.length / 32;
        require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words
        require(bytecodeLenInWords % 2 == 1, "ps"); // bytecode length in words must be odd
        hashedBytecode = sha256(_bytecode) & 0x00000000FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF;
        // Setting the version of the hash
        hashedBytecode = (hashedBytecode | bytes32(uint256(1 << 248)));
        // Setting the length
        hashedBytecode = hashedBytecode | bytes32(bytecodeLenInWords << 224);
    }
```

Evidently, `_bytecode.length ` is being queried twice, leading to expending double the gas cost

### Recommended Mitigation Steps

Consider adding this `uint256 _bytecodeLength = _bytecode.length` to the function block, and then query from `_bytecodeLength` instead of `_bytecode.length` in both instances

## G-32 Remove the last offset from the SharedBridge.sol's and other contract's query to `UnsafeBytes.readAddress`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L488-L527

```solidity
    function _parseL2WithdrawalMessage(
        uint256 _chainId,
        bytes memory _l2ToL1message
    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
        // We check that the message is long enough to read the data.
        // Please note that there are two versions of the message:
        // 1. The message that is sent by `withdraw(address _l1Receiver)`
        // It should be equal to the length of the bytes4 function signature + address l1Receiver + uint256 amount = 4 + 20 + 32 = 56 (bytes).
        // 2. The message that is sent by `withdrawWithMessage(address _l1Receiver, bytes calldata _additionalData)`
        // It should be equal to the length of the following:
        // bytes4 function signature + address l1Receiver + uint256 amount + address l2Sender + bytes _additionalData =
        // = 4 + 20 + 32 + 32 + _additionalData.length >= 68 (bytes).

        // ..snip
        //@audit
            (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
            (l1Token, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
            (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);
        } else {
            revert("ShB Incorrect message function selector");
        }
    }
```

In the last call to `UnsafeBytes.readAddress` we can remove the `offset` since to save gas

### Recommended Mitigation Steps

Consider removing it in the last call, a simple POC to test this on REMIX could be considered below, where we save `~8/10` gas (depending on complecisty)

```
  function getUints() public pure returns (uint, uint) {return (1, 2);}
   function FirstAll() public view {
    uint a; uint b;
    (a, b) = getUints();
    uint g = gasleft();
    (a, b) = getUints();
    console.log(g - gasleft());
   }
    function FirstOne() public view {
    uint a; uint b;
    (a, b) = getUints();
    uint g = gasleft();
    (a, ) = getUints();
    console.log(g - gasleft());
   }
```

`FirstOne()` costs 8 gas lesser than `FirstAll()`, so we can decide not to assign every parameter from function call if it's not needed.

## G-33 Removing code for testing before final production

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L106

```
      // While this does not provide a protection in the production, it is needed for local testing
        // Length of the L2Log encoding should not be equal to the length of other L2Logs' tree nodes preimages
        assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
    }
```

Here we know that `assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);` is redundant and for testing purposes

### Recommended Mitigation Steps

Consider removing codes not ready for final production

## G-34 Private functions used once can be inlined

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

```solidity


92:    function _setL2DefaultAccountBytecodeHash(bytes32 _l2DefaultAccountBytecodeHash) private {

109:    function _setL2BootloaderBytecodeHash(bytes32 _l2BootloaderBytecodeHash) private {

126    function _setVerifier(IVerifier _newVerifier) private {

142    function _setVerifierParams(VerifierParams calldata _newVerifierParams) private {

222    function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure {
```

- Another instance can be seen here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L46

```solidity

46    function _initializeReentrancyGuard() private {
```

- Also more instances can be see in https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity

126    function _addFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {

149    function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {

172    function _removeFunctions(address _facet, bytes4[] memory _selectors) private {

257    function _removeFacet(address _facet) private {

278    function _initializeDiamondCut(address _init, bytes memory _calldata) private {
```

### Recommended Mitigation Steps

Consider inlining the private functions to save gas

## G-35 Unnecessary duplication of checks should be removed

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L386-L456

```solidity
    function finalizeWithdrawal() external override {
        // To avoid rewithdrawing txs that have already happened on the legacy bridge.
        // Note: new withdraws are all recorded here, so double withdrawing them is not possible.
        //@audit
        if (_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)) {
            require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");
        }
        _finalizeWithdrawal(_chainId, _l2BatchNumber, _l2MessageIndex, _l2TxNumberInBatch, _message, _merkleProof);
    }

    function _finalizeWithdrawal() internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
        require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");
        isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true;

        // Handling special case for withdrawal from zkSync Era initiated before Shared Bridge.
        //@audit
        if (_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)) {
            // Checks that the withdrawal wasn't finalized already.
            bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
                _l2BatchNumber,
                _l2MessageIndex
            );
            require(!alreadyFinalized, "Withdrawal is already finalized 2");
        }
//ommited for brevity
    }
```

These functions are both used for finalizing the withdrawals, with multiple checks, issue here now is that the check if the transaction is from the era legacy is implemented twice which is unnecessary.

#### Another instance can be seen here Proof verification is performed twice in `proveBatches()` causing double expenditure of gas.. PREPROCESSOR

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L386-L440

```solidity
    function _proveBatches(
        StoredBatchInfo calldata _prevBatch,
        StoredBatchInfo[] calldata _committedBatches,
        ProofInput calldata _proof
    ) internal {
    //ommited for brevity
        //@audit
        if (_proof.serializedProof.length > 0) {
            _verifyProof(proofPublicInput, _proof);
        }
        // #else
        _verifyProof(proofPublicInput, _proof);
        // #endif

        emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);
        s.totalBatchesVerified = currentTotalBatchesVerified;
    }

```

Evidently, if the proof is not empty, it gets verified, due to the `if` block, case is the `else` has been has been commented out which means that a proof is always going to undergo double verification in as much as it's > 0. Causig double gas expenditure of calling this: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L441-L452

```solidity
    function _verifyProof(uint256[] memory proofPublicInput, ProofInput calldata _proof) internal view {
        // We can only process 1 batch proof at a time.
        require(proofPublicInput.length == 1, "t4");

        bool successVerifyProof = s.verifier.verify(
            proofPublicInput,
            _proof.serializedProof,
            _proof.recursiveAggregationInput
        );
        require(successVerifyProof, "p"); // Proof verification fail
    }

```

### Recommended Mitigation Steps

For the first case, the check can be left just to the internal function while finalizing the withdrawal and for the second one consider verifying only once if `_proof.serializedProof.length > 0` is true.

## G-36 No need of `require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");` while commiting batches with system upgrades

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L273-L306

```solidity
    function _commitBatchesWithSystemContractsUpgrade(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData,
        bytes32 _systemContractUpgradeTxHash
    ) internal {
        //omitted for brevity
        //@audit
        require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");

        //omitted for brevity
        s.l2SystemContractsUpgradeBatchNumber = _newBatchesData[0].batchNumber;

        }
    }

```

This function is used to commit new batches with a system contracts upgrade transaction, as hinted by the `@audit` tag, this execution tries to ensure that the `l2SystemContractsUpgradeBatchNumber` is `0` but that check has already been placed in the primary internal function that calls this. i,e here: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L237-L245

```solidity
        if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {
            _commitBatchesWithoutSystemContractsUpgrade(_lastCommittedBatchData, _newBatchesData);
        } else {
            _commitBatchesWithSystemContractsUpgrade(
                _lastCommittedBatchData,
                _newBatchesData,
                systemContractsUpgradeTxHash
            );
        }
```

So there is already an assurance that `s.l2SystemContractsUpgradeBatchNumber` is always going to be `0` when this function is called.

### Recommended Mitigation Steps

Remove this line: `require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");`

## G-37 Consider importing gas optimised `Libmap`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L6C1-L8C17

```solidity
/// @dev This library is an adaptation of the corresponding Solady library (https://github.com/vectorized/solady/blob/main/src/utils/LibMap.sol)
/// @custom:security-contact security@matterlabs.dev
library LibMap {
```

We can see that protocl tries adapting Solady's library, issue here is that the `LibMap` in current use by the codebase is actually sub-optimal since an implementation is present in the official Solady repository that contains a better level of optimization, i.e to list an optimisation, lookups use bitwise operators instead of divisions and multiplications (result in a 2 gas cost reduction per operation) and then sets are entirely performed in assembly blocks further benefitting from optimized gas costs.

### Recommended Mitigation Steps

Consider importing the latest gas optimised `Libmap` from Solady

### Impact

## G-38 Instead of arrays we can use mappings

### Proof of Concept

Implementing mappings instead of arrays to avoid length checks, so when storing a list or group of items that you wish to organize in a specific order and fetch with a fixed key/index, it’s common practice to use an array data structure, keep in mind that no caveat to this and it works well,

Consider this contract POC:

```solidity

/// fetchValueAtIndex(0) gas cost: 4860
contract SequentialStorage {
    uint256[] sequence;

    constructor() {
        sequence.push() = 1;
        sequence.push() = 2;
        sequence.push() = 3;
    }

    function fetchValueAtIndex(uint256 idx) external view returns (uint256) {
        return sequence[idx];
    }
}

/// fetchValueAtIndex(0) gas cost: 2758
contract KeyedStorage {
    mapping(uint256 => uint256) dataMap;

    constructor() {
        dataMap[0] = 1;
        dataMap[1] = 2;
        dataMap[2] = 3;
    }

    function fetchValueAtIndex(uint256 idx) external view returns (uint256) {
        return dataMap[idx];
    }
}

```

So by using a mapping, we get a gas saving of > 210o gas, this is cause when we read the value of an index of an array, solidity adds bytecode that checks that we are reading from a valid index (i.e an index strictly less than the length of the array) else it reverts with a panic error. So this prevents from reading unallocated or worse, allocated storage/memory locations.

Due to the way mappings are (simply a `key => value` pair), no check like that exists and we are able to read from the a storage slot directly.

Multiple instances in code, could be grepped by using `[]` since they mostly denote an array, i.e: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+%5B%5D+NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON+NOT+language%3ARust&type=code]https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+%5B%5D+NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON+NOT+language%3ARust&type=code) and then we can pinpoint from here for instances where we can apply this.

### Recommended Mitigation Steps

Consider using mappings in as much cases as possible over arrays, gas wise, albeit it's important to note that when using mappings in this manner, the code should ensure that we are not reading an out of bound index of our canonical array.

## G-39 Caching global variables is more expensive than using the actual variable

### Proof of Concept

Take a look at

Consider this instamce that can be seen in https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L04-L127

```solidity

     address sender = msg.sender;

```

### Recommended Mitigation Steps

Consider directly using `msg.sender` or `block.timestamp` instead of caching it)

## G-40 Divisions by the powers of two should use bit shifting

### Proof of Concept

Multiple instances in code, can be pinpointed down with this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+++%2F+2+NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON+NOT+language%3ARust+NOT+language%3ADotenv&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+++%2F+2+NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON+NOT+language%3ARust+NOT+language%3ADotenv&type=code)

Key to note that we are not only considering instances of `X / 2`, ibut even instances that look like: `X /= 2`, for e.g consider this from `Merkle.sol`https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L33

```
_index /= 2;
```

It could be changed to: `_index = _index >> 1;`

### Recommended Mitigation Steps

Use bitshifting for the divisions instead

## G-41 Import libraries only when multiple functions are going to be implemented

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L174, here the `Math` is imported but only `1` function is used

Whereas here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L5 the `SafeCast` is imported but only `1` function is used

### Recommended Mitigation Steps

If only one function is going to be used from an imported library then, it is better we copy that same function into the contract source code.

## G-42 Sequential for loops should be merged

### Proof of Concept

Use this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+for+%28+NOT+language%3AMarkdown+NOT+language%3ATypeScript+NOT+language%3AYul+NOT+language%3ARust&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+for+%28+NOT+language%3AMarkdown+NOT+language%3ATypeScript+NOT+language%3AYul+NOT+language%3ARust&type=code), these are instances where the for loops are implemented, issue is with how some of these for loops are implemented, in this case the ones that are sequential, take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L238-L256

```solidity
    function forceDeployOnAddresses(ForceDeployment[] calldata _deployments) external payable {
        require(
            msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
            "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
        );


        uint256 deploymentsLength = _deployments.length;
        // We need to ensure that the `value` provided by the call is enough to provide `value`
        // for all of the deployments
        uint256 sumOfValues = 0;
        for (uint256 i = 0; i < deploymentsLength; ++i) {
            sumOfValues += _deployments[i].value;
        }
        require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");


        for (uint256 i = 0; i < deploymentsLength; ++i) {
            this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
        }
    }
```

Evidently, the double loop of "for (uint256 i = 0; i < deploymentsLength; ++i) " could be merged to reduce cost, cause in solidity, merging multiple for loops within a function can enhance efficiency and reduce gas costs, especially when they share a common iterating variable, since this minimizes redundant iterations over the same data, so execution becomes more cost-effective.

### Recommended Mitigation Steps

Consider merging similar loops, however, while merging can optimize gas usage and simplify logic, it may also increase code complexity. Therefore there should be a balance between optimization and maintainability.

## G-43 Consider using the `expectedBool == 1` syntax for booleans

### Proof of Concept

Take a look at [isDiamondStorageFrozen()]()

```solidity
    function isDiamondStorageFrozen() external view returns (bool) {
        Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();
        return ds.isFrozen;
    }
```

This function is used to check if the diamond storage is frozen and the function returns a bool, however implenting it with butwise operations would be cheaper, this report focuses on using bitwise operations for bool flags, i.e having the implemented changes be:

```diff
    function isDiamondStorageFrozen() external view returns (bool) {
-        Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();
-        return ds.isFrozen;
+       return ds.isFrozen == 1;
}
```

### Recommended Mitigation Steps

Apply the diff changes

## G-44 Shift Left instead of multiplication saves gas

### Proof of Concept

Whenever possible use shift Left instead of multiplication if possible to save gas
Instances are quite much in scope, but use this search command to pin point some: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++\*++NOT+language%3AMarkdown+NOT+language%3AJSON+NOT+language%3AYul+NOT+language%3ATypeScript+NOT+language%3ARust&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++*++NOT+language%3AMarkdown+NOT+language%3AJSON+NOT+language%3AYul+NOT+language%3ATypeScript+NOT+language%3ARust&type=code)

### Recommended Mitigation Steps

Consider the instaces that could be reimplemented to shift left instead of multiplication.

## G-45 `memory` should be used of instead state variables while emiting events

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L482-L497

```diff

    function _revertBatches(uint256 _newLastBatch) internal {
        require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch
        require(_newLastBatch >= s.totalBatchesExecuted, "v2"); // Already executed batches cannot be reverted


        if (_newLastBatch < s.totalBatchesVerified) {
            s.totalBatchesVerified = _newLastBatch;
        }
        s.totalBatchesCommitted = _newLastBatch;


        // Reset the batch number of the executed system contracts upgrade transaction if the batch
        // where the system contracts upgrade was committed is among the reverted batches.
        if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) {
            delete s.l2SystemContractsUpgradeBatchNumber;
        }


-        emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
+       emit BlocksRevert(_newLastBatch, s.totalBatchesVerified, s.totalBatchesExecuted);
    }
```

### Recommended Mitigation Steps

Apply suggested diff

## G-46 " `` " is cheaper than new bytes(0)

### Proof of Concept

Use this search command for instances: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+new+bytes%280%29+NOT+language%3AMarkdown+NOT+language%3ATypeScript+NOT+language%3AYul+NOT+language%3ARust&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+new+bytes%280%29+NOT+language%3AMarkdown+NOT+language%3ATypeScript+NOT+language%3AYul+NOT+language%3ARust&type=code) https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L308-L311

A more concrete example could be

```solidity
            signature: new bytes(0),
            factoryDeps: _hashFactoryDeps(_factoryDeps),
            paymasterInput: new bytes(0),
            reservedDynamic: new bytes(0)
```

### Recommended Mitigation Steps

Comsider replacing "new bytes(0)" with "``"

## G-47 Always use named returns for more efficiency

### Proof of Concept

The solidity compiler outputs more efficient code when the variable is declared in the return statement. There seem to be very few exceptions to this in practice, so if you see an anonymous return, you should test it with a named return instead to determine which case is most efficient.

For example, ake a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L46-L68

```solidity

    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public virtual override returns (bytes32) {
        // Note that due to commitment delay, the timestamp of the L2 upgrade batch may be earlier than the timestamp
        // of the L1 block at which the upgrade occurred. This means that using timestamp as a signifier of "upgraded"
        // on the L2 side would be inaccurate. The effects of this "back-dating" of L2 upgrade batches will be reduced
        // as the permitted delay window is reduced in the future.
        require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

        _setNewProtocolVersion(_proposedUpgrade.newProtocolVersion);
        _upgradeL1Contract(_proposedUpgrade.l1ContractsUpgradeCalldata);
        _upgradeVerifier(_proposedUpgrade.verifier, _proposedUpgrade.verifierParams);
        _setBaseSystemContracts(_proposedUpgrade.bootloaderHash, _proposedUpgrade.defaultAccountHash);

        bytes32 txHash = _setL2SystemContractUpgrade(
            _proposedUpgrade.l2ProtocolUpgradeTx,
            _proposedUpgrade.factoryDeps,
            _proposedUpgrade.newProtocolVersion
        );

        _postUpgrade(_proposedUpgrade.postUpgradeCalldata);

        emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);
    }
```

The variable is not named and would cost more to return.

### Recommended Mitigation Steps

COnsider specifically naming variables to be returned in each instance

## G-48 Check the last bit of a number to know if it's even/odd instead of the modulo operator

### Proof of Concept

The conventional way to check if a number is even or odd is to do (x % 2 == 0) where x is the number in question. We can instead check if x & uint256(1) == 0. where x is assumed to be a uint256. Bitwise and is cheaper than the modulo op code. In binary, the rightmost bit represents "1" whereas all the bits to the are multiples of 2, which are even. Adding "1" to an even number causes it to be odd.

Use this search command to find out instances where the `%` is used: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++%25+NOT+language%3AYul+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++%25+NOT+language%3AYul+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code)

### Recommended Mitigation Steps

Consider testong if a number is even or odd by checking the last bit.

## G-49 Remove unused `mapping` and `import variables`

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L44-L52

```solidity


    /// @dev Deprecated storage variable related to withdrawal limitations.
    mapping(address => uint256) private __DEPRECATED_lastWithdrawalLimitReset;


    /// @dev Deprecated storage variable related to withdrawal limitations.
    mapping(address => uint256) private __DEPRECATED_withdrawnAmountInWindow;


    /// @dev Deprecated storage variable related to deposit limitations.
    mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;



```

## G-50 Assembly checks for `address(0)` are more gas efficient

### Proof of Concept

it's generally more gas-efficient to use assembly to check for a zero address (address(0)) than to use the == operator.

The reason for this is that the == operator generates additional instructions in the EVM bytecode, which can increase the gas cost of your contract.

Use this search command to find instances [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++%3D%3D+address%280%29+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++%3D%3D+address%280%29+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code)

### Recommended Mitigation Steps

By using assembly to perform the zero address check, we can make our code more gas-efficient and reduce the overall cost of our contract, keep in mind that assembly can be more difficult to read and maintain than Solidity code, so it should be used with caution and only when necessary.

## G-51 To extract calldata values more efficiently we schould use assembly instead of `abi.decode`

### Proof of Concept

We can use assembly to decode our desired calldata values directly instead of using abi.decode, this allows us to avoid decoding calldata values that we will not use.

Use this search command to find instances [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++abi.decode%28+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++abi.decode%28+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code)

### Recommended Mitigation Steps

Consider applying suggestion.

- [Reference](https://code4rena.com/reports/2023-08-goodentry#gas-optimizations:~:text=%5BG%2D02%5D%20Use%20assembly%20in%20place%20of%20abi.decode%20to%20extract%20calldata%20values%20more%20efficiently)

## G-52 Use modifiers instead of functions to save gas

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L82C1-L103C1

```solidity
    /// @dev Returns whether an id corresponds to a registered operation. This
    /// includes Waiting, Ready, and Done operations.
    function isOperation(bytes32 _id) public view returns (bool) {
        return getOperationState(_id) != OperationState.Unset;
    }

    /// @dev Returns whether an operation is pending or not. Note that a "pending" operation may also be "ready".
    function isOperationPending(bytes32 _id) public view returns (bool) {
        OperationState state = getOperationState(_id);
        return state == OperationState.Waiting || state == OperationState.Ready;
    }

    /// @dev Returns whether an operation is ready for execution. Note that a "ready" operation is also "pending".
    function isOperationReady(bytes32 _id) public view returns (bool) {
        return getOperationState(_id) == OperationState.Ready;
    }

    /// @dev Returns whether an operation is done or not.
    function isOperationDone(bytes32 _id) public view returns (bool) {
        return getOperationState(_id) == OperationState.Done;
    }

```

These instances showcase how functions are used to get the operation state.

- Another instance https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L50

```solidity
    function isEmpty(Queue storage _queue) internal view returns (bool) {
```

Now consider two contracts with modifiers and internal view function:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.9;
contract Inlined {
    function isNotExpired(bool _true) internal view {
        require(_true == true, "Exchange: EXPIRED");
    }
function foo(bool _test) public returns(uint){
            isNotExpired(_test);
            return 1;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity 0.8.9;
contract Modifier {
modifier isNotExpired(bool _true) {
        require(_true == true, "Exchange: EXPIRED");
        _;
    }
function foo(bool _test) public isNotExpired(_test)returns(uint){
        return 1;
    }
}
```

Deploying this on remix would show how using the modifier option is cheaper.

### Recommended Mitigation Steps

Consider using modifiers in place of functions(public). _In some cases cases especially with internal functions using the internal functions in place of modifiers is better as would be explained in another report below_

## G-53 It is sometimes cheaper to cache calldata

### Proof of Concept

The `calldataload` instruction is a cheap opcode, but the solidity compiler will sometimes output cheaper code if we cache calldataload.

Multiple instances where this could be applied in scope, use this search command to pinpoint areas: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+calldata++NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+calldata++NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON&type=code)

#### Short POC

```solidity
contract LoopSum {
    function sumArr(uint256[] calldata arr) public pure returns (uint256 sum) {
        uint256 len = arr.length;
        for (uint256 i = 0; i < len; ) {
            sum += arr[i];
            unchecked {
                ++i;
            }
        }
    }
}
```

### Recommended Mitigation Steps

Consider caching the `calldataload`, keep in mind that thiis will not always be the case, so you should first test both possibilities.

## G-54 Admin functions can be made payable

### Proof of Concept

We can make admin specific functions payable to save gas, because the compiler won’t be checking the callvalue of the function, unlike end user functions, admins are trusted and as such won't unnecesary attach msg.value to functions.

Multiple instances in code, could be grepped by considering functions restricted to admins, this search command can help prepoint these modifiers: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++modifier+only+NOT+language%3AYul+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++modifier+only+NOT+language%3AYul+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code) then the functions where most of these modifiers are used can be marked payable, keep in mind that some other instances exist where not modifiers are used to restrict calls to only admins but ` require msg.sender == expectedAdmin` checks are made so this should be checked too.

### Recommended Mitigation Steps

Consider making admin functions payable

## G-55 In some cases using bytes32 instead of string saves gas

### Proof of Concept

> NB: This should only be used if we can limit the length to a certain number of bytes, we should always use one of bytes1 to bytes32 because they are even much more cheaper.

Multiple instances, to list a few:

- Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20

```solidity

string public constant override getName = "AdminFacet";

```

- ANother instance https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27

```solidity
string public constant override getName = "ExecutorFacet";

```

- Another instance is here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25

```solidity


    string public constant override getName = "GettersFacet";

```

- Another instance is here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35

```solidity

   string public constant override getName = "MailboxFacet";


```

### Recommenda

Apply `diffs` to these instances and change `string` to `bytes`, i.e

```diff
-  string ...
+ bytes ...
```

## G-56 Redundant check in DefaultAccount.sol

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L159C2-L189C6

```solidity
   function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {
        require(_signature.length == 65, "Signature length is incorrect");
        uint8 v;
        bytes32 r;
        bytes32 s;
        // Signature loading code
        // we jump 32 (0x20) as the first slot of bytes contains the length
        // we jump 65 (0x41) per signature
        // for v we load 32 bytes ending with v (the first 31 come from s) then apply a mask
        assembly {
            r := mload(add(_signature, 0x20))
            s := mload(add(_signature, 0x40))
            v := and(mload(add(_signature, 0x41)), 0xff)
        }
        //@audit
        require(v == 27 || v == 28, "v is neither 27 nor 28");

        // EIP-2 still allows signature malleability for ecrecover(). Remove this possibility and make the signature
        // unique. Appendix F in the Ethereum Yellow paper (https://ethereum.github.io/yellowpaper/paper.pdf), defines
        // the valid range for s in (301): 0 < s < secp256k1n ÷ 2 + 1, and for v in (302): v ∈ {27, 28}. Most
        // signatures from current libraries generate a unique signature with an s-value in the lower half order.
        //
        // If your library generates malleable signatures, such as s-values in the upper range, calculate a new s-value
        // with 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFEBAAEDCE6AF48A03BBFD25E8CD0364141 - s1 and flip v from 27 to 28 or
        // vice versa. If your library also generates signatures with 0/1 for v instead 27/28, add 27 to v to accept
        // these malleable signatures as well.
        require(uint256(s) <= 0x7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF5D576E7357A4501DDFE92F46681B20A0, "Invalid s");

        address recoveredAddress = ecrecover(_hash, v, r, s);

        return recoveredAddress == address(this) && recoveredAddress != address(0);
    }
```

As seen, this check `  require(v == 27 || v == 28, "v is neither 27 nor 28");` is employed but this is not needed since it's always true, for more info, refer to [this tweet](https://twitter.com/alexberegszaszi/status/1534461421454606336?s=20&t=H0Dv3ZT2bicx00hLWJk7Fg)

### Impact

Unnecessary checks while validating signatures

### Recommended Mitigation Steps

Remove the check: `require(v == 27 || v == 28, "v is neither 27 nor 28");`

## G-57 Chunking the pubdata should be made more efficient

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L21-L57

```solidity
    function chunkAndPublishPubdata(bytes calldata _pubdata) external onlyCallFrom(address(L1_MESSENGER_CONTRACT)) {
        require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");

        bytes32[] memory blobHashes = new bytes32[](MAX_NUMBER_OF_BLOBS);

        // We allocate to the full size of MAX_NUMBER_OF_BLOBS * BLOB_SIZE_BYTES because we need to pad
        // the data on the right with 0s if it doesn't take up the full blob
        bytes memory totalBlobs = new bytes(BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS);

        assembly {
            // The pointer to the allocated memory above. We skip 32 bytes to avoid overwriting the length.
            let ptr := add(totalBlobs, 0x20)
            calldatacopy(ptr, _pubdata.offset, _pubdata.length)
        }

        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
            uint256 start = BLOB_SIZE_BYTES * i;

            // We break if the pubdata isn't enough to cover 2 blobs. On L1 it is expected that the hash
            // will be bytes32(0) if a blob isn't going to be used.
            if (start >= _pubdata.length) {
                break;
            }

            bytes32 blobHash;
            assembly {
                // The pointer to the allocated memory above skipping the length.
                let ptr := add(totalBlobs, 0x20)
                blobHash := keccak256(add(ptr, start), BLOB_SIZE_BYTES)
            }

            blobHashes[i] = blobHash;
        }

        SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.BLOB_ONE_HASH_KEY)), blobHashes[0]);
        SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.BLOB_TWO_HASH_KEY)), blobHashes[1]);
    }
```

Function is used to chunk pubdata into pieces that can fit into blobs, case is that it queries to `constant variables` and then multiplies, when this value can just be hardcoded to the codebase, i.e this line `require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");`, both `BLOB_SIZE_BYTES` and `MAX_NUMBER_OF_BLOBS` have fixed numbers of `2` and `126976` respectively as gotten from https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Constants.sol

This means that the check could be changed to `require(_pubdata.length <= 253_952 "pubdata should fit in 2 blobs");`

### Recommended Mitigation Steps

Consider making the change in as much as the values are going to be constants

## G-58 `TransactionHelper::isEthToken()` is not used anywhere so it should be removed

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L89-L97

```solidity

    function isEthToken(uint256 _addr) internal pure returns (bool) {
        return _addr == uint256(uint160(address(BASE_TOKEN_SYSTEM_CONTRACT))) || _addr == 0;
    }

```

This function is used to know whether the `address` passed is th `Ether` address, and also returns true if the address passed is `0x0` (for conveniency) as stated [here](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L92), issue with this is tht using this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+isEthToken&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+isEthToken&type=code) we can see that this function is not used anywhere and as such is just adding unnecessary gas costs to deploy the contract

### Impact

Remove [this section](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L89-L96) of `TransactionHelper.sol` since it's not being used and is just an unnecessary addition to the bytecode that gets deployed for the contract and as such more gas cost while deployign the contract.

### Recommended Mitigation Steps

Remove the `isEthToken()` function since it's not being used anywhere

## G-59 Count up instead of counting down in `for` statements

Counting down is more gas efficient than counting up because we will get gas refund in the last transaction when making non-zero to zero variable.

For example take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226

```solidity
  for (uint256 i = 0; i < _factoryDeps.length; ++i) {

```

```diff

-  for (uint256 i = 0; i < _factoryDeps.length; ++i) {
+  for (uint256 i = _factoryDeps.length - 1; i >= 0; --i) {

```

### Recommended Mitigation Steps

Apply the diff changes

## G-60 Simplifying conditional checks with Bitwise Operators

This report explores using bitwise operators (`^` - XOR and `&` - AND) as an alternative to standard equality checks (`==`) in Solidity contracts.

- **XOR (^)** checks for differences between bits. If corresponding bits in two variables are the same (both 0 or both 1), the result is 0. Otherwise, the result is 1.
- **AND (&)** performs a bitwise AND operation. The result has a 1 only if the corresponding bits in both variables are 1. Otherwise, the result is 0.

**Optimizing Conditions:**

1. **Checking Equality:**

   - Standard approach: `a == b` checks if all bits in `a` and `b` are the same.
   - Alternative approach: `!(a ^ b)` (logical NOT of XOR). Since XOR returns 0 for equal bits, the negation (`!`) makes it true only for equality.

2. **Checking for Any Condition:**
   - Standard approach: `a || b` checks if either `a` or `b` is true (has a non-zero value).
   - Alternative approach: `(a ^ b) & 1`. This leverages XOR to find any difference and the AND with 1 ensures a non-zero result only if a difference exists.

Both approaches achieve the same outcome, but bitwise operations are slightly more gas-efficient compared to standard comparisons.

An instance in scope:

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L91

```solidity
return state == OperationState.Waiting || state == OperationState.Ready;
```

Checks if the state is either Waiting or Ready.

Optimized code could be like this `return state ^ OperationState.Waiting & state ^ OperationState.Ready;`, so it uses XOR to detect any difference between the state and the desired states, then ensures a non-zero result with AND and 1.

### Recommended Mitigation Steps

Consider applying the fix, but downside is that while bitwise operators can be efficient, code readability would be slightly affected. Consider using them strategically.

## G-61 Consider writing gas-optimal for-loops

Using this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+for+%28+NOT+language%3AMarkdown+NOT+language%3ATypeScript+NOT+language%3AYul+NOT+language%3ARust&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+for+%28+NOT+language%3AMarkdown+NOT+language%3ATypeScript+NOT+language%3AYul+NOT+language%3ARust&type=code), we can see instances of the `for loops`, but most of these instances do not entail with a gas optimal for loops, for example this is what a gas-optimal for loop looks like, if you combine the two tricks below:

```
for (uint256 i; i < limit; ) {

    // inside the loop

    unchecked {
        ++i;
    }
}
```

Main differences here from a conventional for loop is that `i++` becomes `++i` and it is unchecked because the limit variable ensures it won’t overflow.

### Recommended Mitigation Steps

Consider making all loops with the above format

## G-62 [UnsafeBytes.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol) could be better optimized while parsing bytes for transactions

### Proof of Concept

Take a look at all the read functions from https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L19-L45.

One can see that The `UnsafeBytes` library is utilized across `L1ERC20Bridge`, `L1WethBridge`, `Executor`, and the `Mailbox` contracts to parse significantly large payloads of data sequentially in an optimized way _(This can be seen by grepping these reaad functions in the entire scope)_.

Now, each and every utilization points of the library make use of a `memory` argument even though a `calldata` argument could be passed in, i.e (`L1ERC20Bridge::_parseL2WithdrawalMessage`, `L1WethBridge::_parseL2EthWithdrawalMessage`, `Executor::_processL2Logs`, `Mailbox::_parseL2WithdrawalMessage`).

### Recommended Mitigation Steps

Consider updating the library to work on `calldata` arguments instead, this way the gas cost would be significantly reduced as it would utilize `calldataload`, and would not require copying the full `calldata` payload to `memory`, therefor not incurirng any hidden memory expansion gas costs.

## G-63 Do-while loops are cheaper than for loops and should be considered

### Proof of Concept

Consider this article from rareskills for a simple POC on how using do-while loops are cheaper than for loops: https://www.rareskills.io/post/gas-optimization

Now as already hinted in this report they are multiple for loops in scope as can be seen by using this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+for+%28+NOT+language%3AMarkdown+NOT+language%3ATypeScript+NOT+language%3AYul+NOT+language%3ARust&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+for+%28+NOT+language%3AMarkdown+NOT+language%3ATypeScript+NOT+language%3AYul+NOT+language%3ARust&type=code)

### Recommended Mitigation Steps

Consider using do-while loops in the stead of for loops where possible.

## G-64 Consider Short-circuit booleans

In Solidity, short-circuiting behavior in boolean expressions with `||` (logical OR) and `&&` (logical AND) operators optimizes gas usage by evaluating expressions conditionally. For `||`, if the first condition evaluates to true, the second is not evaluated, saving gas in scenarios where the first condition is likely to succeed. Conversely, for `&&`, if the first condition evaluates to false, the second condition is skipped, which is useful for saving gas when the first condition is likely to fail. Placing the less expensive or more likely-to-succeed condition first leverages short-circuiting for efficient gas consumption.

Utilizing short-circuiting effectively requires strategic placement of conditions within `require` statements or similar constructs. For instance, `require(msg.sender == owner || msg.sender == manager)` will not evaluate the second condition if the first is true, making it gas-efficient for frequent success scenarios. Similarly, in expressions like `require(msg.sender == owner && msg.sender == manager)`, failing the first condition skips the second, optimizing gas for scenarios where reverts are common. Thus, arranging conditions based on their gas costs and likelihood of passing can significantly reduce overall gas consumption.

This needs more logic to pinpoint instances, but we can use these two search commands to find out where we can apply short-circuiting:

- `||` - [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+%7C%7C++NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON+NOT+language%3ARust&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+%7C%7C++NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON+NOT+language%3ARust&type=code)
- `&&` - [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+%26%26+NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON+NOT+language%3ARust&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+%26%26+NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON+NOT+language%3ARust&type=code)

### Recommended Mitigation Steps

As hinted, this needs careful logic placed, but consider short circuiting while not overcomplicating readability of code.

## G-65 Shortening an array rather than copying to a new one saves gas

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L399

```solidity


      uint256[] memory proofPublicInput = new uint256[](committedBatchesLength);
```

Or even https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L206

```solidity
         result = new Facet[](facetsLen);

```

And other instances, could be pinpointed using [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+++%3D+new+NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON+NOT+language%3ARust&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+++%3D+new+NOT+language%3ATypeScript+NOT+language%3AMarkdown+NOT+language%3AYul+NOT+language%3AJSON+NOT+language%3ARust&type=code), and then take instances where an array is being created where as we can shorten them

### Recommended Mitigation Steps

If possible, shorten the arrays instead of creating new ones.

## G-66 Use assembly to perform efficient back-to-back calls

### Proof of Concept

Use assembly to reuse memory space when making more than one external call.
An operation that causes the solidity compiler to expand memory is making external calls. When making external calls the compiler has to encode the function signature of the function it wishes to call on the external contract alongside it’s arguments in memory. As we know, solidity does not clear or reuse memory memory so it’ll have to store these data in the next free memory pointer which expands memory further.

With inline assembly, we can either use the scratch space and free memory pointer offset to store this data (as above) if the function arguments do not take up more than 96 bytes in memory. Better still, if we are making more than one external call we can reuse the same memory space as the first calls to store the new arguments in memory without expanding memory unnecessarily. Solidity in this scenario would expand memory by as much as the returned data length is. This is because the returned data is stored in memory (in most cases). If the return data is less than 96 bytes, we can use the scratch space to store it so as to prevent expanding memory.

Take a look at [this gist](https://gist.github.com/Bauchibred/c13b7cf708be0c0e9c5b9145e19b721d), by deploying it, we can see that we save approximately 2,000 gas by using the scratch space to store the function selector and it’s arguments and also reusing the same memory space for the second call while storing the returned data in the zero slot thus not expanding memory.

TLDR: If the arguments of the external function we wish to call is above 64 bytes and if you are making one external call, it wouldn’t save any significant gas writing it in assembly. However, if making more than one call, we can still save gas by reusing the same memory slot for the 2 calls using inline assembly.

> NB: Always remember to update the free memory pointer if the offset it points to is already used, to avoid solidity overriding the data stored there or using the value stored there in an unexpected way.

Instances of this in scope are mostly, where more than one external callhaooens in a sequence, i.e take this code snippet for example https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L171-L179

```solidity
    /// @dev Transfers tokens from the depositor address to the smart contract address.
    /// @return The difference between the contract balance before and after the transferring of funds.
    function _depositFunds(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
        uint256 balanceBefore = _token.balanceOf(address(this));
        _token.safeTransferFrom(_from, address(this), _amount);
        uint256 balanceAfter = _token.balanceOf(address(this));


        return balanceAfter - balanceBefore;
    }
```

### Recommended Mitigation Steps

Note to avoid overwriting the zero slot (0x60 memory offset) if you have undefined dynamic memory values within that call stack. An alternative is to explicitly define dynamic memory values or if used, to set the slot back to 0x00 before exiting the assembly block.

## G-67 Using assembly to validate `msg.sender` is more gas efficient

### Proof of Concept

it's generally more gas-efficient to use assembly to check for a msg,sender

Use this search command to find instances [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++%3D%3D+msg.sender+only+NOT+language%3AYul+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync++%3D%3D+msg.sender+only+NOT+language%3AYul+NOT+language%3AMarkdown+NOT+language%3ATypeScript&type=code)

### Recommended Mitigation Steps

By using assembly to perform the msg.sender check, we can make our code more gas-efficient and reduce the overall cost of the contract, keep in mind that assembly can be more difficult to read and maintain than Solidity code, so it should be used with caution and only when necessary.

## G-68 Proof verification is performed twice in `proveBatches()` causing double expenditure of gas

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L386-L440

```solidity
    function _proveBatches(
        StoredBatchInfo calldata _prevBatch,
        StoredBatchInfo[] calldata _committedBatches,
        ProofInput calldata _proof
    ) internal {
    //ommited for brevity
        //@audit
        if (_proof.serializedProof.length > 0) {
            _verifyProof(proofPublicInput, _proof);
        }
        // #else
        _verifyProof(proofPublicInput, _proof);
        // #endif

        emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);
        s.totalBatchesVerified = currentTotalBatchesVerified;
    }

```

Evidently, if the proof is not empty, it gets verified, due to the `if` block, case is the `else` has been has been commented out which means that a proof is always going to undergo double verification in as much as it's > 0. Causig double gas expenditure of calling this: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L441-L452

```solidity
    function _verifyProof(uint256[] memory proofPublicInput, ProofInput calldata _proof) internal view {
        // We can only process 1 batch proof at a time.
        require(proofPublicInput.length == 1, "t4");

        bool successVerifyProof = s.verifier.verify(
            proofPublicInput,
            _proof.serializedProof,
            _proof.recursiveAggregationInput
        );
        require(successVerifyProof, "p"); // Proof verification fail
    }

```

### Recommended Mitigation Steps

Consider verifying only once if `_proof.serializedProof.length > 0` is true.

## G-69 Use assembly to hash instead of solidity

Using assembly for small `keccak256` hashes saves gas, there are multiple instances of this, but we can use this search command to grep most of them

- Search command : [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+keccak256%28+NOT+language%3AMarkdown+NOT+language%3ATypeScript+NOT+language%3AYul&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+keccak256%28+NOT+language%3AMarkdown+NOT+language%3ATypeScript+NOT+language%3AYul&type=code), i.e an instance could be here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L332

```solidity
        canonicalTxHash = keccak256(transactionEncoding);
```

### Recommended Mitigation Steps

Consider using assembly for the instances that include small ` keccak256` hashes

## G-70 Openzeppelin's SafeCast is not gas optimized, consider using Solady's safeCast library

Solady’s [SafeCast](https://github.com/Vectorized/solady/blob/main/src/utils/SafeCastLib.sol) implementation is more gas efficient than OZ's version. We recommend you switch to that library instead.

Using this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync%20openzeppelin%2Fcontracts%2Futils%2Fmath%2FSafeCast.sol&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync%20openzeppelin%2Fcontracts%2Futils%2Fmath%2FSafeCast.sol&type=code) we can see that Oz's implementation of safe cast is being used, i.e in [Diamond.sol](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L5)

### Recommended Mitigation Steps

Consider using Solady's `SafeCast` instead.
