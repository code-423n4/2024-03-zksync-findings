## Gas Findings

|    | Issue | Instances | Total Gas Saved |
|----|-------|:---------:|:---------:|
| [G-01] | Structs can be packed into fewer storage slots | 4 | 80000 |
| [G-02] | Optimize Storage with Byte Truncation for Time Related State Variables | 1 | 20000 |
| [G-03] | State variables can be packed into fewer storage slots | 1 | 20000 |
| [G-04] | Optimize Storage Layout in Structs by Truncating Time Related Fields | 2 | 40000 |
| [G-05] | A `memory` array's `length` should not be looked up in every iteration of a `for`/`while`-loop | 11 | 33 |
| [G-06] | Avoid Comparisons of Boolean Expressions to Boolean Literals | 1 | 3 |
| [G-07] | `do`-`while` is cheaper than `for`-loops when the initial check can be skipped | 35 | 8925 |
| [G-08] | Use `assembly` for Efficient Event Emission | 80 | 30400 |
| [G-09] | Use custom errors rather than `require()/assert()/revert(with msg)` with string to save gas | 350 | 17500 |
| [G-10] | Avoid Emitting Events Inside Loops | 3 | 1200 |
| [G-11] | Enable IR-based code generation | 106 | - |
| [G-12] | Assembly: Check `msg.sender` using xor and the scratch space | 46 | 966 |
| [G-13] | Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct` | 23 | - |
| [G-14] | Assigning `state` variables directly with struct constructors wastes gas | 1 | 71 |
| [G-15] | Assembly: Use scratch space when building emitted events with two data arguments | 3 | 45 |
| [G-16] | Stack variable is only used once | 285 | 855 |
| [G-17] | `abi.encodePacked `is more gas efficient than `abi.encode` | 35 | 7000 |
| [G-18] | Consider Using `selfbalance()` Over `address(this).balance` | 4 | - |
| [G-19] | Using `require()` instead of `assert()` safes gas | 5 | 165 |
| [G-20] | Use `assembly` to write mutable storage values | 128 | 1408 |
| [G-21] | Using `delete` on a `uint/int` variable is cheaper than assigning it to `0` | 3 | 24 |
| [G-22] | Optimize Ether Transfers with `receive()` Function | 33 | 1485 |
| [G-23] | Use `revert()` to gain maximum gas savings | 352 | 17600 |
| [G-24] | Use local variables for emitting | 10 | 1000 |
| [G-25] | `x.a = x.a + b` always cheaper than `x.a += b` for Structs | 1 | 5 |
| [G-26] | Initializers can be marked as payable | 10 | - |
| [G-27] | Using `constants` instead of `enum` can save gas | 15 | 0 |
| [G-28] | Merging Sequential `for` Loops with Identical Conditions | 4 | 3400 |
| [G-29] | Create variable outside the loop | 48 | 960 |
| [G-30] | Use `assembly` in place of `abi.decode` to extract calldata values more efficiently | 1 | 10 |
| [G-31] | Do not cache `constant`s to save gas | 1 | 0 |
| [G-32] | Shorten the array rather than copying to a new on | 4 | 0 |
| [G-33] | Nested for loops should be avoided due to high gas costs resulting from O^2 time complexity | 1 | 0 |
| [G-34] | Using `delete` on a `bool` variable is cheaper than assigning it to `false` | 3 | 72 |
| [G-35] | Expression ("") is cheaper than `new bytes(0)` | 8 | 400 |
| [G-36] | Use `Array.unsafeAccess()` to avoid repeated array length checks | 11 | 23100 |
| [G-37] | Counting down when iterating, saves gas | 18 | 162 |
| [G-38] | `>=` costs less gas than `>` | 24 | 144 |
| [G-39] | Consider pre-calculating the address of `address(this)` to save gas | 22 | 0 |
| [G-40] | Use `unchecked` for Non-Loop Increment/Decrement Operations | 6 | 180 |
| [G-41] | Using `this` to access functions results in an external call, wasting gas | 8 | 800 |
| [G-42] | Constructors can be marked `payable` | 11 | 264 |
| [G-43] | Multiple accesses of a mapping/array should use a local variable cache | 20 | 2900 |
| [G-44] | Optimize Increment and Decrement in loops with `unchecked` keyword | 28 | 1680 |
| [G-45] | Reduce gas usage by moving to Solidity 0.8.19 or later | 1 | - |
| [G-46] | Reduce deployment costs by tweaking contracts' metadata | 106 | 1123600 |
| [G-47] | Use Pre-Increment/Decrement (++i/--i) to Save Gas | 8 | 40 |
| [G-48] | Nesting `if`-statements is cheaper than using `&&` | 8 | 48 |
| [G-49] | Use `storage` instead of `memory` for state structs/arrays | 20 | 42000 |
| [G-50] | Optimize by Using Assembly for Low-Level Calls' Return Data | 1 | 159 |
| [G-51] | Store `keccak256()` Hash in Immutable Variable | 3 | 126 |
| [G-52] | Cache Function Calls for Efficiency | 21 | - |
| [G-53] | Superfluous Event Fields | 1 | 34 |
| [G-54] | Unutilized Named Return Variables Waste Gas Without Optimizer | 7 | - |
| [G-55] | Use `unchecked` for Math Operations if they already checked | 6 | 510 |
| [G-56] | Using `private` rather than `public`, saves gas | 59 | 1298000 |
| [G-57] | Use Assembly for Hash Calculations | 60 | 60300 |
| [G-58] | Refactor duplicated require()/revert() checks to save gas | 7 | - |
| [G-59] | Use Assembly for Efficient Memory Management in Multiple External Calls | 17 | 48000 |
| [G-60] | Optimize `require/revert` Statements with Assembly | 340 | 102000 |
| [G-61] | Cached Global Variables | 1 | 12 |
| [G-62] | Simple checks for zero `uint` can be done using `assembly` to save gas | 65 | 260 |
| [G-63] | Consider Using += for Mappings | 4 | 160 |
| [G-64] | Consider using solady's `FixedPointMathLib` | 78 | - |
| [G-65] | Avoid Zero to Non-Zero Storage Writes Where Possible | 32 | 707200 |
| [G-66] | Avoid Unnecessary Gas Usage with Shorter `require()/revert()` Strings | 105 | 1890 |
| [G-67] | Use `unchecked` for division which do not divide by -X sonce they can't overflow | 14 | 280 |
| [G-68] | Use solady library where possible to save gas | 24 | 24000 |
| [G-69] | Use `uint256(1)`/`uint256(2)` instead of `true`/`false` to save gas for changes | 7 | 119000 |
| [G-70] | Use Bit Shifting for Multiplication by Powers of Two | 24 | 480 |
| [G-71] | Use Multiple `require()` Statements Instead of chaining | 5 | 15 |
| [G-72] | Delete Unused State Variables | 19 | 380000 |
| [G-73] | Mark Functions That Revert For Normal Users As `payable` | 98 | 2058 |
| [G-74] | Prefer `private` over `public` for Constants to Save Gas | 5 | 15000 |
| [G-75] | `<x> += <y>` costs more gas than `<x> = <x> + <y>` for state variables | 3 | 339 |
| [G-76] | Using `bool`s for storage incurs overhead | 7 | 700 |
| [G-77] | Optimize Gas by Using Only Named Returns | 265 | 11660 |
| [G-78] | Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead | 191 | 1146 |
| [G-79] | Unlimited gas consumption risk due to external call recipients | 2 | - |
| [G-80] | Use assembly to check for `address(0)` | 27 | 1566 |
| [G-81] | `internal`/`private` functions only called once can be inlined to save gas | 99 | 1980 |
| [G-82] | Inefficient Use of String Constants | 5 | 1890 |
| [G-83] | Consider using OZ EnumerateSet in place of nested mappings | 13 | 13000 |
| [G-84] | Declare `immutable` as `private` to save gas | 6 | 18000 |
| [G-85] | State variables should be cached in stack rather than re-reading them from storage | 15 | 2037 |
| [G-86] | Division by powers of two should use bit shifting | 5 | 100 |
| [G-87] | Optimize names to save gas | 59 | 1180 |
| [G-88] | Avoid updating storage when the value hasn't changed | 22 | 17600 |
| [G-89] | Optimize External Calls with Assembly for Memory Efficiency | 39 | 8580 |

Total: 3670 instances of 89 issues with 4287707 gas saved

## Gas Findings Details

### [G-01] Structs can be packed into fewer storage slots

Each slot saved can avoid an extra Gsset (20000 gas) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings.

<details>
<summary><i>4 issue instances in 4 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

/// @audit - Struct used 35 storage slots, but can be packed to 34 storage slots.
//	struct ZkSyncStateTransitionStorage {
//	    uint256 chainId;
//	    FeeParams feeParams;
//	    uint256 l2SystemContractsUpgradeBatchNumber;
//	    bytes32 l2SystemContractsUpgradeTxHash;
//	    uint256 protocolVersion;
//	    mapping(address => uint256) __DEPRECATED_totalDepositedAmountPerUser;
//	    uint256 __DEPRECATED_withdrawnAmountInWindow;
//	    uint256 __DEPRECATED_lastWithdrawalLimitReset;
//	    mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;
//	    UpgradeStorage __DEPRECATED_upgrades;
//	    uint256 priorityTxMaxGasLimit;
//	    bytes32 l2DefaultAccountBytecodeHash;
//	    bytes32 l2BootloaderBytecodeHash;
//	    VerifierParams verifierParams;
//	    PriorityQueue.Queue priorityQueue;
//	    mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;
//	    mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
//	    uint256 totalBatchesCommitted;
//	    uint256 totalBatchesVerified;
//	    uint256 totalBatchesExecuted;
//	    IVerifier verifier;
//	    mapping(address validatorAddress => bool isValidator) validators;
//	    uint256[7] __DEPRECATED_diamondCutStorage;
//	    address baseTokenBridge;
//	    bool zkPorterIsAvailable;
//	    address baseToken;
//	    address stateTransitionManager;
//	    address bridgehub;
//	    address blobVersionedHashRetriever;
//	    address pendingAdmin;
//	    address admin;
//	    address __DEPRECATED_allowList;
//	    address __DEPRECATED_pendingGovernor;
//	    address __DEPRECATED_governor;
//	    uint128 baseTokenGasPriceMultiplierDenominator;
//	    uint128 baseTokenGasPriceMultiplierNominator;
//	}
66: struct ZkSyncStateTransitionStorage {
    /// @dev Storage of variables needed for deprecated diamond cut facet
    uint256[7] __DEPRECATED_diamondCutStorage;
    /// @notice Address which will exercise critical changes to the Diamond Proxy (upgrades, freezing & unfreezing). Replaced by STM
    address __DEPRECATED_governor;
    /// @notice Address that the governor proposed as one that will replace it
    address __DEPRECATED_pendingGovernor;
    /// @notice List of permitted validators
    mapping(address validatorAddress => bool isValidator) validators;
    /// @dev Verifier contract. Used to verify aggregated proof for batches
    IVerifier verifier;
    /// @notice Total number of executed batches i.e. batches[totalBatchesExecuted] points at the latest executed batch
    /// (batch 0 is genesis)
    uint256 totalBatchesExecuted;
    /// @notice Total number of proved batches i.e. batches[totalBatchesProved] points at the latest proved batch
    uint256 totalBatchesVerified;
    /// @notice Total number of committed batches i.e. batches[totalBatchesCommitted] points at the latest committed
    /// batch
    uint256 totalBatchesCommitted;
    /// @dev Stored hashed StoredBatch for batch number
    mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
    /// @dev Stored root hashes of L2 -> L1 logs
    mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;
    /// @dev Container that stores transactions requested from L1
    PriorityQueue.Queue priorityQueue;
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
    /// @dev The maximum number of the L2 gas that a user can request for L1 -> L2 transactions
    /// @dev This is the maximum number of L2 gas that is available for the "body" of the transaction, i.e.
    /// without overhead for proving the batch.
    uint256 priorityTxMaxGasLimit;
    /// @dev Storage of variables needed for upgrade facet
    UpgradeStorage __DEPRECATED_upgrades;
    /// @dev A mapping L2 batch number => message number => flag.
    /// @dev The L2 -> L1 log is sent for every withdrawal, so this mapping is serving as
    /// a flag to indicate that the message was already processed.
    /// @dev Used to indicate that eth withdrawal was already processed
    mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;
    /// @dev The most recent withdrawal time and amount reset
    uint256 __DEPRECATED_lastWithdrawalLimitReset;
    /// @dev The accumulated withdrawn amount during the withdrawal limit window
    uint256 __DEPRECATED_withdrawnAmountInWindow;
    /// @dev A mapping user address => the total deposited amount by the user
    mapping(address => uint256) __DEPRECATED_totalDepositedAmountPerUser;
    /// @dev Stores the protocol version. Note, that the protocol version may not only encompass changes to the
    /// smart contracts, but also to the node behavior.
    uint256 protocolVersion;
    /// @dev Hash of the system contract upgrade transaction. If 0, then no upgrade transaction needs to be done.
    bytes32 l2SystemContractsUpgradeTxHash;
    /// @dev Batch number where the upgrade transaction has happened. If 0, then no upgrade transaction has happened
    /// yet.
    uint256 l2SystemContractsUpgradeBatchNumber;
    /// @dev Address which will exercise non-critical changes to the Diamond Proxy (changing validator set & unfreezing)
    address admin;
    /// @notice Address that the admin proposed as one that will replace admin role
    address pendingAdmin;
    /// @dev Fee params used to derive gasPrice for the L1->L2 transactions. For L2 transactions,
    /// the bootloader gives enough freedom to the operator.
    FeeParams feeParams;
    /// @dev Address of the blob versioned hash getter smart contract used for EIP-4844 versioned hashes.
    address blobVersionedHashRetriever;
    /// new fields
    /// @dev The chainId of the chain
    uint256 chainId;
    /// @dev The address of the bridgehub
    address bridgehub;
    /// @dev The address of the StateTransitionManager
    address stateTransitionManager;
    /// @dev The address of the baseToken contract. Eth is address(1)
    address baseToken;
    /// @dev The address of the baseTokenbridge. Eth also uses the shared bridge
    address baseTokenBridge;
    /// @notice gasPriceMultiplier for each baseToken, so that each L1->L2 transaction pays for its transaction on the destination
    /// we multiply by the nominator, and divide by the denominator
    uint128 baseTokenGasPriceMultiplierNominator;
    uint128 baseTokenGasPriceMultiplierDenominator;
}
```
[66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L66)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

/// @audit - Struct used 4 storage slots, but can be packed to 3 storage slots.
//	struct FacetCut {
//	    bytes4[] selectors;
//	    Action action;
//	    address facet;
//	    bool isFreezable;
//	}
62: struct FacetCut {
        address facet;
        Action action;
        bool isFreezable;
        bytes4[] selectors;
    }
```
[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L62)

```solidity
File: code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

/// @audit - Struct used 8 storage slots, but can be packed to 7 storage slots.
//	struct StateTransitionManagerInitializeData {
//	    uint256 protocolVersion;
//	    Diamond.DiamondCutData diamondCut;
//	    bytes32 genesisBatchCommitment;
//	    bytes32 genesisBatchHash;
//	    address genesisUpgrade;
//	    uint64 genesisIndexRepeatedStorageChanges;
//	    address validatorTimelock;
//	    address governor;
//	}
15: struct StateTransitionManagerInitializeData {
    address governor;
    address validatorTimelock;
    address genesisUpgrade;
    bytes32 genesisBatchHash;
    uint64 genesisIndexRepeatedStorageChanges;
    bytes32 genesisBatchCommitment;
    Diamond.DiamondCutData diamondCut;
    uint256 protocolVersion;
}
```
[15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L15)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

/// @audit - Struct used 8 storage slots, but can be packed to 7 storage slots.
//	struct StoredBatchInfo {
//	    bytes32 commitment;
//	    uint256 timestamp;
//	    bytes32 l2LogsTreeRoot;
//	    bytes32 priorityOperationsHash;
//	    uint256 numberOfLayer1Txs;
//	    bytes32 batchHash;
//	    uint64 indexRepeatedStorageChanges;
//	    uint64 batchNumber;
//	}
83: struct StoredBatchInfo {
        uint64 batchNumber;
        bytes32 batchHash;
        uint64 indexRepeatedStorageChanges;
        uint256 numberOfLayer1Txs;
        bytes32 priorityOperationsHash;
        bytes32 l2LogsTreeRoot;
        uint256 timestamp;
        bytes32 commitment;
    }
```
[83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L83)
</details>

### [G-02] Optimize Storage with Byte Truncation for Time Related State Variables

Certain state variables, particularly timestamps, can be safely stored using `uint32`. 
By optimizing these variables, contracts can utilize storage more efficiently.
This not only results in a reduction in the initial gas costs (due to fewer Gsset operations) but also provides savings in subsequent read and write operations.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

/// @audit - State variables after packing use 3 storage slots, but can be packed to 2 storage slots.
//	mapping(bytes32 operationId => uint256 executionTimestamp) public timestamps;
//	address public securityCouncil;
//	uint32 public minDelay;

20: contract Governance is IGovernance, Ownable2Step
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L20)
</details>

### [G-03] State variables can be packed into fewer storage slots

Each slot saved can avoid an extra Gsset (20000 gas). Reads and writes (if two variables that occupy the same slot are written by the same function) will have a cheaper gas consumption.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: code/system-contracts/contracts/SystemContext.sol

/// @audit - State variables use 17 storage slots, but can be packed to 16 storage slots.
//	uint256 internal basePubdataSpent
//	uint256 public gasPerPubdataByte
//	VirtualBlockUpgradeInfo internal virtualBlockUpgradeInfo
//	BlockInfo internal currentVirtualL2BlockInfo
//	bytes32[MINIBLOCK_HASHES_TO_STORE] internal l2BlockHash
//	bytes32 internal currentL2BlockTxsRollingHash
//	BlockInfo internal currentL2BlockInfo
//	mapping(uint256 batchNumber => bytes32 batchHash) internal batchHashes
//	BlockInfo internal currentBatchInfo
//	uint256 public baseFee
//	uint256 public difficulty = 2.5e15
//	uint256 public blockGasLimit = type(uint32).max
//	uint256 public gasPrice
//	uint256 public chainId
//	address public coinbase = BOOTLOADER_FORMAL_ADDRESS
//	uint16 public txNumberInBlock
//	address public origin

17: contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract
```
[17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L17)
</details>

### [G-04] Optimize Storage Layout in Structs by Truncating Time Related Fields

The field ordering within the following structs isn't optimized for efficient storage in the Ethereum Virtual Machine (EVM). By appropriately rearranging the fields within these structs, you can achieve improved gas efficiency during interactions with these structs. 

In the context of EVM, a well-structured and optimized struct can save a substantial amount of gas. For instance, packing the struct into fewer storage slots could avoid an extra SSTORE operation (costing 20000 gas) during the first setting of the struct. Subsequent read and write operations also experience reduced gas consumption due to optimized struct layout.

Please consider rearranging the fields in the identified structs to capitalize on these potential gas savings and improve overall contract performance.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

/// @audit - Packed struct used 10 storage slots, but can be packed to 9 storage slots.
//	struct ProposedUpgrade {
//	    uint256 newProtocolVersion;
//	    bytes postUpgradeCalldata;
//	    bytes l1ContractsUpgradeCalldata;
//	    VerifierParams verifierParams;
//	    bytes32 defaultAccountHash;
//	    bytes32 bootloaderHash;
//	    bytes[] factoryDeps;
//	    L2CanonicalTransaction l2ProtocolUpgradeTx;
//	    address verifier;
//	    uint32 upgradeTimestamp;
//	}
28: struct ProposedUpgrade {
    L2CanonicalTransaction l2ProtocolUpgradeTx;
    bytes[] factoryDeps;
    bytes32 bootloaderHash;
    bytes32 defaultAccountHash;
    address verifier;
    VerifierParams verifierParams;
    bytes l1ContractsUpgradeCalldata;
    bytes postUpgradeCalldata;
    uint256 upgradeTimestamp;
    uint256 newProtocolVersion;
}
```
[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L28)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

/// @audit - Packed struct used 7 storage slots, but can be packed to 6 storage slots.
//	struct StoredBatchInfo {
//	    bytes32 commitment;
//	    bytes32 l2LogsTreeRoot;
//	    bytes32 priorityOperationsHash;
//	    uint256 numberOfLayer1Txs;
//	    bytes32 batchHash;
//	    uint64 indexRepeatedStorageChanges;
//	    uint64 batchNumber;
//	    uint32 timestamp;
//	}
83: struct StoredBatchInfo {
        uint64 batchNumber;
        bytes32 batchHash;
        uint64 indexRepeatedStorageChanges;
        uint256 numberOfLayer1Txs;
        bytes32 priorityOperationsHash;
        bytes32 l2LogsTreeRoot;
        uint256 timestamp;
        bytes32 commitment;
    }
```
[83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L83)
</details>

### [G-05] A `memory` array's `length` should not be looked up in every iteration of a `for`/`while`-loop

It is more efficient to cache the array length instead of looking it up in every iteration of a for-loop.

Example:

```solidity
- for(uint i = 0; i < array.length; i++)
+ uint length = array.length;
+ for(uint i = 0; i < length; i++);
```

<details>
<summary><i>11 issue instances in 5 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

225: for (uint256 i = 0; i < _calls.length; ++i) {
```
[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L225)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
135: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
185: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
209: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```
[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116) | [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135) | [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185) | [209](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

142: for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
257: for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
289: for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
636: for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {
```
[142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142) | [257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257) | [289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289) | [636](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226: for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226)

```solidity
File: code/system-contracts/contracts/Compressor.sol

61: for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
```
[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L61)
</details>

### [G-06] Avoid Comparisons of Boolean Expressions to Boolean Literals

Direct comparisons of boolean expressions to boolean literals (true or false) can lead to unnecessary gas costs. 
Instead, use the boolean expression directly or its negation in conditional statements for better gas efficiency.

For instance, replace `if (<x> == true)` with `if (<x>)` and `if (<x> == false)` with `if (!<x>)`.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

68: require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
```
[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68)
</details>

### [G-07] `do`-`while` is cheaper than `for`-loops when the initial check can be skipped

Using `do-while` loops instead of `for` loops can be more gas-efficient. 
Even if you add an `if` condition to account for the case where the loop doesn't execute at all, a `do-while` loop can still be cheaper in terms of gas.

Example:
```solidity
/// 774 gas cost
function forLoop() public pure {
    for (uint256 i; i < 10;) {
        unchecked {
            ++i;
        }
    }
}
/// 519 gas cost
function doWhileLoop() public pure {
    uint256 i;
    do {
        unchecked {
            ++i;
        }
    } while (i < 10);
}
```

<details>
<summary><i>35 issue instances in 14 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

225: for (uint256 i = 0; i < _calls.length; ++i)
```
[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L225)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116: for (uint256 i = 0; i < _newBatchesData.length; ++i)
135: for (uint256 i = 0; i < _newBatchesData.length; ++i)
185: for (uint256 i = 0; i < _newBatchesData.length; ++i)
209: for (uint256 i = 0; i < _newBatchesData.length; ++i)
```
[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116) | [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135) | [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185) | [209](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

142: for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE))
257: for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc())
289: for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc())
311: for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc())
351: for (uint256 i = 0; i < nBatches; i = i.uncheckedInc())
405: for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc())
580: for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++)
636: for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE)
667: for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++)
```
[142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142) | [257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257) | [289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289) | [311](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L311) | [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351) | [405](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L405) | [580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580) | [636](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636) | [667](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

208: for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc())
```
[208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

356: for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc())
```
[356](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226: for (uint256 i = 0; i < _factoryDeps.length; ++i)
```
[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

101: for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc())
138: for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc())
158: for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc())
178: for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc())
```
[101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L138) | [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158) | [178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L178)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

29: for (uint256 i; i < pathLength; i = i.uncheckedInc())
```
[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L29)

```solidity
File: code/system-contracts/contracts/Compressor.sol

61: for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2)
127: for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE)
159: for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE)
```
[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L61) | [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L127) | [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L159)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

248: for (uint256 i = 0; i < deploymentsLength; ++i)
253: for (uint256 i = 0; i < deploymentsLength; ++i)
```
[248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L248) | [253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L253)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

38: for (uint256 i = 0; i < immutablesLength; ++i)
```
[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L38)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

30: for (uint256 i = 0; i < hashesLen; ++i)
```
[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L30)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

206: for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i)
218: for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i)
224: for (uint256 i = 0; i < nodesOnCurrentLevel; ++i)
236: for (uint256 i = 0; i < numberOfMessages; ++i)
254: for (uint256 i = 0; i < numberOfBytecodes; ++i)
```
[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206) | [218](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L218) | [224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L224) | [236](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L236) | [254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L254)

```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

36: for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++)
```
[36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)
</details>

### [G-08] Use `assembly` for Efficient Event Emission

To efficiently emit events, consider utilizing assembly by making use of scratch space and the free memory pointer.
This approach can potentially avoid the costs associated with memory expansion.

However, it's crucial to cache and restore the free memory pointer for safe optimization.
Good examples of such practices can be found in well-optimized [Solady's codebases](https://github.com/Vectorized/solady/blob/main/src/tokens/ERC1155.sol#L167).
Please review your code and consider the potential gas savings of this approach.

<details>
<summary><i>80 issue instances in 20 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

155: emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount)
199: emit ClaimedFailedDeposit(_depositSender, _l1Token, amount)
225: emit WithdrawalFinalized(l1Receiver, l1Token, amount)
```
[155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L155) | [199](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L199) | [225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L225)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

155: emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount)
199: emit ClaimedFailedDeposit(_depositSender, _l1Token, amount)
225: emit WithdrawalFinalized(l1Receiver, l1Token, amount)
```
[155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L155) | [199](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L199) | [225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L225)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

168: emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount)
227: emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount)
239: emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash)
367: emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount)
454: emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount)
602: emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount)
```
[168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L168) | [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L227) | [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L239) | [367](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L367) | [454](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L454) | [602](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L602)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

56: emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin)
68: emit NewPendingAdmin(currentPendingAdmin, address(0))
69: emit NewAdmin(previousAdmin, pendingAdmin)
145: emit NewChain(_chainId, _stateTransitionManager, _admin)
```
[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L56) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68) | [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69) | [145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L145)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

47: emit ChangeSecurityCouncil(address(0), _securityCouncil)
50: emit ChangeMinDelay(0, _minDelay)
132: emit TransparentOperationScheduled(id, _delay, _operation)
144: emit ShadowOperationScheduled(_id, _delay)
157: emit OperationCancelled(_id)
180: emit OperationExecuted(id)
199: emit OperationExecuted(id)
250: emit ChangeMinDelay(minDelay, _newDelay)
257: emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil)
```
[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L47) | [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L50) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L132) | [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L144) | [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L157) | [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L180) | [199](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L199) | [250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L250) | [257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L257)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

115: emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin)
127: emit NewPendingAdmin(currentPendingAdmin, address(0))
128: emit NewAdmin(previousAdmin, pendingAdmin)
227: emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion)
235: emit StateTransitionNewChain(_chainId, _stateTransitionContract)
287: emit StateTransitionNewChain(_chainId, stateTransitionAddress)
```
[115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L115) | [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L127) | [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L128) | [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227) | [235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L235) | [287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L287)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

83: emit ValidatorAdded(_chainId, _newValidator)
92: emit ValidatorRemoved(_chainId, _validator)
98: emit NewExecutionDelay(_executionDelay)
```
[83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L83) | [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L92) | [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

28: emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin)
40: emit NewPendingAdmin(pendingAdmin, address(0))
41: emit NewAdmin(previousAdmin, pendingAdmin)
47: emit ValidatorStatusUpdate(_validator, _active)
54: emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable)
63: emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit)
75: emit NewFeeParams(oldFeeParams, _newFeeParams)
86: emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator)
92: emit ValidiumModeStatusUpdate(_validiumMode)
115: emit ExecuteUpgrade(_diamondCut)
125: emit ExecuteUpgrade(_diamondCut)
139: emit Freeze()
149: emit Unfreeze()
```
[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L28) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L41) | [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L47) | [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L54) | [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L63) | [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L75) | [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L86) | [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92) | [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L115) | [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L125) | [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L139) | [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L149)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

261: emit BlockCommit(
                _lastCommittedBatchData.batchNumber,
                _lastCommittedBatchData.batchHash,
                _lastCommittedBatchData.commitment
            )
299: emit BlockCommit(
                _lastCommittedBatchData.batchNumber,
                _lastCommittedBatchData.batchHash,
                _lastCommittedBatchData.commitment
            )
353: emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment)
436: emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified)
496: emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted)
```
[261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261) | [299](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L299) | [353](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353) | [436](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436) | [496](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

343: emit NewPriorityRequest(
            _priorityOpParams.txId,
            canonicalTxHash,
            _priorityOpParams.expirationTimestamp,
            transaction,
            _factoryDeps
        )
```
[343](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L343)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

87: emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade)
104: emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash)
121: emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash)
137: emit NewVerifier(address(oldVerifier), address(_newVerifier))
157: emit NewVerifierParams(oldVerifierParams, _newVerifierParams)
256: emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion)
```
[87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L87) | [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L104) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L121) | [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L137) | [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L157) | [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L256)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

40: emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion)
67: emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade)
```
[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L40) | [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L67)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

121: emit DiamondCut(facetCuts, initAddress, initCalldata)
```
[121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L121)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

68: emit AccountVersionUpdated(msg.sender, _version)
86: emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering)
355: emit ContractDeployed(_sender, _bytecodeHash, _newAddress)
```
[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L68) | [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L86) | [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L355)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

59: emit MarkedAsKnown(_bytecodeHash, _shouldSendToL1)
```
[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L59)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

111: emit L2ToL1LogSent(_l2ToL1Log)
156: emit L1MessageSent(msg.sender, hash, _message)
181: emit BytecodeL1PublicationRequested(_bytecodeHash)
```
[111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L111) | [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L156) | [181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L181)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

49: emit Transfer(_from, _to, _amount)
67: emit Mint(_account, _amount)
79: emit Withdrawal(msg.sender, _l1Receiver, amount)
92: emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData)
```
[49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L49) | [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L67) | [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L79) | [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L92)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

96: emit ValueSetUnderNonce(msg.sender, _key, _value)
```
[96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L96)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

105: emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount)
134: emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount)
```
[105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L105) | [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L134)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

101: emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_)
126: emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_)
147: emit BridgeMint(_to, _amount)
156: emit BridgeBurn(_from, _amount)
```
[101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L101) | [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126) | [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L147) | [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L156)
</details>

### [G-09] Use custom errors rather than `require()/assert()/revert(with msg)` with string to save gas

Custom errors are available from solidity version 0.8.4.
Custom errors save [~50](https://gist.github.com/IllIllI000/ad1bd0d29a0101b25e57c293b4b0c746) gas each time they're hit by [avoiding having to allocate and store the revert string](https://soliditylang.org/blog/2021/04/21/custom-errors/#errors-in-depth).
Alse Custom error are cheaper than `assert()`.
```solidity
    revert CustomError(); // 157 gas
    assert(false); // 164 gas
    revert("Custom Error"); // 406 gas
    require(false, "Custom Error"); // 421 gas
```


<details>
<summary><i>350 issue instances in 46 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

64: require(msg.sender == address(sharedBridge), "Not shared bridge")
66: require(amount == _amount, "Incorrect amount")
141: require(_amount != 0, "0T")
143: require(amount == _amount, "3T")
186: require(amount != 0, "2T")
215: require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw")
```
[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L66) | [141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141) | [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L143) | [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186) | [215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L215)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

64: require(msg.sender == address(sharedBridge), "Not shared bridge")
66: require(amount == _amount, "Incorrect amount")
141: require(_amount != 0, "0T")
143: require(amount == _amount, "3T")
186: require(amount != 0, "2T")
215: require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw")
```
[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L66) | [141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141) | [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L143) | [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186) | [215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L215)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

69: require(msg.sender == address(bridgehub), "ShB not BH")
75: require(
            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
            "L1SharedBridge: not bridgehub or era chain"
        )
84: require(msg.sender == address(legacyBridge), "ShB not legacy bridge")
108: require(_owner != address(0), "ShB owner 0")
121: require(balanceAfter > balanceBefore, "ShB: 0 eth transferred")
129: require(amount > 0, "ShB: 0 amount to transfer")
132: require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred")
138: require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition")
155: require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount")
158: require(msg.value == 0, "ShB m.v > 0 b d.it")
161: require(amount == _amount, "3T")
188: require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed")
194: require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported")
195: require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported")
200: require(_depositAmount == 0, "ShB wrong withdraw amount")
202: require(msg.value == 0, "ShB m.v > 0 for BH d.it 2")
206: require(withdrawAmount == _depositAmount, "5T")
208: require(amount != 0, "6T")
237: require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap")
325: require(proofValid, "yn")
327: require(_amount > 0, "y1")
342: require(dataHash == txDataHash, "ShB: d.it not hap")
349: require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds")
360: require(callSuccess, "ShB: claimFailedDeposit failed")
396: require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal")
417: require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized")
427: require(!alreadyFinalized, "Withdrawal is already finalized 2")
439: require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2")
449: require(callSuccess, "ShB: withdraw failed")
484: require(success, "ShB withd w proof")
501: require(_l2ToL1message.length >= 56, "ShB wrong msg len")
517: require(_l2ToL1message.length == 76, "ShB wrong msg len 2")
563: require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep")
564: require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2")
522: revert("ShB Incorrect message function selector")
```
[69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69) | [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75) | [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L84) | [108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L108) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L121) | [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138) | [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L155) | [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L158) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L161) | [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188) | [194](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L194) | [195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195) | [200](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L200) | [202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202) | [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L206) | [208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L208) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L237) | [325](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L325) | [327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327) | [342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L342) | [349](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L349) | [360](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L360) | [396](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L396) | [417](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L417) | [427](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L427) | [439](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L439) | [449](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L449) | [484](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L484) | [501](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L501) | [517](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L517) | [563](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563) | [564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564) | [522](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L522)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

46: require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin")
62: require(msg.sender == currentPendingAdmin, "n42")
83: require(
            !stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition already registered"
        )
93: require(
            stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition not registered yet"
        )
102: require(!tokenIsRegistered[_token], "Bridgehub: token already registered")
122: require(_chainId != 0, "Bridgehub: chainId cannot be 0")
123: require(_chainId <= type(uint48).max, "Bridgehub: chainId too large")
125: require(
            stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition not registered"
        )
129: require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered")
130: require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set")
132: require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered")
223: require(msg.value == _request.mintValue, "Bridgehub: msg.value mismatch 1")
225: require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value")
269: require(
                    msg.value == _request.mintValue + _request.secondBridgeValue,
                    "Bridgehub: msg.value mismatch 2"
                )
275: require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3")
296: require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch")
300: require(
            _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
            "Bridgehub: second bridge address too low"
        )
```
[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62) | [83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83) | [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L93) | [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102) | [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L122) | [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123) | [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L125) | [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L129) | [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132) | [223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L223) | [225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225) | [269](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L269) | [275](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L275) | [296](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L296) | [300](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L300)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

42: require(_admin != address(0), "Admin should be non zero address")
59: require(msg.sender == address(this), "Only governance contract itself is allowed to call this function")
65: require(msg.sender == securityCouncil, "Only security council is allowed to call this function")
71: require(
            msg.sender == owner() || msg.sender == securityCouncil,
            "Only the owner and security council are allowed to call this function"
        )
155: require(isOperationPending(_id), "Operation must be pending")
172: require(isOperationReady(id), "Operation must be ready before execution")
177: require(isOperationReady(id), "Operation must be ready after execution")
191: require(isOperationPending(id), "Operation must be pending before execution")
196: require(isOperationPending(id), "Operation must be pending after execution")
216: require(!isOperation(_id), "Operation with this proposal id already exists")
217: require(_delay >= minDelay, "Proposed delay is less than minimum delay")
240: require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed")
```
[42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L42) | [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59) | [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L65) | [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L71) | [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L155) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L172) | [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L177) | [191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L191) | [196](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L196) | [216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L216) | [217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L217) | [240](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L240)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

64: require(msg.sender == bridgehub, "StateTransition: only bridgehub")
70: require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin")
82: require(_initializeData.governor != address(0), "StateTransition: governor zero")
106: assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32)
121: require(msg.sender == currentPendingAdmin, "n42")
256: require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch")
```
[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64) | [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L70) | [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L82) | [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L106) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L121) | [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L256)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62: require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin")
68: require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator")
195: require(block.timestamp >= commitBatchTimestamp + delay, "5c")
217: require(block.timestamp >= commitBatchTimestamp + delay, "5c")
```
[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68) | [195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195) | [217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L217)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

25: require(address(_initializeData.verifier) != address(0), "vt")
26: require(_initializeData.admin != address(0), "vy")
27: require(_initializeData.validatorTimelock != address(0), "hc")
28: require(_initializeData.priorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "vu")
51: assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32)
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L26) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27) | [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L28) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L51)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

14: require(_chainId == block.chainid, "pr")
25: require(msg.data.length >= 4 || msg.data.length == 0, "Ut")
30: require(facetAddress != address(0), "F")
31: require(!diamondStorage.isFrozen || !facet.isFreezable, "q1")
```
[14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L14) | [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25) | [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30) | [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L31)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

34: require(msg.sender == pendingAdmin, "n4")
59: require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5")
70: require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6")
90: require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis")
105: require(
            cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
            "StateTransition: cutHash mismatch"
        )
110: require(
            s.protocolVersion == _oldProtocolVersion,
            "StateTransition: protocolVersion mismatch in STC when upgrading"
        )
116: require(
            s.protocolVersion > _oldProtocolVersion,
            "StateTransition: protocolVersion mismatch in STC after upgrading"
        )
136: require(!diamondStorage.isFrozen, "a9")
146: require(diamondStorage.isFrozen, "a7")
```
[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34) | [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L59) | [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L70) | [90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90) | [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L105) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L110) | [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L116) | [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L136) | [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L146)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

37: require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f")
40: require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us")
50: require(logOutput.pubdataHash == 0x00, "v0h")
51: require(_newBatch.pubdataCommitments.length == 1)
61: require(
                logOutput.pubdataHash ==
                    keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),
                "wp"
            )
74: require(_previousBatch.batchHash == logOutput.previousBatchHash, "l")
76: require(logOutput.chainedPriorityTxsHash == _newBatch.priorityOperationsHash, "t")
78: require(logOutput.numberOfLayer1Txs == _newBatch.numberOfLayer1Txs, "ta")
110: require(batchTimestamp == _expectedBatchTimestamp, "tb")
114: require(_previousBatchTimestamp < batchTimestamp, "h3")
122: require(block.timestamp - COMMIT_TIMESTAMP_NOT_OLDER <= batchTimestamp, "h1")
123: require(lastL2BlockTimestamp <= block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA, "h2")
149: require(!_checkBit(processedLogs, uint8(logKey)), "kp")
154: require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm")
157: require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln")
160: require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb")
163: require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc")
166: require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv")
169: require(logSender == L2_BOOTLOADER_ADDRESS, "bl")
172: require(logSender == L2_BOOTLOADER_ADDRESS, "bk")
175: require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc")
178: require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd")
181: require(logSender == L2_BOOTLOADER_ADDRESS, "bu")
182: require(_expectedSystemContractUpgradeTxHash == logValue, "ut")
192: require(processedLogs == 511, "b7")
194: require(processedLogs == 1023, "b8")
226: require(
            IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
            "Executor facet: wrong protocol version"
        )
231: require(_newBatchesData.length == 1, "e4")
233: require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i")
284: require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik")
323: require(currentBatchNumber == s.totalBatchesExecuted + _executedBatchIdx + 1, "k")
324: require(
            _hashStoredBatchInfo(_storedBatch) == s.storedBatchHashes[currentBatchNumber],
            "exe10" // executing batch should be committed
        )
330: require(priorityOperationsHash == _storedBatch.priorityOperationsHash, "x")
358: require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n")
402: require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1")
407: require(
                _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
                "o1"
            )
421: require(currentTotalBatchesVerified <= s.totalBatchesCommitted, "q")
426: assert(block.chainid != 1)
442: require(proofPublicInput.length == 1, "t4")
449: require(successVerifyProof, "p")
482: require(s.totalBatchesCommitted > _newLastBatch, "v1")
483: require(_newLastBatch >= s.totalBatchesExecuted, "v2")
543: require(_batch.systemLogs.length <= MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES, "pu")
567: require(_blobCommitments.length == MAX_NUMBER_OF_BLOBS, "b10")
568: require(_blobHashes.length == MAX_NUMBER_OF_BLOBS, "b11")
616: require(success, "failed to call point evaluation precompile")
618: require(result == BLS_MODULUS, "precompile unexpected output")
631: require(_pubdataCommitments.length > 0, "pl")
632: require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd")
633: require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs")
639: require(blobVersionedHash != bytes32(0), "vh")
663: require(versionedHash == bytes32(0), "lh")
668: require(
                (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
                    (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
                "bh"
            )
681: require(success, "vc")
184: revert("ul")
```
[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L37) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L40) | [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L50) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L51) | [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L61) | [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L74) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L76) | [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L78) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L110) | [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L114) | [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L122) | [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L123) | [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L149) | [154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L154) | [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L157) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L160) | [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L163) | [166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L166) | [169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L169) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L172) | [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L175) | [178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L178) | [181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L181) | [182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L182) | [192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L192) | [194](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L194) | [226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L226) | [231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L231) | [233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L233) | [284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L284) | [323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L323) | [324](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L324) | [330](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L330) | [358](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L358) | [402](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L402) | [407](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L407) | [421](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L421) | [426](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L426) | [442](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L442) | [449](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L449) | [482](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L482) | [483](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L483) | [543](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L543) | [567](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L567) | [568](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L568) | [616](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616) | [618](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L618) | [631](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631) | [632](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L632) | [633](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L633) | [639](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L639) | [663](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L663) | [668](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L668) | [681](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L681) | [184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L184)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

183: require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2")
```
[183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

39: require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox")
110: require(_batchNumber <= s.totalBatchesExecuted, "xx")
117: require(hashedLog != L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH, "tw")
158: require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set")
185: require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox")
206: require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token")
243: require(_request.l2GasPerPubdataByteLimit == REQUIRED_L2_GAS_PRICE_PER_PUBDATA, "qp")
264: require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj")
272: require(_mintValue >= baseCost + _params.l2Value, "mv")
```
[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L110) | [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L117) | [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158) | [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L185) | [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L206) | [243](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L243) | [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L264) | [272](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L272)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

16: require(msg.sender == s.admin, "StateTransition Chain: not admin")
22: require(s.validators[msg.sender], "StateTransition Chain: not validator")
27: require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager")
32: require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub")
37: require(
            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by admin or state transition manager"
        )
45: require(
            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by validator or state transition manager"
        )
53: require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function")
```
[16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16) | [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27) | [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L37) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45) | [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

72: require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet")
190: require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong")
205: require(
            _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
            "The new protocol version should be included in the L2 system upgrade tx"
        )
223: require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps")
224: require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32")
227: require(
                L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
                "Wrong factory dep hash"
            )
238: require(
            _newProtocolVersion > previousProtocolVersion,
            "New protocol version is not greater than the current one"
        )
242: require(
            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
            "Too big protocol version difference"
        )
249: require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized")
250: require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        )
```
[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L72) | [190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L190) | [205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L205) | [223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L223) | [224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L224) | [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L227) | [238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L238) | [242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L242) | [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L249) | [250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L250)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

22: require(
            // Genesis Upgrade difference: Note this is the only thing change > to >=
            _newProtocolVersion >= previousProtocolVersion,
            "New protocol version is not greater than the current one"
        )
27: require(
            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
            "Too big protocol version difference"
        )
33: require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized")
34: require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        )
52: require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet")
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L27) | [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33) | [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L34) | [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L52)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

23: require(_bytecode.length % 32 == 0, "pq")
26: require(bytecodeLenInWords < 2 ** 16, "pp")
27: require(bytecodeLenInWords % 2 == 1, "ps")
41: require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf")
43: require(bytecodeLen(_bytecodeHash) % 2 == 1, "uy")
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L26) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L27) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L41) | [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

107: require(selectors.length > 0, "B")
132: require(_facet.code.length > 0, "G")
141: require(oldFacet.facetAddress == address(0), "J")
155: require(_facet.code.length > 0, "K")
161: require(oldFacet.facetAddress != address(0), "L")
175: require(_facet == address(0), "a1")
181: require(oldFacet.facetAddress != address(0), "a2")
215: require(_isSelectorFreezable == ds.selectorToFacet[selector0].isFreezable, "J1")
280: require(_calldata.length == 0, "H")
297: require(data.length == 32, "lp")
298: require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1")
116: revert("C")
287: revert("I")
```
[107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132) | [141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L141) | [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L155) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L161) | [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175) | [181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L181) | [215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L215) | [280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L280) | [297](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L297) | [298](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L298) | [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L116) | [287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L287)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

24: require(pathLength > 0, "xc")
25: require(pathLength < 256, "bt")
26: require(_index < (1 << pathLength), "px")
```
[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24) | [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L25) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L26)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

65: require(!_queue.isEmpty(), "D")
73: require(!_queue.isEmpty(), "s")
```
[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L65) | [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L73)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

28: require(l2GasForTxBody <= _priorityTxMaxGasLimit, "ui")
30: require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk")
34: require(
            getMinimalPriorityTransactionGasLimit(
                _encoded.length,
                _transaction.factoryDeps.length,
                _transaction.gasPerPubdataByteLimit
            ) <= l2GasForTxBody,
            "up"
        )
48: require(_transaction.from <= type(uint16).max, "ua")
49: require(_transaction.to <= type(uint160).max, "ub")
50: require(_transaction.paymaster == 0, "uc")
51: require(_transaction.value == 0, "ud")
52: require(_transaction.maxFeePerGas == 0, "uq")
53: require(_transaction.maxPriorityFeePerGas == 0, "ux")
54: require(_transaction.reserved[0] == 0, "ue")
55: require(_transaction.reserved[1] <= type(uint160).max, "uf")
56: require(_transaction.reserved[2] == 0, "ug")
57: require(_transaction.reserved[3] == 0, "uo")
58: require(_transaction.signature.length == 0, "uh")
59: require(_transaction.paymasterInput.length == 0, "ul1")
60: require(_transaction.reservedDynamic.length == 0, "um")
115: require(_totalGasLimit >= overhead, "my")
```
[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L28) | [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L30) | [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L34) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L48) | [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L49) | [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L50) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L51) | [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L52) | [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L53) | [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L54) | [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L56) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L57) | [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L58) | [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L59) | [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L60) | [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L115)

```solidity
File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

58: require(lockSlotOldValue == 0, "1B")
75: require(_status == _NOT_ENTERED, "r1")
```
[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L58) | [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L75)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

26: require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract")
37: require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor")
48: require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract")
57: require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor")
```
[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L26) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L37) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L48) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L57)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

92: require(vInt == 27 || vInt == 28, "Invalid v value")
191: require(vInt == 27 || vInt == 28, "Invalid v value")
286: require(vInt == 27 || vInt == 28, "Invalid v value")
37: revert("Unsupported tx type")
```
[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L92) | [191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L191) | [286](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L286) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L37)

```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

22: require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER")
24: require(_delegateTo.code.length > 0, "Delegatee is an EOA")
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22) | [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L24)

```solidity
File: code/system-contracts/contracts/Compressor.sol

51: require(
                encodedData.length * 4 == _bytecode.length,
                "Encoded data length should be 4 times shorter than the original bytecode"
            )
56: require(
                dictionary.length / 8 <= encodedData.length / 2,
                "Dictionary should have at most the same number of entries as the encoded data"
            )
63: require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds")
68: require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode")
119: require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large")
140: require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch")
156: require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs")
171: require(enumIndex == compressedEnumIndex, "rw: enum key mismatch")
187: require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs")
230: require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch")
232: require(
                    _initialValue + convertedValue == _finalValue,
                    "add: initial plus converted not equal to final"
                )
237: require(
                    _initialValue - convertedValue == _finalValue,
                    "sub: initial minus converted not equal to final"
                )
242: revert("unsupported operation")
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L51) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L56) | [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L63) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L68) | [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L119) | [140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L140) | [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L156) | [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L171) | [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L187) | [230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L230) | [232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L232) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L237) | [242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L242)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

29: require(msg.sender == address(this), "Callable only by self")
77: require(
            _nonceOrdering == AccountNonceOrdering.Arbitrary &&
                currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
            "It is only possible to change from sequential to arbitrary ordering"
        )
239: require(
            msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
            "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
        )
251: require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments")
264: require(_bytecodeHash != bytes32(0x0), "BytecodeHash cannot be zero")
265: require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space")
268: require(
            ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0,
            "Code hash is non-zero"
        )
273: require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied")
303: require(knownCodeMarker > 0, "The code hash is not known")
350: require(value == 0, "The value must be zero if we do not call the constructor")
```
[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29) | [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L77) | [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L239) | [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L251) | [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L264) | [265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L265) | [268](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L268) | [273](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L273) | [303](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L303) | [350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L350)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

100: require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value")
160: require(_signature.length == 65, "Signature length is incorrect")
173: require(v == 27 || v == 28, "v is neither 27 nor 28")
184: require(uint256(s) <= 0x7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF5D576E7357A4501DDFE92F46681B20A0, "Invalid s")
202: require(success, "Failed to pay the fee to the operator")
222: assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS)
```
[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L160) | [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L173) | [184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L184) | [202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L202) | [222](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L222)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

35: require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract")
```
[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

20: require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor")
76: require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash")
78: require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd")
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L20) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L76) | [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L78)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

201: require(numberOfL2ToL1Logs <= L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, "Too many L2->L1 logs")
214: require(
            reconstructedChainedLogsHash == chainedLogsHash,
            "reconstructedChainedLogsHash is not equal to chainedLogsHash"
        )
245: require(
            reconstructedChainedMessagesHash == chainedMessagesHash,
            "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
        )
269: require(
            reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
            "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
        )
279: require(
            uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
                STATE_DIFF_COMPRESSION_VERSION_NUMBER,
            "state diff compression version mismatch"
        )
298: require(calldataPtr <= MAX_ALLOWED_PUBDATA_PER_BATCH, "L1 Messenger pubdata is too long")
315: require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array")
```
[201](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L201) | [214](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L214) | [245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L245) | [269](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L269) | [279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L279) | [298](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L298) | [315](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L315)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

33: require(
            msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
                msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
                msg.sender == BOOTLOADER_FORMAL_ADDRESS,
            "Only system contracts with special access can call this method"
        )
41: require(fromBalance >= _amount, "Transfer amount exceeds balance")
```
[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L33) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L41)

```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

60: require(to != address(this), "MsgValueSimulator calls itself")
```
[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L60)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

66: require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high")
85: require(_value != 0, "Nonce value cannot be set to 0")
89: require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used")
115: require(oldMinNonce == _expectedNonce, "Incorrect nonce")
136: require(
            msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
            "Only the contract deployer can increment the deployment nonce"
        )
170: revert("Reusing the same nonce twice")
172: revert("The nonce was not set as used")
```
[66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L66) | [85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L85) | [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L89) | [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L115) | [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L136) | [170](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L170) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L172)

```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

22: require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs")
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L22)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

242: require(_isFirstInBatch, "Upgrade transaction must be first")
245: require(_l2BlockNumber > 0, "L2 block number is never expected to be zero")
249: require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect")
287: require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block")
351: require(
                _l2BlockTimestamp >= currentBatchTimestamp,
                "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
            )
355: require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch")
367: require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch")
368: require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same")
369: require(
                _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
                "The previous hash of the same L2 block must be same"
            )
373: require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock")
385: require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect")
386: require(
                _l2BlockTimestamp > currentL2BlockTimestamp,
                "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
            )
413: require(currentBatchNumber > 0, "The current batch number must be greater than 0")
429: require(
            _newTimestamp > currentBlockTimestamp,
            "The timestamp of the batch must be greater than the timestamp of the previous block"
        )
451: require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental")
452: require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct")
394: revert("Invalid new L2 block number")
```
[242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L242) | [245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L245) | [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L249) | [287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L287) | [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L351) | [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L355) | [367](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L367) | [368](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L368) | [369](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L369) | [373](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L373) | [385](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L385) | [386](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L386) | [413](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L413) | [429](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L429) | [451](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L451) | [452](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L452) | [394](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L394)

```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

46: require(_maxTotalGas >= gasleft(), "Gas limit is too low")
76: require(pubdataAllowance + gasleft() >= pubdataCost + CALL_RETURN_OVERHEAD, "Not enough gas for pubdata")
```
[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L46) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L76)

```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

38: require(returnData.length == 32, "keccak256 returned invalid data")
47: require(returnData.length == 32, "sha returned invalid data")
```
[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L38) | [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L47)

```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

50: assert(_len != 1)
```
[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L50)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

319: require(index < 10, "There are only 10 accessible registers")
350: require(precompileCallSuccess, "Failed to charge gas")
```
[319](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319) | [350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L350)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

363: require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long")
367: require(
                _transaction.paymasterInput.length >= 68,
                "The approvalBased paymaster input must be at least 68 bytes long"
            )
112: revert("Encoding unsupported tx")
388: revert("Unsupported paymaster flow")
```
[363](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L363) | [367](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L367) | [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L112) | [388](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L388)

```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

21: require(_x <= type(uint128).max, "Overflow")
27: require(_x <= type(uint32).max, "Overflow")
33: require(_x <= type(uint24).max, "Overflow")
84: require(_bytecode.length % 32 == 0, "po")
87: require(lengthInWords < 2 ** 16, "pp")
88: require(lengthInWords % 2 == 1, "pr")
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L21) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L27) | [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L33) | [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L84) | [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L87) | [88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L88)

```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

21: require(
            SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
            "This method require system call flag"
        )
31: require(
            SystemContractHelper.isSystemContract(msg.sender),
            "This method require the caller to be system contract"
        )
41: require(msg.sender == caller, "Inappropriate caller")
48: require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader")
55: require(msg.sender == FORCE_DEPLOYER)
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L21) | [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L31) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L41) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L48) | [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L55)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

55: require(_l1Bridge != address(0), "bf")
56: require(_l2TokenProxyBytecodeHash != bytes32(0), "df")
57: require(_aliasedOwner != address(0), "sf")
58: require(_l2TokenProxyBytecodeHash != bytes32(0), "df")
68: require(_l1LegecyBridge != address(0), "bf2")
87: require(
            AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
                AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
            "mq"
        )
92: require(msg.value == 0, "Value should be 0 for ERC20 bridge")
98: require(deployedToken == expectedL2Token, "mt")
101: require(currentL1Token == _l1Token, "gg")
124: require(_amount > 0, "Amount cannot be zero")
129: require(l1Token != address(0), "yh")
176: require(success, "mk")
```
[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L55) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L56) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L57) | [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L58) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L68) | [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L87) | [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92) | [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L98) | [101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L101) | [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L124) | [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L129) | [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L176)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

51: require(_l1Address != address(0), "in6")
120: require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt")
130: require(msg.sender == l2Bridge, "xnt")
137: require(_version == _getInitializedVersion() + 1, "v")
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51) | [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120) | [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L130) | [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L137)

```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

28: require(_x <= type(uint32).max, "Overflow")
```
[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L28)
</details>

### [G-10] Avoid Emitting Events Inside Loops

Emitting an event inside a loop performs a LOG operation N times, where N is the loop length.
Consider refactoring the code to emit the event only once at the end of the loop.
Gas savings should be multiplied by the average loop length.
This approach can improve the gas efficiency of your contract and make transaction costs more predictable for users.

<details>
<summary><i>3 issue instances in 1 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

261: emit BlockCommit(
                _lastCommittedBatchData.batchNumber,
                _lastCommittedBatchData.batchHash,
                _lastCommittedBatchData.commitment
            )
299: emit BlockCommit(
                _lastCommittedBatchData.batchNumber,
                _lastCommittedBatchData.batchHash,
                _lastCommittedBatchData.commitment
            )
353: emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment)
```
[261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261) | [299](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L299) | [353](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353)
</details>

### [G-11] Enable IR-based code generation

The `--via-ir` command line option activates the IR-based code generator in Solidity, which is designed to enable powerful optimization passes that can span across functions. The end result may be a contract that requires less gas to execute its functions.

We recommend you enable this feature, run tests, and benchmark the gas usage of your contract to evaluate if it leads to any tangible gas savings. Experimenting with this feature could lead to a more gas-efficient contract.

[Solidity Documentation](https://docs.soliditylang.org/en/v0.8.20/ir-breaking-changes.html#solidity-ir-based-codegen-changes).

<details>
<summary><i>106 issue instances in 1 files:</i></summary>

```solidity

File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol
File: code/contracts/ethereum/contracts/governance/Governance.sol
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol
File: code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol
File: code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol
File: code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol
File: code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol
File: code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol
File: code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol
File: code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol
File: code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol
File: code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol
File: code/contracts/ethereum/contracts/governance/IGovernance.sol
File: code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol
File: code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol
File: code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol
File: code/contracts/ethereum/contracts/common/Config.sol
File: code/contracts/ethereum/contracts/common/L2ContractAddresses.sol
File: code/contracts/ethereum/contracts/common/Messaging.sol
File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol
File: code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol
File: code/system-contracts/contracts/AccountCodeStorage.sol
File: code/system-contracts/contracts/BootloaderUtilities.sol
File: code/system-contracts/contracts/ComplexUpgrader.sol
File: code/system-contracts/contracts/Compressor.sol
File: code/system-contracts/contracts/Constants.sol
File: code/system-contracts/contracts/ContractDeployer.sol
File: code/system-contracts/contracts/DefaultAccount.sol
File: code/system-contracts/contracts/EmptyContract.sol
File: code/system-contracts/contracts/ImmutableSimulator.sol
File: code/system-contracts/contracts/KnownCodesStorage.sol
File: code/system-contracts/contracts/L1Messenger.sol
File: code/system-contracts/contracts/L2BaseToken.sol
File: code/system-contracts/contracts/MsgValueSimulator.sol
File: code/system-contracts/contracts/NonceHolder.sol
File: code/system-contracts/contracts/PubdataChunkPublisher.sol
File: code/system-contracts/contracts/SystemContext.sol
File: code/system-contracts/contracts/GasBoundCaller.sol
File: code/system-contracts/contracts/libraries/EfficientCall.sol
File: code/system-contracts/contracts/libraries/RLPEncoder.sol
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol
File: code/system-contracts/contracts/libraries/TransactionHelper.sol
File: code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol
File: code/system-contracts/contracts/libraries/Utils.sol
File: code/system-contracts/contracts/interfaces/IAccount.sol
File: code/system-contracts/contracts/interfaces/IAccountCodeStorage.sol
File: code/system-contracts/contracts/interfaces/IBaseToken.sol
File: code/system-contracts/contracts/interfaces/IBootloaderUtilities.sol
File: code/system-contracts/contracts/interfaces/IComplexUpgrader.sol
File: code/system-contracts/contracts/interfaces/ICompressor.sol
File: code/system-contracts/contracts/interfaces/IContractDeployer.sol
File: code/system-contracts/contracts/interfaces/IImmutableSimulator.sol
File: code/system-contracts/contracts/interfaces/IKnownCodesStorage.sol
File: code/system-contracts/contracts/interfaces/IL1Messenger.sol
File: code/system-contracts/contracts/interfaces/IL2StandardToken.sol
File: code/system-contracts/contracts/interfaces/IMailbox.sol
File: code/system-contracts/contracts/interfaces/INonceHolder.sol
File: code/system-contracts/contracts/interfaces/IPaymaster.sol
File: code/system-contracts/contracts/interfaces/IPaymasterFlow.sol
File: code/system-contracts/contracts/interfaces/IPubdataChunkPublisher.sol
File: code/system-contracts/contracts/interfaces/ISystemContext.sol
File: code/system-contracts/contracts/interfaces/ISystemContextDeprecated.sol
File: code/system-contracts/contracts/interfaces/ISystemContract.sol
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol
File: code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol
File: code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol
File: code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol
File: code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol
File: code/contracts/zksync/contracts/interfaces/IPaymaster.sol
File: code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol
File: code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol
File: code/contracts/zksync/contracts/ForceDeployUpgrader.sol
File: code/contracts/zksync/contracts/L2ContractHelper.sol
File: code/contracts/zksync/contracts/SystemContractsCaller.sol
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/EmptyContract.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IAccount.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IAccountCodeStorage.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IBaseToken.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IBootloaderUtilities.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IComplexUpgrader.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ICompressor.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IContractDeployer.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IImmutableSimulator.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IKnownCodesStorage.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IL1Messenger.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IL2StandardToken.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IMailbox.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/INonceHolder.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IPaymaster.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IPaymasterFlow.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IPubdataChunkPublisher.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContextDeprecated.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L1)
</details>

### [G-12] Assembly: Check `msg.sender` using xor and the scratch space

See [this](https://code4rena.com/reports/2023-05-juicebox#g-06-use-assembly-to-validate-msgsender) prior finding for details on the conversion

<details>
<summary><i>46 issue instances in 19 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

64: require(msg.sender == address(sharedBridge), "Not shared bridge");
```
[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

64: require(msg.sender == address(sharedBridge), "Not shared bridge");
```
[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

69: require(msg.sender == address(bridgehub), "ShB not BH");
76: msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
76: msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
84: require(msg.sender == address(legacyBridge), "ShB not legacy bridge");
138: require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");
```
[69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L76) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L76) | [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L84) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

46: require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");
46: require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");
62: require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights
328: _recipient = msg.sender == tx.origin ? msg.sender : AddressAliasHelper.applyL1ToL2Alias(msg.sender);
```
[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46) | [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62) | [328](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L328)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

59: require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
65: require(msg.sender == securityCouncil, "Only security council is allowed to call this function");
72: msg.sender == owner() || msg.sender == securityCouncil,
72: msg.sender == owner() || msg.sender == securityCouncil,
```
[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59) | [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L65) | [72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L72) | [72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L72)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

64: require(msg.sender == bridgehub, "StateTransition: only bridgehub");
70: require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");
70: require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");
121: require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights
```
[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64) | [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L70) | [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L70) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L121)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62: require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");
```
[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

34: require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights
```
[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

16: require(msg.sender == s.admin, "StateTransition Chain: not admin");
27: require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");
32: require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");
38: msg.sender == s.admin || msg.sender == s.stateTransitionManager,
38: msg.sender == s.admin || msg.sender == s.stateTransitionManager,
46: s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
53: require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
```
[16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27) | [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32) | [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L38) | [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L38) | [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L46) | [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

26: require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L26)

```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

22: require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

29: require(msg.sender == address(this), "Callable only by self");
240: msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
240: msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
```
[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29) | [240](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L240) | [240](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L240)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

29: if (msg.sender != BOOTLOADER_FORMAL_ADDRESS) {
222: assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS);
```
[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L29) | [222](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L222)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

35: require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

20: require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L20)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

34: msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
35: msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
36: msg.sender == BOOTLOADER_FORMAL_ADDRESS,
```
[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L34) | [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L35) | [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L36)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

137: msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
```
[137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L137)

```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

41: require(msg.sender == caller, "Inappropriate caller");
48: require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");
55: require(msg.sender == FORCE_DEPLOYER);
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L41) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L48) | [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L55)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

120: require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");
130: require(msg.sender == l2Bridge, "xnt"); // Only L2 bridge can call this method
```
[120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120) | [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L130)
</details>

### [G-13] Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct`

Combining multiple address/ID mappings into a single mapping to a struct can lead to gas savings.
By refactoring multiple mappings into a singular mapping with a struct, you can save on storage slots, which in turn can reduce the gas cost in certain operations.
Prioritize this refactor if optimizing gas is a primary concern for your contract's operations.

<details>
<summary><i>23 issue instances in 7 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

32: mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
        public depositAmount
45: mapping(address => uint256) private __DEPRECATED_lastWithdrawalLimitReset
48: mapping(address => uint256) private __DEPRECATED_withdrawnAmountInWindow
51: mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser
```
[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L32) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L45) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L48) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L51)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

32: mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
        public depositAmount
45: mapping(address => uint256) private __DEPRECATED_lastWithdrawalLimitReset
48: mapping(address => uint256) private __DEPRECATED_withdrawnAmountInWindow
51: mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser
```
[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L32) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L45) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L48) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L51)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

48: mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress
52: mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
        public
        override depositHappened
57: mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
        public isWithdrawalFinalized
61: mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled
65: mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance
```
[48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L48) | [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L52) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57) | [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L61) | [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L65)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

21: mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered
23: mapping(address _token => bool) public tokenIsRegistered
26: mapping(uint256 _chainId => address) public stateTransitionManager
29: mapping(uint256 _chainId => address) public baseToken
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21) | [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L23) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L26) | [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L29)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

30: mapping(uint256 => address) public stateTransition
48: mapping(uint256 => bytes32) public upgradeCutHash
```
[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L30) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L48)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

47: mapping(uint256 => LibMap.Uint32Map) internal committedBatchTimestamp
50: mapping(uint256 _chainId => mapping(address _validator => bool)) public validators
```
[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L47) | [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

36: mapping(uint256 account => uint256 packedMinAndDeploymentNonce) internal rawNonces
41: mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues
```
[36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L36) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L41)
</details>

### [G-14] Assigning `state` variables directly with struct constructors wastes gas

Utilizing named struct constructors for `state`(only state) variable assignments can lead to inefficient gas usage.
When a struct is initialized with named arguments, the Solidity compiler must first organize these fields in memory, which consumes additional gas.
To optimize gas usage, it is recommended to assign struct fields directly in storage using dot notation.
```solidity
    // stateStruct = TestStruct(20, 20); // 4633 gas
    // stateStruct = TestStruct({ var1: 20, var2: 20 }); // 4633 gas
    // stateStruct.var1 = 20;
    // stateStruct.var2 = 20; // 4562 gas
```

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: code/system-contracts/contracts/SystemContext.sol

316: currentL2BlockInfo = BlockInfo({number: _l2BlockNumber, timestamp: _l2BlockTimestamp})
```
[316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L316)
</details>

### [G-15] Assembly: Use scratch space when building emitted events with two data arguments

Using the scratch space for more than one, but at most two words worth of data (non-indexed arguments) will save gas over needing Solidity's abi memory expansion used for emitting normally.

<details>
<summary><i>3 issue instances in 2 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

83: emit ValidatorAdded(_chainId, _newValidator)
92: emit ValidatorRemoved(_chainId, _validator)
```
[83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L83) | [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L92)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

121: emit DiamondCut(facetCuts, initAddress, initCalldata)
```
[121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L121)
</details>

### [G-16] Stack variable is only used once

If the variable is only accessed once, it's cheaper to use the assigned value directly that one time, and save the 3 gas the extra stack assignment would spend

<details>
<summary><i>285 issue instances in 39 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

/// @audit - `constructorInputHash` variable
76: bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""))
/// @audit - `salt` variable
77: bytes32 salt = bytes32(uint256(uint160(_l1Token)))
/// @audit - `amount` variable
142: uint256 amount = _depositFundsToSharedBridge(msg.sender, IERC20(_l1Token), _amount)
/// @audit - `balanceBefore` variable
161: uint256 balanceBefore = _token.balanceOf(address(sharedBridge))
/// @audit - `balanceAfter` variable
163: uint256 balanceAfter = _token.balanceOf(address(sharedBridge))
```
[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76) | [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L77) | [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L142) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L161) | [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L163)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

/// @audit - `constructorInputHash` variable
76: bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""))
/// @audit - `salt` variable
77: bytes32 salt = bytes32(uint256(uint160(_l1Token)))
/// @audit - `amount` variable
142: uint256 amount = _depositFundsToSharedBridge(msg.sender, IERC20(_l1Token), _amount)
/// @audit - `balanceBefore` variable
161: uint256 balanceBefore = _token.balanceOf(address(sharedBridge))
/// @audit - `balanceAfter` variable
163: uint256 balanceAfter = _token.balanceOf(address(sharedBridge))
```
[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76) | [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L77) | [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L142) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L161) | [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L163)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

/// @audit - `amount` variable
160: uint256 amount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _amount)
/// @audit - `balanceBefore` variable
174: uint256 balanceBefore = _token.balanceOf(address(this))
/// @audit - `balanceAfter` variable
176: uint256 balanceAfter = _token.balanceOf(address(this))
/// @audit - `withdrawAmount` variable
205: uint256 withdrawAmount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount)
/// @audit - `l2TxCalldata` variable
217: bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, amount)
/// @audit - `gettersData` variable
249: bytes memory gettersData = _getERC20Getters(_l1Token)
/// @audit - `name` variable
256: bytes memory name = bytes("Ether")
/// @audit - `symbol` variable
257: bytes memory symbol = bytes("ETH")
/// @audit - `decimals` variable
258: bytes memory decimals = abi.encode(uint8(18))
/// @audit - `proofValid` variable
316: bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
                _chainId,
                _l2TxHash,
                _l2BatchNumber,
                _l2MessageIndex,
                _l2TxNumberInBatch,
                _merkleProof,
                TxStatus.Failure
            )
/// @audit - `weCanCheckDepositHere` variable
333: bool weCanCheckDepositHere = !_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)
/// @audit - `dataHash` variable
340: bytes32 dataHash = depositHappened[_chainId][_l2TxHash]
/// @audit - `txDataHash` variable
341: bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount))
/// @audit - `callSuccess` variable
355: bool callSuccess
/// @audit - `alreadyFinalized` variable
423: bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
                _l2BatchNumber,
                _l2MessageIndex
            )
/// @audit - `messageParams` variable
430: MessageParams memory messageParams = MessageParams({
            l2BatchNumber: _l2BatchNumber,
            l2MessageIndex: _l2MessageIndex,
            l2TxNumberInBatch: _l2TxNumberInBatch
        })
/// @audit - `callSuccess` variable
444: bool callSuccess
/// @audit - `baseTokenWithdrawal` variable
467: bool baseTokenWithdrawal = (l1Token == bridgehub.baseToken(_chainId))
/// @audit - `l2Sender` variable
468: address l2Sender = baseTokenWithdrawal ? L2_BASE_TOKEN_SYSTEM_CONTRACT_ADDR : l2BridgeAddress[_chainId]
/// @audit - `success` variable
477: bool success = bridgehub.proveL2MessageInclusion(
            _chainId,
            _messageParams.l2BatchNumber,
            _messageParams.l2MessageIndex,
            l2ToL1Message,
            _merkleProof
        )
/// @audit - `l2TxCalldata` variable
571: bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount)
/// @audit - `request` variable
584: L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
                chainId: ERA_CHAIN_ID,
                l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
                mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
                l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
                l2Calldata: l2TxCalldata,
                l2GasLimit: _l2TxGasLimit,
                l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
                factoryDeps: new bytes[](0),
                refundRecipient: refundRecipient
            })
/// @audit - `txDataHash` variable
598: bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount))
```
[160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L160) | [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L174) | [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176) | [205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L205) | [217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L217) | [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L249) | [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L256) | [257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L257) | [258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L258) | [316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L316) | [333](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L333) | [340](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L340) | [341](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L341) | [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L355) | [423](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L423) | [430](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L430) | [444](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L444) | [467](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L467) | [468](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L468) | [477](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L477) | [571](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L571) | [584](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L584) | [598](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L598)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

/// @audit - `oldPendingAdmin` variable
53: address oldPendingAdmin = pendingAdmin
/// @audit - `previousAdmin` variable
64: address previousAdmin = admin
/// @audit - `stateTransition` variable
159: address stateTransition = getStateTransition(_chainId)
/// @audit - `stateTransition` variable
171: address stateTransition = getStateTransition(_chainId)
/// @audit - `stateTransition` variable
185: address stateTransition = getStateTransition(_chainId)
/// @audit - `stateTransition` variable
204: address stateTransition = getStateTransition(_chainId)
/// @audit - `stateTransition` variable
236: address stateTransition = getStateTransition(_request.chainId)
/// @audit - `refundRecipient` variable
237: address refundRecipient = _actualRefundRecipient(_request.refundRecipient)
/// @audit - `stateTransition` variable
286: address stateTransition = getStateTransition(_request.chainId)
/// @audit - `refundRecipient` variable
298: address refundRecipient = _actualRefundRecipient(_request.refundRecipient)
```
[53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L53) | [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L64) | [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L159) | [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L171) | [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L185) | [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L204) | [236](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L236) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L237) | [286](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L286) | [298](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L298)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

/// @audit - `batchZero` variable
90: IExecutor.StoredBatchInfo memory batchZero = IExecutor.StoredBatchInfo(
            0,
            _initializeData.genesisBatchHash,
            _initializeData.genesisIndexRepeatedStorageChanges,
            0,
            EMPTY_STRING_KECCAK,
            DEFAULT_L2_LOGS_TREE_ROOT_HASH,
            0,
            _initializeData.genesisBatchCommitment
        )
/// @audit - `oldPendingAdmin` variable
112: address oldPendingAdmin = pendingAdmin
/// @audit - `previousAdmin` variable
123: address previousAdmin = admin
/// @audit - `systemContextCalldata` variable
178: bytes memory systemContextCalldata = abi.encodeCall(ISystemContext.setChainId, (_chainId))
/// @audit - `uintEmptyArray` variable
179: uint256[] memory uintEmptyArray
/// @audit - `bytesEmptyArray` variable
180: bytes[] memory bytesEmptyArray
/// @audit - `proposedUpgrade` variable
202: ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
            l2ProtocolUpgradeTx: l2ProtocolUpgradeTx,
            factoryDeps: bytesEmptyArray,
            bootloaderHash: bytes32(0),
            defaultAccountHash: bytes32(0),
            verifier: address(0),
            verifierParams: VerifierParams({
                recursionNodeLevelVkHash: bytes32(0),
                recursionLeafLevelVkHash: bytes32(0),
                recursionCircuitsSetVksHash: bytes32(0)
            }),
            l1ContractsUpgradeCalldata: new bytes(0),
            postUpgradeCalldata: new bytes(0),
            upgradeTimestamp: 0,
            newProtocolVersion: protocolVersion
        })
/// @audit - `emptyArray` variable
219: Diamond.FacetCut[] memory emptyArray
/// @audit - `cutData` variable
220: Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({
            facetCuts: emptyArray,
            initAddress: genesisUpgrade,
            initCalldata: abi.encodeCall(IDefaultUpgrade.upgrade, (proposedUpgrade))
        })
/// @audit - `cutHashInput` variable
255: bytes32 cutHashInput = keccak256(_diamondCut)
/// @audit - `stateTransitionContract` variable
277: DiamondProxy stateTransitionContract = new DiamondProxy{salt: bytes32(0)}(block.chainid, diamondCut)
```
[90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L90) | [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L112) | [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L123) | [178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L178) | [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L179) | [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L180) | [202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L202) | [219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L219) | [220](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L220) | [255](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L255) | [277](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L277)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

/// @audit - `timestamp` variable
115: uint32 timestamp = uint32(block.timestamp)
/// @audit - `timestamp` variable
134: uint32 timestamp = uint32(block.timestamp)
/// @audit - `delay` variable
183: uint256 delay = executionDelay
/// @audit - `commitBatchTimestamp` variable
186: uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
                    _newBatchesData[i].batchNumber
                )
/// @audit - `delay` variable
207: uint256 delay = executionDelay
/// @audit - `commitBatchTimestamp` variable
210: uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber)
/// @audit - `contractAddress` variable
226: address contractAddress = stateTransitionManager.stateTransition(_chainId)
```
[115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L115) | [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L134) | [183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L183) | [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L186) | [207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L207) | [210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L210) | [226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L226)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

/// @audit - `oldPendingAdmin` variable
25: address oldPendingAdmin = s.pendingAdmin
/// @audit - `previousAdmin` variable
36: address previousAdmin = s.admin
/// @audit - `oldPriorityTxMaxGasLimit` variable
61: uint256 oldPriorityTxMaxGasLimit = s.priorityTxMaxGasLimit
/// @audit - `oldFeeParams` variable
72: FeeParams memory oldFeeParams = s.feeParams
/// @audit - `oldNominator` variable
80: uint128 oldNominator = s.baseTokenGasPriceMultiplierNominator
/// @audit - `oldDenominator` variable
81: uint128 oldDenominator = s.baseTokenGasPriceMultiplierDenominator
/// @audit - `cutHashInput` variable
104: bytes32 cutHashInput = keccak256(abi.encode(_diamondCut))
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L25) | [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L36) | [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L61) | [72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L72) | [80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L80) | [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L81) | [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

/// @audit - `commitment` variable
84: bytes32 commitment = _createBatchCommitment(_newBatch, logOutput.stateDiffHash, blobCommitments, blobHashes)
/// @audit - `lastL2BlockTimestamp` variable
116: uint256 lastL2BlockTimestamp = _packedBatchAndL2BlockTimestamp & PACKED_L2_BLOCK_TIMESTAMP_MASK
/// @audit - `expectedUpgradeTxHash` variable
291: bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0)
/// @audit - `priorityOp` variable
312: PriorityOperation memory priorityOp = s.priorityQueue.popFront()
/// @audit - `priorityOperationsHash` variable
329: bytes32 priorityOperationsHash = _collectOperationsFromPriorityQueue(_storedBatch.numberOfLayer1Txs)
/// @audit - `verifierParams` variable
396: VerifierParams memory verifierParams = s.verifierParams
/// @audit - `successVerifyProof` variable
444: bool successVerifyProof = s.verifier.verify(
            proofPublicInput,
            _proof.serializedProof,
            _proof.recursiveAggregationInput
        )
/// @audit - `passThroughDataHash` variable
506: bytes32 passThroughDataHash = keccak256(_batchPassThroughData(_newBatchData))
/// @audit - `metadataHash` variable
507: bytes32 metadataHash = keccak256(_batchMetaParameters())
/// @audit - `auxiliaryOutputHash` variable
508: bytes32 auxiliaryOutputHash = keccak256(
            _batchAuxiliaryOutput(_newBatchData, _stateDiffHash, _blobCommitments, _blobHashes)
        )
/// @audit - `l2ToL1LogsHash` variable
545: bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs)
/// @audit - `precompileInput` variable
610: bytes memory precompileInput = abi.encodePacked(_versionedHash, _openingPoint, _openingValueCommitmentProof)
/// @audit - `openingPoint` variable
643: bytes32 openingPoint = bytes32(
                uint256(uint128(bytes16(_pubdataCommitments[i:i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET])))
            )
/// @audit - `versionedHash` variable
662: bytes32 versionedHash = _getBlobVersionedHash(versionedHashIndex)
```
[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L84) | [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L116) | [291](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L291) | [312](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L312) | [329](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L329) | [396](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L396) | [444](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L444) | [506](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L506) | [507](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L507) | [508](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L508) | [545](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L545) | [610](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L610) | [643](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L643) | [662](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L662)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

/// @audit - `ds` variable
158: Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage()
/// @audit - `selectorsArrayLen` variable
168: uint256 selectorsArrayLen = ds.facetToSelectors[_facet].selectors.length
/// @audit - `selector0` variable
170: bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0]
/// @audit - `facetToSelectors` variable
210: Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr]
/// @audit - `ds` variable
218: Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage()
/// @audit - `ds` variable
224: Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage()
/// @audit - `ds` variable
230: Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage()
```
[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L158) | [168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L168) | [170](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L170) | [210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L210) | [218](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L218) | [224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L224) | [230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L230)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

/// @audit - `amount` variable
41: uint256 amount = address(this).balance
/// @audit - `sharedBridgeAddress` variable
42: address sharedBridgeAddress = s.baseTokenBridge
/// @audit - `l2Log` variable
92: L2Log memory l2Log = L2Log({
            l2ShardId: 0,
            isService: true,
            txNumberInBatch: _l2TxNumberInBatch,
            sender: L2_BOOTLOADER_ADDRESS,
            key: _l2TxHash,
            value: bytes32(uint256(_status))
        })
/// @audit - `calculatedRootHash` variable
123: bytes32 calculatedRootHash = Merkle.calculateRoot(_proof, _index, hashedLog)
/// @audit - `actualRootHash` variable
124: bytes32 actualRootHash = s.l2LogsRootHashes[_batchNumber]
/// @audit - `l2GasPrice` variable
148: uint256 l2GasPrice = _deriveL2GasPrice(_gasPrice, _l2GasPerPubdataByteLimit)
/// @audit - `fullPubdataPriceBaseToken` variable
167: uint256 fullPubdataPriceBaseToken = pubdataPriceBaseToken +
            batchOverheadBaseToken /
            uint256(feeParams.maxPubdataPerBatch)
/// @audit - `l2GasPrice` variable
171: uint256 l2GasPrice = feeParams.minimalL2GasPrice + batchOverheadBaseToken / uint256(feeParams.maxL2GasPerBatch)
/// @audit - `minL2GasPriceBaseToken` variable
172: uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata
/// @audit - `baseCost` variable
271: uint256 baseCost = _params.l2GasPrice * _params.l2GasLimit
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41) | [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L42) | [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L92) | [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L123) | [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L124) | [148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L148) | [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L167) | [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L171) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L172) | [271](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L271)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

/// @audit - `previousDefaultAccountBytecodeHash` variable
100: bytes32 previousDefaultAccountBytecodeHash = s.l2DefaultAccountBytecodeHash
/// @audit - `previousBootloaderBytecodeHash` variable
117: bytes32 previousBootloaderBytecodeHash = s.l2BootloaderBytecodeHash
/// @audit - `oldVerifier` variable
135: IVerifier oldVerifier = s.verifier
/// @audit - `oldVerifierParams` variable
155: VerifierParams memory oldVerifierParams = s.verifierParams
```
[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L100) | [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L117) | [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L135) | [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L155)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

/// @audit - `txHash` variable
59: bytes32 txHash = _setL2SystemContractUpgrade(
            _proposedUpgrade.l2ProtocolUpgradeTx,
            _proposedUpgrade.factoryDeps,
            _proposedUpgrade.newProtocolVersion
        )
```
[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L59)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

/// @audit - `version` variable
40: uint8 version = uint8(_bytecodeHash[0])
/// @audit - `senderBytes` variable
66: bytes32 senderBytes = bytes32(uint256(uint160(_sender)))
/// @audit - `data` variable
67: bytes32 data = keccak256(
            bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
        )
```
[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L40) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L66) | [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L67)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

/// @audit - `position` variable
88: bytes32 position = DIAMOND_STORAGE_POSITION
/// @audit - `facetCutsLength` variable
100: uint256 facetCutsLength = facetCuts.length
/// @audit - `ds` variable
127: DiamondStorage storage ds = getDiamondStorage()
/// @audit - `selectorsLength` variable
137: uint256 selectorsLength = _selectors.length
/// @audit - `oldFacet` variable
140: SelectorToFacet memory oldFacet = ds.selectorToFacet[selector]
/// @audit - `ds` variable
150: DiamondStorage storage ds = getDiamondStorage()
/// @audit - `selectorsLength` variable
157: uint256 selectorsLength = _selectors.length
/// @audit - `ds` variable
173: DiamondStorage storage ds = getDiamondStorage()
/// @audit - `selectorsLength` variable
177: uint256 selectorsLength = _selectors.length
/// @audit - `selectorsLength` variable
192: uint256 selectorsLength = ds.facetToSelectors[_facet].selectors.length
/// @audit - `selector0` variable
214: bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0]
```
[88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L88) | [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L100) | [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L127) | [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L137) | [140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L140) | [150](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L150) | [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L157) | [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L173) | [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L177) | [192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L192) | [214](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L214)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

/// @audit - `mapValue` variable
23: uint256 mapValue = _map.map[_index / 8]
/// @audit - `bitOffset` variable
27: uint256 bitOffset = (_index & 7) * 32
/// @audit - `oldValue` variable
54: uint32 oldValue = uint32(mapValue >> bitOffset)
/// @audit - `newValueXorOldValue` variable
57: uint256 newValueXorOldValue = uint256(oldValue ^ _value)
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L23) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L27) | [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L54) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L57)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

/// @audit - `overheadForLength` variable
135: uint256 overheadForLength = MEMORY_OVERHEAD_GAS * _encodingLength
```
[135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L135)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

/// @audit - `constructedBytecodeHash` variable
60: bytes32 constructedBytecodeHash = Utils.constructedBytecodeHash(codeHash)
/// @audit - `addressAsKey` variable
69: uint256 addressAsKey = uint256(uint160(_address))
/// @audit - `addressAsKey` variable
79: uint256 addressAsKey = uint256(uint160(_address))
```
[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L60) | [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L69) | [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L79)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

/// @audit - `encodedGasPrice` variable
56: bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas)
/// @audit - `encodedGasLimit` variable
57: bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit)
/// @audit - `rInt` variable
81: uint256 rInt = uint256(bytes32(_transaction.signature[0:32]))
/// @audit - `sInt` variable
86: uint256 sInt = uint256(bytes32(_transaction.signature[32:64]))
/// @audit - `listLength` variable
105: uint256 listLength = encodedNonce.length +
                encodedGasParam.length +
                encodedTo.length +
                encodedValue.length +
                encodedDataLength.length +
                _transaction.data.length +
                rEncoded.length +
                sEncoded.length +
                vEncoded.length
/// @audit - `encodedChainId` variable
143: bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid)
/// @audit - `encodedNonce` variable
144: bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce)
/// @audit - `encodedGasPrice` variable
145: bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas)
/// @audit - `encodedGasLimit` variable
146: bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit)
/// @audit - `encodedTo` variable
147: bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)))
/// @audit - `encodedValue` variable
148: bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value)
/// @audit - `rInt` variable
180: uint256 rInt = uint256(bytes32(_transaction.signature[0:32]))
/// @audit - `sInt` variable
185: uint256 sInt = uint256(bytes32(_transaction.signature[32:64]))
/// @audit - `listLength` variable
198: uint256 listLength = encodedFixedLengthParams.length +
                encodedDataLength.length +
                _transaction.data.length +
                encodedAccessListLength.length +
                rEncoded.length +
                sEncoded.length +
                vEncoded.length
/// @audit - `encodedChainId` variable
236: bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid)
/// @audit - `encodedNonce` variable
237: bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce)
/// @audit - `encodedMaxPriorityFeePerGas` variable
238: bytes memory encodedMaxPriorityFeePerGas = RLPEncoder.encodeUint256(_transaction.maxPriorityFeePerGas)
/// @audit - `encodedMaxFeePerGas` variable
239: bytes memory encodedMaxFeePerGas = RLPEncoder.encodeUint256(_transaction.maxFeePerGas)
/// @audit - `encodedGasLimit` variable
240: bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit)
/// @audit - `encodedTo` variable
241: bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)))
/// @audit - `encodedValue` variable
242: bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value)
/// @audit - `rInt` variable
275: uint256 rInt = uint256(bytes32(_transaction.signature[0:32]))
/// @audit - `sInt` variable
280: uint256 sInt = uint256(bytes32(_transaction.signature[32:64]))
/// @audit - `listLength` variable
293: uint256 listLength = encodedFixedLengthParams.length +
                encodedDataLength.length +
                _transaction.data.length +
                encodedAccessListLength.length +
                rEncoded.length +
                sEncoded.length +
                vEncoded.length
```
[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L56) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L57) | [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L81) | [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L86) | [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L105) | [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L143) | [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L144) | [145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L145) | [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L146) | [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L147) | [148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L148) | [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L180) | [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L185) | [198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L198) | [236](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L236) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L237) | [238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L238) | [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L239) | [240](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L240) | [241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L241) | [242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L242) | [275](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L275) | [280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L280) | [293](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L293)

```solidity
File: code/system-contracts/contracts/Compressor.sol

/// @audit - `encodedChunk` variable
65: uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk)
/// @audit - `realChunk` variable
66: uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4)
/// @audit - `numberOfInitialWrites` variable
121: uint256 numberOfInitialWrites = uint256(_compressedStateDiffs.readUint16(0))
/// @audit - `derivedKey` variable
137: bytes32 derivedKey = stateDiff.readBytes32(52)
/// @audit - `compressedEnumIndex` variable
168: uint256 compressedEnumIndex = _sliceToUint256(
                _compressedStateDiffs[stateDiffPtr:stateDiffPtr + _enumerationIndexSize]
            )
```
[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L65) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L66) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L121) | [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L137) | [168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L168)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

/// @audit - `constructorInputHash` variable
103: bytes32 constructorInputHash = EfficientCall.keccak(_input)
/// @audit - `hash` variable
105: bytes32 hash = keccak256(
            bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, constructorInputHash)
        )
/// @audit - `hash` variable
121: bytes32 hash = keccak256(
            bytes.concat(CREATE_PREFIX, bytes32(uint256(uint160(_sender))), bytes32(_senderNonce))
        )
/// @audit - `senderNonce` variable
188: uint256 senderNonce = NONCE_HOLDER_SYSTEM_CONTRACT.incrementDeploymentNonce(msg.sender)
/// @audit - `knownCodeMarker` variable
302: uint256 knownCodeMarker = KNOWN_CODE_STORAGE_CONTRACT.getMarker(_bytecodeHash)
/// @audit - `constructingBytecodeHash` variable
311: bytes32 constructingBytecodeHash = Utils.constructingBytecodeHash(_bytecodeHash)
/// @audit - `returnData` variable
343: bytes memory returnData = EfficientCall.mimicCall(gasleft(), _newAddress, _input, _sender, true, _isSystem)
/// @audit - `immutables` variable
347: ImmutableData[] memory immutables = abi.decode(returnData, (ImmutableData[]))
```
[103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L103) | [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L105) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L121) | [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L188) | [302](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L302) | [311](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L311) | [343](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L343) | [347](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L347)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

/// @audit - `codeAddress` variable
46: address codeAddress = SystemContractHelper.getCodeAddress()
/// @audit - `txHash` variable
94: bytes32 txHash = _suggestedSignedHash != bytes32(0) ? _suggestedSignedHash : _transaction.encodeHash()
/// @audit - `totalRequiredBalance` variable
99: uint256 totalRequiredBalance = _transaction.totalRequiredBalance()
/// @audit - `value` variable
133: uint128 value = Utils.safeCastToU128(_transaction.value)
/// @audit - `gas` variable
135: uint32 gas = Utils.safeCastToU32(gasleft())
/// @audit - `success` variable
149: bool success = EfficientCall.rawCall(gas, to, value, data, isSystemCall)
/// @audit - `success` variable
201: bool success = _transaction.payToTheBootloader()
```
[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L46) | [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L94) | [99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L99) | [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L133) | [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L135) | [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L149) | [201](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L201)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

/// @audit - `immutablesLength` variable
37: uint256 immutablesLength = _immutables.length
/// @audit - `index` variable
39: uint256 index = _immutables[i].index
/// @audit - `value` variable
40: bytes32 value = _immutables[i].value
```
[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L37) | [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L39) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L40)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

/// @audit - `hashesLen` variable
29: uint256 hashesLen = _hashes.length
/// @audit - `version` variable
75: uint8 version = uint8(_bytecodeHash[0])
```
[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L29) | [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L75)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

/// @audit - `l2ToL1Log` variable
75: L2ToL1Log memory l2ToL1Log = L2ToL1Log({
            l2ShardId: 0,
            isService: _isService,
            txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),
            sender: msg.sender,
            key: _key,
            value: _value
        })
/// @audit - `gasToPay` variable
89: uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) + 2 * keccakGasCost(64)
/// @audit - `hashedLog` variable
95: bytes32 hashedLog = keccak256(
            abi.encodePacked(
                _l2ToL1Log.l2ShardId,
                _l2ToL1Log.isService,
                _l2ToL1Log.txNumberInBlock,
                _l2ToL1Log.sender,
                _l2ToL1Log.key,
                _l2ToL1Log.value
            )
        )
/// @audit - `gasBeforeMessageHashing` variable
117: uint256 gasBeforeMessageHashing = gasleft()
/// @audit - `gasSpentOnMessageHashing` variable
119: uint256 gasSpentOnMessageHashing = gasBeforeMessageHashing - gasleft()
/// @audit - `l2ToL1Log` variable
125: L2ToL1Log memory l2ToL1Log = L2ToL1Log({
            l2ShardId: 0,
            isService: true,
            txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),
            sender: address(this),
            key: bytes32(uint256(uint160(msg.sender))),
            value: hash
        })
/// @audit - `gasToPay` variable
148: uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) +
            3 *
            keccakGasCost(64) +
            gasSpentOnMessageHashing +
            COMPUTATIONAL_PRICE_FOR_PUBDATA *
            pubdataLen
/// @audit - `gasToPay` variable
175: uint256 gasToPay = sha256GasCost(bytecodeLen) +
            keccakGasCost(64) +
            COMPUTATIONAL_PRICE_FOR_PUBDATA *
            pubdataLen
/// @audit - `l2ToL1LogsTreeRoot` variable
230: bytes32 l2ToL1LogsTreeRoot = l2ToL1LogsTreeArray[0]
/// @audit - `numberOfMessages` variable
233: uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]))
/// @audit - `hashedMessage` variable
239: bytes32 hashedMessage = EfficientCall.keccak(
                _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentMessageLength]
            )
/// @audit - `numberOfBytecodes` variable
251: uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]))
/// @audit - `enumerationIndexSize` variable
289: uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))
/// @audit - `compressedStateDiffs` variable
292: bytes calldata compressedStateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr +
            compressedStateDiffSize]
/// @audit - `stateDiffs` variable
303: bytes calldata stateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr +
            (numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE)]
/// @audit - `stateDiffHash` variable
307: bytes32 stateDiffHash = COMPRESSOR_CONTRACT.verifyCompressedStateDiffs(
            numberOfStateDiffs,
            enumerationIndexSize,
            stateDiffs,
            compressedStateDiffs
        )
```
[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L75) | [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L89) | [95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L95) | [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L117) | [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L119) | [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L125) | [148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L148) | [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L175) | [230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L230) | [233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L233) | [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L239) | [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L251) | [289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L289) | [292](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L292) | [303](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L303) | [307](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L307)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

/// @audit - `message` variable
76: bytes memory message = _getL1WithdrawMessage(_l1Receiver, amount)
/// @audit - `message` variable
89: bytes memory message = _getExtendedWithdrawMessage(_l1Receiver, amount, msg.sender, _additionalData)
```
[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L76) | [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L89)

```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

/// @audit - `addressAsUint` variable
27: uint256 addressAsUint = SystemContractHelper.getExtraAbiData(1)
/// @audit - `mask` variable
28: uint256 mask = SystemContractHelper.getExtraAbiData(2)
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L27) | [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L28)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

/// @audit - `addressAsKey` variable
47: uint256 addressAsKey = uint256(uint160(_address))
/// @audit - `addressAsKey` variable
58: uint256 addressAsKey = uint256(uint160(_address))
/// @audit - `accountInfo` variable
83: IContractDeployer.AccountInfo memory accountInfo = DEPLOYER_SYSTEM_CONTRACT.getAccountInfo(msg.sender)
/// @audit - `addressAsKey` variable
92: uint256 addressAsKey = uint256(uint160(msg.sender))
/// @audit - `addressAsKey` variable
103: uint256 addressAsKey = uint256(uint160(msg.sender))
/// @audit - `addressAsKey` variable
126: uint256 addressAsKey = uint256(uint160(_address))
/// @audit - `addressAsKey` variable
155: uint256 addressAsKey = uint256(uint160(_address))
```
[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L47) | [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L58) | [83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L83) | [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L92) | [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L103) | [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L126) | [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L155)

```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

/// @audit - `totalBlobs` variable
28: bytes memory totalBlobs = new bytes(BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS)
/// @audit - `start` variable
37: uint256 start = BLOB_SIZE_BYTES * i
/// @audit - `blobHash` variable
45: bytes32 blobHash
```
[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L28) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L37) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L45)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

/// @audit - `currentBatchTimestamp` variable
350: uint128 currentBatchTimestamp = currentBatchInfo.timestamp
/// @audit - `prevL2BlockHash` variable
376: bytes32 prevL2BlockHash = _getLatest257L2blockHash(currentL2BlockNumber - 1)
/// @audit - `pendingL2BlockHash` variable
378: bytes32 pendingL2BlockHash = _calculateL2BlockHash(
                currentL2BlockNumber,
                currentL2BlockTimestamp,
                prevL2BlockHash,
                currentL2BlockTxsRollingHash
            )
/// @audit - `packedTimestamps` variable
416: uint256 packedTimestamps = (uint256(currentBatchTimestamp) << 128) | currentL2BlockTimestamp
/// @audit - `currentBlockTimestamp` variable
428: uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp
/// @audit - `newBlockInfo` variable
459: BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp})
/// @audit - `newBlockInfo` variable
476: BlockInfo memory newBlockInfo = BlockInfo({number: uint128(_number), timestamp: uint128(_newTimestamp)})
```
[350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L350) | [376](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L376) | [378](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L378) | [416](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L416) | [428](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L428) | [459](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L459) | [476](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L476)

```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

/// @audit - `pubdataAllowance` variable
49: uint256 pubdataAllowance = _maxTotalGas > expectedForCompute ? _maxTotalGas - expectedForCompute : 0
/// @audit - `pubdataSpent` variable
63: uint256 pubdataSpent = pubdataPublishedAfter > pubdataPublishedBefore
            ? pubdataPublishedAfter - pubdataPublishedBefore
            : 0
/// @audit - `pubdataPrice` variable
67: uint256 pubdataPrice = REAL_SYSTEM_CONTEXT_CONTRACT.gasPerPubdataByte()
```
[49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L49) | [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L63) | [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L67)

```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

/// @audit - `success` variable
65: bool success = rawCall(_gas, _address, _value, _data, _isSystem)
/// @audit - `success` variable
79: bool success = rawStaticCall(_gas, _address, _data)
/// @audit - `success` variable
93: bool success = rawDelegateCall(_gas, _address, _data)
/// @audit - `success` variable
113: bool success = rawMimicCall(_gas, _address, _data, _whoToMimic, _isConstructor, _isSystem)
/// @audit - `callAddr` variable
162: address callAddr = RAW_FAR_CALL_BY_REF_CALL_ADDRESS
/// @audit - `callAddr` variable
176: address callAddr = RAW_FAR_CALL_BY_REF_CALL_ADDRESS
/// @audit - `callAddr` variable
201: address callAddr = MIMIC_CALL_BY_REF_CALL_ADDRESS
/// @audit - `cleanupMask` variable
202: uint256 cleanupMask = ADDRESS_MASK
/// @audit - `size` variable
217: uint256 size
/// @audit - `shrinkTo` variable
261: uint32 shrinkTo = uint32(msg.data.length - (_data.length + dataOffset))
/// @audit - `gas` variable
264: uint32 gas = Utils.safeCastToU32(_gas)
/// @audit - `farCallAbi` variable
265: uint256 farCallAbi = SystemContractsCaller.getFarCallABIWithEmptyFatPointer(
            gas,
            // Only rollup is supported for now
            0,
            CalldataForwardingMode.ForwardFatPointer,
            _isConstructor,
            _isSystem
        )
```
[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L65) | [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L79) | [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L93) | [113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L113) | [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L162) | [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L176) | [201](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L201) | [202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L202) | [217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L217) | [261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L261) | [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L264) | [265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L265)

```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

/// @audit - `shiftedVal` variable
15: bytes20 shiftedVal = bytes20(_val)
/// @audit - `lbs` variable
36: uint256 lbs = 31 - hbs
/// @audit - `lbs` variable
71: uint256 lbs = 31 - hbs
```
[15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L15) | [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L36) | [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L71)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

/// @audit - `callAddr` variable
49: address callAddr = TO_L1_CALL_ADDRESS
/// @audit - `callAddr` variable
64: address callAddr = CODE_ADDRESS_CALL_ADDRESS
/// @audit - `callAddr` variable
75: address callAddr = LOAD_CALLDATA_INTO_ACTIVE_PTR_CALL_ADDRESS
/// @audit - `callAddr` variable
86: address callAddr = PTR_PACK_INTO_ACTIVE_CALL_ADDRESS
/// @audit - `callAddr` variable
95: address callAddr = PTR_ADD_INTO_ACTIVE_CALL_ADDRESS
/// @audit - `cleanupMask` variable
96: uint256 cleanupMask = UINT32_MASK
/// @audit - `callAddr` variable
107: address callAddr = PTR_SHRINK_INTO_ACTIVE_CALL_ADDRESS
/// @audit - `cleanupMask` variable
108: uint256 cleanupMask = UINT32_MASK
/// @audit - `callAddr` variable
153: address callAddr = PRECOMPILE_CALL_ADDRESS
/// @audit - `cleanupMask` variable
157: uint256 cleanupMask = UINT64_MASK
/// @audit - `cleanupMask` variable
169: uint256 cleanupMask = UINT128_MASK
/// @audit - `callAddr` variable
170: address callAddr = SET_CONTEXT_VALUE_CALL_ADDRESS
/// @audit - `callAddr` variable
182: address callAddr = EVENT_INITIALIZE_ADDRESS
/// @audit - `callAddr` variable
192: address callAddr = EVENT_WRITE_ADDRESS
/// @audit - `callAddr` variable
204: address callAddr = META_CALL_ADDRESS
/// @audit - `shifted` variable
217: uint256 shifted = (meta << (256 - size - offset))
/// @audit - `callAddr` variable
297: address callAddr = CALLFLAGS_CALL_ADDRESS
/// @audit - `callAddr` variable
308: address callAddr = PTR_CALLDATA_CALL_ADDRESS
/// @audit - `callAddr` variable
321: address callAddr = GET_EXTRA_ABI_DATA_ADDRESS
/// @audit - `callFlags` variable
330: uint256 callFlags = getCallFlags()
/// @audit - `precompileCallSuccess` variable
345: bool precompileCallSuccess = unsafePrecompileCall(
            0, // The precompile parameters are formal ones. We only need the precompile call to burn gas.
            _gasToPay,
            _pubdataToSpend
        )
```
[49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L49) | [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L64) | [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L75) | [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L86) | [95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L95) | [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L96) | [107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L107) | [108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L108) | [153](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L153) | [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L157) | [169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L169) | [170](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L170) | [182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L182) | [192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L192) | [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L204) | [217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L217) | [297](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L297) | [308](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L308) | [321](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L321) | [330](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L330) | [345](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L345)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

/// @audit - `dataLength` variable
83: uint32 dataLength = uint32(Utils.safeCastToU32(data.length))
```
[83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L83)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

/// @audit - `structHash` variable
119: bytes32 structHash = keccak256(
            abi.encode(
                EIP712_TRANSACTION_TYPE_HASH,
                _transaction.txType,
                _transaction.from,
                _transaction.to,
                _transaction.gasLimit,
                _transaction.gasPerPubdataByteLimit,
                _transaction.maxFeePerGas,
                _transaction.maxPriorityFeePerGas,
                _transaction.paymaster,
                _transaction.nonce,
                _transaction.value,
                EfficientCall.keccak(_transaction.data),
                keccak256(abi.encodePacked(_transaction.factoryDeps)),
                EfficientCall.keccak(_transaction.paymasterInput)
            )
        )
/// @audit - `domainSeparator` variable
138: bytes32 domainSeparator = keccak256(
            abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
        )
/// @audit - `encodedGasPrice` variable
159: bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas)
/// @audit - `encodedGasLimit` variable
160: bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit)
/// @audit - `listLength` variable
190: uint256 listLength = encodedNonce.length +
                encodedGasParam.length +
                encodedTo.length +
                encodedValue.length +
                encodedDataLength.length +
                _transaction.data.length +
                encodedChainId.length
/// @audit - `encodedChainId` variable
228: bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid)
/// @audit - `encodedNonce` variable
229: bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce)
/// @audit - `encodedGasPrice` variable
230: bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas)
/// @audit - `encodedGasLimit` variable
231: bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit)
/// @audit - `encodedTo` variable
232: bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)))
/// @audit - `encodedValue` variable
233: bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value)
/// @audit - `listLength` variable
265: uint256 listLength = encodedFixedLengthParams.length +
                encodedDataLength.length +
                _transaction.data.length +
                encodedAccessListLength.length
/// @audit - `encodedChainId` variable
298: bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid)
/// @audit - `encodedNonce` variable
299: bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce)
/// @audit - `encodedMaxPriorityFeePerGas` variable
300: bytes memory encodedMaxPriorityFeePerGas = RLPEncoder.encodeUint256(_transaction.maxPriorityFeePerGas)
/// @audit - `encodedMaxFeePerGas` variable
301: bytes memory encodedMaxFeePerGas = RLPEncoder.encodeUint256(_transaction.maxFeePerGas)
/// @audit - `encodedGasLimit` variable
302: bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit)
/// @audit - `encodedTo` variable
303: bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)))
/// @audit - `encodedValue` variable
304: bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value)
/// @audit - `listLength` variable
337: uint256 listLength = encodedFixedLengthParams.length +
                encodedDataLength.length +
                _transaction.data.length +
                encodedAccessListLength.length
/// @audit - `currentAllowance` variable
377: uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster)
/// @audit - `bootloaderAddr` variable
396: address bootloaderAddr = BOOTLOADER_FORMAL_ADDRESS
/// @audit - `amount` variable
397: uint256 amount = _transaction.maxFeePerGas * _transaction.gasLimit
```
[119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L119) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L138) | [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L159) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L160) | [190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L190) | [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L228) | [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L229) | [230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L230) | [231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L231) | [232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L232) | [233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L233) | [265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L265) | [298](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L298) | [299](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L299) | [300](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L300) | [301](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L301) | [302](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L302) | [303](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L303) | [304](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L304) | [337](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L337) | [377](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377) | [396](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L396) | [397](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L397)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

/// @audit - `l2StandardToken` variable
64: address l2StandardToken = address(new L2StandardERC20{salt: bytes32(0)}())
/// @audit - `deployedToken` variable
97: address deployedToken = _deployL2Token(_l1Token, _data)
/// @audit - `salt` variable
110: bytes32 salt = _getCreate2Salt(_l1Token)
/// @audit - `message` variable
131: bytes memory message = _getL1WithdrawMessage(_l1Receiver, l1Token, _amount)
/// @audit - `constructorInputHash` variable
150: bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""))
/// @audit - `salt` variable
151: bytes32 salt = _getCreate2Salt(_l1Token)
```
[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L64) | [97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L97) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L110) | [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L131) | [150](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150) | [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L151)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

/// @audit - `beaconAddress` variable
119: address beaconAddress = _getBeacon()
```
[119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L119)

```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

/// @audit - `senderBytes` variable
107: bytes32 senderBytes = bytes32(uint256(uint160(_sender)))
/// @audit - `data` variable
108: bytes32 data = keccak256(
            bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
        )
```
[107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L107) | [108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L108)

```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

/// @audit - `dataLength` variable
44: uint32 dataLength = uint32(Utils.safeCastToU32(data.length))
```
[44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L44)
</details>

### [G-17] `abi.encodePacked `is more gas efficient than `abi.encode`

`abi.encode()` pads all elementary types to 32 bytes, whereas `abi.encodePacked()` will only use the minimal required memory to encode the data.
```solidity
    function testPacking() public pure returns (bytes memory) {
        // return abi.encode("string"); // 1120 gas
        // return abi.encodePacked("string"); // 913 gas
    }
```

<details>
<summary><i>35 issue instances in 13 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

76: abi.encode(l2TokenBeacon, "")
```
[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

76: abi.encode(l2TokenBeacon, "")
```
[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

210: abi.encode(_prevMsgSender, _l1Token, amount)
258: abi.encode(uint8(18))
259: abi.encode(name, symbol, decimals)
265: abi.encode(data1, data2, data3)
341: abi.encode(_depositSender, _l1Token, _amount)
598: abi.encode(_prevMsgSender, _l1Token, _amount)
```
[210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L210) | [258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L258) | [259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L259) | [265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L265) | [341](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L341) | [598](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L598)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

205: abi.encode(_operation)
```
[205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L205)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

100: abi.encode(batchZero)
102: abi.encode(_initializeData.diamondCut)
138: abi.encode(_diamondCut)
147: abi.encode(_cutData)
156: abi.encode(_cutData)
```
[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100) | [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138) | [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L147) | [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L156)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

104: abi.encode(_diamondCut)
```
[104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

313: abi.encode(concatHash, priorityOp.canonicalTxHash)
512: abi.encode(passThroughDataHash, metadataHash, auxiliaryOutputHash)
588: abi.encode(_storedBatchInfo)
680: abi.encode(_index)
```
[313](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313) | [512](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L512) | [588](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L588) | [680](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L680)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

323: abi.encode(transaction)
```
[323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L323)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

192: abi.encode(_l2ProtocolUpgradeTx)
```
[192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L192)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

106: abi.encode(chainedLogsHash, hashedLog)
122: abi.encode(chainedMessagesHash, hash)
164: abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash)
212: abi.encode(reconstructedChainedLogsHash, hashedLog)
226: abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
243: abi.encode(reconstructedChainedMessagesHash, hashedMessage)
260: abi.encode(
                    reconstructedChainedL1BytecodesRevealDataHash,
                    Utils.hashL2Bytecode(
                        _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
                    )
                )
```
[106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L106) | [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L122) | [164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L164) | [212](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L212) | [226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L226) | [243](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L243) | [260](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L260)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

159: abi.encode(_block)
227: abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash)
403: abi.encode(currentL2BlockTxsRollingHash, _txHash)
```
[159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L159) | [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L227) | [403](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L403)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

120: abi.encode(
                EIP712_TRANSACTION_TYPE_HASH,
                _transaction.txType,
                _transaction.from,
                _transaction.to,
                _transaction.gasLimit,
                _transaction.gasPerPubdataByteLimit,
                _transaction.maxFeePerGas,
                _transaction.maxPriorityFeePerGas,
                _transaction.paymaster,
                _transaction.nonce,
                _transaction.value,
                EfficientCall.keccak(_transaction.data),
                keccak256(abi.encodePacked(_transaction.factoryDeps)),
                EfficientCall.keccak(_transaction.paymasterInput)
            )
139: abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
```
[120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L120) | [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

150: abi.encode(address(l2TokenBeacon), "")
171: abi.encode(address(l2TokenBeacon), "")
```
[150](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150) | [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L171)
</details>

### [G-18] Consider Using `selfbalance()` Over `address(this).balance`

The `selfbalance()` function from Yul can be more gas-efficient than using `address(this).balance` in certain scenarios.
Although the Solidity compiler is sometimes optimized enough to handle this, manually switching to `selfbalance()` could yield gas savings.

Note: Always thoroughly test both approaches to confirm the actual gas savings.

<details>
<summary><i>4 issue instances in 3 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

118: address(this).balance
120: address(this).balance
```
[118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118) | [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

41: address(this).balance
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

100: address(this).balance
```
[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100)
</details>

### [G-19] Using `require()` instead of `assert()` safes gas

Since `assert()` can't contain any message, it is recommended to use `require()` without message instead.
Using `require()` saves 33 gas per call.
```solidity
    require(false); // 133 gas
    assert(false); // 166 gas 
```


<details>
<summary><i>5 issue instances in 5 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

106: assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32)
```
[106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L106)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

51: assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32)
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L51)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

426: assert(block.chainid != 1)
```
[426](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L426)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

222: assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS)
```
[222](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L222)

```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

50: assert(_len != 1)
```
[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L50)
</details>

### [G-20] Use `assembly` to write mutable storage values

Writing to storage using `assembly` is more gas efficient.
```solidity
    function writeStorage() external {
        // storageNumber = 10; // 2358 gas
        // assembly {
        //     sstore(storageNumber.slot, 10) // 2350 gas
        // }
        // storageAddr = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc3; // 2411 gas
        // assembly {
        //     sstore(storageAddr.slot, 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc3) // 2350 gas
        // }
    }
```

<details>
<summary><i>128 issue instances in 20 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

154: depositAmount[msg.sender][_l1Token][l2TxHash] = _amount
```
[154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L154)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

154: depositAmount[msg.sender][_l1Token][l2TxHash] = _amount
```
[154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L154)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

111: eraFirstPostUpgradeBatch = _eraFirstPostUpgradeBatch
112: l2BridgeAddress[ERA_CHAIN_ID] = ERA_ERC20_BRIDGE_ADDRESS
122: chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
                chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
                balanceAfter -
                balanceBefore
133: chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount
143: l2BridgeAddress[_chainId] = _l2BridgeAddress
238: depositHappened[_chainId][_txHash] = _txDataHash
418: isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true
600: depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash
```
[111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L111) | [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L112) | [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L122) | [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133) | [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L143) | [238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L238) | [418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L418) | [600](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L600)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

55: pendingAdmin = _newPendingAdmin
65: admin = currentPendingAdmin
87: stateTransitionManagerIsRegistered[_stateTransitionManager] = true
97: stateTransitionManagerIsRegistered[_stateTransitionManager] = false
103: tokenIsRegistered[_token] = true
109: sharedBridge = IL1SharedBridge(_sharedBridge)
134: stateTransitionManager[_chainId] = _stateTransitionManager
135: baseToken[_chainId] = _baseToken
```
[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55) | [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L65) | [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L87) | [97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L97) | [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L103) | [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L109) | [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134) | [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L135)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

46: securityCouncil = _securityCouncil
49: minDelay = _minDelay
179: timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP
198: timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP
219: timestamps[_id] = block.timestamp + _delay
251: minDelay = _newDelay
258: securityCouncil = _newSecurityCouncil
```
[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L46) | [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L49) | [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L179) | [198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L198) | [219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L219) | [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L251) | [258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L258)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

85: genesisUpgrade = _initializeData.genesisUpgrade
86: protocolVersion = _initializeData.protocolVersion
87: validatorTimelock = _initializeData.validatorTimelock
100: storedBatchZero = keccak256(abi.encode(batchZero))
102: initialCutHash = keccak256(abi.encode(_initializeData.diamondCut))
114: pendingAdmin = _newPendingAdmin
124: admin = currentPendingAdmin
133: validatorTimelock = _validatorTimelock
138: initialCutHash = keccak256(abi.encode(_diamondCut))
147: upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData))
148: protocolVersion = _newProtocolVersion
156: upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData))
234: stateTransition[_chainId] = _stateTransitionContract
282: stateTransition[_chainId] = stateTransitionAddress
```
[85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L85) | [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L86) | [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L87) | [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100) | [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102) | [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L114) | [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L124) | [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L133) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138) | [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L147) | [148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L148) | [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L156) | [234](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L234) | [282](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L282)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

57: executionDelay = _executionDelay
74: stateTransitionManager = _stateTransitionManager
82: validators[_chainId][_newValidator] = true
91: validators[_chainId][_validator] = false
97: executionDelay = _executionDelay
```
[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57) | [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L74) | [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L82) | [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L91) | [97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L97)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

30: s.chainId = _initializeData.chainId
31: s.bridgehub = _initializeData.bridgehub
32: s.stateTransitionManager = _initializeData.stateTransitionManager
33: s.baseToken = _initializeData.baseToken
34: s.baseTokenBridge = _initializeData.baseTokenBridge
35: s.protocolVersion = _initializeData.protocolVersion
37: s.verifier = _initializeData.verifier
38: s.admin = _initializeData.admin
39: s.validators[_initializeData.validatorTimelock] = true
41: s.storedBatchHashes[0] = _initializeData.storedBatchZero
42: s.verifierParams = _initializeData.verifierParams
43: s.l2BootloaderBytecodeHash = _initializeData.l2BootloaderBytecodeHash
44: s.l2DefaultAccountBytecodeHash = _initializeData.l2DefaultAccountBytecodeHash
45: s.priorityTxMaxGasLimit = _initializeData.priorityTxMaxGasLimit
46: s.feeParams = _initializeData.feeParams
47: s.blobVersionedHashRetriever = _initializeData.blobVersionedHashRetriever
```
[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L30) | [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L31) | [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L32) | [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L33) | [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L34) | [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L35) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L37) | [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L38) | [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L39) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L41) | [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L42) | [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L43) | [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L44) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L45) | [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L46) | [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L47)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

27: s.pendingAdmin = _newPendingAdmin
37: s.admin = pendingAdmin
46: s.validators[_validator] = _active
53: s.zkPorterIsAvailable = _zkPorterIsAvailable
62: s.priorityTxMaxGasLimit = _newPriorityTxMaxGasLimit
73: s.feeParams = _newFeeParams
83: s.baseTokenGasPriceMultiplierNominator = _nominator
84: s.baseTokenGasPriceMultiplierDenominator = _denominator
91: s.feeParams.pubdataPricingMode = _validiumMode
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L27) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L37) | [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L46) | [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L53) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L62) | [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L73) | [83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L83) | [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L84) | [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L91)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

247: s.totalBatchesCommitted = s.totalBatchesCommitted + _newBatchesData.length
260: s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData)
287: s.l2SystemContractsUpgradeBatchNumber = _newBatchesData[0].batchNumber
298: s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData)
333: s.l2LogsRootHashes[currentBatchNumber] = _storedBatch.l2LogsTreeRoot
357: s.totalBatchesExecuted = newTotalBatchesExecuted
437: s.totalBatchesVerified = currentTotalBatchesVerified
486: s.totalBatchesVerified = _newLastBatch
488: s.totalBatchesCommitted = _newLastBatch
```
[247](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L247) | [260](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L260) | [287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L287) | [298](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L298) | [333](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L333) | [357](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L357) | [437](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L437) | [486](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L486) | [488](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L488)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

103: s.l2DefaultAccountBytecodeHash = _l2DefaultAccountBytecodeHash
120: s.l2BootloaderBytecodeHash = _l2BootloaderBytecodeHash
136: s.verifier = _newVerifier
156: s.verifierParams = _newVerifierParams
214: s.l2SystemContractsUpgradeTxHash = l2ProtocolUpgradeTxHash
255: s.protocolVersion = _newProtocolVersion
```
[103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L103) | [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L120) | [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L136) | [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L156) | [214](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L214) | [255](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L255)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

39: s.protocolVersion = _newProtocolVersion
```
[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L39)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

59: accountInfo[_address] = _newInfo
66: accountInfo[msg.sender].supportedAAVersion = _version
```
[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L59) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L66)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

41: immutableDataStorage[uint256(uint160(_dest))][index] = value
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L41)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

106: chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog))
122: chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash))
164: chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash))
329: chainedLogsHash = bytes32(0)
330: numberOfLogsToProcess = 0
331: chainedMessagesHash = bytes32(0)
332: chainedL1BytecodesRevealDataHash = bytes32(0)
```
[106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L106) | [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L122) | [164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L164) | [329](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L329) | [330](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L330) | [331](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L331) | [332](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L332)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

43: balance[_from] = fromBalance - _amount
```
[43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L43)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

72: rawNonces[addressAsKey] = (oldRawNonce + _value)
94: nonceValues[addressAsKey][_key] = _value
118: rawNonces[addressAsKey] = oldRawNonce + 1
144: rawNonces[addressAsKey] = (oldRawNonce + DEPLOY_NONCE_MULTIPLIER)
```
[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L72) | [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L94) | [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L118) | [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L144)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

85: chainId = _newChainId
100: origin = _newOrigin
106: gasPrice = _gasPrice
113: basePubdataSpent = _basePubdataSpent
114: gasPerPubdataByte = _gasPerPubdataByte
213: l2BlockHash[_block % MINIBLOCK_HASHES_TO_STORE] = _hash
271: currentVirtualL2BlockInfo = currentL2BlockInfo
285: virtualBlockUpgradeInfo.virtualBlockStartBatch = currentBatchNumber
303: virtualBlockUpgradeInfo.virtualBlockFinishL2Block = _l2BlockNumber
307: currentVirtualL2BlockInfo = virtualBlockInfo
316: currentL2BlockInfo = BlockInfo({number: _l2BlockNumber, timestamp: _l2BlockTimestamp})
322: currentL2BlockTxsRollingHash = bytes32(0)
403: currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash))
456: batchHashes[previousBatchNumber] = _prevBatchHash
461: currentBatchInfo = newBlockInfo
463: baseFee = _baseFee
477: currentBatchInfo = newBlockInfo
479: baseFee = _baseFee
487: txNumberInBlock = 0
```
[85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L85) | [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L100) | [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L106) | [113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L113) | [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L114) | [213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L213) | [271](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L271) | [285](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L285) | [303](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L303) | [307](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L307) | [316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L316) | [322](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L322) | [403](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L403) | [456](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L456) | [461](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L461) | [463](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L463) | [477](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L477) | [479](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L479) | [487](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L487)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

60: l1Bridge = _l1Bridge
61: l2TokenProxyBytecodeHash = _l2TokenProxyBytecodeHash
65: l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(l2StandardToken)
99: l1TokenAddress[expectedL2Token] = _l1Token
```
[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L60) | [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L61) | [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L65) | [99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L99)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

52: l1Address = _l1Address
54: l2Bridge = msg.sender
95: decimals_ = decimalsUint8
100: availableGetters = getters
124: availableGetters = _availableGetters
```
[52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L52) | [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L54) | [95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L95) | [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L100) | [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L124)
</details>

### [G-21] Using `delete` on a `uint/int` variable is cheaper than assigning it to `0`

```solidity
function test() external {
    delete foo; // 5148 gas
    foo = 0; // 5156 gas
}
```

<details>
<summary><i>3 issue instances in 3 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

276: baseTokenMsgValue = 0
```
[276](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L276)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

330: numberOfLogsToProcess = 0
```
[330](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L330)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

487: txNumberInBlock = 0
```
[487](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L487)
</details>

### [G-22] Optimize Ether Transfers with `receive()` Function

Consider using `receive()` function instead of a specific `deposit()` (or similar) function.
If there are several functions in the contract that can receive Ether, it is recommended to use `receive()` for the most frequently used function.
```solidity
function deposit() external payable { // 5401 gas
    // your logic
}

receive() external payable {  // 5356 gas
    // your logic
}
```

The `receive()` or `fallback()` function can handle incoming Ether transfers directly, providing more gas-efficient way to manage deposits.

<details>
<summary><i>33 issue instances in 14 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

98: function deposit(
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte
    ) external payable returns (bytes32 l2TxHash)
133: function deposit(
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte,
        address _refundRecipient
    ) public payable nonReentrant returns (bytes32 l2TxHash)
```
[98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L98) | [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L133)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

98: function deposit(
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte
    ) external payable returns (bytes32 l2TxHash)
133: function deposit(
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte,
        address _refundRecipient
    ) public payable nonReentrant returns (bytes32 l2TxHash)
```
[98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L98) | [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L133)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

137: function receiveEth(uint256 _chainId) external payable
148: function bridgehubDepositBaseToken(
        uint256 _chainId,
        address _prevMsgSender,
        address _l1Token,
        uint256 _amount
    ) external payable virtual onlyBridgehubOrEra(_chainId)
182: function bridgehubDeposit(
        uint256 _chainId,
        address _prevMsgSender,
        uint256, // l2Value, needed for Weth deposits in the future
        bytes calldata _data
    ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request)
554: function depositLegacyErc20Bridge(
        address _prevMsgSender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte,
        address _refundRecipient
    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash)
```
[137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L137) | [148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L148) | [182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L182) | [554](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L554)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

217: function requestL2TransactionDirect(
        L2TransactionRequestDirect calldata _request
    ) external payable override nonReentrant returns (bytes32 canonicalTxHash)
262: function requestL2TransactionTwoBridges(
        L2TransactionRequestTwoBridgesOuter calldata _request
    ) external payable override nonReentrant returns (bytes32 canonicalTxHash)
```
[217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L217) | [262](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L262)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

167: function execute(Operation calldata _operation) external payable onlyOwnerOrSecurityCouncil
186: function executeInstant(Operation calldata _operation) external payable onlySecurityCouncil
```
[167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L167) | [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L186)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

47: function bridgehubRequestL2Transaction(
        BridgehubL2TransactionRequest memory _request
    ) external payable onlyBridgehub returns (bytes32 canonicalTxHash)
197: function requestL2Transaction(
        address _contractL2,
        uint256 _l2Value,
        bytes calldata _calldata,
        uint256 _l2GasLimit,
        uint256 _l2GasPerPubdataByteLimit,
        bytes[] calldata _factoryDeps,
        address _refundRecipient
    ) external payable returns (bytes32 canonicalTxHash)
```
[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L47) | [197](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L197)

```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

21: function upgrade(address _delegateTo, bytes calldata _calldata) external payable
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L21)

```solidity
File: code/system-contracts/contracts/Compressor.sol

44: function publishCompressedBytecode(
        bytes calldata _bytecode,
        bytes calldata _rawCompressedData
    ) external payable onlyCallFromBootloader returns (bytes32 bytecodeHash)
110: function verifyCompressedStateDiffs(
        uint256 _numberOfStateDiffs,
        uint256 _enumerationIndexSize,
        bytes calldata _stateDiffs,
        bytes calldata _compressedStateDiffs
    ) external payable onlyCallFrom(address(L1_MESSENGER_CONTRACT)) returns (bytes32 stateDiffHash)
```
[44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L44) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L110)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

132: function create2(
        bytes32 _salt,
        bytes32 _bytecodeHash,
        bytes calldata _input
    ) external payable override returns (address)
147: function create(
        bytes32 _salt,
        bytes32 _bytecodeHash,
        bytes calldata _input
    ) external payable override returns (address)
162: function create2Account(
        bytes32 _salt,
        bytes32 _bytecodeHash,
        bytes calldata _input,
        AccountAbstractionVersion _aaVersion
    ) public payable override onlySystemCall returns (address)
182: function createAccount(
        bytes32, // salt
        bytes32 _bytecodeHash,
        bytes calldata _input,
        AccountAbstractionVersion _aaVersion
    ) public payable override onlySystemCall returns (address)
213: function forceDeployOnAddress(ForceDeployment calldata _deployment, address _sender) external payable onlySelf
238: function forceDeployOnAddresses(ForceDeployment[] calldata _deployments) external payable
```
[132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L132) | [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L147) | [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L162) | [182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L182) | [213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L213) | [238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L238)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

67: function validateTransaction(
        bytes32, // _txHash
        bytes32 _suggestedSignedHash,
        Transaction calldata _transaction
    ) external payable override ignoreNonBootloader ignoreInDelegateCall returns (bytes4 magic)
112: function executeTransaction(
        bytes32, // _txHash
        bytes32, // _suggestedSignedHash
        Transaction calldata _transaction
    ) external payable override ignoreNonBootloader ignoreInDelegateCall
125: function executeTransactionFromOutside(Transaction calldata _transaction) external payable override
196: function payForTransaction(
        bytes32, // _txHash
        bytes32, // _suggestedSignedHash
        Transaction calldata _transaction
    ) external payable ignoreNonBootloader ignoreInDelegateCall
212: function prepareForPaymaster(
        bytes32, // _txHash
        bytes32, // _suggestedSignedHash
        Transaction calldata _transaction
    ) external payable ignoreNonBootloader ignoreInDelegateCall
```
[67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L67) | [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L112) | [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L125) | [196](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L196) | [212](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L212)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

72: function withdraw(address _l1Receiver) external payable override
85: function withdrawWithMessage(address _l1Receiver, bytes memory _additionalData) external payable override
```
[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L72) | [85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L85)

```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

35: function gasBoundCall(address _to, uint256 _maxTotalGas, bytes calldata _data) external payable
```
[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L35)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

79: function finalizeDeposit(
        address _l1Sender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        bytes calldata _data
    ) external payable override
```
[79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L79)

```solidity
File: code/contracts/zksync/contracts/ForceDeployUpgrader.sol

13: function forceDeploy(IContractDeployer.ForceDeployment[] calldata _forceDeployments) external payable
```
[13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L13)
</details>

### [G-23] Use `revert()` to gain maximum gas savings

If you dont need Error messages, or you want gain maximum gas savings - `revert()` is a cheapest way to revert transaction in terms of gas.
```solidity
    revert(); // 117 gas 
    require(false); // 132 gas
    revert CustomError(); // 157 gas
    assert(false); // 164 gas
    revert("Custom Error"); // 406 gas
    require(false, "Custom Error"); // 421 gas
```


<details>
<summary><i>352 issue instances in 46 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

64: require(msg.sender == address(sharedBridge), "Not shared bridge")
66: require(amount == _amount, "Incorrect amount")
141: require(_amount != 0, "0T")
143: require(amount == _amount, "3T")
186: require(amount != 0, "2T")
215: require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw")
```
[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L66) | [141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141) | [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L143) | [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186) | [215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L215)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

64: require(msg.sender == address(sharedBridge), "Not shared bridge")
66: require(amount == _amount, "Incorrect amount")
141: require(_amount != 0, "0T")
143: require(amount == _amount, "3T")
186: require(amount != 0, "2T")
215: require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw")
```
[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L66) | [141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141) | [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L143) | [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186) | [215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L215)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

69: require(msg.sender == address(bridgehub), "ShB not BH")
75: require(
            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
            "L1SharedBridge: not bridgehub or era chain"
        )
84: require(msg.sender == address(legacyBridge), "ShB not legacy bridge")
108: require(_owner != address(0), "ShB owner 0")
121: require(balanceAfter > balanceBefore, "ShB: 0 eth transferred")
129: require(amount > 0, "ShB: 0 amount to transfer")
132: require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred")
138: require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition")
155: require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount")
158: require(msg.value == 0, "ShB m.v > 0 b d.it")
161: require(amount == _amount, "3T")
188: require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed")
194: require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported")
195: require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported")
200: require(_depositAmount == 0, "ShB wrong withdraw amount")
202: require(msg.value == 0, "ShB m.v > 0 for BH d.it 2")
206: require(withdrawAmount == _depositAmount, "5T")
208: require(amount != 0, "6T")
237: require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap")
325: require(proofValid, "yn")
327: require(_amount > 0, "y1")
342: require(dataHash == txDataHash, "ShB: d.it not hap")
349: require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds")
360: require(callSuccess, "ShB: claimFailedDeposit failed")
396: require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal")
417: require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized")
427: require(!alreadyFinalized, "Withdrawal is already finalized 2")
439: require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2")
449: require(callSuccess, "ShB: withdraw failed")
484: require(success, "ShB withd w proof")
501: require(_l2ToL1message.length >= 56, "ShB wrong msg len")
517: require(_l2ToL1message.length == 76, "ShB wrong msg len 2")
563: require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep")
564: require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2")
522: revert("ShB Incorrect message function selector")
```
[69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69) | [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75) | [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L84) | [108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L108) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L121) | [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138) | [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L155) | [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L158) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L161) | [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188) | [194](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L194) | [195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195) | [200](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L200) | [202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202) | [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L206) | [208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L208) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L237) | [325](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L325) | [327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327) | [342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L342) | [349](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L349) | [360](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L360) | [396](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L396) | [417](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L417) | [427](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L427) | [439](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L439) | [449](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L449) | [484](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L484) | [501](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L501) | [517](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L517) | [563](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563) | [564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564) | [522](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L522)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

46: require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin")
62: require(msg.sender == currentPendingAdmin, "n42")
83: require(
            !stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition already registered"
        )
93: require(
            stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition not registered yet"
        )
102: require(!tokenIsRegistered[_token], "Bridgehub: token already registered")
122: require(_chainId != 0, "Bridgehub: chainId cannot be 0")
123: require(_chainId <= type(uint48).max, "Bridgehub: chainId too large")
125: require(
            stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition not registered"
        )
129: require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered")
130: require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set")
132: require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered")
223: require(msg.value == _request.mintValue, "Bridgehub: msg.value mismatch 1")
225: require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value")
269: require(
                    msg.value == _request.mintValue + _request.secondBridgeValue,
                    "Bridgehub: msg.value mismatch 2"
                )
275: require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3")
296: require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch")
300: require(
            _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
            "Bridgehub: second bridge address too low"
        )
```
[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62) | [83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83) | [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L93) | [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102) | [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L122) | [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123) | [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L125) | [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L129) | [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132) | [223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L223) | [225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225) | [269](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L269) | [275](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L275) | [296](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L296) | [300](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L300)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

42: require(_admin != address(0), "Admin should be non zero address")
59: require(msg.sender == address(this), "Only governance contract itself is allowed to call this function")
65: require(msg.sender == securityCouncil, "Only security council is allowed to call this function")
71: require(
            msg.sender == owner() || msg.sender == securityCouncil,
            "Only the owner and security council are allowed to call this function"
        )
155: require(isOperationPending(_id), "Operation must be pending")
172: require(isOperationReady(id), "Operation must be ready before execution")
177: require(isOperationReady(id), "Operation must be ready after execution")
191: require(isOperationPending(id), "Operation must be pending before execution")
196: require(isOperationPending(id), "Operation must be pending after execution")
216: require(!isOperation(_id), "Operation with this proposal id already exists")
217: require(_delay >= minDelay, "Proposed delay is less than minimum delay")
240: require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed")
```
[42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L42) | [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59) | [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L65) | [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L71) | [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L155) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L172) | [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L177) | [191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L191) | [196](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L196) | [216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L216) | [217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L217) | [240](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L240)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

64: require(msg.sender == bridgehub, "StateTransition: only bridgehub")
70: require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin")
82: require(_initializeData.governor != address(0), "StateTransition: governor zero")
106: assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32)
121: require(msg.sender == currentPendingAdmin, "n42")
256: require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch")
```
[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64) | [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L70) | [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L82) | [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L106) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L121) | [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L256)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62: require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin")
68: require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator")
195: require(block.timestamp >= commitBatchTimestamp + delay, "5c")
217: require(block.timestamp >= commitBatchTimestamp + delay, "5c")
80: revert AddressAlreadyValidator(_chainId)
89: revert ValidatorDoesNotExist(_chainId)
```
[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68) | [195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195) | [217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L217) | [80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L80) | [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L89)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

25: require(address(_initializeData.verifier) != address(0), "vt")
26: require(_initializeData.admin != address(0), "vy")
27: require(_initializeData.validatorTimelock != address(0), "hc")
28: require(_initializeData.priorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "vu")
51: assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32)
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L26) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27) | [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L28) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L51)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

14: require(_chainId == block.chainid, "pr")
25: require(msg.data.length >= 4 || msg.data.length == 0, "Ut")
30: require(facetAddress != address(0), "F")
31: require(!diamondStorage.isFrozen || !facet.isFreezable, "q1")
```
[14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L14) | [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25) | [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30) | [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L31)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

34: require(msg.sender == pendingAdmin, "n4")
59: require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5")
70: require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6")
90: require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis")
105: require(
            cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
            "StateTransition: cutHash mismatch"
        )
110: require(
            s.protocolVersion == _oldProtocolVersion,
            "StateTransition: protocolVersion mismatch in STC when upgrading"
        )
116: require(
            s.protocolVersion > _oldProtocolVersion,
            "StateTransition: protocolVersion mismatch in STC after upgrading"
        )
136: require(!diamondStorage.isFrozen, "a9")
146: require(diamondStorage.isFrozen, "a7")
```
[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34) | [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L59) | [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L70) | [90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90) | [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L105) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L110) | [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L116) | [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L136) | [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L146)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

37: require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f")
40: require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us")
50: require(logOutput.pubdataHash == 0x00, "v0h")
51: require(_newBatch.pubdataCommitments.length == 1)
61: require(
                logOutput.pubdataHash ==
                    keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),
                "wp"
            )
74: require(_previousBatch.batchHash == logOutput.previousBatchHash, "l")
76: require(logOutput.chainedPriorityTxsHash == _newBatch.priorityOperationsHash, "t")
78: require(logOutput.numberOfLayer1Txs == _newBatch.numberOfLayer1Txs, "ta")
110: require(batchTimestamp == _expectedBatchTimestamp, "tb")
114: require(_previousBatchTimestamp < batchTimestamp, "h3")
122: require(block.timestamp - COMMIT_TIMESTAMP_NOT_OLDER <= batchTimestamp, "h1")
123: require(lastL2BlockTimestamp <= block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA, "h2")
149: require(!_checkBit(processedLogs, uint8(logKey)), "kp")
154: require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm")
157: require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln")
160: require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb")
163: require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc")
166: require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv")
169: require(logSender == L2_BOOTLOADER_ADDRESS, "bl")
172: require(logSender == L2_BOOTLOADER_ADDRESS, "bk")
175: require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc")
178: require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd")
181: require(logSender == L2_BOOTLOADER_ADDRESS, "bu")
182: require(_expectedSystemContractUpgradeTxHash == logValue, "ut")
192: require(processedLogs == 511, "b7")
194: require(processedLogs == 1023, "b8")
226: require(
            IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
            "Executor facet: wrong protocol version"
        )
231: require(_newBatchesData.length == 1, "e4")
233: require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i")
284: require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik")
323: require(currentBatchNumber == s.totalBatchesExecuted + _executedBatchIdx + 1, "k")
324: require(
            _hashStoredBatchInfo(_storedBatch) == s.storedBatchHashes[currentBatchNumber],
            "exe10" // executing batch should be committed
        )
330: require(priorityOperationsHash == _storedBatch.priorityOperationsHash, "x")
358: require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n")
402: require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1")
407: require(
                _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
                "o1"
            )
421: require(currentTotalBatchesVerified <= s.totalBatchesCommitted, "q")
426: assert(block.chainid != 1)
442: require(proofPublicInput.length == 1, "t4")
449: require(successVerifyProof, "p")
482: require(s.totalBatchesCommitted > _newLastBatch, "v1")
483: require(_newLastBatch >= s.totalBatchesExecuted, "v2")
543: require(_batch.systemLogs.length <= MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES, "pu")
567: require(_blobCommitments.length == MAX_NUMBER_OF_BLOBS, "b10")
568: require(_blobHashes.length == MAX_NUMBER_OF_BLOBS, "b11")
616: require(success, "failed to call point evaluation precompile")
618: require(result == BLS_MODULUS, "precompile unexpected output")
631: require(_pubdataCommitments.length > 0, "pl")
632: require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd")
633: require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs")
639: require(blobVersionedHash != bytes32(0), "vh")
663: require(versionedHash == bytes32(0), "lh")
668: require(
                (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
                    (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
                "bh"
            )
681: require(success, "vc")
184: revert("ul")
```
[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L37) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L40) | [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L50) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L51) | [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L61) | [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L74) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L76) | [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L78) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L110) | [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L114) | [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L122) | [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L123) | [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L149) | [154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L154) | [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L157) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L160) | [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L163) | [166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L166) | [169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L169) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L172) | [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L175) | [178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L178) | [181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L181) | [182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L182) | [192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L192) | [194](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L194) | [226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L226) | [231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L231) | [233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L233) | [284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L284) | [323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L323) | [324](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L324) | [330](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L330) | [358](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L358) | [402](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L402) | [407](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L407) | [421](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L421) | [426](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L426) | [442](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L442) | [449](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L449) | [482](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L482) | [483](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L483) | [543](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L543) | [567](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L567) | [568](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L568) | [616](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616) | [618](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L618) | [631](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631) | [632](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L632) | [633](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L633) | [639](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L639) | [663](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L663) | [668](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L668) | [681](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L681) | [184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L184)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

183: require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2")
```
[183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

39: require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox")
110: require(_batchNumber <= s.totalBatchesExecuted, "xx")
117: require(hashedLog != L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH, "tw")
158: require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set")
185: require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox")
206: require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token")
243: require(_request.l2GasPerPubdataByteLimit == REQUIRED_L2_GAS_PRICE_PER_PUBDATA, "qp")
264: require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj")
272: require(_mintValue >= baseCost + _params.l2Value, "mv")
```
[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L110) | [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L117) | [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158) | [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L185) | [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L206) | [243](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L243) | [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L264) | [272](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L272)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

16: require(msg.sender == s.admin, "StateTransition Chain: not admin")
22: require(s.validators[msg.sender], "StateTransition Chain: not validator")
27: require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager")
32: require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub")
37: require(
            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by admin or state transition manager"
        )
45: require(
            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by validator or state transition manager"
        )
53: require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function")
```
[16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16) | [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27) | [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L37) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45) | [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

72: require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet")
190: require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong")
205: require(
            _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
            "The new protocol version should be included in the L2 system upgrade tx"
        )
223: require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps")
224: require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32")
227: require(
                L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
                "Wrong factory dep hash"
            )
238: require(
            _newProtocolVersion > previousProtocolVersion,
            "New protocol version is not greater than the current one"
        )
242: require(
            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
            "Too big protocol version difference"
        )
249: require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized")
250: require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        )
```
[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L72) | [190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L190) | [205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L205) | [223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L223) | [224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L224) | [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L227) | [238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L238) | [242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L242) | [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L249) | [250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L250)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

22: require(
            // Genesis Upgrade difference: Note this is the only thing change > to >=
            _newProtocolVersion >= previousProtocolVersion,
            "New protocol version is not greater than the current one"
        )
27: require(
            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
            "Too big protocol version difference"
        )
33: require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized")
34: require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        )
52: require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet")
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L27) | [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33) | [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L34) | [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L52)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

23: require(_bytecode.length % 32 == 0, "pq")
26: require(bytecodeLenInWords < 2 ** 16, "pp")
27: require(bytecodeLenInWords % 2 == 1, "ps")
41: require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf")
43: require(bytecodeLen(_bytecodeHash) % 2 == 1, "uy")
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L26) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L27) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L41) | [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

107: require(selectors.length > 0, "B")
132: require(_facet.code.length > 0, "G")
141: require(oldFacet.facetAddress == address(0), "J")
155: require(_facet.code.length > 0, "K")
161: require(oldFacet.facetAddress != address(0), "L")
175: require(_facet == address(0), "a1")
181: require(oldFacet.facetAddress != address(0), "a2")
215: require(_isSelectorFreezable == ds.selectorToFacet[selector0].isFreezable, "J1")
280: require(_calldata.length == 0, "H")
297: require(data.length == 32, "lp")
298: require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1")
116: revert("C")
287: revert("I")
```
[107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132) | [141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L141) | [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L155) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L161) | [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175) | [181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L181) | [215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L215) | [280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L280) | [297](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L297) | [298](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L298) | [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L116) | [287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L287)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

24: require(pathLength > 0, "xc")
25: require(pathLength < 256, "bt")
26: require(_index < (1 << pathLength), "px")
```
[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24) | [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L25) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L26)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

65: require(!_queue.isEmpty(), "D")
73: require(!_queue.isEmpty(), "s")
```
[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L65) | [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L73)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

28: require(l2GasForTxBody <= _priorityTxMaxGasLimit, "ui")
30: require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk")
34: require(
            getMinimalPriorityTransactionGasLimit(
                _encoded.length,
                _transaction.factoryDeps.length,
                _transaction.gasPerPubdataByteLimit
            ) <= l2GasForTxBody,
            "up"
        )
48: require(_transaction.from <= type(uint16).max, "ua")
49: require(_transaction.to <= type(uint160).max, "ub")
50: require(_transaction.paymaster == 0, "uc")
51: require(_transaction.value == 0, "ud")
52: require(_transaction.maxFeePerGas == 0, "uq")
53: require(_transaction.maxPriorityFeePerGas == 0, "ux")
54: require(_transaction.reserved[0] == 0, "ue")
55: require(_transaction.reserved[1] <= type(uint160).max, "uf")
56: require(_transaction.reserved[2] == 0, "ug")
57: require(_transaction.reserved[3] == 0, "uo")
58: require(_transaction.signature.length == 0, "uh")
59: require(_transaction.paymasterInput.length == 0, "ul1")
60: require(_transaction.reservedDynamic.length == 0, "um")
115: require(_totalGasLimit >= overhead, "my")
```
[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L28) | [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L30) | [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L34) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L48) | [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L49) | [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L50) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L51) | [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L52) | [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L53) | [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L54) | [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L56) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L57) | [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L58) | [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L59) | [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L60) | [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L115)

```solidity
File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

58: require(lockSlotOldValue == 0, "1B")
75: require(_status == _NOT_ENTERED, "r1")
```
[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L58) | [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L75)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

26: require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract")
37: require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor")
48: require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract")
57: require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor")
```
[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L26) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L37) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L48) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L57)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

92: require(vInt == 27 || vInt == 28, "Invalid v value")
191: require(vInt == 27 || vInt == 28, "Invalid v value")
286: require(vInt == 27 || vInt == 28, "Invalid v value")
37: revert("Unsupported tx type")
```
[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L92) | [191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L191) | [286](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L286) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L37)

```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

22: require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER")
24: require(_delegateTo.code.length > 0, "Delegatee is an EOA")
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22) | [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L24)

```solidity
File: code/system-contracts/contracts/Compressor.sol

51: require(
                encodedData.length * 4 == _bytecode.length,
                "Encoded data length should be 4 times shorter than the original bytecode"
            )
56: require(
                dictionary.length / 8 <= encodedData.length / 2,
                "Dictionary should have at most the same number of entries as the encoded data"
            )
63: require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds")
68: require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode")
119: require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large")
140: require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch")
156: require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs")
171: require(enumIndex == compressedEnumIndex, "rw: enum key mismatch")
187: require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs")
230: require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch")
232: require(
                    _initialValue + convertedValue == _finalValue,
                    "add: initial plus converted not equal to final"
                )
237: require(
                    _initialValue - convertedValue == _finalValue,
                    "sub: initial minus converted not equal to final"
                )
242: revert("unsupported operation")
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L51) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L56) | [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L63) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L68) | [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L119) | [140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L140) | [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L156) | [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L171) | [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L187) | [230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L230) | [232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L232) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L237) | [242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L242)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

29: require(msg.sender == address(this), "Callable only by self")
77: require(
            _nonceOrdering == AccountNonceOrdering.Arbitrary &&
                currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
            "It is only possible to change from sequential to arbitrary ordering"
        )
239: require(
            msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
            "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
        )
251: require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments")
264: require(_bytecodeHash != bytes32(0x0), "BytecodeHash cannot be zero")
265: require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space")
268: require(
            ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0,
            "Code hash is non-zero"
        )
273: require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied")
303: require(knownCodeMarker > 0, "The code hash is not known")
350: require(value == 0, "The value must be zero if we do not call the constructor")
```
[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29) | [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L77) | [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L239) | [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L251) | [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L264) | [265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L265) | [268](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L268) | [273](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L273) | [303](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L303) | [350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L350)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

100: require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value")
160: require(_signature.length == 65, "Signature length is incorrect")
173: require(v == 27 || v == 28, "v is neither 27 nor 28")
184: require(uint256(s) <= 0x7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF5D576E7357A4501DDFE92F46681B20A0, "Invalid s")
202: require(success, "Failed to pay the fee to the operator")
222: assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS)
```
[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L160) | [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L173) | [184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L184) | [202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L202) | [222](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L222)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

35: require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract")
```
[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

20: require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor")
76: require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash")
78: require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd")
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L20) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L76) | [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L78)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

201: require(numberOfL2ToL1Logs <= L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, "Too many L2->L1 logs")
214: require(
            reconstructedChainedLogsHash == chainedLogsHash,
            "reconstructedChainedLogsHash is not equal to chainedLogsHash"
        )
245: require(
            reconstructedChainedMessagesHash == chainedMessagesHash,
            "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
        )
269: require(
            reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
            "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
        )
279: require(
            uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
                STATE_DIFF_COMPRESSION_VERSION_NUMBER,
            "state diff compression version mismatch"
        )
298: require(calldataPtr <= MAX_ALLOWED_PUBDATA_PER_BATCH, "L1 Messenger pubdata is too long")
315: require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array")
```
[201](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L201) | [214](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L214) | [245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L245) | [269](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L269) | [279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L279) | [298](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L298) | [315](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L315)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

33: require(
            msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
                msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
                msg.sender == BOOTLOADER_FORMAL_ADDRESS,
            "Only system contracts with special access can call this method"
        )
41: require(fromBalance >= _amount, "Transfer amount exceeds balance")
```
[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L33) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L41)

```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

60: require(to != address(this), "MsgValueSimulator calls itself")
```
[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L60)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

66: require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high")
85: require(_value != 0, "Nonce value cannot be set to 0")
89: require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used")
115: require(oldMinNonce == _expectedNonce, "Incorrect nonce")
136: require(
            msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
            "Only the contract deployer can increment the deployment nonce"
        )
170: revert("Reusing the same nonce twice")
172: revert("The nonce was not set as used")
```
[66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L66) | [85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L85) | [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L89) | [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L115) | [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L136) | [170](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L170) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L172)

```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

22: require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs")
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L22)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

242: require(_isFirstInBatch, "Upgrade transaction must be first")
245: require(_l2BlockNumber > 0, "L2 block number is never expected to be zero")
249: require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect")
287: require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block")
351: require(
                _l2BlockTimestamp >= currentBatchTimestamp,
                "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
            )
355: require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch")
367: require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch")
368: require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same")
369: require(
                _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
                "The previous hash of the same L2 block must be same"
            )
373: require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock")
385: require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect")
386: require(
                _l2BlockTimestamp > currentL2BlockTimestamp,
                "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
            )
413: require(currentBatchNumber > 0, "The current batch number must be greater than 0")
429: require(
            _newTimestamp > currentBlockTimestamp,
            "The timestamp of the batch must be greater than the timestamp of the previous block"
        )
451: require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental")
452: require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct")
394: revert("Invalid new L2 block number")
```
[242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L242) | [245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L245) | [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L249) | [287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L287) | [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L351) | [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L355) | [367](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L367) | [368](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L368) | [369](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L369) | [373](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L373) | [385](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L385) | [386](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L386) | [413](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L413) | [429](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L429) | [451](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L451) | [452](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L452) | [394](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L394)

```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

46: require(_maxTotalGas >= gasleft(), "Gas limit is too low")
76: require(pubdataAllowance + gasleft() >= pubdataCost + CALL_RETURN_OVERHEAD, "Not enough gas for pubdata")
```
[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L46) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L76)

```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

38: require(returnData.length == 32, "keccak256 returned invalid data")
47: require(returnData.length == 32, "sha returned invalid data")
```
[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L38) | [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L47)

```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

50: assert(_len != 1)
```
[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L50)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

319: require(index < 10, "There are only 10 accessible registers")
350: require(precompileCallSuccess, "Failed to charge gas")
```
[319](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319) | [350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L350)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

363: require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long")
367: require(
                _transaction.paymasterInput.length >= 68,
                "The approvalBased paymaster input must be at least 68 bytes long"
            )
112: revert("Encoding unsupported tx")
388: revert("Unsupported paymaster flow")
```
[363](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L363) | [367](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L367) | [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L112) | [388](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L388)

```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

21: require(_x <= type(uint128).max, "Overflow")
27: require(_x <= type(uint32).max, "Overflow")
33: require(_x <= type(uint24).max, "Overflow")
84: require(_bytecode.length % 32 == 0, "po")
87: require(lengthInWords < 2 ** 16, "pp")
88: require(lengthInWords % 2 == 1, "pr")
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L21) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L27) | [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L33) | [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L84) | [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L87) | [88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L88)

```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

21: require(
            SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
            "This method require system call flag"
        )
31: require(
            SystemContractHelper.isSystemContract(msg.sender),
            "This method require the caller to be system contract"
        )
41: require(msg.sender == caller, "Inappropriate caller")
48: require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader")
55: require(msg.sender == FORCE_DEPLOYER)
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L21) | [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L31) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L41) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L48) | [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L55)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

55: require(_l1Bridge != address(0), "bf")
56: require(_l2TokenProxyBytecodeHash != bytes32(0), "df")
57: require(_aliasedOwner != address(0), "sf")
58: require(_l2TokenProxyBytecodeHash != bytes32(0), "df")
68: require(_l1LegecyBridge != address(0), "bf2")
87: require(
            AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
                AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
            "mq"
        )
92: require(msg.value == 0, "Value should be 0 for ERC20 bridge")
98: require(deployedToken == expectedL2Token, "mt")
101: require(currentL1Token == _l1Token, "gg")
124: require(_amount > 0, "Amount cannot be zero")
129: require(l1Token != address(0), "yh")
176: require(success, "mk")
```
[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L55) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L56) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L57) | [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L58) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L68) | [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L87) | [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92) | [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L98) | [101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L101) | [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L124) | [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L129) | [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L176)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

51: require(_l1Address != address(0), "in6")
120: require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt")
130: require(msg.sender == l2Bridge, "xnt")
137: require(_version == _getInitializedVersion() + 1, "v")
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51) | [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120) | [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L130) | [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L137)

```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

28: require(_x <= type(uint32).max, "Overflow")
```
[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L28)
</details>

### [G-24] Use local variables for emitting

Use the function/modifier's local copy of the state variable, rather than incurring an extra Gwarmaccess (100 gas).
In the unlikely event that the state variable hasn't already been used by the function/modifier, consider whether it is really necessary to include it in the event, given the fact that it incurs a Gcoldsload (2100 gas), or whether it can be passed in to or back out of the functions that do use it.

<details>
<summary><i>10 issue instances in 7 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

225: emit WithdrawalFinalized(l1Receiver, l1Token, amount)
```
[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L225)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

225: emit WithdrawalFinalized(l1Receiver, l1Token, amount)
```
[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L225)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

602: emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount)
```
[602](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L602)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

69: emit NewAdmin(previousAdmin, pendingAdmin)
```
[69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

250: emit ChangeMinDelay(minDelay, _newDelay)
257: emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil)
```
[250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L250) | [257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L257)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

128: emit NewAdmin(previousAdmin, pendingAdmin)
227: emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion)
```
[128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L128) | [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

101: emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_)
126: emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_)
```
[101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L101) | [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126)
</details>

### [G-25] `x.a = x.a + b` always cheaper than `x.a += b` for Structs

Using direct assignment operations (e.g., `x.a = x.a + b`) is more gas-efficient compared to compound assignment operations (e.g., `x.a += b`).
Examples:
```solidity
    // direct write to storage   -> 5337 gas
    // struct storage pointer    -> 5341 gas
    // memory struct             -> 4628 gas
    // memory function param     -> 1109 gas
    x.a += b;

    // direct write to storage   -> 5330 gas
    // struct storage pointer    -> 5334 gas
    // memory struct             -> 4625 gas
    // memory function param     -> 1106 gas
    x.a = struct.a + b;
```


<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: code/system-contracts/contracts/SystemContext.sol

295: virtualBlockInfo.number += _maxVirtualBlocksToCreate
```
[295](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L295)
</details>

### [G-26] Initializers can be marked as payable

Payable functions cost less gas to execute, because the compiler does not have to add extra checks to ensure that no payment is provided.
Initializers can be safely marked as payable, because only the deployer or the factory contract would call the function without carrying any funds.

<details>
<summary><i>10 issue instances in 8 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

60: function initialize() external reentrancyGuardInitializer
```
[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L60)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

60: function initialize() external reentrancyGuardInitializer
```
[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L60)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

104: function initialize(
        address _owner,
        uint256 _eraFirstPostUpgradeBatch
    ) external reentrancyGuardInitializer initializer
142: function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner
```
[104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L104) | [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L142)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

41: function initialize(address _owner) external reentrancyGuardInitializer
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L41)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

79: function initialize(
        StateTransitionManagerInitializeData calldata _initializeData
    ) external reentrancyGuardInitializer
```
[79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L79)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

24: function initialize(InitializeData calldata _initializeData) external reentrancyGuardInitializer returns (bytes32)
```
[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L24)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

49: function initialize(
        address _l1Bridge,
        address _l1LegecyBridge,
        bytes32 _l2TokenProxyBytecodeHash,
        address _aliasedOwner
    ) external reinitializer(2)
```
[49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L49)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

50: function bridgeInitialize(address _l1Address, bytes memory _data) external initializer
111: function reinitializeToken(
        ERC20Getters calldata _availableGetters,
        string memory _newName,
        string memory _newSymbol,
        uint8 _version
    ) external onlyNextVersion(_version) reinitializer(_version)
```
[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L50) | [111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L111)
</details>

### [G-27] Using `constants` instead of `enum` can save gas

`Enum` is expensive and it is [more efficient to use constants](https://www.codehawks.com/finding/clm84992q02j9w9ruebun36d9) instead.
An illustrative example of this approach can be found in the [ReentrancyGuard.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/181d518609a9f006fcb97af63e6952e603cf100e/contracts/utils/ReentrancyGuard.sol#L34-L35)

<details>
<summary><i>15 issue instances in 12 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

12: enum UpgradeState {
    None,
    Transparent,
    Shadow
}
39: enum PubdataPricingMode {
    Rollup,
    Validium
}
```
[12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L12) | [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L39)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

80: enum Action {
        Add,
        Replace,
        Remove
    }
```
[80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L80)

```solidity
File: code/contracts/ethereum/contracts/governance/IGovernance.sol

14: enum OperationState {
        Unset,
        Waiting,
        Ready,
        Done
    }
```
[14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L14)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

8: enum SystemLogKey {
    L2_TO_L1_LOGS_TREE_ROOT_KEY,
    TOTAL_L2_TO_L1_PUBDATA_KEY,
    STATE_DIFF_HASH_KEY,
    PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY,
    PREV_BATCH_HASH_KEY,
    CHAINED_PRIORITY_TXN_HASH_KEY,
    NUMBER_OF_LAYER_1_TXS_KEY,
    BLOB_ONE_HASH_KEY,
    BLOB_TWO_HASH_KEY,
    EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY
}
22: enum PubdataSource {
    Calldata,
    Blob
}
```
[8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L8) | [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L22)

```solidity
File: code/contracts/ethereum/contracts/common/Messaging.sol

8: enum TxStatus {
    Failure,
    Success
}
```
[8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L8)

```solidity
File: code/system-contracts/contracts/Constants.sol

110: enum SystemLogKey {
    L2_TO_L1_LOGS_TREE_ROOT_KEY,
    TOTAL_L2_TO_L1_PUBDATA_KEY,
    STATE_DIFF_HASH_KEY,
    PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY,
    PREV_BATCH_HASH_KEY,
    CHAINED_PRIORITY_TXN_HASH_KEY,
    NUMBER_OF_LAYER_1_TXS_KEY,
    BLOB_ONE_HASH_KEY,
    BLOB_TWO_HASH_KEY,
    EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY
}
```
[110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L110)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

24: enum Global {
    CalldataPtr,
    CallFlags,
    ExtraABIData1,
    ExtraABIData2,
    ReturndataPtr
}
```
[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L24)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

56: enum CalldataForwardingMode {
    UseHeap,
    ForwardFatPointer,
    UseAuxHeap
}
```
[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L56)

```solidity
File: code/system-contracts/contracts/interfaces/IContractDeployer.sol

11: enum AccountAbstractionVersion {
        None,
        Version1
    }
23: enum AccountNonceOrdering {
        Sequential,
        Arbitrary
    }
```
[11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IContractDeployer.sol#L11) | [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IContractDeployer.sol#L23)

```solidity
File: code/system-contracts/contracts/interfaces/IPaymaster.sol

7: enum ExecutionResult {
    Revert,
    Success
}
```
[7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IPaymaster.sol#L7)

```solidity
File: code/contracts/zksync/contracts/interfaces/IPaymaster.sol

7: enum ExecutionResult {
    Revert,
    Success
}
```
[7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L7)

```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

20: enum CalldataForwardingMode {
    UseHeap,
    ForwardFatPointer,
    UseAuxHeap
}
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L20)
</details>

### [G-28] Merging Sequential `for` Loops with Identical Conditions

Contracts with multiple sequential `for` loops with identical conditions can be merged.
Merging these loops can significantly reduce gas consumption and enhance contract performance.
While this optimization streamlines the code and improves efficiency, it's important to balance this with code clarity and maintainability.
Thorough testing is recommended to ensure the merged loops function correctly without introducing complexity or bugs.
```solidity
    // two loops 16683 gas
    // one loop  14912 gas
    for (uint256 i = 0; i < inputLen; i++) {
        // do something
    }
    for (uint256 i = 0; i < inputLen; i++) {
        emit Event(i);
    }
```

<details>
<summary><i>4 issue instances in 2 files:</i></summary>

```solidity
File: code/system-contracts/contracts/Compressor.sol

127: for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE)
159: for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE)
```
[127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L127) | [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L159)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

248: for (uint256 i = 0; i < deploymentsLength; ++i)
253: for (uint256 i = 0; i < deploymentsLength; ++i)
```
[248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L248) | [253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L253)
</details>

### [G-29] Create variable outside the loop

Creating variables inside the loop consum more gas compared to declaring them outside and just reaffecting values to them inside the loop.
```solidity
    // uint256 outsideVar = anyValue;
    for (uint256 i = 0; i < 10; i++) {
        // outsideVar = value;     // 1984 gas
        uint256 insideVar = value; // 2012 gas 
    }
```

<details>
<summary><i>48 issue instances in 9 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

186: uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
                    _newBatchesData[i].batchNumber
                )
210: uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber)
```
[186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L186) | [210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L210)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

291: bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0)
312: PriorityOperation memory priorityOp = s.priorityQueue.popFront()
412: bytes32 currentBatchCommitment = _committedBatches[i].commitment
637: bytes32 blobVersionedHash = _getBlobVersionedHash(versionedHashIndex)
643: bytes32 openingPoint = bytes32(
                uint256(uint128(bytes16(_pubdataCommitments[i:i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET])))
            )
```
[291](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L291) | [312](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L312) | [412](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L412) | [637](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L637) | [643](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L643)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

209: address facetAddr = ds.facets[i]
210: Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr]
```
[209](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L209) | [210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L210)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

357: bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i])
```
[357](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L357)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

102: Action action = facetCuts[i].action
103: address facet = facetCuts[i].facet
104: bool isFacetFreezable = facetCuts[i].isFreezable
105: bytes4[] memory selectors = facetCuts[i].selectors
139: bytes4 selector = _selectors[i]
140: SelectorToFacet memory oldFacet = ds.selectorToFacet[selector]
159: bytes4 selector = _selectors[i]
160: SelectorToFacet memory oldFacet = ds.selectorToFacet[selector]
179: bytes4 selector = _selectors[i]
180: SelectorToFacet memory oldFacet = ds.selectorToFacet[selector]
```
[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L102) | [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L103) | [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L104) | [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L105) | [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L139) | [140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L140) | [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L159) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L160) | [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L179) | [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L180)

```solidity
File: code/system-contracts/contracts/Compressor.sol

62: uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8
65: uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk)
66: uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4)
128: bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE]
129: uint64 enumIndex = stateDiff.readUint64(84)
137: bytes32 derivedKey = stateDiff.readBytes32(52)
138: uint256 initValue = stateDiff.readUint256(92)
139: uint256 finalValue = stateDiff.readUint256(124)
143: uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]))
145: uint8 operation = metadata & OPERATION_BITMASK
146: uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET
160: bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE]
161: uint64 enumIndex = stateDiff.readUint64(84)
166: uint256 initValue = stateDiff.readUint256(92)
167: uint256 finalValue = stateDiff.readUint256(124)
168: uint256 compressedEnumIndex = _sliceToUint256(
                _compressedStateDiffs[stateDiffPtr:stateDiffPtr + _enumerationIndexSize]
            )
174: uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]))
176: uint8 operation = metadata & OPERATION_BITMASK
177: uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET
```
[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L62) | [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L65) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L66) | [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L128) | [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L129) | [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L137) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L138) | [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L139) | [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L143) | [145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L145) | [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L146) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L160) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L161) | [166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L166) | [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L167) | [168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L168) | [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L174) | [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L176) | [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L177)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

39: uint256 index = _immutables[i].index
40: bytes32 value = _immutables[i].value
```
[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L39) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L40)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

207: bytes32 hashedLog = EfficientCall.keccak(
                _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + L2_TO_L1_LOG_SERIALIZE_SIZE]
            )
224: uint256 i = 0
237: uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]))
239: bytes32 hashedMessage = EfficientCall.keccak(
                _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentMessageLength]
            )
255: uint32 currentBytecodeLength = uint32(
                bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])
            )
```
[207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L207) | [224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L224) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L237) | [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L239) | [255](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L255)

```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

37: uint256 start = BLOB_SIZE_BYTES * i
45: bytes32 blobHash
```
[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L37) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L45)
</details>

### [G-30] Use `assembly` in place of `abi.decode` to extract calldata values more efficiently

Instead of using abi.decode, we can use assembly to decode our desired calldata values directly.
This will allow us to avoid decoding calldata values that we will not use.
[More details](https://code4rena.com/reports/2023-05-juicebox#g-04-use-assembly-in-place-of-abidecode-to-extract-calldata-values-more-efficiently)

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

617: (, uint256 result) = abi.decode(data, (uint256, uint256))
```
[617](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L617)
</details>

### [G-31] Do not cache `constant`s to save gas

Using `constant` variables directly in your functions is the most gas-efficient approach, as Solidity's compiler optimizes their usage.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

88: bytes32 position = DIAMOND_STORAGE_POSITION
```
[88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L88)
</details>

### [G-32] Shorten the array rather than copying to a new on

In Solidity, harnessing inline assembly empowers you to modify an array's length slot directly, obviating the need to duplicate elements into a new array of the desired size.
This method shines in terms of gas efficiency, as it sidesteps the computational overhead tied to array replication.
However, it's important to exercise caution when using this technique, as it bypasses the type-checking and safety features of high-level Solidity.

Always exercise due diligence to ensure that the array doesn't contain critical data beyond the adjusted length.
Data exceeding the new length will become inaccessible, yet it will still occupy storage space.

<details>
<summary><i>4 issue instances in 3 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

578: blobAuxOutputWords = new bytes32[](2 * TOTAL_BLOBS_IN_COMMITMENT)
634: blobCommitments = new bytes32[](MAX_NUMBER_OF_BLOBS)
```
[578](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L578) | [634](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L634)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

206: result = new Facet[](facetsLen)
```
[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L206)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

355: hashedFactoryDeps = new uint256[](factoryDepsLen)
```
[355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L355)
</details>

### [G-33] Nested for loops should be avoided due to high gas costs resulting from O^2 time complexity

In Solidity, avoiding nested for loops is a recommended practice primarily due to the high gas costs associated with them.
These loops can lead to quadratic (O^2) time complexity, especially when they iterate over large data sets or perform complex computations.
Since every operation in a smart contract consumes gas, and users pay for this gas, optimizing for lower gas usage is crucial.
Nested loops, which inherently have higher computational complexity, can significantly increase the gas costs of a contract.
To optimize for efficiency, it's advisable to minimize the use of loops, limit their range, and reduce computations within each loop iteration.
Alternative patterns like map/filter/reduce might often be cheaper than traditional for loops in terms of gas usage

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

224: for (uint256 i = 0; i < nodesOnCurrentLevel; ++i)
```
[224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L224)
</details>

### [G-34] Using `delete` on a `bool` variable is cheaper than assigning it to `false`

```solidity
function test() external {
    delete bar; // 5184 gas
    bar = false; // 5208 gas
}
```

<details>
<summary><i>3 issue instances in 3 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

97: stateTransitionManagerIsRegistered[_stateTransitionManager] = false
```
[97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L97)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

91: validators[_chainId][_validator] = false
```
[91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L91)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

147: diamondStorage.isFrozen = false
```
[147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L147)
</details>

### [G-35] Expression ("") is cheaper than `new bytes(0)`

In Solidity, using an empty string ("") instead of `new bytes(0)` in expressions can result in cheaper gas costs.
This is because `new bytes(0)` creates a dynamic byte array, leading to additional overhead.
By simply using ("") when an empty bytes array is needed, you can optimize for gas efficiency.
```solidity
function test() external {
    // bytes memory foo = ""; // 170 gas
    // bytes memory foo = new bytes(0); // 241 gas
    // abi.encodePacked("string", new bytes(0), "6"); // 904 gas
    // abi.encodePacked("string", "", "6"); // 674 gas
}
```


<details>
<summary><i>8 issue instances in 2 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

196: new bytes(0)
198: new bytes(0)
199: new bytes(0)
213: new bytes(0)
214: new bytes(0)
```
[196](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L196) | [198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L198) | [199](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L199) | [213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L213) | [214](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L214)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

308: new bytes(0)
310: new bytes(0)
311: new bytes(0)
```
[308](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L308) | [310](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L310) | [311](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L311)
</details>

### [G-36] Use `Array.unsafeAccess()` to avoid repeated array length checks

When using storage arrays, solidity adds an internal lookup of the array's length (a Gcoldsload 2100 gas) to ensure you don't read past the array's end.
You can avoid this lookup by using `Array.unsafeAccess()` in cases where the length has already been checked, as is the case with the instances below.

<details>
<summary><i>11 issue instances in 5 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

225: for (uint256 i = 0; i < _calls.length; ++i) {
```
[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L225)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
135: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
185: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
209: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```
[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116) | [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135) | [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185) | [209](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

142: for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
257: for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
289: for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
636: for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {
```
[142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142) | [257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257) | [289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289) | [636](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226: for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226)

```solidity
File: code/system-contracts/contracts/Compressor.sol

61: for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
```
[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L61)
</details>

### [G-37] Counting down when iterating, saves gas

Counting down saves 6 gas per loop, since checks for zero are more efficient than checks against any other value.

<details>
<summary><i>18 issue instances in 9 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

225: for (uint256 i = 0; i < _calls.length; ++i) {
```
[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L225)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
135: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
185: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
209: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```
[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116) | [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135) | [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185) | [209](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

580: for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
667: for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580) | [667](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226: for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

248: for (uint256 i = 0; i < deploymentsLength; ++i) {
253: for (uint256 i = 0; i < deploymentsLength; ++i) {
```
[248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L248) | [253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L253)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

38: for (uint256 i = 0; i < immutablesLength; ++i) {
```
[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L38)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

30: for (uint256 i = 0; i < hashesLen; ++i) {
```
[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L30)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

206: for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {
218: for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {
224: for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {
236: for (uint256 i = 0; i < numberOfMessages; ++i) {
254: for (uint256 i = 0; i < numberOfBytecodes; ++i) {
```
[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206) | [218](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L218) | [224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L224) | [236](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L236) | [254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L254)

```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

36: for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)
</details>

### [G-38] `>=` costs less gas than `>`

The compiler uses opcodes GT and ISZERO for solidity code that uses >, but only requires LT for >=, which saves 3 gas. If < is being used, the condition can be inverted.
In cases where a for-loop is being used, one can count down rather than up, in order to use the optimal operator.

<details>
<summary><i>24 issue instances in 12 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

129: require(amount > 0, "ShB: 0 amount to transfer");
327: require(_amount > 0, "y1");
```
[129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129) | [327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

329: } else if (_refundRecipient.code.length > 0) {
```
[329](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L329)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

429: if (_proof.serializedProof.length > 0) {
593: return (_bitMap & (1 << _index)) > 0;
631: require(_pubdataCommitments.length > 0, "pl");
```
[429](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L429) | [593](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L593) | [631](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

158: require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");
277: if (refundRecipient.code.length > 0) {
```
[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158) | [277](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L277)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

107: require(selectors.length > 0, "B"); // no functions for diamond cut
132: require(_facet.code.length > 0, "G");
155: require(_facet.code.length > 0, "K");
```
[107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132) | [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L155)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

24: require(pathLength > 0, "xc");
```
[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

102: if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {
```
[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L102)

```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

24: require(_delegateTo.code.length > 0, "Delegatee is an EOA");
```
[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L24)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

303: require(knownCodeMarker > 0, "The code hash is not known");
332: if (value > 0) {
339: if (value > 0) {
```
[303](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L303) | [332](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L332) | [339](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L339)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

156: return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);
```
[156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L156)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

152: currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0
245: require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");
287: require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");
355: require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");
413: require(currentBatchNumber > 0, "The current batch number must be greater than 0");
```
[152](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L152) | [245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L245) | [287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L287) | [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L355) | [413](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L413)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

124: require(_amount > 0, "Amount cannot be zero");
```
[124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L124)
</details>

### [G-39] Consider pre-calculating the address of `address(this)` to save gas

Use foundry's script.sol or solady's LibRlp.sol to save the value in a constant, which will avoid having to spend gas to push the value on the stack every time it's used.

<details>
<summary><i>22 issue instances in 13 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

65: uint256 amount = IERC20(_token).balanceOf(address(this));
```
[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

65: uint256 amount = IERC20(_token).balanceOf(address(this));
```
[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

118: uint256 balanceBefore = address(this).balance;
120: uint256 balanceAfter = address(this).balance;
127: uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
131: uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
174: uint256 balanceBefore = _token.balanceOf(address(this));
175: _token.safeTransferFrom(_from, address(this), _amount);
176: uint256 balanceAfter = _token.balanceOf(address(this));
```
[118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118) | [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120) | [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127) | [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131) | [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L174) | [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175) | [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

59: require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
```
[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

265: bytes32(uint256(uint160(address(this)))),
```
[265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L265)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

41: uint256 amount = address(this).balance;
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

29: require(msg.sender == address(this), "Callable only by self");
333: BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo(address(this), _newAddress, value);
```
[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29) | [333](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L333)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

47: if (codeAddress != address(this)) {
100: require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");
188: return recoveredAddress == address(this) && recoveredAddress != address(0);
```
[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L47) | [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100) | [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L188)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

129: sender: address(this),
```
[129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L129)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

106: balance[address(this)] -= amount;
```
[106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L106)

```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

60: require(to != address(this), "MsgValueSimulator calls itself");
```
[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L60)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

377: uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);
```
[377](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

153: L2ContractHelper.computeCreate2Address(address(this), salt, l2TokenProxyBytecodeHash, constructorInputHash);
```
[153](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L153)
</details>

### [G-40] Use `unchecked` for Non-Loop Increment/Decrement Operations

Disclaimer: `You should be sure that underflow is not possible `
Using `unchecked` increments can save gas by bypassing the built-in overflow checks.
This can save 30-40 gas per iteration.
It is recommended to use unchecked increments when overflow is not possible.

<details>
<summary><i>6 issue instances in 2 files:</i></summary>

```solidity
File: code/system-contracts/contracts/Compressor.sol

135: numInitialWritesProcessed++
144: stateDiffPtr++
```
[135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L135) | [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L144)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

109: numberOfLogsToProcess++
224: ++i
284: calldataPtr++
290: calldataPtr++
```
[109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L109) | [224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L224) | [284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L284) | [290](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L290)
</details>

### [G-41] Using `this` to access functions results in an external call, wasting gas

Using `this.<fn>()` to call an external function from within the contract unnecessarily wastes gas. This is because calling an external function requires a gas overhead of 100 gas.

Instead, you can reduce the gas cost by making the function public and calling it directly without `this`. The Ethereum Virtual Machine (EVM) does not require additional gas for calling public functions internally.

Always aim for efficient gas usage when writing Solidity contracts to optimize for cost and performance.

<details>
<summary><i>8 issue instances in 5 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

118: uint256 balanceBefore = address(this).balance;
120: uint256 balanceAfter = address(this).balance;
```
[118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118) | [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

41: uint256 amount = address(this).balance;
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

254: this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
```
[254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L254)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

100: require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");
```
[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

75: try this.decodeString(nameBytes) returns (string memory nameString) {
81: try this.decodeString(symbolBytes) returns (string memory symbolString) {
93: try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {
```
[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L75) | [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L81) | [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L93)
</details>

### [G-42] Constructors can be marked `payable`

Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided.

A constructor can safely be marked as `payable`, since only the deployer would be able to pass funds, and the project itself would not pass any funds. 
T
his could save an average of about 21 gas per call, in addition to the extra deployment cost.

<details>
<summary><i>11 issue instances in 10 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

55: constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
55: constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
```
[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55) | [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

90: constructor(
        address _l1WethAddress,
        IBridgehub _bridgehub,
        IL1ERC20Bridge _legacyBridge
    ) reentrancyGuardInitializer {
```
[90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

38: constructor() reentrancyGuardInitializer {}
```
[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

41: constructor(address _admin, address _securityCouncil, uint256 _minDelay) {
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L41)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

58: constructor(address _bridgehub) reentrancyGuardInitializer {
```
[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

54: constructor(address _initialOwner, uint32 _executionDelay) {
```
[54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L54)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

19: constructor() reentrancyGuardInitializer {}
```
[19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

11: constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
```
[11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

41: constructor() {
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L41)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

40: constructor() {
```
[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L40)
</details>

### [G-43] Multiple accesses of a mapping/array should use a local variable cache

Leveraging a local variable to cache these values when accessed more than once can yield a gas saving of approximately 42 units per access.
This reduction is attributed to eliminating the need for recalculating the key's keccak256 hash (which costs Gkeccak256 - 30 gas) and the associated stack operations.
For arrays, this also prevents the overhead of re-computing offsets in memory or calldata.

<details>
<summary><i>20 issue instances in 2 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

/// @audit `chainBalance[_targetChainId]` is used 4 times
122: chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
123: chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
133: chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
133: chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
/// @audit `l2BridgeAddress[_chainId]` is used 2 times
188: require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
221: l2Contract: l2BridgeAddress[_chainId],
/// @audit `depositHappened[_chainId]` is used 2 times
237: require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");
238: depositHappened[_chainId][_txHash] = _txDataHash;
/// @audit `chainBalance[_chainId]` is used 2 times
349: require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
350: chainBalance[_chainId][_l1Token] -= _amount;
/// @audit `isWithdrawalFinalized[_chainId]` is used 2 times
417: require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");
418: isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true;
/// @audit `chainBalance[_chainId]` is used 2 times
439: require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds
440: chainBalance[_chainId][l1Token] -= amount;
/// @audit `l2BridgeAddress[ERA_CHAIN_ID]` is used 2 times
563: require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
586: l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
```
[122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L122) | [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L123) | [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133) | [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133) | [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188) | [221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L221) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L237) | [238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L238) | [349](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L349) | [350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L350) | [417](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L417) | [418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L418) | [439](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L439) | [440](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L440) | [563](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563) | [586](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L586)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

/// @audit `validators[_chainId]` is used 2 times
79: if (validators[_chainId][_newValidator]) {
82: validators[_chainId][_newValidator] = true;
/// @audit `validators[_chainId]` is used 2 times
88: if (!validators[_chainId][_validator]) {
91: validators[_chainId][_validator] = false;
```
[79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L79) | [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L82) | [88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L88) | [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L91)
</details>

### [G-44] Optimize Increment and Decrement in loops with `unchecked` keyword

Use `unchecked{i++}` or `unchecked{++i}` instead of `i++` or `++i` when it is not possible for them to overflow.
This is applicable for Solidity version `0.8.0` or higher to `0.8.23` and saves 30-40 gas per loop.

<details>
<summary><i>28 issue instances in 9 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

225: for (uint256 i = 0; i < _calls.length; ++i) {
```
[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L225)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
135: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
185: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
209: for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```
[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116) | [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135) | [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185) | [209](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

580: for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
636: for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {
667: for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580) | [636](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636) | [667](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226: for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

248: for (uint256 i = 0; i < deploymentsLength; ++i) {
248: for (uint256 i = 0; i < deploymentsLength; ++i) {
253: for (uint256 i = 0; i < deploymentsLength; ++i) {
```
[248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L248) | [248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L248) | [253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L253)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

38: for (uint256 i = 0; i < immutablesLength; ++i) {
```
[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L38)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

30: for (uint256 i = 0; i < hashesLen; ++i) {
```
[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L30)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

206: for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {
206: for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {
206: for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {
206: for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {
206: for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {
218: for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {
218: for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {
218: for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {
218: for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {
224: for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {
236: for (uint256 i = 0; i < numberOfMessages; ++i) {
236: for (uint256 i = 0; i < numberOfMessages; ++i) {
254: for (uint256 i = 0; i < numberOfBytecodes; ++i) {
```
[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206) | [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206) | [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206) | [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206) | [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206) | [218](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L218) | [218](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L218) | [218](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L218) | [218](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L218) | [224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L224) | [236](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L236) | [236](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L236) | [254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L254)

```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

36: for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)
</details>

### [G-45] Reduce gas usage by moving to Solidity 0.8.19 or later

See [this](https://soliditylang.org/blog/2023/02/22/solidity-0.8.19-release-announcement/#preventing-dead-code-in-runtime-bytecode) link for the full details. Additionally, every new release has new optimizations, which will save gas.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol

2: pragma solidity ^0.8.0;
```
[2](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L2)
</details>

### [G-46] Reduce deployment costs by tweaking contracts' metadata

The Solidity compiler appends 53 bytes of metadata to the smart contract code which translates to an extra 10,600 gas (200 per bytecode) + the calldata cost (16 gas per non-zero bytes, 4 gas per zero-byte).
This translates to up to 848 additional gas in calldata cost.
One way to reduce this cost is by optimizing the IPFS hash that gets appended to the smart contract code.

Why is this important?
- The metadata adds an extra 53 bytes, resulting in an additional 10,600 gas cost for deployment.
- It also incurs up to 848 additional gas in calldata cost.

Options to Reduce Gas:
1. Use the `--no-cbor-metadata` compiler option to exclude metadata, but this might affect contract verification.
2. Mine for code comments that lead to an IPFS hash with more zeros, reducing calldata costs.

<details>
<summary><i>106 issue instances in 105 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

1: Consider optimizing the IPFS hash during deployment.
1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L1) | [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/governance/IGovernance.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/common/Config.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/common/L2ContractAddresses.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/common/Messaging.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L1)

```solidity
File: code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L1)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L1)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L1)

```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L1)

```solidity
File: code/system-contracts/contracts/Compressor.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L1)

```solidity
File: code/system-contracts/contracts/Constants.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L1)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L1)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L1)

```solidity
File: code/system-contracts/contracts/EmptyContract.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/EmptyContract.sol#L1)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L1)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L1)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L1)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L1)

```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L1)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L1)

```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L1)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L1)

```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L1)

```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L1)

```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L1)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L1)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L1)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L1)

```solidity
File: code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L1)

```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IAccount.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IAccount.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IAccountCodeStorage.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IAccountCodeStorage.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IBaseToken.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IBaseToken.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IBootloaderUtilities.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IBootloaderUtilities.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IComplexUpgrader.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IComplexUpgrader.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/ICompressor.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ICompressor.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IContractDeployer.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IContractDeployer.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IImmutableSimulator.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IImmutableSimulator.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IKnownCodesStorage.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IKnownCodesStorage.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IL1Messenger.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IL1Messenger.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IL2StandardToken.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IL2StandardToken.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IMailbox.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IMailbox.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/INonceHolder.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/INonceHolder.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IPaymaster.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IPaymaster.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IPaymasterFlow.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IPaymasterFlow.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/IPubdataChunkPublisher.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IPubdataChunkPublisher.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/ISystemContext.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/ISystemContextDeprecated.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContextDeprecated.sol#L1)

```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L1)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L1)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L1)

```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L1)

```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L1)

```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L1)

```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L1)

```solidity
File: code/contracts/zksync/contracts/interfaces/IPaymaster.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L1)

```solidity
File: code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L1)

```solidity
File: code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L1)

```solidity
File: code/contracts/zksync/contracts/ForceDeployUpgrader.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L1)

```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L1)

```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L1)
</details>

### [G-47] Use Pre-Increment/Decrement (++i/--i) to Save Gas

Using pre-increment (++i) or pre-decrement (--i) operators is more gas-efficient compared to their post counterparts (i++ or i--).
This is because pre-increment/decrement operators avoid the need for an additional temporary variable that stores the original value of the iterator.
This subtle difference results in saving of around 5 gas units per operation, which can accumulate to substantial savings in gas costs in contracts with frequent increment/decrement operations.

<details>
<summary><i>8 issue instances in 4 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

580: for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
667: for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580) | [667](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)

```solidity
File: code/system-contracts/contracts/Compressor.sol

135: numInitialWritesProcessed++;
144: stateDiffPtr++;
```
[135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L135) | [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L144)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

109: numberOfLogsToProcess++;
284: calldataPtr++;
290: calldataPtr++;
```
[109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L109) | [284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L284) | [290](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L290)

```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

36: for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
[36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)
</details>

### [G-48] Nesting `if`-statements is cheaper than using `&&`

Optimization of condition checks in your smart contract is a crucial aspect in ensuring gas efficiency. Specifically, substituting multiple `&&` checks with nested `if` statements can lead to substantial gas savings.

When evaluating multiple conditions within a single `if` statement using the `&&` operator, each condition will consume gas even if a preceding condition fails. However, if these checks are broken down into nested `if` statements, execution halts as soon as a condition fails, saving the gas that would have been consumed by subsequent checks.

This practice is especially beneficial in scenarios where the `if` statement isn't followed by an `else` statement. The reason being, when an `else` statement is present, all conditions must be checked regardless to determine the correct branch of execution.

By reworking your code to utilize nested `if` statements, you can optimize gas usage, reduce execution cost, and enhance your contract's performance.

<details>
<summary><i>8 issue instances in 5 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

361: if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {
```
[361](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L361)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

102: if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {
```
[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L102)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

139: if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) {
```
[139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L139)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

88: if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {
169: if (isUsed && !_shouldBeUsed) {
171: } else if (!isUsed && _shouldBeUsed) {
```
[88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L88) | [169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L169) | [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L171)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

277: if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
360: if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {
```
[277](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L277) | [360](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L360)
</details>

### [G-49] Use `storage` instead of `memory` for state structs/arrays

When fetching data from storage, assigning it to a memory variable causes all fields of the struct/array to be read from storage, incurring a Gcoldsload (2100 gas) for each field.
Reading fields from the new memory variable incurs an additional MLOAD rather than a cheap stack read.

Instead, declare variables with the storage keyword and cache any fields that need to be re-read in stack variables.
This approach is more cost-efficient, only incurring the Gcoldsload for fields actually read.

The only time it makes sense to read the whole struct/array into a memory variable is if the full struct/array is being returned by the function, passed to a function that requires memory, or read from another memory array/struct.

<details>
<summary><i>20 issue instances in 8 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

27: Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L27)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

72: FeeParams memory oldFeeParams = s.feeParams;
```
[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L72)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

135: bytes memory emittedL2Logs = _newBatch.systemLogs;
312: PriorityOperation memory priorityOp = s.priorityQueue.popFront();
396: VerifierParams memory verifierParams = s.verifierParams;
```
[135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L135) | [312](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L312) | [396](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L396)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

157: FeeParams memory feeParams = s.feeParams;
323: bytes memory transactionEncoding = abi.encode(transaction);
```
[157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L157) | [323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L323)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

155: VerifierParams memory oldVerifierParams = s.verifierParams;
192: bytes memory encodedTransaction = abi.encode(_l2ProtocolUpgradeTx);
```
[155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L155) | [192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L192)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

97: FacetCut[] memory facetCuts = _diamondCut.facetCuts;
99: bytes memory initCalldata = _diamondCut.initCalldata;
105: bytes4[] memory selectors = facetCuts[i].selectors;
140: SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
160: SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
180: SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
```
[97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L97) | [99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L99) | [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L105) | [140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L140) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L160) | [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L180)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

75: AccountInfo memory currentInfo = accountInfo[msg.sender];
```
[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L75)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

135: VirtualBlockUpgradeInfo memory currentVirtualBlockUpgradeInfo = virtualBlockUpgradeInfo;
173: BlockInfo memory batchInfo = currentBatchInfo;
181: BlockInfo memory blockInfo = currentL2BlockInfo;
275: BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;
```
[135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L135) | [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L173) | [181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L181) | [275](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L275)
</details>

### [G-50] Optimize by Using Assembly for Low-Level Calls' Return Data

Even second return value from a low-level call is not assigned, it is still copied to memory, leading to additional gas costs.
By employing assembly, you can bypass this memory copying, achieving a 159 gas saving.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

63: (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call(
```
[63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L63)
</details>

### [G-51] Store `keccak256()` Hash in Immutable Variable

`keccak256()` should only need to be called on a specific string literal once. 
It should be saved to an immutable variable, and the variable used instead.
If the hash is being used as a part of a function selector, the cast to `bytes4` should also only be done once.

<details>
<summary><i>3 issue instances in 2 files:</i></summary>

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

139: abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
139: abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
```
[139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139) | [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139)

```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

85: bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");
```
[85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L85)
</details>

### [G-52] Cache Function Calls for Efficiency

Function calls, especially external function calls, can be quite expensive in terms of gas. 
If you need to retrieve the same data more than once in a function, it is more efficient to call 
the function once, store the result in a local variable, and then use that variable later in the 
code instead of making the function call again.

<details>
<summary><i>21 issue instances in 5 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

161: uint256 balanceBefore = _token.balanceOf(address(sharedBridge));
163: uint256 balanceAfter = _token.balanceOf(address(sharedBridge));
161: uint256 balanceBefore = _token.balanceOf(address(sharedBridge));
163: uint256 balanceAfter = _token.balanceOf(address(sharedBridge));
```
[161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L161) | [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L163) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L161) | [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L163)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

174: uint256 balanceBefore = _token.balanceOf(address(this));
176: uint256 balanceAfter = _token.balanceOf(address(this));
506: (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
518: (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
519: (l1Token, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
507: (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);
520: (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);
```
[174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L174) | [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176) | [506](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L506) | [518](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L518) | [519](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L519) | [507](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L507) | [520](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L520)

```solidity
File: code/system-contracts/contracts/Compressor.sol

129: uint64 enumIndex = stateDiff.readUint64(84);
161: uint64 enumIndex = stateDiff.readUint64(84);
138: uint256 initValue = stateDiff.readUint256(92);
166: uint256 initValue = stateDiff.readUint256(92);
139: uint256 finalValue = stateDiff.readUint256(124);
167: uint256 finalValue = stateDiff.readUint256(124);
```
[129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L129) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L161) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L138) | [166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L166) | [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L139) | [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L167)

```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

51: uint256 pubdataPublishedBefore = REAL_SYSTEM_CONTEXT_CONTRACT.getCurrentPubdataSpent();
59: uint256 pubdataPublishedAfter = REAL_SYSTEM_CONTEXT_CONTRACT.getCurrentPubdataSpent();
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L51) | [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L59)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

88: AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
89: AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
```
[88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L88) | [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L89)
</details>

### [G-53] Superfluous Event Fields

Event logs in the Ethereum Virtual Machine (EVM) automatically include certain block data such as the `block.timestamp` and `block.number`.
Explicitly including these values in your event arguments results in superfluous data that unnecessarily consumes gas.
This redundancy not only leads to higher execution costs for your smart contract functions but also increases the amount of data stored on the Ethereum blockchain, which in turn, inflates storage and processing requirements for all participating nodes. 

By removing these redundant fields from your events, you can potentially save a significant amount of gas.
This optimization will not only make your smart contract more efficient but also more cost-effective to execute.
This practice emphasizes the importance of optimizing smart contract code to achieve maximum efficiency and minimal gas costs, contributing to the sustainability of the Ethereum ecosystem.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

343: emit NewPriorityRequest(
            _priorityOpParams.txId,
            canonicalTxHash,
            _priorityOpParams.expirationTimestamp,
            transaction,
            _factoryDeps
        );
```
[343](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L343)
</details>

### [G-54] Unutilized Named Return Variables Waste Gas Without Optimizer

Utilizing named return variables without assignment or explicit return in functions can lead to unnecessary gas costs without an active optimizer.
To enhance gas efficiency, you might consider opting for unnamed return variables, especially when they aren't explicitly used or returned.
Keeping the current configuration without an active optimizer can result in extra gas costs associated with superfluous stack variables.

<details>
<summary><i>7 issue instances in 7 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

/// @audit - Redundant `return _chainId;` statement in functions with named return variables
114: function createNewChain(
        uint256 _chainId,
        address _stateTransitionManager,
        address _baseToken,
        uint256, //_salt
        address _admin,
        bytes calldata _initData
    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
```
[114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

117: function getCodeSize(uint256 _input) external view override returns (uint256 codeSize) {
```
[117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L117)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

/// @audit - Redundant `return
            keccak256(
                bytes.concat(
                    encodedListLength,
                    encodedNonce,
                    encodedGasParam,
                    encodedTo,
                    encodedValue,
                    encodedDataLength,
                    _transaction.data,
                    vEncoded,
                    rEncoded,
                    sEncoded
                )
            );` statement in functions with named return variables
44: function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {
```
[44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L44)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

/// @audit - Redundant `return accountInfo[_address];` statement in functions with named return variables
34: function getAccountInfo(address _address) external view returns (AccountInfo memory info) {
```
[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L34)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

/// @audit - Redundant `return deploymentNonce;` statement in functions with named return variables
125: function getDeploymentNonce(address _address) external view returns (uint256 deploymentNonce) {
```
[125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L125)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

132: function getBlockHashEVM(uint256 _block) external view returns (bytes32 hash) {
```
[132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L132)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

164: function _deployBeaconProxy(bytes32 salt) internal returns (BeaconProxy proxy) {
```
[164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L164)
</details>

### [G-55] Use `unchecked` for Math Operations if they already checked

Some subtraction operations in the contract have implicit checks that prevent underflow. 
To optimize gas, consider wrapping such operations in an `unchecked` block. 
Always review the logic thoroughly before making changes to ensure the safety of operations.

<details>
<summary><i>6 issue instances in 6 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

/// @audit - mathematical operation `balanceAfter - balanceBefore` checked above in line:
/// 121: require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");
132: require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
```
[132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

/// @audit - mathematical operation `_newProtocolVersion - previousProtocolVersion` checked above in line:
/// 238: require(
            _newProtocolVersion > previousProtocolVersion,
            "New protocol version is not greater than the current one"
        );
243: _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
```
[243](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L243)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

/// @audit - mathematical operation `_newProtocolVersion - previousProtocolVersion` checked above in line:
/// 22: require(
            // Genesis Upgrade difference: Note this is the only thing change > to >=
            _newProtocolVersion >= previousProtocolVersion,
            "New protocol version is not greater than the current one"
        );
28: _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
```
[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L28)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

/// @audit - mathematical operation `_totalGasLimit - overhead` checked above in line:
/// 115: require(_totalGasLimit >= overhead, "my"); // provided gas limit doesn't cover transaction overhead
118: txBodyGasLimit = _totalGasLimit - overhead;
```
[118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L118)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

/// @audit - mathematical operation `fromBalance - _amount` checked above in line:
/// 41: require(fromBalance >= _amount, "Transfer amount exceeds balance");
43: balance[_from] = fromBalance - _amount;
```
[43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L43)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

/// @audit - mathematical operation `previousBatchNumber + 1` checked above in line:
/// 452: require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
459: BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp});
```
[459](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L459)
</details>

### [G-56] Using `private` rather than `public`, saves gas

Public storage variables increase the contract's size due to the implicit generation of public getter functions. 
This makes the contract larger and could increase deployment and interaction costs.

If you do not require other contracts to read these variables, consider making them `private`. 

Example:
```solidity
/// 145426 gas to deploy
contract PublicState {
    address public first;
    address public second;
}
/// 77126 gas to deploy
contract PrivateState {
    address private first;
    address private second;
}
```

<details>
<summary><i>59 issue instances in 14 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

23: IL1SharedBridge public immutable override sharedBridge;
27: mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
        public isWithdrawalFinalized;
32: mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
        public depositAmount;
36: address public l2Bridge;
39: address public l2TokenBeacon;
42: bytes32 public l2TokenProxyBytecodeHash;
23: IL1SharedBridge public immutable override sharedBridge;
27: mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
        public isWithdrawalFinalized;
32: mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
        public depositAmount;
36: address public l2Bridge;
39: address public l2TokenBeacon;
42: bytes32 public l2TokenProxyBytecodeHash;
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L23) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27) | [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L32) | [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L36) | [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L39) | [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L42) | [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L23) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27) | [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L32) | [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L36) | [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L39) | [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L42)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

34: address public immutable override l1WethAddress;
37: IBridgehub public immutable override bridgehub;
40: IL1ERC20Bridge public immutable override legacyBridge;
48: mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;
52: mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
        public
        override depositHappened;
57: mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
        public isWithdrawalFinalized;
```
[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L34) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L37) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L40) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L48) | [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L52) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

18: IL1SharedBridge public sharedBridge;
21: mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;
23: mapping(address _token => bool) public tokenIsRegistered;
26: mapping(uint256 _chainId => address) public stateTransitionManager;
29: mapping(uint256 _chainId => address) public baseToken;
32: address public admin;
```
[18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L18) | [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21) | [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L23) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L26) | [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L29) | [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L32)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

26: address public securityCouncil;
32: mapping(bytes32 operationId => uint256 executionTimestamp) public timestamps;
35: uint256 public minDelay;
```
[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L26) | [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L32) | [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L35)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

27: address public immutable bridgehub;
30: mapping(uint256 => address) public stateTransition;
33: bytes32 public storedBatchZero;
36: bytes32 public initialCutHash;
39: address public genesisUpgrade;
42: uint256 public protocolVersion;
45: address public validatorTimelock;
48: mapping(uint256 => bytes32) public upgradeCutHash;
51: address public admin;
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L27) | [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L30) | [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L33) | [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L36) | [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L39) | [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L42) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L45) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L48) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L51)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

26: string public constant override getName = "ValidatorTimelock";
44: IStateTransitionManager public stateTransitionManager;
50: mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
53: uint32 public executionDelay;
```
[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26) | [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L44) | [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50) | [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L53)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

20: string public constant override getName = "AdminFacet";
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

27: string public constant override getName = "ExecutorFacet";
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

25: string public constant override getName = "GettersFacet";
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

35: string public constant override getName = "MailboxFacet";
```
[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

23: uint256 public override totalSupply;
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L23)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

26: uint256 public chainId;
30: address public origin;
34: uint256 public gasPrice;
37: uint256 public blockGasLimit = type(uint32).max;
41: address public coinbase = BOOTLOADER_FORMAL_ADDRESS;
44: uint256 public difficulty = 2.5e15;
48: uint256 public baseFee;
89: uint16 public txNumberInBlock;
92: uint256 public gasPerPubdataByte;
```
[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L26) | [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L30) | [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L34) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L37) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L41) | [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L44) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L48) | [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L89) | [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L92)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

25: address public override l1Bridge;
29: UpgradeableBeacon public l2TokenBeacon;
35: mapping(address l2TokenAddress => address l1TokenAddress) public override l1TokenAddress;
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L25) | [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L29) | [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L35)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

34: address public override l2Bridge;
37: address public override l1Address;
```
[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L34) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L37)
</details>

### [G-57] Use Assembly for Hash Calculations

In certain cases, using inline assembly to calculate hashes can lead to significant gas savings. Solidity's built-in keccak256 function is convenient but costs more gas than the equivalent assembly code. However, it's important to note that using assembly should be done with care as it's less readable and could increase the risk of introducing errors.

<details>
<summary><i>60 issue instances in 17 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

76: bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
76: bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
```
[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

210: bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));
341: bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));
598: bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
```
[210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L210) | [341](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L341) | [598](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L598)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

205: return keccak256(abi.encode(_operation));
```
[205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L205)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

100: storedBatchZero = keccak256(abi.encode(batchZero));
102: initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));
138: initialCutHash = keccak256(abi.encode(_diamondCut));
147: upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
156: upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
255: bytes32 cutHashInput = keccak256(_diamondCut);
```
[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100) | [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138) | [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L147) | [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L156) | [255](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L255)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

104: bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
```
[104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

63: keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),
313: concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));
460: keccak256(
506: bytes32 passThroughDataHash = keccak256(_batchPassThroughData(_newBatchData));
507: bytes32 metadataHash = keccak256(_batchMetaParameters());
508: bytes32 auxiliaryOutputHash = keccak256(
512: return keccak256(abi.encode(passThroughDataHash, metadataHash, auxiliaryOutputHash));
545: bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs);
588: return keccak256(abi.encode(_storedBatchInfo));
654: blobCommitments[versionedHashIndex] = keccak256(
```
[63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L63) | [313](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313) | [460](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L460) | [506](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L506) | [507](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L507) | [508](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L508) | [512](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L512) | [545](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L545) | [588](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L588) | [654](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L654)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

112: bytes32 hashedLog = keccak256(
138: value: keccak256(_message.data)
332: canonicalTxHash = keccak256(transactionEncoding);
```
[112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L112) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L138) | [332](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L332)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

212: bytes32 l2ProtocolUpgradeTxHash = keccak256(encodedTransaction);
```
[212](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L212)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

67: bytes32 data = keccak256(
```
[67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L67)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

18: 0x33774e659306e47509050e97cb651e731180a42d458212294d30751925c551a2; // keccak256("diamond.zksync.init") - 1
22: 0xc8fcad8db84d3cc18b4c41d551ea0ee66dd599cde068d998e57d5e09332c131b; // keccak256("diamond.standard.diamond.storage") - 1;
```
[18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L18) | [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L22)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

29: txHash = keccak256(bytes.concat(signedTxHash, EfficientCall.keccak(_transaction.signature)));
120: keccak256(
211: keccak256(
306: keccak256(
```
[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L29) | [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L120) | [211](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L211) | [306](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L306)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

105: bytes32 hash = keccak256(
121: bytes32 hash = keccak256(
```
[105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L105) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L121)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

95: bytes32 hashedLog = keccak256(
106: chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));
122: chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));
164: chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));
212: reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));
225: l2ToL1LogsTreeArray[i] = keccak256(
243: reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));
259: reconstructedChainedL1BytecodesRevealDataHash = keccak256(
```
[95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L95) | [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L106) | [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L122) | [164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L164) | [212](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L212) | [225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L225) | [243](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L243) | [259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L259)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

159: hash = keccak256(abi.encode(_block));
227: return keccak256(abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash));
234: return keccak256(abi.encodePacked(uint32(_blockNumber)));
403: currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));
```
[159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L159) | [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L227) | [234](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L234) | [403](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L403)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

85: keccak256(
119: bytes32 structHash = keccak256(
133: keccak256(abi.encodePacked(_transaction.factoryDeps)),
138: bytes32 domainSeparator = keccak256(
139: abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
139: abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
142: return keccak256(abi.encodePacked("\x19\x01", domainSeparator, structHash));
203: keccak256(
275: keccak256(
347: keccak256(
```
[85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L85) | [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L119) | [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L133) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L138) | [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139) | [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139) | [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L142) | [203](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L203) | [275](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L275) | [347](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L347)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

150: bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""));
```
[150](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150)

```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

108: bytes32 data = keccak256(
```
[108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L108)
</details>

### [G-58] Refactor duplicated require()/revert() checks to save gas

Duplicate require()/revert() checks can be refactored into a modifier or function, saving deployment costs.

<details>
<summary><i>7 issue instances in 3 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

195: require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
217: require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
```
[195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195) | [217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L217)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

92: require(vInt == 27 || vInt == 28, "Invalid v value");
191: require(vInt == 27 || vInt == 28, "Invalid v value");
286: require(vInt == 27 || vInt == 28, "Invalid v value");
```
[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L92) | [191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L191) | [286](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L286)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

56: require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
58: require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
```
[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L56) | [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L58)
</details>

### [G-59] Use Assembly for Efficient Memory Management in Multiple External Calls

When making multiple external calls in a Solidity contract, it may be more efficient to use inline assembly to reuse the memory space allocated for function arguments and return data.
This can prevent unnecessary memory expansion and reduce gas costs.

Example:
```solidity
contract Solidity {
    // cost: 7262
    function call(address calledAddress) external pure returns(uint256) {
        Called called = Called(calledAddress);
        uint256 res1 = called.add(1, 2);
        uint256 res2 = called.add(3, 4);

        uint256 res = res1 + res2;
        return res;
    }
}

contract Assembly {
    // cost: 5281
    function call(address calledAddress) external view returns(uint256) {
        assembly {
            // check that calledAddress has code deployed to it
            if iszero(extcodesize(calledAddress)) {
                revert(0x00, 0x00)
            }

            // first call
            mstore(0x00, hex"771602f7")
            mstore(0x04, 0x01)
            mstore(0x24, 0x02)
            let success := staticcall(gas(), calledAddress, 0x00, 0x44, 0x60, 0x20)
            if iszero(success) {
                revert(0x00, 0x00)
            }
            let res1 := mload(0x60)

            // second call
            mstore(0x04, 0x03)
            mstore(0x24, 0x4)
            success := staticcall(gas(), calledAddress, 0x00, 0x44, 0x60, 0x20)
            if iszero(success) {
                revert(0x00, 0x00)
            }
            let res2 := mload(0x60)

            // add results
            let res := add(res1, res2)

            // return data
            mstore(0x60, res)
            return(0x60, 0x20)
        }
    }
}
```

<details>
<summary><i>17 issue instances in 3 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

/// @audit function `tranferTokenToSharedBridge()` has multiple external calls
65: uint256 amount = IERC20(_token).balanceOf(address(this));
67: IERC20(_token).safeTransfer(address(sharedBridge), amount);
/// @audit function `tranferTokenToSharedBridge()` has multiple external calls
65: uint256 amount = IERC20(_token).balanceOf(address(this));
67: IERC20(_token).safeTransfer(address(sharedBridge), amount);
```
[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65) | [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67) | [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65) | [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

/// @audit function `transferFundsFromLegacy()` has multiple external calls
127: uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
128: uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
130: IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);
131: uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
/// @audit function `_claimFailedDeposit()` has multiple external calls
316: bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
                _chainId,
                _l2TxHash,
                _l2BatchNumber,
                _l2MessageIndex,
                _l2TxNumberInBatch,
                _merkleProof,
                TxStatus.Failure
            );
362: IERC20(_l1Token).safeTransfer(_depositSender, _amount);
/// @audit function `_finalizeWithdrawal()` has multiple external calls
423: bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
                _l2BatchNumber,
                _l2MessageIndex
            );
452: IERC20(l1Token).safeTransfer(l1Receiver, amount);
/// @audit function `_checkWithdrawal()` has multiple external calls
467: bool baseTokenWithdrawal = (l1Token == bridgehub.baseToken(_chainId));
477: bool success = bridgehub.proveL2MessageInclusion(
            _chainId,
            _messageParams.l2BatchNumber,
            _messageParams.l2MessageIndex,
            l2ToL1Message,
            _merkleProof
        );
```
[127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127) | [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L128) | [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L130) | [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131) | [316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L316) | [362](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L362) | [423](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L423) | [452](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L452) | [467](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L467) | [477](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L477)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

/// @audit function `processPaymasterInput()` has multiple external calls
377: uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);
382: IERC20(token).safeApprove(paymaster, 0);
383: IERC20(token).safeApprove(paymaster, minAllowance);
```
[377](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377) | [382](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L382) | [383](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L383)
</details>

### [G-60] Optimize `require/revert` Statements with Assembly

Using inline assembly for revert statements in Solidity can offer gas optimizations.
The typical `require` or `revert` statements in Solidity perform additional memory operations and type checks which can be avoided by using low-level assembly code.

In certain contracts, particularly those that might revert often or are otherwise sensitive to gas costs, using assembly to handle reversion can offer meaningful savings.
These savings primarily come from avoiding memory expansion costs and extra type checks that the Solidity compiler performs.

Example:
```solidity
/// calling restrictedAction(2) with a non-owner address: 24042
function restrictedAction(uint256 num)  external {
    require(owner == msg.sender, "caller is not owner");
    specialNumber = num;
}

// calling restrictedAction(2) with a non-owner address: 23734
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
```

<details>
<summary><i>340 issue instances in 43 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

64: require(msg.sender == address(sharedBridge), "Not shared bridge");
66: require(amount == _amount, "Incorrect amount");
141: require(_amount != 0, "0T"); // empty deposit
143: require(amount == _amount, "3T"); // The token has non-standard transfer logic
186: require(amount != 0, "2T"); // empty deposit
215: require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw");
64: require(msg.sender == address(sharedBridge), "Not shared bridge");
66: require(amount == _amount, "Incorrect amount");
141: require(_amount != 0, "0T"); // empty deposit
143: require(amount == _amount, "3T"); // The token has non-standard transfer logic
186: require(amount != 0, "2T"); // empty deposit
215: require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw");
```
[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L66) | [141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141) | [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L143) | [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186) | [215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L215) | [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L66) | [141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141) | [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L143) | [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186) | [215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L215)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

69: require(msg.sender == address(bridgehub), "ShB not BH");
75: require(
            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
            "L1SharedBridge: not bridgehub or era chain"
        );
84: require(msg.sender == address(legacyBridge), "ShB not legacy bridge");
108: require(_owner != address(0), "ShB owner 0");
121: require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");
129: require(amount > 0, "ShB: 0 amount to transfer");
132: require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
138: require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");
155: require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");
158: require(msg.value == 0, "ShB m.v > 0 b d.it");
161: require(amount == _amount, "3T"); // The token has non-standard transfer logic
188: require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
194: require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");
195: require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");
200: require(_depositAmount == 0, "ShB wrong withdraw amount");
202: require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
206: require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic
208: require(amount != 0, "6T"); // empty deposit amount
237: require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");
325: require(proofValid, "yn");
327: require(_amount > 0, "y1");
342: require(dataHash == txDataHash, "ShB: d.it not hap");
349: require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
396: require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");
417: require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");
427: require(!alreadyFinalized, "Withdrawal is already finalized 2");
439: require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds
484: require(success, "ShB withd w proof"); // withdrawal wrong proof
501: require(_l2ToL1message.length >= 56, "ShB wrong msg len"); // wrong messsage length
517: require(_l2ToL1message.length == 76, "ShB wrong msg len 2");
522: revert("ShB Incorrect message function selector");
563: require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
564: require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
```
[69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69) | [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75) | [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L84) | [108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L108) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L121) | [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138) | [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L155) | [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L158) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L161) | [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188) | [194](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L194) | [195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195) | [200](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L200) | [202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202) | [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L206) | [208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L208) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L237) | [325](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L325) | [327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327) | [342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L342) | [349](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L349) | [396](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L396) | [417](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L417) | [427](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L427) | [439](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L439) | [484](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L484) | [501](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L501) | [517](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L517) | [522](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L522) | [563](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563) | [564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

46: require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");
62: require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights
83: require(
            !stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition already registered"
        );
93: require(
            stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition not registered yet"
        );
102: require(!tokenIsRegistered[_token], "Bridgehub: token already registered");
122: require(_chainId != 0, "Bridgehub: chainId cannot be 0");
123: require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");
125: require(
            stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition not registered"
        );
129: require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");
130: require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
132: require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");
223: require(msg.value == _request.mintValue, "Bridgehub: msg.value mismatch 1");
225: require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");
269: require(
                    msg.value == _request.mintValue + _request.secondBridgeValue,
                    "Bridgehub: msg.value mismatch 2"
                );
275: require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3");
296: require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch");
300: require(
            _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
            "Bridgehub: second bridge address too low"
        ); // to avoid calls to precompiles
```
[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62) | [83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83) | [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L93) | [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102) | [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L122) | [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123) | [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L125) | [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L129) | [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132) | [223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L223) | [225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225) | [269](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L269) | [275](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L275) | [296](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L296) | [300](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L300)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

42: require(_admin != address(0), "Admin should be non zero address");
59: require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
65: require(msg.sender == securityCouncil, "Only security council is allowed to call this function");
71: require(
            msg.sender == owner() || msg.sender == securityCouncil,
            "Only the owner and security council are allowed to call this function"
        );
155: require(isOperationPending(_id), "Operation must be pending");
172: require(isOperationReady(id), "Operation must be ready before execution");
177: require(isOperationReady(id), "Operation must be ready after execution");
191: require(isOperationPending(id), "Operation must be pending before execution");
196: require(isOperationPending(id), "Operation must be pending after execution");
216: require(!isOperation(_id), "Operation with this proposal id already exists");
217: require(_delay >= minDelay, "Proposed delay is less than minimum delay");
```
[42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L42) | [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59) | [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L65) | [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L71) | [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L155) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L172) | [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L177) | [191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L191) | [196](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L196) | [216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L216) | [217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L217)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

64: require(msg.sender == bridgehub, "StateTransition: only bridgehub");
70: require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");
82: require(_initializeData.governor != address(0), "StateTransition: governor zero");
121: require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights
256: require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");
```
[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64) | [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L70) | [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L82) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L121) | [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L256)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62: require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");
68: require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
195: require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
217: require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
```
[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68) | [195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195) | [217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L217)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

25: require(address(_initializeData.verifier) != address(0), "vt");
26: require(_initializeData.admin != address(0), "vy");
27: require(_initializeData.validatorTimelock != address(0), "hc");
28: require(_initializeData.priorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "vu");
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L26) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27) | [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L28)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

14: require(_chainId == block.chainid, "pr");
25: require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
30: require(facetAddress != address(0), "F"); // Proxy has no facet for this selector
31: require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen
```
[14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L14) | [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25) | [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30) | [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L31)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

34: require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights
59: require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");
70: require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");
90: require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed
105: require(
            cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
            "StateTransition: cutHash mismatch"
        );
110: require(
            s.protocolVersion == _oldProtocolVersion,
            "StateTransition: protocolVersion mismatch in STC when upgrading"
        );
116: require(
            s.protocolVersion > _oldProtocolVersion,
            "StateTransition: protocolVersion mismatch in STC after upgrading"
        );
136: require(!diamondStorage.isFrozen, "a9"); // diamond proxy is frozen already
146: require(diamondStorage.isFrozen, "a7"); // diamond proxy is not frozen
```
[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34) | [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L59) | [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L70) | [90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90) | [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L105) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L110) | [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L116) | [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L136) | [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L146)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

37: require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f"); // only commit next batch
40: require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us");
50: require(logOutput.pubdataHash == 0x00, "v0h");
51: require(_newBatch.pubdataCommitments.length == 1);
61: require(
                logOutput.pubdataHash ==
                    keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),
                "wp"
            );
74: require(_previousBatch.batchHash == logOutput.previousBatchHash, "l");
76: require(logOutput.chainedPriorityTxsHash == _newBatch.priorityOperationsHash, "t");
78: require(logOutput.numberOfLayer1Txs == _newBatch.numberOfLayer1Txs, "ta");
110: require(batchTimestamp == _expectedBatchTimestamp, "tb");
114: require(_previousBatchTimestamp < batchTimestamp, "h3");
122: require(block.timestamp - COMMIT_TIMESTAMP_NOT_OLDER <= batchTimestamp, "h1"); // New batch timestamp is too small
123: require(lastL2BlockTimestamp <= block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA, "h2"); // The last L2 block timestamp is too big
149: require(!_checkBit(processedLogs, uint8(logKey)), "kp");
154: require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");
157: require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");
160: require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");
163: require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");
166: require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");
169: require(logSender == L2_BOOTLOADER_ADDRESS, "bl");
172: require(logSender == L2_BOOTLOADER_ADDRESS, "bk");
175: require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");
178: require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");
181: require(logSender == L2_BOOTLOADER_ADDRESS, "bu");
182: require(_expectedSystemContractUpgradeTxHash == logValue, "ut");
184: revert("ul");
192: require(processedLogs == 511, "b7");
194: require(processedLogs == 1023, "b8");
226: require(
            IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
            "Executor facet: wrong protocol version"
        );
231: require(_newBatchesData.length == 1, "e4");
233: require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data
284: require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");
323: require(currentBatchNumber == s.totalBatchesExecuted + _executedBatchIdx + 1, "k"); // Execute batches in order
324: require(
            _hashStoredBatchInfo(_storedBatch) == s.storedBatchHashes[currentBatchNumber],
            "exe10" // executing batch should be committed
        );
330: require(priorityOperationsHash == _storedBatch.priorityOperationsHash, "x"); // priority operations hash does not match to expected
358: require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.
402: require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");
407: require(
                _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
                "o1"
            );
421: require(currentTotalBatchesVerified <= s.totalBatchesCommitted, "q");
442: require(proofPublicInput.length == 1, "t4");
449: require(successVerifyProof, "p"); // Proof verification fail
482: require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch
483: require(_newLastBatch >= s.totalBatchesExecuted, "v2"); // Already executed batches cannot be reverted
543: require(_batch.systemLogs.length <= MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES, "pu");
567: require(_blobCommitments.length == MAX_NUMBER_OF_BLOBS, "b10");
568: require(_blobHashes.length == MAX_NUMBER_OF_BLOBS, "b11");
616: require(success, "failed to call point evaluation precompile");
618: require(result == BLS_MODULUS, "precompile unexpected output");
631: require(_pubdataCommitments.length > 0, "pl");
632: require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");
633: require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");
639: require(blobVersionedHash != bytes32(0), "vh");
663: require(versionedHash == bytes32(0), "lh");
668: require(
                (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
                    (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
                "bh"
            );
681: require(success, "vc");
```
[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L37) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L40) | [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L50) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L51) | [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L61) | [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L74) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L76) | [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L78) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L110) | [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L114) | [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L122) | [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L123) | [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L149) | [154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L154) | [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L157) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L160) | [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L163) | [166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L166) | [169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L169) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L172) | [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L175) | [178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L178) | [181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L181) | [182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L182) | [184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L184) | [192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L192) | [194](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L194) | [226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L226) | [231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L231) | [233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L233) | [284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L284) | [323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L323) | [324](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L324) | [330](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L330) | [358](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L358) | [402](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L402) | [407](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L407) | [421](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L421) | [442](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L442) | [449](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L449) | [482](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L482) | [483](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L483) | [543](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L543) | [567](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L567) | [568](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L568) | [616](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616) | [618](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L618) | [631](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631) | [632](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L632) | [633](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L633) | [639](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L639) | [663](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L663) | [668](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L668) | [681](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L681)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

183: require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");
```
[183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

39: require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");
110: require(_batchNumber <= s.totalBatchesExecuted, "xx");
117: require(hashedLog != L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH, "tw");
158: require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");
185: require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");
206: require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");
243: require(_request.l2GasPerPubdataByteLimit == REQUIRED_L2_GAS_PRICE_PER_PUBDATA, "qp");
264: require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj");
272: require(_mintValue >= baseCost + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost
```
[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L110) | [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L117) | [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158) | [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L185) | [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L206) | [243](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L243) | [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L264) | [272](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L272)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

16: require(msg.sender == s.admin, "StateTransition Chain: not admin");
22: require(s.validators[msg.sender], "StateTransition Chain: not validator");
27: require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");
32: require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");
37: require(
            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by admin or state transition manager"
        );
45: require(
            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by validator or state transition manager"
        );
53: require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
```
[16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16) | [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27) | [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L37) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45) | [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

72: require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");
190: require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");
205: require(
            _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
            "The new protocol version should be included in the L2 system upgrade tx"
        );
223: require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");
224: require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");
227: require(
                L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
                "Wrong factory dep hash"
            );
238: require(
            _newProtocolVersion > previousProtocolVersion,
            "New protocol version is not greater than the current one"
        );
242: require(
            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
            "Too big protocol version difference"
        );
249: require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
250: require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        );
```
[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L72) | [190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L190) | [205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L205) | [223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L223) | [224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L224) | [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L227) | [238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L238) | [242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L242) | [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L249) | [250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L250)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

22: require(
            // Genesis Upgrade difference: Note this is the only thing change > to >=
            _newProtocolVersion >= previousProtocolVersion,
            "New protocol version is not greater than the current one"
        );
27: require(
            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
            "Too big protocol version difference"
        );
33: require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
34: require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        );
52: require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L27) | [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33) | [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L34) | [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L52)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

23: require(_bytecode.length % 32 == 0, "pq");
26: require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words
27: require(bytecodeLenInWords % 2 == 1, "ps"); // bytecode length in words must be odd
41: require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash
43: require(bytecodeLen(_bytecodeHash) % 2 == 1, "uy"); // Code length in words must be odd
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L26) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L27) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L41) | [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

107: require(selectors.length > 0, "B"); // no functions for diamond cut
116: revert("C"); // undefined diamond cut action
132: require(_facet.code.length > 0, "G");
141: require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists
155: require(_facet.code.length > 0, "K");
161: require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address
175: require(_facet == address(0), "a1"); // facet address must be zero
181: require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet
215: require(_isSelectorFreezable == ds.selectorToFacet[selector0].isFreezable, "J1");
280: require(_calldata.length == 0, "H"); // Non-empty calldata for zero address
287: revert("I"); // delegatecall failed
```
[107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107) | [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L116) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132) | [141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L141) | [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L155) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L161) | [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175) | [181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L181) | [215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L215) | [280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L280) | [287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L287)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

24: require(pathLength > 0, "xc");
25: require(pathLength < 256, "bt");
26: require(_index < (1 << pathLength), "px");
```
[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24) | [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L25) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L26)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

65: require(!_queue.isEmpty(), "D"); // priority queue is empty
73: require(!_queue.isEmpty(), "s"); // priority queue is empty
```
[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L65) | [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L73)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

28: require(l2GasForTxBody <= _priorityTxMaxGasLimit, "ui");
30: require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");
34: require(
            getMinimalPriorityTransactionGasLimit(
                _encoded.length,
                _transaction.factoryDeps.length,
                _transaction.gasPerPubdataByteLimit
            ) <= l2GasForTxBody,
            "up"
        );
48: require(_transaction.from <= type(uint16).max, "ua");
49: require(_transaction.to <= type(uint160).max, "ub");
50: require(_transaction.paymaster == 0, "uc");
51: require(_transaction.value == 0, "ud");
52: require(_transaction.maxFeePerGas == 0, "uq");
53: require(_transaction.maxPriorityFeePerGas == 0, "ux");
54: require(_transaction.reserved[0] == 0, "ue");
55: require(_transaction.reserved[1] <= type(uint160).max, "uf");
56: require(_transaction.reserved[2] == 0, "ug");
57: require(_transaction.reserved[3] == 0, "uo");
58: require(_transaction.signature.length == 0, "uh");
59: require(_transaction.paymasterInput.length == 0, "ul1");
60: require(_transaction.reservedDynamic.length == 0, "um");
115: require(_totalGasLimit >= overhead, "my"); // provided gas limit doesn't cover transaction overhead
```
[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L28) | [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L30) | [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L34) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L48) | [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L49) | [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L50) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L51) | [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L52) | [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L53) | [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L54) | [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L56) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L57) | [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L58) | [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L59) | [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L60) | [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L115)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

26: require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
37: require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");
48: require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");
57: require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");
```
[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L26) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L37) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L48) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L57)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

37: revert("Unsupported tx type");
92: require(vInt == 27 || vInt == 28, "Invalid v value");
191: require(vInt == 27 || vInt == 28, "Invalid v value");
286: require(vInt == 27 || vInt == 28, "Invalid v value");
```
[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L37) | [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L92) | [191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L191) | [286](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L286)

```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

22: require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");
24: require(_delegateTo.code.length > 0, "Delegatee is an EOA");
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22) | [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L24)

```solidity
File: code/system-contracts/contracts/Compressor.sol

51: require(
                encodedData.length * 4 == _bytecode.length,
                "Encoded data length should be 4 times shorter than the original bytecode"
            );
56: require(
                dictionary.length / 8 <= encodedData.length / 2,
                "Dictionary should have at most the same number of entries as the encoded data"
            );
63: require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");
68: require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");
119: require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");
140: require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");
156: require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");
171: require(enumIndex == compressedEnumIndex, "rw: enum key mismatch");
187: require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");
230: require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");
232: require(
                    _initialValue + convertedValue == _finalValue,
                    "add: initial plus converted not equal to final"
                );
237: require(
                    _initialValue - convertedValue == _finalValue,
                    "sub: initial minus converted not equal to final"
                );
242: revert("unsupported operation");
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L51) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L56) | [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L63) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L68) | [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L119) | [140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L140) | [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L156) | [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L171) | [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L187) | [230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L230) | [232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L232) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L237) | [242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L242)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

29: require(msg.sender == address(this), "Callable only by self");
77: require(
            _nonceOrdering == AccountNonceOrdering.Arbitrary &&
                currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
            "It is only possible to change from sequential to arbitrary ordering"
        );
239: require(
            msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
            "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
        );
251: require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");
264: require(_bytecodeHash != bytes32(0x0), "BytecodeHash cannot be zero");
265: require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");
268: require(
            ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0,
            "Code hash is non-zero"
        );
273: require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied");
303: require(knownCodeMarker > 0, "The code hash is not known");
350: require(value == 0, "The value must be zero if we do not call the constructor");
```
[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29) | [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L77) | [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L239) | [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L251) | [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L264) | [265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L265) | [268](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L268) | [273](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L273) | [303](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L303) | [350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L350)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

100: require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");
160: require(_signature.length == 65, "Signature length is incorrect");
202: require(success, "Failed to pay the fee to the operator");
```
[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L160) | [202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L202)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

35: require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

20: require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");
76: require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
78: require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd");
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L20) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L76) | [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L78)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

201: require(numberOfL2ToL1Logs <= L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, "Too many L2->L1 logs");
214: require(
            reconstructedChainedLogsHash == chainedLogsHash,
            "reconstructedChainedLogsHash is not equal to chainedLogsHash"
        );
245: require(
            reconstructedChainedMessagesHash == chainedMessagesHash,
            "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
        );
269: require(
            reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
            "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
        );
279: require(
            uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
                STATE_DIFF_COMPRESSION_VERSION_NUMBER,
            "state diff compression version mismatch"
        );
298: require(calldataPtr <= MAX_ALLOWED_PUBDATA_PER_BATCH, "L1 Messenger pubdata is too long");
315: require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");
```
[201](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L201) | [214](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L214) | [245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L245) | [269](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L269) | [279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L279) | [298](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L298) | [315](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L315)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

33: require(
            msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
                msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
                msg.sender == BOOTLOADER_FORMAL_ADDRESS,
            "Only system contracts with special access can call this method"
        );
41: require(fromBalance >= _amount, "Transfer amount exceeds balance");
```
[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L33) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L41)

```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

60: require(to != address(this), "MsgValueSimulator calls itself");
67: // If the transfer of ETH fails, we do the most Ethereum-like behaviour in such situation: revert(0,0)
            if (!success) {
                assembly {
                    revert(0, 0)
                }
            }

            // If value is non-zero, we also provide additional gas to the callee.
            userGas += GAS_TO_PASS;
```
[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L60) | [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L67)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

66: require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");
85: require(_value != 0, "Nonce value cannot be set to 0");
89: require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");
115: require(oldMinNonce == _expectedNonce, "Incorrect nonce");
136: require(
            msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
            "Only the contract deployer can increment the deployment nonce"
        );
170: revert("Reusing the same nonce twice");
172: revert("The nonce was not set as used");
```
[66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L66) | [85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L85) | [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L89) | [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L115) | [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L136) | [170](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L170) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L172)

```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

22: require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L22)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

242: require(_isFirstInBatch, "Upgrade transaction must be first");
245: require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");
249: require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");
287: require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");
351: require(
                _l2BlockTimestamp >= currentBatchTimestamp,
                "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
            );
355: require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");
367: require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");
368: require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");
369: require(
                _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
                "The previous hash of the same L2 block must be same"
            );
373: require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");
385: require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");
386: require(
                _l2BlockTimestamp > currentL2BlockTimestamp,
                "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
            );
394: revert("Invalid new L2 block number");
413: require(currentBatchNumber > 0, "The current batch number must be greater than 0");
429: require(
            _newTimestamp > currentBlockTimestamp,
            "The timestamp of the batch must be greater than the timestamp of the previous block"
        );
451: require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");
452: require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
```
[242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L242) | [245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L245) | [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L249) | [287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L287) | [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L351) | [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L355) | [367](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L367) | [368](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L368) | [369](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L369) | [373](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L373) | [385](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L385) | [386](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L386) | [394](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L394) | [413](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L413) | [429](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L429) | [451](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L451) | [452](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L452)

```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

46: require(_maxTotalGas >= gasleft(), "Gas limit is too low");
76: require(pubdataAllowance + gasleft() >= pubdataCost + CALL_RETURN_OVERHEAD, "Not enough gas for pubdata");
```
[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L46) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L76)

```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

38: require(returnData.length == 32, "keccak256 returned invalid data");
47: require(returnData.length == 32, "sha returned invalid data");
```
[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L38) | [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L47)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

319: require(index < 10, "There are only 10 accessible registers");
350: require(precompileCallSuccess, "Failed to charge gas");
```
[319](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319) | [350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L350)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

112: revert("Encoding unsupported tx");
363: require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");
367: require(
                _transaction.paymasterInput.length >= 68,
                "The approvalBased paymaster input must be at least 68 bytes long"
            );
388: revert("Unsupported paymaster flow");
```
[112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L112) | [363](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L363) | [367](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L367) | [388](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L388)

```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

21: require(_x <= type(uint128).max, "Overflow");
27: require(_x <= type(uint32).max, "Overflow");
33: require(_x <= type(uint24).max, "Overflow");
84: require(_bytecode.length % 32 == 0, "po");
87: require(lengthInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words
88: require(lengthInWords % 2 == 1, "pr"); // bytecode length in words must be odd
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L21) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L27) | [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L33) | [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L84) | [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L87) | [88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L88)

```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

21: require(
            SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
            "This method require system call flag"
        );
31: require(
            SystemContractHelper.isSystemContract(msg.sender),
            "This method require the caller to be system contract"
        );
41: require(msg.sender == caller, "Inappropriate caller");
48: require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");
55: require(msg.sender == FORCE_DEPLOYER);
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L21) | [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L31) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L41) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L48) | [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L55)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

55: require(_l1Bridge != address(0), "bf");
56: require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
57: require(_aliasedOwner != address(0), "sf");
58: require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
68: require(_l1LegecyBridge != address(0), "bf2");
87: require(
            AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
                AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
            "mq"
        );
92: require(msg.value == 0, "Value should be 0 for ERC20 bridge");
98: require(deployedToken == expectedL2Token, "mt");
101: require(currentL1Token == _l1Token, "gg"); // Double check that the expected value equal to real one
124: require(_amount > 0, "Amount cannot be zero");
129: require(l1Token != address(0), "yh");
176: require(success, "mk");
```
[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L55) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L56) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L57) | [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L58) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L68) | [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L87) | [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92) | [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L98) | [101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L101) | [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L124) | [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L129) | [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L176)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

51: require(_l1Address != address(0), "in6"); // Should be non-zero address
120: require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");
130: require(msg.sender == l2Bridge, "xnt"); // Only L2 bridge can call this method
137: require(_version == _getInitializedVersion() + 1, "v");
161: if (availableGetters.ignoreName) revert();
167: if (availableGetters.ignoreSymbol) revert();
173: if (availableGetters.ignoreDecimals) revert();
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51) | [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120) | [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L130) | [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L137) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L161) | [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167) | [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173)

```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

28: require(_x <= type(uint32).max, "Overflow");
```
[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L28)
</details>

### [G-61] Cached Global Variables

Storing global variables in local storage might appear as a useful caching mechanism. 
However, in Solidity, accessing global variables directly is often more gas-efficient than caching them. 
Consider removing these redundant assignments and use the global variables directly.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

329: uint256 value = msg.value;
```
[329](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L329)
</details>

### [G-62] Simple checks for zero `uint` can be done using `assembly` to save gas

The usage of inline `assembly` to check if variable is the `zero` can save gas compared to traditional `require` or `if` statement checks.
```solidity
    // gas 396 gas | 399 gas
    assembly {
        if iszero(value) { // use iszero(iszero(value)) for != add 3 gas
            revert(0, 0)
        }
    }
    require(value != 0); // 401 gas
    require(value == 0); // 401 gas

<details>
<summary><i>65 issue instances in 29 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

141: require(_amount != 0, "0T"); // empty deposit
186: require(amount != 0, "2T"); // empty deposit
141: require(_amount != 0, "0T"); // empty deposit
186: require(amount != 0, "2T"); // empty deposit
```
[141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141) | [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186) | [141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141) | [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

158: require(msg.value == 0, "ShB m.v > 0 b d.it");
200: require(_depositAmount == 0, "ShB wrong withdraw amount");
202: require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
208: require(amount != 0, "6T"); // empty deposit amount
237: require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");
```
[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L158) | [200](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L200) | [202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202) | [208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L208) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L237)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

122: require(_chainId != 0, "Bridgehub: chainId cannot be 0");
225: require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");
```
[122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L122) | [225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

107: if (timestamp == 0) {
```
[107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L107)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

25: require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

90: require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed
```
[90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

50: require(logOutput.pubdataHash == 0x00, "v0h");
237: if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {
            _commitBatchesWithoutSystemContractsUpgrade(_lastCommittedBatchData, _newBatchesData);
284: require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");
361: if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {
633: require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");
```
[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L50) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L237) | [284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L284) | [361](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L361) | [633](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L633)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

169: if (selectorsArrayLen != 0) {
```
[169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L169)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

186: if (_l2ProtocolUpgradeTx.txType == 0) {
            return bytes32(0);
250: require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        );
```
[186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L186) | [250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L250)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

34: require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        );
```
[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L34)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

23: require(_bytecode.length % 32 == 0, "pq");
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

194: if (selectorsLength == 0) {
            ds.facetToSelectors[_facet].facetPosition = ds.facets.length.toUint16();
213: if (selectorPosition != 0) {
250: if (lastSelectorPosition == 0) {
            _removeFacet(_facet);
280: require(_calldata.length == 0, "H"); // Non-empty calldata for zero address
```
[194](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L194) | [213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L213) | [250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L250) | [280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L280)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

50: require(_transaction.paymaster == 0, "uc");
51: require(_transaction.value == 0, "ud");
52: require(_transaction.maxFeePerGas == 0, "uq");
53: require(_transaction.maxPriorityFeePerGas == 0, "ux");
54: require(_transaction.reserved[0] == 0, "ue");
56: require(_transaction.reserved[2] == 0, "ug");
57: require(_transaction.reserved[3] == 0, "uo");
58: require(_transaction.signature.length == 0, "uh");
59: require(_transaction.paymasterInput.length == 0, "ul1");
60: require(_transaction.reservedDynamic.length == 0, "um");
```
[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L50) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L51) | [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L52) | [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L53) | [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L54) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L56) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L57) | [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L58) | [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L59) | [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L60)

```solidity
File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

58: require(lockSlotOldValue == 0, "1B");
```
[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L58)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

102: if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {
131: if (
            uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS &&
            codeHash != 0x00 &&
            !Utils.isContractConstructing(codeHash)
        ) {
            codeSize = Utils.bytecodeLenInBytes(codeHash);
```
[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L102) | [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L131)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

96: if (_transaction.reserved[0] != 0) {
```
[96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L96)

```solidity
File: code/system-contracts/contracts/Compressor.sol

130: if (enumIndex != 0) {
162: if (enumIndex == 0) {
229: if (_operation == 0 || _operation == 3) {
                require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");
```
[130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L130) | [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L162) | [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L229)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

47: if (
            _address > address(MAX_SYSTEM_CONTRACT_ADDRESS) &&
            ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getRawCodeHash(_address) == 0
        ) {
268: require(
            ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0,
            "Code hash is non-zero"
        );
273: require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied");
350: require(value == 0, "The value must be zero if we do not call the constructor");
```
[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L47) | [268](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L268) | [273](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L273) | [350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L350)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

47: if (getMarker(_bytecodeHash) == 0) {
            _validateBytecode(_bytecodeHash);
```
[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L47)

```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

62: if (value != 0) {
            (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call(
                abi.encodeCall(REAL_BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo, (msg.sender, to, value))
            );
```
[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L62)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

85: require(_value != 0, "Nonce value cannot be set to 0");
88: if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {
            require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");
```
[85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L85) | [88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L88)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

268: if (virtualBlockUpgradeInfo.virtualBlockFinishL2Block != 0) {
277: if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
289: } else if (_maxVirtualBlocksToCreate == 0) {
360: if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {
            // Since currentL2BlockNumber and currentL2BlockTimestamp are zero it means that it is
            // the first ever batch with L2 blocks, so we need to initialize those.
            _upgradeL2Blocks(_l2BlockNumber, _expectedPrevL2BlockHash, _isFirstInBatch);
373: require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");
```
[268](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L268) | [277](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L277) | [289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L289) | [360](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L360) | [373](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L373)

```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

73: if (pubdataCost != 0) {
            // Here we double check that the additional cost is not higher than the maximum allowed.
            // Note, that the `gasleft()` can be spent on pubdata too.
            require(pubdataAllowance + gasleft() >= pubdataCost + CALL_RETURN_OVERHEAD, "Not enough gas for pubdata");
```
[73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L73)

```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

131: if (_value == 0) {
            _loadFarCallABIIntoActivePtr(_gas, _data, false, _isSystem);
```
[131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L131)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

98: if (value == 0) {
            // Doing the system call directly
            assembly {
                success := call(to, callAddr, 0, 0, farCallAbi, 0, 0)
```
[98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L98)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

184: if (_transaction.reserved[0] != 0) {
            encodedChainId = bytes.concat(RLPEncoder.encodeUint256(block.chainid), hex"80_80");
```
[184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L184)

```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

84: require(_bytecode.length % 32 == 0, "po");
```
[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L84)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

92: require(msg.value == 0, "Value should be 0 for ERC20 bridge");
```
[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92)

```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

59: if (value == 0) {
            // Doing the system call directly
            assembly {
                success := call(to, callAddr, 0, 0, farCallAbi, 0, 0)
```
[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L59)
</details>

### [G-63] Consider Using += for Mappings

Using the += operator for mappings can save around 40 gas due to avoiding the recalculation of the mapping value's hash. 
Consider refactoring the code to use this more efficient approach.

<details>
<summary><i>4 issue instances in 2 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

219: timestamps[_id] = block.timestamp + _delay;
```
[219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L219)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

72: rawNonces[addressAsKey] = (oldRawNonce + _value);
118: rawNonces[addressAsKey] = oldRawNonce + 1;
144: rawNonces[addressAsKey] = (oldRawNonce + DEPLOY_NONCE_MULTIPLIER);
```
[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L72) | [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L118) | [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L144)
</details>

### [G-64] Consider using solady's `FixedPointMathLib`

Utilizing gas-optimized math functions from libraries like [Solady](https://github.com/Vectorized/solady/blob/main/src/utils/FixedPointMathLib.sol) can lead to more efficient smart contracts.
This is particularly beneficial in contracts where these operations are frequently used.

<details>
<summary><i>78 issue instances in 21 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

106: assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
```
[106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L106)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

51: assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L51)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

578: blobAuxOutputWords = new bytes32[](2 * TOTAL_BLOBS_IN_COMMITMENT);
581: blobAuxOutputWords[i * 2] = _blobHashes[i];
582: blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
632: require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");
```
[578](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L578) | [581](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L581) | [582](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L582) | [632](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L632)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

149: return l2GasPrice * _l2GasLimit;
159: uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
163: pubdataPriceBaseToken = L1_GAS_PER_PUBDATA_BYTE * l1GasPriceConverted;
166: uint256 batchOverheadBaseToken = uint256(feeParams.batchOverheadL1Gas) * l1GasPriceConverted;
271: uint256 baseCost = _params.l2GasPrice * _params.l2GasLimit;
159: uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
            s.baseTokenGasPriceMultiplierDenominator;
168: batchOverheadBaseToken /
            uint256(feeParams.maxPubdataPerBatch);
171: uint256 l2GasPrice = feeParams.minimalL2GasPrice + batchOverheadBaseToken / uint256(feeParams.maxL2GasPerBatch);
172: uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata;
```
[149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L149) | [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L159) | [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L163) | [166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L166) | [271](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L271) | [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L159) | [168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L168) | [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L171) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L172)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

50: codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));
25: uint256 bytecodeLenInWords = _bytecode.length / 32;
26: require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words
```
[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L50) | [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L26)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

27: uint256 bitOffset = (_index & 7) * 32;
48: uint256 bitOffset = (_index & 7) * 32;
23: uint256 mapValue = _map.map[_index / 8];
43: uint256 mapIndex = _index / 8;
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L27) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L48) | [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L23) | [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L43)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

33: _index /= 2;
```
[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L33)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

83: costForComputation += Math.ceilDiv(_encodingLength * L1_TX_DELTA_544_ENCODING_BYTES, 544);
86: costForComputation += _numberOfFactoryDependencies * L1_TX_DELTA_FACTORY_DEPS_L2_GAS;
95: costForPubdata = L1_TX_INTRINSIC_PUBDATA * _l2GasPricePerPubdata;
98: costForPubdata += _numberOfFactoryDependencies * L1_TX_DELTA_FACTORY_DEPS_PUBDATA * _l2GasPricePerPubdata;
98: costForPubdata += _numberOfFactoryDependencies * L1_TX_DELTA_FACTORY_DEPS_PUBDATA * _l2GasPricePerPubdata;
135: uint256 overheadForLength = MEMORY_OVERHEAD_GAS * _encodingLength;
30: require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");
```
[83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L83) | [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L86) | [95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L95) | [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L98) | [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L98) | [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L135) | [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L30)

```solidity
File: code/contracts/ethereum/contracts/common/Config.sol

14: uint256 constant MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES = 4 + L2_TO_L1_LOG_SERIALIZE_SIZE * 512;
```
[14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L14)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

97: vInt += 8 + block.chainid * 2;
```
[97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L97)

```solidity
File: code/system-contracts/contracts/Compressor.sol

52: encodedData.length * 4 == _bytecode.length,
62: uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
66: uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);
127: for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
159: for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
203: dictionary = _rawCompressedData[2:2 + dictionaryLen * 8];
204: encodedData = _rawCompressedData[2 + dictionaryLen * 8:];
253: number >>= (256 - (_calldataSlice.length * 8));
57: dictionary.length / 8 <= encodedData.length / 2,
57: dictionary.length / 8 <= encodedData.length / 2,
```
[52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L52) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L62) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L66) | [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L127) | [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L159) | [203](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L203) | [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L204) | [253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L253) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L57) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L57)

```solidity
File: code/system-contracts/contracts/Constants.sol

94: uint256 constant MAX_MSG_VALUE = 2 ** 128 - 1;
```
[94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L94)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

51: return KECCAK_ROUND_GAS_COST * (_length / KECCAK_ROUND_NUMBER_OF_BYTES + 1);
62: return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1);
89: uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) + 2 * keccakGasCost(64);
149: 3 *
            keccakGasCost(64) +
152: COMPUTATIONAL_PRICE_FOR_PUBDATA *
            pubdataLen;
177: COMPUTATIONAL_PRICE_FOR_PUBDATA *
            pubdataLen;
226: abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
226: abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
304: (numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE)];
305: calldataPtr += numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE;
51: return KECCAK_ROUND_GAS_COST * (_length / KECCAK_ROUND_NUMBER_OF_BYTES + 1);
62: return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1);
223: nodesOnCurrentLevel /= 2;
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L51) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L62) | [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L89) | [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L149) | [152](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L152) | [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L177) | [226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L226) | [226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L226) | [304](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L304) | [305](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L305) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L51) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L62) | [223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L223)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

180: deploymentNonce = _rawMinNonce / DEPLOY_NONCE_MULTIPLIER;
28: uint256 private constant DEPLOY_NONCE_MULTIPLIER = 2 ** 128;
31: uint256 private constant MAXIMAL_MIN_NONCE_INCREMENT = 2 ** 32;
```
[180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L180) | [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L28) | [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L31)

```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

22: require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");
28: bytes memory totalBlobs = new bytes(BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS);
37: uint256 start = BLOB_SIZE_BYTES * i;
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L22) | [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L28) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L37)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

123: return gasPerPubdataByte * getCurrentPubdataSpent();
```
[123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L123)

```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

71: uint256 pubdataCost = pubdataPrice * pubdataSpent;
```
[71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L71)

```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

37: uint256 shiftedVal = _val << (lbs * 8);
72: uint256 shiftedVal = uint256(_len) << (lbs * 8);
```
[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L37) | [72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L72)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

41: uint256 constant META_GAS_PER_PUBDATA_BYTE_OFFSET = 0 * 8;
42: uint256 constant META_HEAP_SIZE_OFFSET = 8 * 8;
43: uint256 constant META_AUX_HEAP_SIZE_OFFSET = 12 * 8;
44: uint256 constant META_SHARD_ID_OFFSET = 28 * 8;
45: uint256 constant META_CALLER_SHARD_ID_OFFSET = 29 * 8;
46: uint256 constant META_CODE_SHARD_ID_OFFSET = 30 * 8;
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L41) | [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L42) | [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L43) | [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L44) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L45) | [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L46)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

397: uint256 amount = _transaction.maxFeePerGas * _transaction.gasLimit;
411: requiredBalance = _transaction.maxFeePerGas * _transaction.gasLimit + _transaction.value;
```
[397](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L397) | [411](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L411)

```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

40: codeLength = bytecodeLenInWords(_bytecodeHash) << 5; // _bytecodeHash * 32
46: codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));
86: uint256 lengthInWords = _bytecode.length / 32;
87: require(lengthInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words
```
[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L40) | [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L46) | [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L86) | [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L87)
</details>

### [G-65] Avoid Zero to Non-Zero Storage Writes Where Possible

Changing a storage variable from zero to non-zero costs 22,100 gas in total. (20,000 gas for a zero to non-zero write and 2,100 for a cold storage access)
Consider using non-zero architecture to avoid high gas costs for zero to non-zero storage writes.

Example:

```solidity
- uint256 public counter = 0;  // rewrite this costs more
+ uint256 public counter = 1;  // rewrite this costs less
```

<details>
<summary><i>32 issue instances in 10 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

111: eraFirstPostUpgradeBatch = _eraFirstPostUpgradeBatch;
```
[111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L111)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

179: timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP;
198: timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP;
219: timestamps[_id] = block.timestamp + _delay;
251: minDelay = _newDelay;
```
[179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L179) | [198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L198) | [219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L219) | [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L251)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

86: protocolVersion = _initializeData.protocolVersion;
100: storedBatchZero = keccak256(abi.encode(batchZero));
102: initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));
138: initialCutHash = keccak256(abi.encode(_diamondCut));
148: protocolVersion = _newProtocolVersion;
```
[86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L86) | [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100) | [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138) | [148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L148)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

97: executionDelay = _executionDelay;
```
[97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L97)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

106: chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));
122: chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));
164: chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));
329: chainedLogsHash = bytes32(0);
331: chainedMessagesHash = bytes32(0);
332: chainedL1BytecodesRevealDataHash = bytes32(0);
```
[106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L106) | [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L122) | [164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L164) | [329](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L329) | [331](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L331) | [332](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L332)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

43: balance[_from] = fromBalance - _amount;
107: totalSupply -= amount;
```
[43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L43) | [107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L107)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

72: rawNonces[addressAsKey] = (oldRawNonce + _value);
118: rawNonces[addressAsKey] = oldRawNonce + 1;
144: rawNonces[addressAsKey] = (oldRawNonce + DEPLOY_NONCE_MULTIPLIER);
```
[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L72) | [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L118) | [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L144)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

85: chainId = _newChainId;
106: gasPrice = _gasPrice;
113: basePubdataSpent = _basePubdataSpent;
114: gasPerPubdataByte = _gasPerPubdataByte;
322: currentL2BlockTxsRollingHash = bytes32(0);
403: currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));
463: baseFee = _baseFee;
479: baseFee = _baseFee;
```
[85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L85) | [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L106) | [113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L113) | [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L114) | [322](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L322) | [403](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L403) | [463](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L463) | [479](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L479)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

61: l2TokenProxyBytecodeHash = _l2TokenProxyBytecodeHash;
```
[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L61)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

95: decimals_ = decimalsUint8;
```
[95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L95)
</details>

### [G-66] Avoid Unnecessary Gas Usage with Shorter `require()/revert()` Strings

Long require() or revert() strings that exceed 32 bytes can lead to extra gas costs.

This unnecessary gas consumption can be avoided by ensuring your `require()` or `revert()` strings are 32 bytes or shorter.
This optimizes your contract's gas efficiency without compromising the clarity and specificity of your error messages.

<details>
<summary><i>105 issue instances in 26 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

75: require(
            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
            "L1SharedBridge: not bridgehub or era chain"
        );
155: require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");
195: require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");
427: require(!alreadyFinalized, "Withdrawal is already finalized 2");
522: revert("ShB Incorrect message function selector");
564: require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
```
[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75) | [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L155) | [195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195) | [427](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L427) | [522](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L522) | [564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

83: require(
            !stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition already registered"
        );
93: require(
            stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition not registered yet"
        );
102: require(!tokenIsRegistered[_token], "Bridgehub: token already registered");
125: require(
            stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition not registered"
        );
132: require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");
225: require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");
300: require(
            _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
            "Bridgehub: second bridge address too low"
        ); // to avoid calls to precompiles
```
[83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83) | [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L93) | [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102) | [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L125) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132) | [225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225) | [300](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L300)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

59: require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
65: require(msg.sender == securityCouncil, "Only security council is allowed to call this function");
71: require(
            msg.sender == owner() || msg.sender == securityCouncil,
            "Only the owner and security council are allowed to call this function"
        );
172: require(isOperationReady(id), "Operation must be ready before execution");
177: require(isOperationReady(id), "Operation must be ready after execution");
191: require(isOperationPending(id), "Operation must be pending before execution");
196: require(isOperationPending(id), "Operation must be pending after execution");
216: require(!isOperation(_id), "Operation with this proposal id already exists");
217: require(_delay >= minDelay, "Proposed delay is less than minimum delay");
230: revert(add(returnData, 0x20), mload(returnData))
                }
            }
        }
    }

    /// @notice Verifies if the predecessor operation is completed.
    /// @param _predecessorId The hash of the operation that should be completed.
    /// @dev Doesn't check the operation to be complete if the input is zero.
    function _checkPredecessorDone(bytes32 _predecessorId) internal view {
        require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");
```
[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59) | [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L65) | [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L71) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L172) | [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L177) | [191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L191) | [196](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L196) | [216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L216) | [217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L217) | [230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L230)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

256: require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");
```
[256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L256)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62: require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");
68: require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
```
[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

90: require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed
105: require(
            cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
            "StateTransition: cutHash mismatch"
        );
110: require(
            s.protocolVersion == _oldProtocolVersion,
            "StateTransition: protocolVersion mismatch in STC when upgrading"
        );
116: require(
            s.protocolVersion > _oldProtocolVersion,
            "StateTransition: protocolVersion mismatch in STC after upgrading"
        );
```
[90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90) | [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L105) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L110) | [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L116)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

226: require(
            IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
            "Executor facet: wrong protocol version"
        );
616: require(success, "failed to call point evaluation precompile");
```
[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L226) | [616](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

39: require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");
158: require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");
185: require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");
206: require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");
```
[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39) | [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158) | [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L185) | [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L206)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

22: require(s.validators[msg.sender], "StateTransition Chain: not validator");
27: require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");
32: require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");
37: require(
            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by admin or state transition manager"
        );
45: require(
            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by validator or state transition manager"
        );
53: require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27) | [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L37) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45) | [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

190: require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");
205: require(
            _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
            "The new protocol version should be included in the L2 system upgrade tx"
        );
238: require(
            _newProtocolVersion > previousProtocolVersion,
            "New protocol version is not greater than the current one"
        );
242: require(
            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
            "Too big protocol version difference"
        );
249: require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
250: require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        );
```
[190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L190) | [205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L205) | [238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L238) | [242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L242) | [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L249) | [250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L250)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

22: require(
            // Genesis Upgrade difference: Note this is the only thing change > to >=
            _newProtocolVersion >= previousProtocolVersion,
            "New protocol version is not greater than the current one"
        );
27: require(
            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
            "Too big protocol version difference"
        );
33: require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
34: require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        );
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L27) | [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33) | [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L34)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

26: require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
37: require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");
48: require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");
57: require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");
```
[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L26) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L37) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L48) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L57)

```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

22: require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22)

```solidity
File: code/system-contracts/contracts/Compressor.sol

51: require(
                encodedData.length * 4 == _bytecode.length,
                "Encoded data length should be 4 times shorter than the original bytecode"
            );
56: require(
                dictionary.length / 8 <= encodedData.length / 2,
                "Dictionary should have at most the same number of entries as the encoded data"
            );
63: require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");
68: require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");
119: require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");
156: require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");
187: require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");
230: require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");
232: require(
                    _initialValue + convertedValue == _finalValue,
                    "add: initial plus converted not equal to final"
                );
237: require(
                    _initialValue - convertedValue == _finalValue,
                    "sub: initial minus converted not equal to final"
                );
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L51) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L56) | [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L63) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L68) | [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L119) | [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L156) | [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L187) | [230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L230) | [232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L232) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L237)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

77: require(
            _nonceOrdering == AccountNonceOrdering.Arbitrary &&
                currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
            "It is only possible to change from sequential to arbitrary ordering"
        );
239: require(
            msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
            "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
        );
251: require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");
265: require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");
350: require(value == 0, "The value must be zero if we do not call the constructor");
```
[77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L77) | [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L239) | [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L251) | [265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L265) | [350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L350)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

100: require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");
202: require(success, "Failed to pay the fee to the operator");
```
[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100) | [202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L202)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

35: require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

76: require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
```
[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L76)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

214: require(
            reconstructedChainedLogsHash == chainedLogsHash,
            "reconstructedChainedLogsHash is not equal to chainedLogsHash"
        );
245: require(
            reconstructedChainedMessagesHash == chainedMessagesHash,
            "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
        );
269: require(
            reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
            "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
        );
279: require(
            uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
                STATE_DIFF_COMPRESSION_VERSION_NUMBER,
            "state diff compression version mismatch"
        );
315: require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");
```
[214](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L214) | [245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L245) | [269](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L269) | [279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L279) | [315](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L315)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

33: require(
            msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
                msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
                msg.sender == BOOTLOADER_FORMAL_ADDRESS,
            "Only system contracts with special access can call this method"
        );
```
[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L33)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

66: require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");
136: require(
            msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
            "Only the contract deployer can increment the deployment nonce"
        );
```
[66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L66) | [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L136)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

242: require(_isFirstInBatch, "Upgrade transaction must be first");
245: require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");
249: require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");
287: require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");
351: require(
                _l2BlockTimestamp >= currentBatchTimestamp,
                "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
            );
355: require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");
367: require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");
368: require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");
369: require(
                _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
                "The previous hash of the same L2 block must be same"
            );
373: require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");
385: require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");
386: require(
                _l2BlockTimestamp > currentL2BlockTimestamp,
                "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
            );
413: require(currentBatchNumber > 0, "The current batch number must be greater than 0");
429: require(
            _newTimestamp > currentBlockTimestamp,
            "The timestamp of the batch must be greater than the timestamp of the previous block"
        );
452: require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
```
[242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L242) | [245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L245) | [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L249) | [287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L287) | [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L351) | [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L355) | [367](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L367) | [368](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L368) | [369](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L369) | [373](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L373) | [385](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L385) | [386](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L386) | [413](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L413) | [429](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L429) | [452](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L452)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

319: require(index < 10, "There are only 10 accessible registers");
```
[319](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

363: require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");
367: require(
                _transaction.paymasterInput.length >= 68,
                "The approvalBased paymaster input must be at least 68 bytes long"
            );
```
[363](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L363) | [367](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L367)

```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

21: require(
            SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
            "This method require system call flag"
        );
31: require(
            SystemContractHelper.isSystemContract(msg.sender),
            "This method require the caller to be system contract"
        );
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L21) | [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L31)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

92: require(msg.value == 0, "Value should be 0 for ERC20 bridge");
```
[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92)
</details>

### [G-67] Use `unchecked` for division which do not divide by -X sonce they can't overflow

Solidity introduced the `unchecked` block in version 0.8.0 as a measure to provide control over arithmetic operations. 
Any operation inside this block will not trigger the built-in overflow and underflow checks, thus saving gas costs. 
Since a division operation between two `uint`s (unsigned integers) can never result in an overflow or underflow, it's an ideal candidate for the use of `unchecked {}` block.
This practice enables optimal gas usage without risking any arithmetic anomalies.

<details>
<summary><i>14 issue instances in 8 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

159: uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
            s.baseTokenGasPriceMultiplierDenominator;
168: batchOverheadBaseToken /
            uint256(feeParams.maxPubdataPerBatch);
171: uint256 l2GasPrice = feeParams.minimalL2GasPrice + batchOverheadBaseToken / uint256(feeParams.maxL2GasPerBatch);
172: uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata;
```
[159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L159) | [168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L168) | [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L171) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L172)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

25: uint256 bytecodeLenInWords = _bytecode.length / 32;
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

23: uint256 mapValue = _map.map[_index / 8];
43: uint256 mapIndex = _index / 8;
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L23) | [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L43)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

30: require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");
```
[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L30)

```solidity
File: code/system-contracts/contracts/Compressor.sol

57: dictionary.length / 8 <= encodedData.length / 2,
57: dictionary.length / 8 <= encodedData.length / 2,
```
[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L57) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L57)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

51: return KECCAK_ROUND_GAS_COST * (_length / KECCAK_ROUND_NUMBER_OF_BYTES + 1);
62: return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1);
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L51) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L62)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

180: deploymentNonce = _rawMinNonce / DEPLOY_NONCE_MULTIPLIER;
```
[180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L180)

```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

86: uint256 lengthInWords = _bytecode.length / 32;
```
[86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L86)
</details>

### [G-68] Use solady library where possible to save gas

The following OpenZeppelin imports have a Solady equivalent, as such they can be used to save GAS as Solady modules have been specifically designed to be as GAS efficient as possible.

<details>
<summary><i>24 issue instances in 12 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

4: import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";
6: import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
4: import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";
6: import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```
[4](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L4) | [6](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L6) | [4](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L4) | [6](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L6)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

4: import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
6: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
7: import {IERC20Metadata} from "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";
9: import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";
10: import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```
[4](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L4) | [6](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L6) | [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L7) | [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L9) | [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L10)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

4: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```
[4](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L4)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

4: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```
[4](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L4)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

16: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```
[16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L16)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

4: import {Ownable2Step} from "@openzeppelin/contracts/access/Ownable2Step.sol";
```
[4](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L4)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

4: import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
```
[4](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L4)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

4: import {SafeCast} from "@openzeppelin/contracts/utils/math/SafeCast.sol";
```
[4](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L4)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

4: import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
```
[4](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L4)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

4: import "../openzeppelin/token/ERC20/IERC20.sol";
6: import "../openzeppelin/token/ERC20/utils/SafeERC20.sol";
```
[4](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L4) | [6](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L6)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

4: import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
6: import {BeaconProxy} from "@openzeppelin/contracts/proxy/beacon/BeaconProxy.sol";
7: import {UpgradeableBeacon} from "@openzeppelin/contracts/proxy/beacon/UpgradeableBeacon.sol";
```
[4](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L4) | [6](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L6) | [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L7)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

4: import {ERC20PermitUpgradeable} from "@openzeppelin/contracts-upgradeable/token/ERC20/extensions/draft-ERC20PermitUpgradeable.sol";
6: import {UpgradeableBeacon} from "@openzeppelin/contracts/proxy/beacon/UpgradeableBeacon.sol";
7: import {ERC1967Upgrade} from "@openzeppelin/contracts/proxy/ERC1967/ERC1967Upgrade.sol";
```
[4](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L4) | [6](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L6) | [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L7)
</details>

### [G-69] Use `uint256(1)`/`uint256(2)` instead of `true`/`false` to save gas for changes

Boolean variables in Solidity are more expensive than `uint256` or any type that takes up a full word, due to additional gas costs associated with write operations.
When using boolean variables, each write operation emits an extra SLOAD to read the slot's contents, replace the bits taken up by the boolean, and then write back.
This process cannot be disabled and leads to extra gas consumption.

By using `uint256(1)` and `uint256(2)` for representing true and false states, you can avoid a `Gwarmaccess` (100 gas) cost and also avoid a `Gsset` (20000 gas) cost when changing from `false` to `true`, after having been `true` in the past.
This approach helps in optimizing gas usage, making your contract more cost-effective.

[Usage in OpenZeppelin ReentrancyGuard.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27)

<details>
<summary><i>7 issue instances in 4 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

27: mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
        public isWithdrawalFinalized;
27: mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
        public isWithdrawalFinalized;
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

57: mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
        public isWithdrawalFinalized;
61: mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;
```
[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57) | [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L61)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

21: mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;
23: mapping(address _token => bool) public tokenIsRegistered;
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21) | [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L23)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

50: mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50)
</details>

### [G-70] Use Bit Shifting for Multiplication by Powers of Two

When multiplying by powers of two (e.g., 2, 4, 8), it is more efficient to use bit shifting.

`<x> * 2` can be replaced with `<x> << 1`, as both operations are equivalent.
However, the multiplication approach may incur additional gas overhead due to potential jumps to and from a compiler utility function that introduces checks.

This overhead can be minimized by using bit shifting when multiplying by powers of two.

<details>
<summary><i>24 issue instances in 10 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

106: assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
```
[106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L106)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

51: assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L51)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

581: blobAuxOutputWords[i * 2] = _blobHashes[i];
582: blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
```
[581](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L581) | [582](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L582)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

50: codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));
```
[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L50)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

27: uint256 bitOffset = (_index & 7) * 32;
48: uint256 bitOffset = (_index & 7) * 32;
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L27) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L48)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

97: vInt += 8 + block.chainid * 2;
```
[97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L97)

```solidity
File: code/system-contracts/contracts/Compressor.sol

52: encodedData.length * 4 == _bytecode.length,
62: uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
66: uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);
203: dictionary = _rawCompressedData[2:2 + dictionaryLen * 8];
204: encodedData = _rawCompressedData[2 + dictionaryLen * 8:];
253: number >>= (256 - (_calldataSlice.length * 8));
```
[52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L52) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L62) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L66) | [203](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L203) | [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L204) | [253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L253)

```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

37: uint256 shiftedVal = _val << (lbs * 8);
72: uint256 shiftedVal = uint256(_len) << (lbs * 8);
```
[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L37) | [72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L72)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

41: uint256 constant META_GAS_PER_PUBDATA_BYTE_OFFSET = 0 * 8;
42: uint256 constant META_HEAP_SIZE_OFFSET = 8 * 8;
43: uint256 constant META_AUX_HEAP_SIZE_OFFSET = 12 * 8;
44: uint256 constant META_SHARD_ID_OFFSET = 28 * 8;
45: uint256 constant META_CALLER_SHARD_ID_OFFSET = 29 * 8;
46: uint256 constant META_CODE_SHARD_ID_OFFSET = 30 * 8;
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L41) | [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L42) | [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L43) | [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L44) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L45) | [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L46)

```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

40: codeLength = bytecodeLenInWords(_bytecodeHash) << 5; // _bytecodeHash * 32
46: codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));
```
[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L40) | [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L46)
</details>

### [G-71] Use Multiple `require()` Statements Instead of chaining

Breaking down complex conditions in `require()` into separate statements improves code readability and gas efficiency.
Instead of chaining conditions with `&&` within a single `require()`, consider using separate `require()` statements for each condition.

<details>
<summary><i>5 issue instances in 5 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

75: require(
            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
```
[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

668: require(
                (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
```
[668](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L668)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

41: require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L41)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

77: require(
            _nonceOrdering == AccountNonceOrdering.Arbitrary &&
                currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
            "It is only possible to change from sequential to arbitrary ordering"
        );
```
[77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L77)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

76: require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
```
[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L76)
</details>

### [G-72] Delete Unused State Variables

State variables that aren't used in the contract not only clutter the codebase but also consume unnecessary gas during deployment.
Specifically, setting non-zero initial values for state variables costs significant gas.
By removing these unused state variables, you can save on both deployment gas and potential future storage gas costs.
This optimization not only reduces gas expenditures but also enhances code clarity and maintainability.
Always ensure a thorough review to confirm that these variables are indeed redundant before removal.

<details>
<summary><i>19 issue instances in 4 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/common/L2ContractAddresses.sol

/// @audit Unused state variable: L2_KNOWN_CODE_STORAGE_SYSTEM_CONTRACT_ADDR
9: address constant L2_KNOWN_CODE_STORAGE_SYSTEM_CONTRACT_ADDR = address(0x8004);
/// @audit Unused state variable: L2_DEPLOYER_SYSTEM_CONTRACT_ADDR
12: address constant L2_DEPLOYER_SYSTEM_CONTRACT_ADDR = address(0x8006);
```
[9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L9) | [12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L12)

```solidity
File: code/system-contracts/contracts/Constants.sol

/// @audit Unused state variable: ECRECOVER_SYSTEM_CONTRACT
31: address constant ECRECOVER_SYSTEM_CONTRACT = address(0x01);
/// @audit Unused state variable: ECADD_SYSTEM_CONTRACT
33: address constant ECADD_SYSTEM_CONTRACT = address(0x06);
/// @audit Unused state variable: ECMUL_SYSTEM_CONTRACT
34: address constant ECMUL_SYSTEM_CONTRACT = address(0x07);
/// @audit Unused state variable: BOOTLOADER_UTILITIES
76: IBootloaderUtilities constant BOOTLOADER_UTILITIES = IBootloaderUtilities(address(SYSTEM_CONTRACTS_OFFSET + 0x0c));
/// @audit Unused state variable: EVENT_WRITER_CONTRACT
79: address constant EVENT_WRITER_CONTRACT = address(SYSTEM_CONTRACTS_OFFSET + 0x0d);
/// @audit Unused state variable: MAX_MSG_VALUE
94: uint256 constant MAX_MSG_VALUE = 2 ** 128 - 1;
/// @audit Unused state variable: COMPRESSED_REPEATED_WRITE_SIZE
137: uint256 constant COMPRESSED_REPEATED_WRITE_SIZE = ENUM_INDEX_LENGTH + VALUE_LENGTH;
```
[31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L31) | [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L33) | [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L34) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L76) | [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L79) | [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L94) | [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L137)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

/// @audit Unused state variable: MIMIC_CALL_CALL_ADDRESS
16: address constant MIMIC_CALL_CALL_ADDRESS = address((1 << 16) - 5);
/// @audit Unused state variable: SYSTEM_MIMIC_CALL_CALL_ADDRESS
17: address constant SYSTEM_MIMIC_CALL_CALL_ADDRESS = address((1 << 16) - 6);
/// @audit Unused state variable: SYSTEM_MIMIC_CALL_BY_REF_CALL_ADDRESS
19: address constant SYSTEM_MIMIC_CALL_BY_REF_CALL_ADDRESS = address((1 << 16) - 8);
/// @audit Unused state variable: RAW_FAR_CALL_CALL_ADDRESS
20: address constant RAW_FAR_CALL_CALL_ADDRESS = address((1 << 16) - 9);
/// @audit Unused state variable: SET_PUBDATA_PRICE_CALL_ADDRESS
25: address constant SET_PUBDATA_PRICE_CALL_ADDRESS = address((1 << 16) - 14);
/// @audit Unused state variable: INCREMENT_TX_COUNTER_CALL_ADDRESS
26: address constant INCREMENT_TX_COUNTER_CALL_ADDRESS = address((1 << 16) - 15);
/// @audit Unused state variable: PTR_RETURNDATA_CALL_ADDRESS
29: address constant PTR_RETURNDATA_CALL_ADDRESS = address((1 << 16) - 18);
/// @audit Unused state variable: LOAD_LATEST_RETURNDATA_INTO_ACTIVE_PTR_CALL_ADDRESS
33: address constant LOAD_LATEST_RETURNDATA_INTO_ACTIVE_PTR_CALL_ADDRESS = address((1 << 16) - 22);
/// @audit Unused state variable: MULTIPLICATION_HIGH_ADDRESS
37: address constant MULTIPLICATION_HIGH_ADDRESS = address((1 << 16) - 26);
```
[16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L16) | [17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L17) | [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L19) | [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L20) | [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L25) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L26) | [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L29) | [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L33) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L37)

```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

/// @audit Unused state variable: BOOTLOADER_ADDRESS
70: address constant BOOTLOADER_ADDRESS = address(SYSTEM_CONTRACTS_OFFSET + 0x01);
```
[70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L70)
</details>

### [G-73] Mark Functions That Revert For Normal Users As `payable`

Functions guaranteed to revert when called by normal users can be marked `payable`.
If a function modifier such as onlyOwner is used, the function will revert if a normal user tries to pay the function.
Marking the function as payable will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided.

The extra opcodes avoided are CALLVALUE(2),DUP1(3),ISZERO(3),PUSH2(3),JUMPI(10),PUSH1(3),DUP1(3),REVERT(0),JUMPDEST(1),POP(2), which costs an average of about 21 gas per call to the function, in addition to the extra deployment cost.

<details>
<summary><i>98 issue instances in 18 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

116: function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
142: function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner {
148: function bridgehubDepositBaseToken(
        uint256 _chainId,
        address _prevMsgSender,
        address _l1Token,
        uint256 _amount
    ) external payable virtual onlyBridgehubOrEra(_chainId) {
182: function bridgehubDeposit(
        uint256 _chainId,
        address _prevMsgSender,
        uint256, // l2Value, needed for Weth deposits in the future
        bytes calldata _data
    ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
232: function bridgehubConfirmL2Transaction(
        uint256 _chainId,
        bytes32 _txDataHash,
        bytes32 _txHash
    ) external override onlyBridgehub {
554: function depositLegacyErc20Bridge(
        address _prevMsgSender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte,
        address _refundRecipient
    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
615: function finalizeWithdrawalLegacyErc20Bridge(
        uint256 _l2BatchNumber,
        uint256 _l2MessageIndex,
        uint16 _l2TxNumberInBatch,
        bytes calldata _message,
        bytes32[] calldata _merkleProof
    ) external override onlyLegacyBridge returns (address l1Receiver, address l1Token, uint256 amount) {
644: function claimFailedDepositLegacyErc20Bridge(
        address _depositSender,
        address _l1Token,
        uint256 _amount,
        bytes32 _l2TxHash,
        uint256 _l2BatchNumber,
        uint256 _l2MessageIndex,
        uint16 _l2TxNumberInBatch,
        bytes32[] calldata _merkleProof
    ) external override onlyLegacyBridge {
```
[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L116) | [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L142) | [148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L148) | [182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L182) | [232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L232) | [554](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L554) | [615](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L615) | [644](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L644)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

51: function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
82: function addStateTransitionManager(address _stateTransitionManager) external onlyOwner {
92: function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner {
101: function addToken(address _token) external onlyOwner {
108: function setSharedBridge(address _sharedBridge) external onlyOwner {
114: function createNewChain(
        uint256 _chainId,
        address _stateTransitionManager,
        address _baseToken,
        uint256, //_salt
        address _admin,
        bytes calldata _initData
    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L51) | [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L82) | [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L92) | [101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L101) | [108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108) | [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

129: function scheduleTransparent(Operation calldata _operation, uint256 _delay) external onlyOwner {
142: function scheduleShadow(bytes32 _id, uint256 _delay) external onlyOwner {
154: function cancel(bytes32 _id) external onlyOwner {
167: function execute(Operation calldata _operation) external payable onlyOwnerOrSecurityCouncil {
186: function executeInstant(Operation calldata _operation) external payable onlySecurityCouncil {
249: function updateDelay(uint256 _newDelay) external onlySelf {
256: function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
```
[129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L129) | [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L142) | [154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L154) | [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L167) | [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L186) | [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L249) | [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L256)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

110: function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
132: function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {
137: function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {
142: function setNewVersionUpgrade(
        Diamond.DiamondCutData calldata _cutData,
        uint256 _oldProtocolVersion,
        uint256 _newProtocolVersion
    ) external onlyOwner {
152: function setUpgradeDiamondCut(
        Diamond.DiamondCutData calldata _cutData,
        uint256 _oldProtocolVersion
    ) external onlyOwner {
160: function freezeChain(uint256 _chainId) external onlyOwner {
165: function unfreezeChain(uint256 _chainId) external onlyOwner {
170: function revertBatches(uint256 _chainId, uint256 _newLastBatch) external onlyOwnerOrAdmin {
229: function registerAlreadyDeployedStateTransition(
        uint256 _chainId,
        address _stateTransitionContract
    ) external onlyOwner {
239: function createNewChain(
        uint256 _chainId,
        address _baseToken,
        address _sharedBridge,
        address _admin,
        bytes calldata _diamondCut
    ) external onlyBridgehub {
```
[110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L110) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L132) | [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L137) | [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L142) | [152](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L152) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L160) | [165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L165) | [170](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L170) | [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L229) | [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L239)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

73: function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {
78: function addValidator(uint256 _chainId, address _newValidator) external onlyChainAdmin(_chainId) {
87: function removeValidator(uint256 _chainId, address _validator) external onlyChainAdmin(_chainId) {
96: function setExecutionDelay(uint32 _executionDelay) external onlyOwner {
108: function commitBatches(
        StoredBatchInfo calldata,
        CommitBatchInfo[] calldata _newBatchesData
    ) external onlyValidator(ERA_CHAIN_ID) {
126: function commitBatchesSharedBridge(
        uint256 _chainId,
        StoredBatchInfo calldata,
        CommitBatchInfo[] calldata _newBatchesData
    ) external onlyValidator(_chainId) {
146: function revertBatches(uint256) external onlyValidator(ERA_CHAIN_ID) {
153: function revertBatchesSharedBridge(uint256 _chainId, uint256) external onlyValidator(_chainId) {
160: function proveBatches(
        StoredBatchInfo calldata,
        StoredBatchInfo[] calldata,
        ProofInput calldata
    ) external onlyValidator(ERA_CHAIN_ID) {
171: function proveBatchesSharedBridge(
        uint256 _chainId,
        StoredBatchInfo calldata,
        StoredBatchInfo[] calldata,
        ProofInput calldata
    ) external onlyValidator(_chainId) {
182: function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {
203: function executeBatchesSharedBridge(
        uint256 _chainId,
        StoredBatchInfo[] calldata _newBatchesData
    ) external onlyValidator(_chainId) {
```
[73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L73) | [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L78) | [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L87) | [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96) | [108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L108) | [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L126) | [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L146) | [153](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L153) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L160) | [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L171) | [182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L182) | [203](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L203)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

23: function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {
45: function setValidator(address _validator, bool _active) external onlyStateTransitionManager {
51: function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {
58: function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager {
67: function changeFeeParams(FeeParams calldata _newFeeParams) external onlyAdminOrStateTransitionManager {
79: function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {
88: function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {
100: function upgradeChainFromVersion(
        uint256 _oldProtocolVersion,
        Diamond.DiamondCutData calldata _diamondCut
    ) external onlyAdminOrStateTransitionManager {
123: function executeUpgrade(Diamond.DiamondCutData calldata _diamondCut) external onlyStateTransitionManager {
133: function freezeDiamond() external onlyAdminOrStateTransitionManager {
143: function unfreezeDiamond() external onlyAdminOrStateTransitionManager {
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L23) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L45) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L51) | [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L58) | [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L67) | [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79) | [88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L88) | [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L100) | [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L123) | [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L133) | [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L143)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

199: function commitBatches(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData
    ) external nonReentrant onlyValidator {
207: function commitBatchesSharedBridge(
        uint256, // _chainId
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData
    ) external nonReentrant onlyValidator {
337: function executeBatchesSharedBridge(
        uint256,
        StoredBatchInfo[] calldata _batchesData
    ) external nonReentrant onlyValidator {
345: function executeBatches(StoredBatchInfo[] calldata _batchesData) external nonReentrant onlyValidator {
368: function proveBatches(
        StoredBatchInfo calldata _prevBatch,
        StoredBatchInfo[] calldata _committedBatches,
        ProofInput calldata _proof
    ) external nonReentrant onlyValidator {
377: function proveBatchesSharedBridge(
        uint256, // _chainId
        StoredBatchInfo calldata _prevBatch,
        StoredBatchInfo[] calldata _committedBatches,
        ProofInput calldata _proof
    ) external nonReentrant onlyValidator {
472: function revertBatches(uint256 _newLastBatch) external nonReentrant onlyValidatorOrStateTransitionManager {
477: function revertBatchesSharedBridge(uint256, uint256 _newLastBatch) external nonReentrant onlyValidator {
```
[199](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L199) | [207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L207) | [337](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L337) | [345](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L345) | [368](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L368) | [377](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L377) | [472](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L472) | [477](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L477)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

38: function transferEthToSharedBridge() external onlyBaseTokenBridge {
47: function bridgehubRequestL2Transaction(
        BridgehubL2TransactionRequest memory _request
    ) external payable onlyBridgehub returns (bytes32 canonicalTxHash) {
```
[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L38) | [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L47)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

35: function storeAccountConstructingCodeHash(address _address, bytes32 _hash) external override onlyDeployer {
46: function storeAccountConstructedCodeHash(address _address, bytes32 _hash) external override onlyDeployer {
54: function markAccountCodeHashAsConstructed(address _address) external override onlyDeployer {
```
[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L35) | [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L46) | [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L54)

```solidity
File: code/system-contracts/contracts/Compressor.sol

44: function publishCompressedBytecode(
        bytes calldata _bytecode,
        bytes calldata _rawCompressedData
    ) external payable onlyCallFromBootloader returns (bytes32 bytecodeHash) {
110: function verifyCompressedStateDiffs(
        uint256 _numberOfStateDiffs,
        uint256 _enumerationIndexSize,
        bytes calldata _stateDiffs,
        bytes calldata _compressedStateDiffs
    ) external payable onlyCallFrom(address(L1_MESSENGER_CONTRACT)) returns (bytes32 stateDiffHash) {
```
[44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L44) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L110)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

65: function updateAccountVersion(AccountAbstractionVersion _version) external onlySystemCall {
74: function updateNonceOrdering(AccountNonceOrdering _nonceOrdering) external onlySystemCall {
162: function create2Account(
        bytes32 _salt,
        bytes32 _bytecodeHash,
        bytes calldata _input,
        AccountAbstractionVersion _aaVersion
    ) public payable override onlySystemCall returns (address) {
182: function createAccount(
        bytes32, // salt
        bytes32 _bytecodeHash,
        bytes calldata _input,
        AccountAbstractionVersion _aaVersion
    ) public payable override onlySystemCall returns (address) {
213: function forceDeployOnAddress(ForceDeployment calldata _deployment, address _sender) external payable onlySelf {
```
[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L65) | [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L74) | [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L162) | [182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L182) | [213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L213)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

27: function markFactoryDeps(bool _shouldSendToL1, bytes32[] calldata _hashes) external onlyCallFromBootloader {
39: function markBytecodeAsPublished(bytes32 _bytecodeHash) external onlyCompressor {
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L27) | [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L39)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

70: function sendL2ToL1Log(
        bool _isService,
        bytes32 _key,
        bytes32 _value
    ) external onlyCallFromSystemContract returns (uint256 logIdInMerkleTree) {
161: function requestBytecodeL1Publication(
        bytes32 _bytecodeHash
    ) external override onlyCallFrom(address(KNOWN_CODE_STORAGE_CONTRACT)) {
194: function publishPubdataAndClearState(
        bytes calldata _totalL2ToL1PubdataAndStateDiffs
    ) external onlyCallFromBootloader {
```
[70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L70) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L161) | [194](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L194)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

64: function mint(address _account, uint256 _amount) external override onlyCallFromBootloader {
```
[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L64)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

65: function increaseMinNonce(uint256 _value) public onlySystemCall returns (uint256 oldMinNonce) {
82: function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall {
110: function incrementMinNonceIfEquals(uint256 _expectedNonce) external onlySystemCall {
```
[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L65) | [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L82) | [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L110)

```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

21: function chunkAndPublishPubdata(bytes calldata _pubdata) external onlyCallFrom(address(L1_MESSENGER_CONTRACT)) {
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L21)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

84: function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {
99: function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {
105: function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {
112: function setPubdataInfo(uint256 _gasPerPubdataByte, uint256 _basePubdataSpent) external onlyCallFromBootloader {
341: function setL2Block(
        uint128 _l2BlockNumber,
        uint128 _l2BlockTimestamp,
        bytes32 _expectedPrevL2BlockHash,
        bool _isFirstInBatch,
        uint128 _maxVirtualBlocksToCreate
    ) external onlyCallFromBootloader {
402: function appendTransactionToCurrentL2Block(bytes32 _txHash) external onlyCallFromBootloader {
408: function publishTimestampDataToL1() external onlyCallFromBootloader {
444: function setNewBatch(
        bytes32 _prevBatchHash,
        uint128 _newTimestamp,
        uint128 _expectedNewNumber,
        uint256 _baseFee
    ) external onlyCallFromBootloader {
471: function unsafeOverrideBatch(
        uint256 _newTimestamp,
        uint256 _number,
        uint256 _baseFee
    ) external onlyCallFromBootloader {
481: function incrementTxNumberInBatch() external onlyCallFromBootloader {
485: function resetTxNumberInBatch() external onlyCallFromBootloader {
```
[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L84) | [99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L99) | [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L105) | [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L112) | [341](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L341) | [402](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L402) | [408](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L408) | [444](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L444) | [471](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L471) | [481](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L481) | [485](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L485)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

111: function reinitializeToken(
        ERC20Getters calldata _availableGetters,
        string memory _newName,
        string memory _newSymbol,
        uint8 _version
    ) external onlyNextVersion(_version) reinitializer(_version) {
145: function bridgeMint(address _to, uint256 _amount) external override onlyBridge {
154: function bridgeBurn(address _from, uint256 _amount) external override onlyBridge {
```
[111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L111) | [145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L145) | [154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L154)
</details>

### [G-74] Prefer `private` over `public` for Constants to Save Gas

Using `private` instead of `public` for constants can save gas.

The compiler doesn't need to create non-payable getter functions for deployment calldata, store the bytes of the value outside of where it's used, or add another entry to the method ID table, saving 3406-3606 gas in deployment.

If needed, the values can be read from the verified contract source code, or a single getter function that returns a tuple of the values of all currently public constants can be implemented.

<details>
<summary><i>5 issue instances in 5 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

26: string public constant override getName = "ValidatorTimelock";
```
[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

20: string public constant override getName = "AdminFacet";
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

27: string public constant override getName = "ExecutorFacet";
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

25: string public constant override getName = "GettersFacet";
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

35: string public constant override getName = "MailboxFacet";
```
[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35)
</details>

### [G-75] `<x> += <y>` costs more gas than `<x> = <x> + <y>` for state variables

Using the addition operator instead of plus-equals saves gas.
Replace `<x> += <y>` or `<x> -= <y>` with `<x> = <x> + <y>` or `<x> = <x> - <y>`.

<details>
<summary><i>3 issue instances in 2 files:</i></summary>

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

65: totalSupply += _amount;
107: totalSupply -= amount;
```
[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L65) | [107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L107)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

483: txNumberInBlock += 1;
```
[483](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L483)
</details>

### [G-76] Using `bool`s for storage incurs overhead

Utilizing booleans for storage is less gas-efficient compared to using types that consume a full word like uint256.
Every write operation on a boolean necessitates an extra SLOAD operation to read the slot's current value, modify the boolean bits, and then write back.
This additional step is the compiler's measure against contract upgrades and pointer aliasing.

To enhance gas efficiency, consider using `uint256(0)` for false and `uint256(1)` for true, bypassing the extra Gwarmaccess (100 gas) incurred by the SLOAD.

<details>
<summary><i>7 issue instances in 4 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

27: mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
        public isWithdrawalFinalized;
27: mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
        public isWithdrawalFinalized;
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

57: mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
        public isWithdrawalFinalized;
61: mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;
```
[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57) | [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L61)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

21: mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;
23: mapping(address _token => bool) public tokenIsRegistered;
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21) | [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L23)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

50: mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50)
</details>

### [G-77] Optimize Gas by Using Only Named Returns

The Solidity compiler can generate more efficient bytecode when using named returns.
It's recommended to replace anonymous returns with named returns for potential gas savings.

Example:
```solidity
/// 985 gas cost
function add(uint256 x, uint256 y) public pure returns (uint256) {
    return x + y;
}
/// 941 gas cost
function addNamed(uint256 x, uint256 y) public pure returns (uint256 res) {
    res = x + y;
}
```

<details>
<summary><i>265 issue instances in 60 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

75: function l2TokenAddress(address _l1Token) external view returns (address) {
160: function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
75: function l2TokenAddress(address _l1Token) external view returns (address) {
160: function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```
[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L75) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160) | [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L75) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

173: function _depositFunds(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
243: function _getDepositL2Calldata(
        address _l1Sender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount
    ) internal view returns (bytes memory) {
254: function _getERC20Getters(address _token) internal view returns (bytes memory) {
374: function _isEraLegacyWithdrawal(uint256 _chainId, uint256 _l2BatchNumber) internal view returns (bool) {
```
[173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L173) | [243](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L243) | [254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L254) | [374](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L374)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

75: function getStateTransition(uint256 _chainId) public view returns (address) {
152: function proveL2MessageInclusion(
        uint256 _chainId,
        uint256 _batchNumber,
        uint256 _index,
        L2Message calldata _message,
        bytes32[] calldata _proof
    ) external view override returns (bool) {
164: function proveL2LogInclusion(
        uint256 _chainId,
        uint256 _batchNumber,
        uint256 _index,
        L2Log memory _log,
        bytes32[] calldata _proof
    ) external view override returns (bool) {
176: function proveL1ToL2TransactionStatus(
        uint256 _chainId,
        bytes32 _l2TxHash,
        uint256 _l2BatchNumber,
        uint256 _l2MessageIndex,
        uint16 _l2TxNumberInBatch,
        bytes32[] calldata _merkleProof,
        TxStatus _status
    ) external view override returns (bool) {
198: function l2TransactionBaseCost(
        uint256 _chainId,
        uint256 _gasPrice,
        uint256 _l2GasLimit,
        uint256 _l2GasPerPubdataByteLimit
    ) external view returns (uint256) {
```
[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L75) | [152](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L152) | [164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L164) | [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L176) | [198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L198)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

84: function isOperation(bytes32 _id) public view returns (bool) {
89: function isOperationPending(bytes32 _id) public view returns (bool) {
95: function isOperationReady(bytes32 _id) public view returns (bool) {
100: function isOperationDone(bytes32 _id) public view returns (bool) {
105: function getOperationState(bytes32 _id) public view returns (OperationState) {
204: function hashOperation(Operation calldata _operation) public pure returns (bytes32) {
```
[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L84) | [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L89) | [95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L95) | [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L100) | [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L105) | [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L204)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

73: function getChainAdmin(uint256 _chainId) external view override returns (address) {
```
[73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L73)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

102: function getCommittedBatchTimestamp(uint256 _chainId, uint256 _l2BatchNumber) external view returns (uint256) {
```
[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L102)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

24: function initialize(InitializeData calldata _initializeData) external reentrancyGuardInitializer returns (bytes32) {
```
[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L24)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

32: function _commitOneBatch(
        StoredBatchInfo memory _previousBatch,
        CommitBatchInfo calldata _newBatch,
        bytes32 _expectedSystemContractUpgradeTxHash
    ) internal view returns (StoredBatchInfo memory) {
453: function _getBatchProofPublicInput(
        bytes32 _prevBatchCommitment,
        bytes32 _currentBatchCommitment,
        VerifierParams memory _verifierParams
    ) internal pure returns (uint256) {
500: function _createBatchCommitment(
        CommitBatchInfo calldata _newBatchData,
        bytes32 _stateDiffHash,
        bytes32[] memory _blobCommitments,
        bytes32[] memory _blobHashes
    ) internal view returns (bytes32) {
514: function _batchPassThroughData(CommitBatchInfo calldata _batch) internal pure returns (bytes memory) {
524: function _batchMetaParameters() internal view returns (bytes memory) {
536: function _batchAuxiliaryOutput(
        CommitBatchInfo calldata _batch,
        bytes32 _stateDiffHash,
        bytes32[] memory _blobCommitments,
        bytes32[] memory _blobHashes
    ) internal pure returns (bytes memory) {
587: function _hashStoredBatchInfo(StoredBatchInfo memory _storedBatchInfo) internal pure returns (bytes32) {
592: function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {
597: function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {
```
[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L32) | [453](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L453) | [500](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L500) | [514](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L514) | [524](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L524) | [536](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L536) | [587](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L587) | [592](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L592) | [597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

32: function getVerifier() external view returns (address) {
37: function getAdmin() external view returns (address) {
42: function getPendingAdmin() external view returns (address) {
47: function getBridgehub() external view returns (address) {
52: function getStateTransitionManager() external view returns (address) {
57: function getBaseToken() external view returns (address) {
62: function getBaseTokenBridge() external view returns (address) {
67: function baseTokenGasPriceMultiplierNominator() external view returns (uint128) {
72: function baseTokenGasPriceMultiplierDenominator() external view returns (uint128) {
77: function getTotalBatchesCommitted() external view returns (uint256) {
82: function getTotalBatchesVerified() external view returns (uint256) {
87: function getTotalBatchesExecuted() external view returns (uint256) {
92: function getTotalPriorityTxs() external view returns (uint256) {
97: function getFirstUnprocessedPriorityTx() external view returns (uint256) {
102: function getPriorityQueueSize() external view returns (uint256) {
107: function priorityQueueFrontOperation() external view returns (PriorityOperation memory) {
112: function isValidator(address _address) external view returns (bool) {
117: function l2LogsRootHash(uint256 _batchNumber) external view returns (bytes32) {
122: function storedBatchHash(uint256 _batchNumber) external view returns (bytes32) {
127: function getL2BootloaderBytecodeHash() external view returns (bytes32) {
132: function getL2DefaultAccountBytecodeHash() external view returns (bytes32) {
137: function getVerifierParams() external view returns (VerifierParams memory) {
142: function getProtocolVersion() external view returns (uint256) {
147: function getL2SystemContractsUpgradeTxHash() external view returns (bytes32) {
152: function getL2SystemContractsUpgradeBatchNumber() external view returns (uint256) {
157: function isDiamondStorageFrozen() external view returns (bool) {
176: function getPriorityTxMaxGasLimit() external view returns (uint256) {
181: function isFunctionFreezable(bytes4 _selector) external view returns (bool) {
188: function isEthWithdrawalFinalized(uint256 _l2BatchNumber, uint256 _l2MessageIndex) external view returns (bool) {
193: function getPubdataPricingMode() external view returns (PubdataPricingMode) {
217: function facetFunctionSelectors(address _facet) external view returns (bytes4[] memory) {
223: function facetAddresses() external view returns (address[] memory) {
229: function facetAddress(bytes4 _selector) external view returns (address) {
239: function getTotalBlocksCommitted() external view returns (uint256) {
244: function getTotalBlocksVerified() external view returns (uint256) {
249: function getTotalBlocksExecuted() external view returns (uint256) {
254: function storedBlockHash(uint256 _batchNumber) external view returns (bytes32) {
259: function getL2SystemContractsUpgradeBlockNumber() external view returns (uint256) {
```
[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L32) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L37) | [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L42) | [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L47) | [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L52) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L57) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L62) | [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L67) | [72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L72) | [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L77) | [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L82) | [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L87) | [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L92) | [97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L97) | [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L102) | [107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L107) | [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L112) | [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L117) | [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L122) | [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L127) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L132) | [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L137) | [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L142) | [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L147) | [152](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L152) | [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L157) | [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L176) | [181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L181) | [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L188) | [193](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L193) | [217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L217) | [223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L223) | [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L229) | [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L239) | [244](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L244) | [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L249) | [254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L254) | [259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L259)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

54: function proveL2MessageInclusion(
        uint256 _batchNumber,
        uint256 _index,
        L2Message memory _message,
        bytes32[] calldata _proof
    ) public view returns (bool) {
64: function proveL2LogInclusion(
        uint256 _batchNumber,
        uint256 _index,
        L2Log memory _log,
        bytes32[] calldata _proof
    ) external view returns (bool) {
74: function proveL1ToL2TransactionStatus(
        bytes32 _l2TxHash,
        uint256 _l2BatchNumber,
        uint256 _l2MessageIndex,
        uint16 _l2TxNumberInBatch,
        bytes32[] calldata _merkleProof,
        TxStatus _status
    ) public view returns (bool) {
104: function _proveL2LogInclusion(
        uint256 _batchNumber,
        uint256 _index,
        L2Log memory _log,
        bytes32[] calldata _proof
    ) internal view returns (bool) {
130: function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {
143: function l2TransactionBaseCost(
        uint256 _gasPrice,
        uint256 _l2GasLimit,
        uint256 _l2GasPerPubdataByteLimit
    ) public view returns (uint256) {
156: function _deriveL2GasPrice(uint256 _l1GasPrice, uint256 _gasPerPubdata) internal view returns (uint256) {
```
[54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L54) | [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L64) | [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L74) | [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L104) | [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L130) | [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L143) | [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L156)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

180: function _setL2SystemContractUpgrade(
        L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
        bytes[] calldata _factoryDeps,
        uint256 _newProtocolVersion
    ) internal returns (bytes32) {
```
[180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L180)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

47: function upgrade(ProposedUpgrade calldata _proposedUpgrade) public virtual override returns (bytes32) {
```
[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L47)

```solidity
File: code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

13: function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```
[13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L13)

```solidity
File: code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

14: function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {
```
[14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L14)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

60: function computeCreate2Address(
        address _sender,
        bytes32 _salt,
        bytes32 _bytecodeHash,
        bytes32 _constructorInputHash
    ) internal pure returns (address) {
```
[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L60)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol

11: function uncheckedInc(uint256 _number) internal pure returns (uint256) {
16: function uncheckedAdd(uint256 _lhs, uint256 _rhs) internal pure returns (uint256) {
```
[11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L11) | [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L16)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

18: function calculateRoot(
        bytes32[] calldata _path,
        uint256 _index,
        bytes32 _itemHash
    ) internal pure returns (bytes32) {
```
[18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L18)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

35: function getFirstUnprocessedPriorityTx(Queue storage _queue) internal view returns (uint256) {
40: function getTotalPriorityTxs(Queue storage _queue) internal view returns (uint256) {
45: function getSize(Queue storage _queue) internal view returns (uint256) {
50: function isEmpty(Queue storage _queue) internal view returns (bool) {
64: function front(Queue storage _queue) internal view returns (PriorityOperation memory) {
```
[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L35) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L40) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L45) | [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L50) | [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L64)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

69: function getMinimalPriorityTransactionGasLimit(
        uint256 _encodingLength,
        uint256 _numberOfFactoryDependencies,
        uint256 _l2GasPricePerPubdata
    ) internal pure returns (uint256) {
```
[69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L69)

```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

23: function isWithdrawalFinalized(uint256 _l2BatchNumber, uint256 _l2MessageIndex) external view returns (bool);
60: function l2TokenAddress(address _l1Token) external view returns (address);
62: function sharedBridge() external view returns (IL1SharedBridge);
64: function l2TokenBeacon() external view returns (address);
66: function l2Bridge() external view returns (address);
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L23) | [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L60) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L62) | [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L64) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L66)

```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

57: function isWithdrawalFinalized(
        uint256 _chainId,
        uint256 _l2BatchNumber,
        uint256 _l2MessageIndex
    ) external view returns (bool);
113: function l1WethAddress() external view returns (address);
115: function bridgehub() external view returns (IBridgehub);
117: function legacyBridge() external view returns (IL1ERC20Bridge);
119: function l2BridgeAddress(uint256 _chainId) external view returns (address);
121: function depositHappened(uint256 _chainId, bytes32 _l2TxHash) external view returns (bytes32);
```
[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L57) | [113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L113) | [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L115) | [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L117) | [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L119) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L121)

```solidity
File: code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol

16: function l1TokenAddress(address _l2Token) external view returns (address);
18: function l2TokenAddress(address _l1Token) external view returns (address);
20: function l1Bridge() external view returns (address);
```
[16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L16) | [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L18) | [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L20)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol

59: function stateTransitionManagerIsRegistered(address _stateTransitionManager) external view returns (bool);
60: function stateTransitionManager(uint256 _chainId) external view returns (address);
62: function tokenIsRegistered(address _baseToken) external view returns (bool);
64: function baseToken(uint256 _chainId) external view returns (address);
66: function sharedBridge() external view returns (IL1SharedBridge);
68: function getStateTransition(uint256 _chainId) external view returns (address);
72: function proveL2MessageInclusion(
        uint256 _chainId,
        uint256 _batchNumber,
        uint256 _index,
        L2Message calldata _message,
        bytes32[] calldata _proof
    ) external view returns (bool);
80: function proveL2LogInclusion(
        uint256 _chainId,
        uint256 _batchNumber,
        uint256 _index,
        L2Log memory _log,
        bytes32[] calldata _proof
    ) external view returns (bool);
88: function proveL1ToL2TransactionStatus(
        uint256 _chainId,
        bytes32 _l2TxHash,
        uint256 _l2BatchNumber,
        uint256 _l2MessageIndex,
        uint16 _l2TxNumberInBatch,
        bytes32[] calldata _merkleProof,
        TxStatus _status
    ) external view returns (bool);
106: function l2TransactionBaseCost(
        uint256 _chainId,
        uint256 _gasPrice,
        uint256 _l2GasLimit,
        uint256 _l2GasPerPubdataByteLimit
    ) external view returns (uint256);
```
[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L59) | [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L60) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L62) | [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L64) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L66) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L68) | [72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L72) | [80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L80) | [88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L88) | [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L106)

```solidity
File: code/contracts/ethereum/contracts/governance/IGovernance.sol

40: function isOperation(bytes32 _id) external view returns (bool);
42: function isOperationPending(bytes32 _id) external view returns (bool);
44: function isOperationReady(bytes32 _id) external view returns (bool);
46: function isOperationDone(bytes32 _id) external view returns (bool);
48: function getOperationState(bytes32 _id) external view returns (OperationState);
60: function hashOperation(Operation calldata _operation) external pure returns (bytes32);
```
[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L40) | [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L42) | [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L44) | [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L46) | [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L48) | [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L60)

```solidity
File: code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

42: function bridgehub() external view returns (address);
52: function stateTransition(uint256 _chainId) external view returns (address);
54: function storedBatchZero() external view returns (bytes32);
56: function initialCutHash() external view returns (bytes32);
58: function genesisUpgrade() external view returns (address);
60: function upgradeCutHash(uint256 _protocolVersion) external view returns (bytes32);
62: function protocolVersion() external view returns (uint256);
70: function getChainAdmin(uint256 _chainId) external view returns (address);
```
[42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L42) | [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L52) | [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L54) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L56) | [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L58) | [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L60) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L62) | [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L70)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol

62: function initialize(InitializeData calldata _initData) external returns (bytes32);
```
[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L62)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol

19: function getVerifier() external view returns (address);
22: function getAdmin() external view returns (address);
25: function getPendingAdmin() external view returns (address);
28: function getBridgehub() external view returns (address);
31: function getStateTransitionManager() external view returns (address);
34: function getBaseToken() external view returns (address);
37: function getBaseTokenBridge() external view returns (address);
40: function getTotalBatchesCommitted() external view returns (uint256);
43: function getTotalBatchesVerified() external view returns (uint256);
46: function getTotalBatchesExecuted() external view returns (uint256);
49: function getTotalPriorityTxs() external view returns (uint256);
56: function getFirstUnprocessedPriorityTx() external view returns (uint256);
59: function getPriorityQueueSize() external view returns (uint256);
62: function priorityQueueFrontOperation() external view returns (PriorityOperation memory);
65: function isValidator(address _address) external view returns (bool);
73: function storedBatchHash(uint256 _batchNumber) external view returns (bytes32);
76: function getL2BootloaderBytecodeHash() external view returns (bytes32);
79: function getL2DefaultAccountBytecodeHash() external view returns (bytes32);
82: function getVerifierParams() external view returns (VerifierParams memory);
85: function isDiamondStorageFrozen() external view returns (bool);
88: function getProtocolVersion() external view returns (uint256);
91: function getL2SystemContractsUpgradeTxHash() external view returns (bytes32);
98: function getL2SystemContractsUpgradeBatchNumber() external view returns (uint256);
101: function getPriorityTxMaxGasLimit() external view returns (uint256);
106: function isEthWithdrawalFinalized(uint256 _l2BatchNumber, uint256 _l2MessageIndex) external view returns (bool);
109: function getPubdataPricingMode() external view returns (PubdataPricingMode);
112: function baseTokenGasPriceMultiplierNominator() external view returns (uint128);
115: function baseTokenGasPriceMultiplierDenominator() external view returns (uint128);
130: function facets() external view returns (Facet[] memory);
133: function facetFunctionSelectors(address _facet) external view returns (bytes4[] memory);
142: function isFunctionFreezable(bytes4 _selector) external view returns (bool);
```
[19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L19) | [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L22) | [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L25) | [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L28) | [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L31) | [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L34) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L37) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L40) | [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L43) | [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L46) | [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L49) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L56) | [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L59) | [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L62) | [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L65) | [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L73) | [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L76) | [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L79) | [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L82) | [85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L85) | [88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L88) | [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L91) | [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L98) | [101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L101) | [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L106) | [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L109) | [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L112) | [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L115) | [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L130) | [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L133) | [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L142)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol

14: function getTotalBlocksCommitted() external view returns (uint256);
18: function getTotalBlocksVerified() external view returns (uint256);
22: function getTotalBlocksExecuted() external view returns (uint256);
28: function storedBlockHash(uint256 _batchNumber) external view returns (bytes32);
36: function getL2SystemContractsUpgradeBlockNumber() external view returns (uint256);
```
[14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L14) | [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L18) | [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L22) | [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L28) | [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L36)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

18: function proveL2MessageInclusion(
        uint256 _batchNumber,
        uint256 _index,
        L2Message calldata _message,
        bytes32[] calldata _proof
    ) external view returns (bool);
31: function proveL2LogInclusion(
        uint256 _batchNumber,
        uint256 _index,
        L2Log memory _log,
        bytes32[] calldata _proof
    ) external view returns (bool);
47: function proveL1ToL2TransactionStatus(
        bytes32 _l2TxHash,
        uint256 _l2BatchNumber,
        uint256 _l2MessageIndex,
        uint16 _l2TxNumberInBatch,
        bytes32[] calldata _merkleProof,
        TxStatus _status
    ) external view returns (bool);
107: function l2TransactionBaseCost(
        uint256 _gasPrice,
        uint256 _l2GasLimit,
        uint256 _l2GasPerPubdataByteLimit
    ) external view returns (uint256);
```
[18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L18) | [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L31) | [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L47) | [107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L107)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol

19: function verify(
        uint256[] calldata _publicInputs,
        uint256[] calldata _proof,
        uint256[] calldata _recursiveAggregationInput
    ) external view returns (bool);
27: function verificationKeyHash() external pure returns (bytes32);
```
[19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L19) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L27)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol

9: function getName() external view returns (string memory);
```
[9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L9)

```solidity
File: code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol

8: function upgrade(ProposedUpgrade calldata _upgrade) external returns (bytes32);
```
[8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L8)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

89: function getCodeHash(uint256 _input) external view override returns (bytes32) {
```
[89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L89)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

139: function encodeEIP2930TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {
229: function encodeEIP1559TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {
```
[139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L139) | [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L229)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

40: function extendedAccountVersion(address _address) public view returns (AccountAbstractionVersion) {
132: function create2(
        bytes32 _salt,
        bytes32 _bytecodeHash,
        bytes calldata _input
    ) external payable override returns (address) {
147: function create(
        bytes32 _salt,
        bytes32 _bytecodeHash,
        bytes calldata _input
    ) external payable override returns (address) {
162: function create2Account(
        bytes32 _salt,
        bytes32 _bytecodeHash,
        bytes calldata _input,
        AccountAbstractionVersion _aaVersion
    ) public payable override onlySystemCall returns (address) {
182: function createAccount(
        bytes32, // salt
        bytes32 _bytecodeHash,
        bytes calldata _input,
        AccountAbstractionVersion _aaVersion
    ) public payable override onlySystemCall returns (address) {
```
[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L40) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L132) | [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L147) | [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L162) | [182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L182)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

159: function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {
```
[159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L159)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

27: function getImmutable(address _dest, uint256 _index) external view override returns (bytes32) {
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L27)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

50: function keccakGasCost(uint256 _length) internal pure returns (uint256) {
61: function sha256GasCost(uint256 _length) internal pure returns (uint256) {
```
[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L50) | [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L61)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

56: function balanceOf(uint256 _account) external view override returns (uint256) {
112: function _getL1WithdrawMessage(address _to, uint256 _amount) internal pure returns (bytes memory) {
117: function _getExtendedWithdrawMessage(
        address _to,
        uint256 _amount,
        address _sender,
        bytes memory _additionalData
    ) internal pure returns (bytes memory) {
128: function name() external pure override returns (string memory) {
134: function symbol() external pure override returns (string memory) {
140: function decimals() external pure override returns (uint8) {
```
[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L56) | [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L112) | [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L117) | [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L128) | [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L134) | [140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L140)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

46: function getMinNonce(address _address) public view returns (uint256) {
57: function getRawNonce(address _address) public view returns (uint256) {
102: function getValueUnderNonce(uint256 _key) public view returns (uint256) {
154: function isNonceUsed(address _address, uint256 _nonce) public view returns (bool) {
```
[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L46) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L57) | [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L102) | [154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L154)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

116: function getCurrentPubdataSpent() public view returns (uint256) {
121: function getCurrentPubdataCost() external view returns (uint256) {
190: function getBlockNumber() public view returns (uint128) {
198: function getBlockTimestamp() public view returns (uint128) {
205: function _getLatest257L2blockHash(uint256 _block) internal view returns (bytes32) {
221: function _calculateL2BlockHash(
        uint128 _blockNumber,
        uint128 _blockTimestamp,
        bytes32 _prevL2BlockHash,
        bytes32 _blockTxsRollingHash
    ) internal pure returns (bytes32) {
233: function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {
```
[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L116) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L121) | [190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L190) | [198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L198) | [205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L205) | [221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L221) | [233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L233)

```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

36: function keccak(bytes calldata _data) internal view returns (bytes32) {
45: function sha(bytes calldata _data) internal view returns (bytes32) {
```
[36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L36) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L45)

```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

49: function encodeNonSingleBytesLen(uint64 _len) internal pure returns (bytes memory) {
56: function encodeListLen(uint64 _len) internal pure returns (bytes memory) {
```
[49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L49) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L56)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

329: function isSystemCall() internal view returns (bool) {
338: function isSystemContract(address _address) internal pure returns (bool) {
```
[329](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L329) | [338](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L338)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

94: function isEthToken(uint256 _addr) internal pure returns (bool) {
118: function _encodeHashEIP712Transaction(Transaction calldata _transaction) private view returns (bytes32) {
147: function _encodeHashLegacyTransaction(Transaction calldata _transaction) private view returns (bytes32) {
219: function _encodeHashEIP2930Transaction(Transaction calldata _transaction) private view returns (bytes32) {
289: function _encodeHashEIP1559Transaction(Transaction calldata _transaction) private view returns (bytes32) {
```
[94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L94) | [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L118) | [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L147) | [219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L219) | [289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L289)

```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

19: function safeCastToU128(uint256 _x) internal pure returns (uint128) {
25: function safeCastToU32(uint256 _x) internal pure returns (uint32) {
31: function safeCastToU24(uint256 _x) internal pure returns (uint24) {
51: function isContractConstructed(bytes32 _bytecodeHash) internal pure returns (bool) {
56: function isContractConstructing(bytes32 _bytecodeHash) internal pure returns (bool) {
63: function constructingBytecodeHash(bytes32 _bytecodeHash) internal pure returns (bytes32) {
71: function constructedBytecodeHash(bytes32 _bytecodeHash) internal pure returns (bytes32) {
```
[19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L19) | [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L25) | [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L31) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L51) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L56) | [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L63) | [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L71)

```solidity
File: code/system-contracts/contracts/interfaces/IBaseToken.sol

6: function balanceOf(uint256) external view returns (uint256);
9: function totalSupply() external view returns (uint256);
11: function name() external pure returns (string memory);
13: function symbol() external pure returns (string memory);
15: function decimals() external pure returns (uint8);
```
[6](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IBaseToken.sol#L6) | [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IBaseToken.sol#L9) | [11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IBaseToken.sol#L11) | [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IBaseToken.sol#L13) | [15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IBaseToken.sol#L15)

```solidity
File: code/system-contracts/contracts/interfaces/IImmutableSimulator.sol

11: function getImmutable(address _dest, uint256 _index) external view returns (bytes32);
```
[11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IImmutableSimulator.sol#L11)

```solidity
File: code/system-contracts/contracts/interfaces/IKnownCodesStorage.sol

17: function getMarker(bytes32 _hash) external view returns (uint256);
```
[17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IKnownCodesStorage.sol#L17)

```solidity
File: code/system-contracts/contracts/interfaces/IL1Messenger.sol

48: function sendToL1(bytes memory _message) external returns (bytes32);
```
[48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IL1Messenger.sol#L48)

```solidity
File: code/system-contracts/contracts/interfaces/IL2StandardToken.sol

13: function l1Address() external view returns (address);
15: function l2Bridge() external view returns (address);
```
[13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IL2StandardToken.sol#L13) | [15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IL2StandardToken.sol#L15)

```solidity
File: code/system-contracts/contracts/interfaces/INonceHolder.sol

17: function getMinNonce(address _address) external view returns (uint256);
21: function getRawNonce(address _address) external view returns (uint256);
24: function increaseMinNonce(uint256 _value) external returns (uint256);
30: function getValueUnderNonce(uint256 _key) external view returns (uint256);
37: function getDeploymentNonce(address _address) external view returns (uint256);
40: function incrementDeploymentNonce(address _address) external returns (uint256);
46: function isNonceUsed(address _address, uint256 _nonce) external view returns (bool);
```
[17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/INonceHolder.sol#L17) | [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/INonceHolder.sol#L21) | [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/INonceHolder.sol#L24) | [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/INonceHolder.sol#L30) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/INonceHolder.sol#L37) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/INonceHolder.sol#L40) | [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/INonceHolder.sol#L46)

```solidity
File: code/system-contracts/contracts/interfaces/ISystemContext.sol

29: function chainId() external view returns (uint256);
31: function origin() external view returns (address);
33: function gasPrice() external view returns (uint256);
35: function blockGasLimit() external view returns (uint256);
37: function coinbase() external view returns (address);
39: function difficulty() external view returns (uint256);
41: function baseFee() external view returns (uint256);
43: function txNumberInBlock() external view returns (uint16);
45: function getBlockHashEVM(uint256 _block) external view returns (bytes32);
49: function getBlockNumber() external view returns (uint128);
51: function getBlockTimestamp() external view returns (uint128);
```
[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L29) | [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L31) | [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L33) | [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L35) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L37) | [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L39) | [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L41) | [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L43) | [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L45) | [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L49) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L51)

```solidity
File: code/system-contracts/contracts/interfaces/ISystemContextDeprecated.sol

11: function currentBlockInfo() external view returns (uint256);
```
[11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContextDeprecated.sol#L11)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

109: function _deployL2Token(address _l1Token, bytes calldata _data) internal returns (address) {
138: function _getL1WithdrawMessage(
        address _to,
        address _l1Token,
        uint256 _amount
    ) internal pure returns (bytes memory) {
149: function l2TokenAddress(address _l1Token) public view override returns (address) {
```
[109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L109) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L138) | [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L149)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

158: function name() public view override returns (string memory) {
164: function symbol() public view override returns (string memory) {
170: function decimals() public view override returns (uint8) {
```
[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L158) | [164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L164) | [170](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L170)

```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol

33: function l1TokenAddress(address _l2Token) external view returns (address);
35: function l2TokenAddress(address _l1Token) external view returns (address);
37: function l1Bridge() external view returns (address);
```
[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L33) | [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L35) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L37)

```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol

15: function l1Address() external view returns (address);
17: function l2Bridge() external view returns (address);
```
[15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L15) | [17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L17)

```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

22: function sendToL1(bytes memory _message) external returns (bytes32);
53: function create2(bytes32 _salt, bytes32 _bytecodeHash, bytes calldata _input) external returns (address);
90: function sendMessageToL1(bytes memory _message) internal returns (bytes32) {
101: function computeCreate2Address(
        address _sender,
        bytes32 _salt,
        bytes32 _bytecodeHash,
        bytes32 _constructorInputHash
    ) internal pure returns (address) {
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L22) | [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L53) | [90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L90) | [101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L101)

```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

27: function safeCastToU32(uint256 _x) internal pure returns (uint32) {
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L27)
</details>

### [G-78] Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead

Usage of uints/ints smaller than 32 bytes (256 bits) incurs overhead. The Ethereum Virtual Machine (EVM) operates on 32 bytes at a time. Therefore, if an element is smaller than 32 bytes, the EVM must use more operations to reduce the size of the element from 32 bytes to the desired size. 

Operations involving smaller size uints/ints cost extra gas due to the compiler having to clear the higher bits of the memory word before operating on the small size integer. This also includes the associated stack operations of doing so. 

It's recommended to use larger sizes and downcast where needed to optimize for gas efficiency.

<details>
<summary><i>191 issue instances in 40 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

258: bytes memory decimals = abi.encode(uint8(18));
503: (uint32 functionSignature, uint256 offset) = UnsafeBytes.readUint32(_l2ToL1message, 0);
```
[258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L258) | [503](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L503)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

123: require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");
```
[123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

53: uint32 public executionDelay;
55: constructor(address _initialOwner, uint32 _executionDelay) {
96: function setExecutionDelay(uint32 _executionDelay) external onlyOwner {
115: uint32 timestamp = uint32(block.timestamp);
134: uint32 timestamp = uint32(block.timestamp);
183: uint256 delay = executionDelay; // uint32
        unchecked {
207: uint256 delay = executionDelay; // uint32
        unchecked {
```
[53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L53) | [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55) | [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96) | [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L115) | [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L134) | [183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L183) | [207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L207)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

79: function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {
80: uint128 oldNominator = s.baseTokenGasPriceMultiplierNominator;
81: uint128 oldDenominator = s.baseTokenGasPriceMultiplierDenominator;
```
[79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79) | [80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L80) | [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L81)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

39: uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));
40: require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us");
52: } else if (pubdataSource == uint8(PubdataSource.Blob)) {
59: } else if (pubdataSource == uint8(PubdataSource.Calldata)) {
149: require(!_checkBit(processedLogs, uint8(logKey)), "kp");
150: processedLogs = _setBit(processedLogs, uint8(logKey));
520: uint64(0), // index repeated storage changes in zkPorter
                bytes32(0) // zkPorter batch hash
            );
```
[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L39) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L40) | [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L52) | [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L59) | [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L149) | [150](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L150) | [520](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L520)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

67: function baseTokenGasPriceMultiplierNominator() external view returns (uint128) {
72: function baseTokenGasPriceMultiplierDenominator() external view returns (uint128) {
```
[67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L67) | [72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L72)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

283: _params.expirationTimestamp = uint64(block.timestamp + PRIORITY_EXPIRATION); // Safe to cast
338: layer2Tip: uint192(0) // TODO: Restore after fee modeling will be stable. (SMA-1230)
            })
        );
```
[283](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L283) | [338](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L338)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

40: uint8 version = uint8(_bytecodeHash[0]);
71: return address(uint160(uint256(data)));
```
[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L40) | [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L71)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

208: uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16();
```
[208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L208)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

48: require(_transaction.from <= type(uint16).max, "ua");
49: require(_transaction.to <= type(uint160).max, "ub");
55: require(_transaction.reserved[1] <= type(uint160).max, "uf");
```
[48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L48) | [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L49) | [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol

40: function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external;
84: uint128 oldNominator,
        uint128 oldDenominator,
        uint128 newNominator,
        uint128 newDenominator
    );
```
[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L40) | [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L84)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol

112: function baseTokenGasPriceMultiplierNominator() external view returns (uint128);
115: function baseTokenGasPriceMultiplierDenominator() external view returns (uint128);
```
[112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L112) | [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L115)

```solidity
File: code/contracts/ethereum/contracts/common/Config.sol

115: address constant BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS = address(uint160(type(uint16).max));
```
[115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L115)

```solidity
File: code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

22: uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
30: l2Address = address(uint160(l1Address) + offset);
40: l1Address = address(uint160(l2Address) - offset);
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L22) | [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L30) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L40)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

92: address account = address(uint160(_input));
93: if (uint160(account) <= CURRENT_MAX_PRECOMPILE_ADDRESS) {
120: address account = address(uint160(_input));
132: uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS &&
            codeHash != 0x00 &&
            !Utils.isContractConstructing(codeHash)
        ) {
```
[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L92) | [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L93) | [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L120) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L132)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

61: bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
68: uint64 txDataLen = uint64(_transaction.data.length);
116: encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));
147: bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
164: uint64 txDataLen = uint64(_transaction.data.length);
207: encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));
241: bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
259: uint64 txDataLen = uint64(_transaction.data.length);
302: encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));
```
[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L61) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L68) | [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L116) | [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L147) | [164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L164) | [207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L207) | [241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L241) | [259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L259) | [302](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L302)

```solidity
File: code/system-contracts/contracts/Compressor.sol

65: uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);
66: uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);
129: uint64 enumIndex = stateDiff.readUint64(84);
143: uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
145: uint8 operation = metadata & OPERATION_BITMASK;
146: uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
161: uint64 enumIndex = stateDiff.readUint64(84);
174: uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
176: uint8 operation = metadata & OPERATION_BITMASK;
177: uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
```
[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L65) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L66) | [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L129) | [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L143) | [145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L145) | [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L146) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L161) | [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L174) | [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L176) | [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L177)

```solidity
File: code/system-contracts/contracts/Constants.sol

20: uint160 constant SYSTEM_CONTRACTS_OFFSET = {{SYSTEM_CONTRACTS_OFFSET}}; // 2^15
25: uint160 constant REAL_SYSTEM_CONTRACTS_OFFSET = 0x8000;
29: uint160 constant MAX_SYSTEM_CONTRACT_ADDRESS = 0xffff; // 2^16 - 1
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L20) | [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L25) | [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L29)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

109: newAddress = address(uint160(uint256(hash)));
125: newAddress = address(uint160(uint256(hash)));
265: require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");
```
[109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L109) | [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L125) | [265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L265)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

84: uint32(gasleft()),
            address(NONCE_HOLDER_SYSTEM_CONTRACT),
            0,
            abi.encodeCall(INonceHolder.incrementMinNonceIfEquals, (_transaction.nonce))
        );
132: address to = address(uint160(_transaction.to));
133: uint128 value = Utils.safeCastToU128(_transaction.value);
135: uint32 gas = Utils.safeCastToU32(gasleft());
161: uint8 v;
```
[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L84) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L132) | [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L133) | [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L135) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L161)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

75: uint8 version = uint8(_bytecodeHash[0]);
```
[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L75)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

154: SystemContractHelper.burnGas(Utils.safeCastToU32(gasToPay), uint32(pubdataLen));
179: SystemContractHelper.burnGas(Utils.safeCastToU32(gasToPay), uint32(pubdataLen));
200: uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
233: uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
237: uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
251: uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
255: uint32 currentBytecodeLength = uint32(
                bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])
            );
286: uint24 compressedStateDiffSize = uint24(bytes3(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 3]));
289: uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));
300: uint32 numberOfStateDiffs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
```
[154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L154) | [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L179) | [200](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L200) | [233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L233) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L237) | [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L251) | [255](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L255) | [286](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L286) | [289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L289) | [300](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L300)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

57: return balance[address(uint160(_account))];
140: function decimals() external pure override returns (uint8) {
```
[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L57) | [140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L140)

```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

32: to = address(uint160(addressAsUint));
```
[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L32)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

89: uint16 public txNumberInBlock;
133: uint128 blockNumber = currentVirtualL2BlockInfo.number;
172: function getBatchNumberAndTimestamp() public view returns (uint128 batchNumber, uint128 batchTimestamp) {
180: function getL2BlockNumberAndTimestamp() public view returns (uint128 blockNumber, uint128 blockTimestamp) {
190: function getBlockNumber() public view returns (uint128) {
198: function getBlockTimestamp() public view returns (uint128) {
222: uint128 _blockNumber,
        uint128 _blockTimestamp,
        bytes32 _prevL2BlockHash,
        bytes32 _blockTxsRollingHash
    ) internal pure returns (bytes32) {
233: function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {
234: return keccak256(abi.encodePacked(uint32(_blockNumber)));
241: function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {
264: uint128 _l2BlockNumber,
        uint128 _maxVirtualBlocksToCreate,
        uint128 _newTimestamp
    ) internal {
278: uint128 currentBatchNumber = currentBatchInfo.number;
314: function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal {
342: uint128 _l2BlockNumber,
        uint128 _l2BlockTimestamp,
        bytes32 _expectedPrevL2BlockHash,
        bool _isFirstInBatch,
        uint128 _maxVirtualBlocksToCreate
    ) external onlyCallFromBootloader {
350: uint128 currentBatchTimestamp = currentBatchInfo.timestamp;
358: (uint128 currentL2BlockNumber, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();
409: (uint128 currentBatchNumber, uint128 currentBatchTimestamp) = getBatchNumberAndTimestamp();
410: (, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();
427: function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {
428: uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp;
446: uint128 _newTimestamp,
        uint128 _expectedNewNumber,
        uint256 _baseFee
    ) external onlyCallFromBootloader {
450: (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();
476: BlockInfo memory newBlockInfo = BlockInfo({number: uint128(_number), timestamp: uint128(_newTimestamp)});
497: (uint128 blockNumber, uint128 blockTimestamp) = getBatchNumberAndTimestamp();
```
[89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L89) | [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L133) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L172) | [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L180) | [190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L190) | [198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L198) | [222](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L222) | [233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L233) | [234](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L234) | [241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L241) | [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L264) | [278](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L278) | [314](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L314) | [342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L342) | [350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L350) | [358](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L358) | [409](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L409) | [410](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L410) | [427](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L427) | [428](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L428) | [446](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L446) | [450](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L450) | [476](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L476) | [497](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L497)

```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

264: uint32 gas = Utils.safeCastToU32(_gas);
```
[264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L264)

```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

29: encoded[0] = (_val == 0) ? bytes1(uint8(128)) : bytes1(uint8(_val));
34: encoded[0] = bytes1(uint8(hbs + 0x81));
60: function _encodeLength(uint64 _len, uint256 _offset) private pure returns (bytes memory encoded) {
64: encoded[0] = bytes1(uint8(_len + _offset));
69: encoded[0] = bytes1(uint8(_offset + hbs + 56));
86: if (_number > type(uint128).max) {
90: if (_number > type(uint64).max) {
94: if (_number > type(uint32).max) {
98: if (_number > type(uint16).max) {
102: if (_number > type(uint8).max) {
```
[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L29) | [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L34) | [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L60) | [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L64) | [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L69) | [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L86) | [90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L90) | [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L94) | [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L98) | [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L102)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

94: function ptrAddIntoActive(uint32 _value) internal view {
106: function ptrShrinkIntoActive(uint32 _shrink) internal view {
125: uint32 _inputMemoryOffset,
        uint32 _inputMemoryLength,
        uint32 _outputMemoryOffset,
        uint32 _outputMemoryLength,
        uint64 _perPrecompileInterpreted
    ) internal pure returns (uint256 rawParams) {
168: function setValueForNextFarCall(uint128 _value) internal returns (bool success) {
228: pubdataPublished = uint32(extractNumberFromMeta(meta, META_GAS_PER_PUBDATA_BYTE_OFFSET, 32));
238: heapSize = uint32(extractNumberFromMeta(meta, META_HEAP_SIZE_OFFSET, 32));
247: auxHeapSize = uint32(extractNumberFromMeta(meta, META_AUX_HEAP_SIZE_OFFSET, 32));
255: shardId = uint8(extractNumberFromMeta(meta, META_SHARD_ID_OFFSET, 8));
264: callerShardId = uint8(extractNumberFromMeta(meta, META_CALLER_SHARD_ID_OFFSET, 8));
273: codeShardId = uint8(extractNumberFromMeta(meta, META_CODE_SHARD_ID_OFFSET, 8));
339: return uint160(_address) <= uint160(MAX_SYSTEM_CONTRACT_ADDRESS);
344: function burnGas(uint32 _gasToPay, uint32 _pubdataToSpend) internal view {
```
[94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L94) | [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L106) | [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L125) | [168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L168) | [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L228) | [238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L238) | [247](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L247) | [255](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L255) | [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L264) | [273](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L273) | [339](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L339) | [344](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L344)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

76: function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {
79: uint32 dataStart;
83: uint32 dataLength = uint32(Utils.safeCastToU32(data.length));
124: uint32 gasLimit,
        address to,
        uint128 value,
        bytes memory data
    ) internal returns (bool success, bytes memory returnData) {
151: uint32 gasLimit,
        address to,
        uint128 value,
        bytes memory data
    ) internal returns (bytes memory returnData) {
215: uint32 dataOffset,
        uint32 memoryPage,
        uint32 dataStart,
        uint32 dataLength,
        uint32 gasPassed,
        uint8 shardId,
        CalldataForwardingMode forwardingMode,
        bool isConstructorCall,
        bool isSystemCall
    ) internal pure returns (uint256 farCallAbi) {
251: uint32 gasPassed,
        uint8 shardId,
        CalldataForwardingMode forwardingMode,
        bool isConstructorCall,
        bool isSystemCall
    ) internal pure returns (uint256 farCallAbiWithEmptyFatPtr) {
```
[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L76) | [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L79) | [83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L83) | [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L124) | [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L151) | [215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L215) | [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L251)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

15: uint8 constant EIP_712_TX_TYPE = 0x71;
18: uint8 constant LEGACY_TX_TYPE = 0x0;
20: uint8 constant EIP_2930_TX_TYPE = 0x01;
22: uint8 constant EIP_1559_TX_TYPE = 0x02;
164: bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
171: uint64 txDataLen = uint64(_transaction.data.length);
199: encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));
232: bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
249: uint64 txDataLen = uint64(_transaction.data.length);
271: encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));
303: bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
321: uint64 txDataLen = uint64(_transaction.data.length);
343: encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));
375: address paymaster = address(uint160(_transaction.paymaster));
406: if (address(uint160(_transaction.paymaster)) != address(0)) {
```
[15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L15) | [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L18) | [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L20) | [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L22) | [164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L164) | [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L171) | [199](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L199) | [232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L232) | [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L249) | [271](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L271) | [303](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L303) | [321](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L321) | [343](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L343) | [375](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L375) | [406](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L406)

```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

21: require(_x <= type(uint128).max, "Overflow");
23: return uint128(_x);
27: require(_x <= type(uint32).max, "Overflow");
29: return uint32(_x);
33: require(_x <= type(uint24).max, "Overflow");
35: return uint24(_x);
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L21) | [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L23) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L27) | [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L29) | [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L33) | [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L35)

```solidity
File: code/system-contracts/contracts/interfaces/IBaseToken.sol

16: function decimals() external pure returns (uint8);
```
[16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IBaseToken.sol#L16)

```solidity
File: code/system-contracts/contracts/interfaces/ICompressor.sol

6: uint8 constant OPERATION_BITMASK = 7;
8: uint8 constant LENGTH_BITS_OFFSET = 3;
10: uint8 constant MAX_ENUMERATION_INDEX_SIZE = 8;
```
[6](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ICompressor.sol#L6) | [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ICompressor.sol#L8) | [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ICompressor.sol#L10)

```solidity
File: code/system-contracts/contracts/interfaces/ISystemContext.sol

44: function txNumberInBlock() external view returns (uint16);
50: function getBlockNumber() external view returns (uint128);
52: function getBlockTimestamp() external view returns (uint128);
54: function getBatchNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);
56: function getL2BlockNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);
```
[44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L44) | [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L50) | [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L52) | [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L54) | [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContext.sol#L56)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

166: uint32(gasleft()),
            DEPLOYER_SYSTEM_CONTRACT,
            0,
            abi.encodeCall(
                IContractDeployer.create2,
                (salt, l2TokenProxyBytecodeHash, abi.encode(address(l2TokenBeacon), ""))
            )
        );
```
[166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L166)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

31: uint8 private decimals_;
93: try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {
115: uint8 _version
    ) external onlyNextVersion(_version) reinitializer(_version) {
134: modifier onlyNextVersion(uint8 _version) {
171: function decimals() public view override returns (uint8) {
184: (result) = abi.decode(_input, (uint8));
```
[31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L31) | [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L93) | [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L115) | [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L134) | [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L171) | [184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L184)

```solidity
File: code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol

6: event BridgeInitialize(address indexed l1Token, string name, string symbol, uint8 decimals);
```
[6](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L6)

```solidity
File: code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol

22: uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
30: l2Address = address(uint160(l1Address) + offset);
40: l1Address = address(uint160(l2Address) - offset);
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L22) | [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L30) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L40)

```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

68: uint160 constant SYSTEM_CONTRACTS_OFFSET = 0x8000; // 2^15
112: return address(uint160(uint256(data)));
```
[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L68) | [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L112)

```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

28: require(_x <= type(uint32).max, "Overflow");
30: return uint32(_x);
37: function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {
40: uint32 dataStart;
44: uint32 dataLength = uint32(Utils.safeCastToU32(data.length));
77: uint32 gasLimit,
        address to,
        uint128 value,
        bytes memory data
    ) internal returns (bool success, bytes memory returnData) {
96: uint32 dataOffset,
        uint32 memoryPage,
        uint32 dataStart,
        uint32 dataLength,
        uint32 gasPassed,
        uint8 shardId,
        CalldataForwardingMode forwardingMode,
        bool isConstructorCall,
        bool isSystemCall
    ) internal pure returns (uint256 farCallAbi) {
122: uint32 gasPassed,
        uint8 shardId,
        CalldataForwardingMode forwardingMode,
        bool isConstructorCall,
        bool isSystemCall
    ) internal pure returns (uint256 farCallAbiWithEmptyFatPtr) {
```
[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L28) | [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L30) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L37) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L40) | [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L44) | [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L77) | [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L96) | [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L122)
</details>

### [G-79] Unlimited gas consumption risk due to external call recipients

When calling an external function without specifying a gas limit , the called contract may consume all the remaining gas, causing the tx to be reverted.
To mitigate this, it is recommended to explicitly set a gas limit when making low level external calls.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

226: (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```
[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L226)

```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

57: bytes memory returnData = EfficientCall.call(gasleft(), _to, msg.value, _data, false);
```
[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L57)
</details>

### [G-80] Use assembly to check for `address(0)`

The usage of inline assembly to check if variable is the zero can save gas compared to traditional `require` or `if` statement checks. 

The assembly check uses the `extcodesize` operation which is generally cheaper in terms of gas.

[More information can be found here.](https://medium.com/@kalexotsu/solidity-assembly-checking-if-an-address-is-0-efficiently-d2bfe071331)

<details>
<summary><i>27 issue instances in 11 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

108: require(_owner != address(0), "ShB owner 0");
188: require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
563: require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
578: if (_refundRecipient == address(0)) {
                refundRecipient = _prevMsgSender != tx.origin
                    ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
```
[108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L108) | [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188) | [563](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563) | [578](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L578)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

130: require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
132: require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");
326: if (_refundRecipient == address(0)) {
            // If the `_refundRecipient` is not provided, we use the `msg.sender` as the recipient.
            _recipient = msg.sender == tx.origin ? msg.sender : AddressAliasHelper.applyL1ToL2Alias(msg.sender);
```
[130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130) | [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132) | [326](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L326)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

42: require(_admin != address(0), "Admin should be non zero address");
```
[42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L42)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

82: require(_initializeData.governor != address(0), "StateTransition: governor zero");
246: if (stateTransition[_chainId] != address(0)) {
```
[82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L82) | [246](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L246)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

25: require(address(_initializeData.verifier) != address(0), "vt");
26: require(_initializeData.admin != address(0), "vy");
27: require(_initializeData.validatorTimelock != address(0), "hc");
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25) | [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L26) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

30: require(facetAddress != address(0), "F"); // Proxy has no facet for this selector
```
[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

183: require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");
```
[183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

141: require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists
161: require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address
175: require(_facet == address(0), "a1"); // facet address must be zero
181: require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet
279: if (_init == address(0)) {
            require(_calldata.length == 0, "H"); // Non-empty calldata for zero address
```
[141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L141) | [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L161) | [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175) | [181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L181) | [279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L279)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

406: if (address(uint160(_transaction.paymaster)) != address(0)) {
```
[406](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L406)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

55: require(_l1Bridge != address(0), "bf");
57: require(_aliasedOwner != address(0), "sf");
68: require(_l1LegecyBridge != address(0), "bf2");
96: if (currentL1Token == address(0)) {
            address deployedToken = _deployL2Token(_l1Token, _data);
129: require(l1Token != address(0), "yh");
```
[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L55) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L57) | [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L68) | [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L96) | [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L129)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

51: require(_l1Address != address(0), "in6"); // Should be non-zero address
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51)
</details>

### [G-81] `internal`/`private` functions only called once can be inlined to save gas

`internal` functions that are only called once should be inlined to save gas. 
Not inlining such functions costs an extra 20 to 40 gas due to the additional `JUMP` instructions and stack operations required for function calls.

<details>
<summary><i>99 issue instances in 27 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

/// @audit function `_depositFundsToSharedBridge()` called only once
160: function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
/// @audit function `_depositFundsToSharedBridge()` called only once
160: function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```
[160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

/// @audit function `_getERC20Getters()` called only once
254: function _getERC20Getters(address _token) internal view returns (bytes memory) {
/// @audit function `_checkWithdrawal()` called only once
458: function _checkWithdrawal(
        uint256 _chainId,
        MessageParams memory _messageParams,
        bytes calldata _message,
        bytes32[] calldata _merkleProof
    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
/// @audit function `_parseL2WithdrawalMessage()` called only once
487: function _parseL2WithdrawalMessage(
        uint256 _chainId,
        bytes memory _l2ToL1message
    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
```
[254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L254) | [458](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L458) | [487](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L487)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

/// @audit function `_setChainIdUpgrade()` called only once
177: function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
```
[177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

/// @audit function `_verifyBatchTimestamp()` called only once
103: function _verifyBatchTimestamp(
        uint256 _packedBatchAndL2BlockTimestamp,
        uint256 _expectedBatchTimestamp,
        uint256 _previousBatchTimestamp
    ) internal view {
/// @audit function `_processL2Logs()` called only once
130: function _processL2Logs(
        CommitBatchInfo calldata _newBatch,
        bytes32 _expectedSystemContractUpgradeTxHash
    ) internal pure returns (LogProcessingOutput memory logOutput) {
/// @audit function `_commitBatchesWithoutSystemContractsUpgrade()` called only once
253: function _commitBatchesWithoutSystemContractsUpgrade(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData
    ) internal {
/// @audit function `_commitBatchesWithSystemContractsUpgrade()` called only once
273: function _commitBatchesWithSystemContractsUpgrade(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData,
        bytes32 _systemContractUpgradeTxHash
    ) internal {
/// @audit function `_collectOperationsFromPriorityQueue()` called only once
308: function _collectOperationsFromPriorityQueue(uint256 _nPriorityOps) internal returns (bytes32 concatHash) {
/// @audit function `_executeOneBatch()` called only once
321: function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {
/// @audit function `_getBatchProofPublicInput()` called only once
453: function _getBatchProofPublicInput(
        bytes32 _prevBatchCommitment,
        bytes32 _currentBatchCommitment,
        VerifierParams memory _verifierParams
    ) internal pure returns (uint256) {
/// @audit function `_createBatchCommitment()` called only once
500: function _createBatchCommitment(
        CommitBatchInfo calldata _newBatchData,
        bytes32 _stateDiffHash,
        bytes32[] memory _blobCommitments,
        bytes32[] memory _blobHashes
    ) internal view returns (bytes32) {
/// @audit function `_batchPassThroughData()` called only once
515: function _batchPassThroughData(CommitBatchInfo calldata _batch) internal pure returns (bytes memory) {
/// @audit function `_batchMetaParameters()` called only once
525: function _batchMetaParameters() internal view returns (bytes memory) {
/// @audit function `_batchAuxiliaryOutput()` called only once
537: function _batchAuxiliaryOutput(
        CommitBatchInfo calldata _batch,
        bytes32 _stateDiffHash,
        bytes32[] memory _blobCommitments,
        bytes32[] memory _blobHashes
    ) internal pure returns (bytes memory) {
/// @audit function `_encodeBlobAuxilaryOutput()` called only once
561: function _encodeBlobAuxilaryOutput(
        bytes32[] memory _blobCommitments,
        bytes32[] memory _blobHashes
    ) internal pure returns (bytes32[] memory blobAuxOutputWords) {
/// @audit function `_checkBit()` called only once
592: function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {
/// @audit function `_setBit()` called only once
597: function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {
/// @audit function `_pointEvaluationPrecompile()` called only once
605: function _pointEvaluationPrecompile(
        bytes32 _versionedHash,
        bytes32 _openingPoint,
        bytes calldata _openingValueCommitmentProof
    ) internal view {
/// @audit function `_verifyBlobInformation()` called only once
625: function _verifyBlobInformation(
        bytes calldata _pubdataCommitments,
        bytes32[] memory _blobHashes
    ) internal view returns (bytes32[] memory blobCommitments) {
```
[103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L103) | [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L130) | [253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L253) | [273](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L273) | [308](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L308) | [321](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L321) | [453](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L453) | [500](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L500) | [515](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515) | [525](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525) | [537](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537) | [561](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L561) | [592](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L592) | [597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597) | [605](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L605) | [625](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L625)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

/// @audit function `_L2MessageToLog()` called only once
130: function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {
/// @audit function `_requestL2Transaction()` called only once
258: function _requestL2Transaction(
        uint256 _mintValue,
        WritePriorityOpParams memory _params,
        bytes memory _calldata,
        bytes[] memory _factoryDeps
    ) internal returns (bytes32 canonicalTxHash) {
/// @audit function `_serializeL2Transaction()` called only once
289: function _serializeL2Transaction(
        WritePriorityOpParams memory _priorityOpParams,
        bytes memory _calldata,
        bytes[] memory _factoryDeps
    ) internal pure returns (L2CanonicalTransaction memory transaction) {
/// @audit function `_writePriorityOp()` called only once
316: function _writePriorityOp(
        WritePriorityOpParams memory _priorityOpParams,
        bytes memory _calldata,
        bytes[] memory _factoryDeps
    ) internal returns (bytes32 canonicalTxHash) {
/// @audit function `_hashFactoryDeps()` called only once
353: function _hashFactoryDeps(bytes[] memory _factoryDeps) internal pure returns (uint256[] memory hashedFactoryDeps) {
```
[130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L130) | [258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L258) | [289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L289) | [316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L316) | [353](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L353)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

/// @audit function `_setL2DefaultAccountBytecodeHash()` called only once
92: function _setL2DefaultAccountBytecodeHash(bytes32 _l2DefaultAccountBytecodeHash) private {
/// @audit function `_setL2BootloaderBytecodeHash()` called only once
109: function _setL2BootloaderBytecodeHash(bytes32 _l2BootloaderBytecodeHash) private {
/// @audit function `_setVerifier()` called only once
126: function _setVerifier(IVerifier _newVerifier) private {
/// @audit function `_setVerifierParams()` called only once
142: function _setVerifierParams(VerifierParams calldata _newVerifierParams) private {
/// @audit function `_upgradeVerifier()` called only once
163: function _upgradeVerifier(address _newVerifier, VerifierParams calldata _verifierParams) internal {
/// @audit function `_setBaseSystemContracts()` called only once
171: function _setBaseSystemContracts(bytes32 _bootloaderHash, bytes32 _defaultAccountHash) internal {
/// @audit function `_setL2SystemContractUpgrade()` called only once
180: function _setL2SystemContractUpgrade(
        L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
        bytes[] calldata _factoryDeps,
        uint256 _newProtocolVersion
    ) internal returns (bytes32) {
/// @audit function `_verifyFactoryDeps()` called only once
222: function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure {
/// @audit function `_setNewProtocolVersion()` called only once
236: function _setNewProtocolVersion(uint256 _newProtocolVersion) internal virtual {
/// @audit function `_upgradeL1Contract()` called only once
263: function _upgradeL1Contract(bytes calldata _customCallDataForUpgrade) internal virtual {}
/// @audit function `_postUpgrade()` called only once
269: function _postUpgrade(bytes calldata _customCallDataForUpgrade) internal virtual {}
```
[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L92) | [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L109) | [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L126) | [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L142) | [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L163) | [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L171) | [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L180) | [222](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L222) | [236](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L236) | [263](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L263) | [269](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L269)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

/// @audit function `_setNewProtocolVersion()` called only once
20: function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

/// @audit function `bytecodeLen()` called only once
49: function bytecodeLen(bytes32 _bytecodeHash) internal pure returns (uint256 codeLengthInWords) {
```
[49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L49)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

/// @audit function `_addFunctions()` called only once
126: function _addFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {
/// @audit function `_replaceFunctions()` called only once
149: function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {
/// @audit function `_removeFunctions()` called only once
172: function _removeFunctions(address _facet, bytes4[] memory _selectors) private {
/// @audit function `_removeFacet()` called only once
257: function _removeFacet(address _facet) private {
/// @audit function `_initializeDiamondCut()` called only once
278: function _initializeDiamondCut(address _init, bytes memory _calldata) private {
```
[126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L126) | [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L149) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L172) | [257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L257) | [278](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L278)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

/// @audit function `getMinimalPriorityTransactionGasLimit()` called only once
69: function getMinimalPriorityTransactionGasLimit(
        uint256 _encodingLength,
        uint256 _numberOfFactoryDependencies,
        uint256 _l2GasPricePerPubdata
    ) internal pure returns (uint256) {
/// @audit function `getTransactionBodyGasLimit()` called only once
109: function getTransactionBodyGasLimit(
        uint256 _totalGasLimit,
        uint256 _encodingLength
    ) internal pure returns (uint256 txBodyGasLimit) {
/// @audit function `getOverheadForTransaction()` called only once
128: function getOverheadForTransaction(
        uint256 _encodingLength
    ) internal pure returns (uint256 batchOverheadForTransaction) {
```
[69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L69) | [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L109) | [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L128)

```solidity
File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

/// @audit function `_initializeReentrancyGuard()` called only once
46: function _initializeReentrancyGuard() private {
```
[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L46)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

/// @audit function `encodeLegacyTransactionHash()` called only once
44: function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {
/// @audit function `encodeEIP2930TransactionHash()` called only once
139: function encodeEIP2930TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {
/// @audit function `encodeEIP1559TransactionHash()` called only once
229: function encodeEIP1559TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {
```
[44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L44) | [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L139) | [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L229)

```solidity
File: code/system-contracts/contracts/Compressor.sol

/// @audit function `_decodeRawBytecode()` called only once
197: function _decodeRawBytecode(
        bytes calldata _rawCompressedData
    ) internal pure returns (bytes calldata dictionary, bytes calldata encodedData) {
```
[197](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L197)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

/// @audit function `_performDeployOnAddress()` called only once
283: function _performDeployOnAddress(
        bytes32 _bytecodeHash,
        address _newAddress,
        AccountAbstractionVersion _aaVersion,
        bytes calldata _input
    ) internal {
/// @audit function `_storeConstructingByteCodeHashOnAddress()` called only once
309: function _storeConstructingByteCodeHashOnAddress(address _newAddress, bytes32 _bytecodeHash) internal {
```
[283](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L283) | [309](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L309)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

/// @audit function `_validateTransaction()` called only once
78: function _validateTransaction(
        bytes32 _suggestedSignedHash,
        Transaction calldata _transaction
    ) internal returns (bytes4 magic) {
/// @audit function `_execute()` called only once
131: function _execute(Transaction calldata _transaction) internal {
/// @audit function `_isValidSignature()` called only once
159: function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {
```
[78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L78) | [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L131) | [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L159)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

/// @audit function `_validateBytecode()` called only once
74: function _validateBytecode(bytes32 _bytecodeHash) internal pure {
```
[74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L74)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

/// @audit function `sha256GasCost()` called only once
61: function sha256GasCost(uint256 _length) internal pure returns (uint256) {
```
[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L61)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

/// @audit function `_getL1WithdrawMessage()` called only once
112: function _getL1WithdrawMessage(address _to, uint256 _amount) internal pure returns (bytes memory) {
/// @audit function `_getExtendedWithdrawMessage()` called only once
117: function _getExtendedWithdrawMessage(
        address _to,
        uint256 _amount,
        address _sender,
        bytes memory _additionalData
    ) internal pure returns (bytes memory) {
```
[112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L112) | [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L117)

```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

/// @audit function `_getAbiParams()` called only once
25: function _getAbiParams() internal view returns (uint256 value, bool isSystemCall, address to) {
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L25)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

/// @audit function `_calculateL2BlockHash()` called only once
221: function _calculateL2BlockHash(
        uint128 _blockNumber,
        uint128 _blockTimestamp,
        bytes32 _prevL2BlockHash,
        bytes32 _blockTxsRollingHash
    ) internal pure returns (bytes32) {
/// @audit function `_calculateLegacyL2BlockHash()` called only once
233: function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {
/// @audit function `_upgradeL2Blocks()` called only once
241: function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {
/// @audit function `_setVirtualBlock()` called only once
263: function _setVirtualBlock(
        uint128 _l2BlockNumber,
        uint128 _maxVirtualBlocksToCreate,
        uint128 _newTimestamp
    ) internal {
/// @audit function `_ensureBatchConsistentWithL2Block()` called only once
427: function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {
```
[221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L221) | [233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L233) | [241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L241) | [263](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L263) | [427](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L427)

```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

/// @audit function `rawCall()` called only once
124: function rawCall(
        uint256 _gas,
        address _address,
        uint256 _value,
        bytes calldata _data,
        bool _isSystem
    ) internal returns (bool success) {
/// @audit function `rawStaticCall()` called only once
159: function rawStaticCall(uint256 _gas, address _address, bytes calldata _data) internal view returns (bool success) {
/// @audit function `rawDelegateCall()` called only once
173: function rawDelegateCall(uint256 _gas, address _address, bytes calldata _data) internal returns (bool success) {
/// @audit function `rawMimicCall()` called only once
191: function rawMimicCall(
        uint256 _gas,
        address _address,
        bytes calldata _data,
        address _whoToMimic,
        bool _isConstructor,
        bool _isSystem
    ) internal returns (bool success) {
/// @audit function `propagateRevert()` called only once
232: function propagateRevert() internal pure {
```
[124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L124) | [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L159) | [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L173) | [191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L191) | [232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L232)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

/// @audit function `unsafePrecompileCall()` called only once
148: function unsafePrecompileCall(
        uint256 _rawParams,
        uint32 _gasToBurn,
        uint32 _pubdataToSpend
    ) internal view returns (bool success) {
/// @audit function `getZkSyncMetaBytes()` called only once
203: function getZkSyncMetaBytes() internal view returns (uint256 meta) {
/// @audit function `getPubdataPublishedFromMeta()` called only once
227: function getPubdataPublishedFromMeta(uint256 meta) internal pure returns (uint32 pubdataPublished) {
/// @audit function `getHeapSizeFromMeta()` called only once
237: function getHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 heapSize) {
/// @audit function `getAuxHeapSizeFromMeta()` called only once
246: function getAuxHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 auxHeapSize) {
/// @audit function `getShardIdFromMeta()` called only once
254: function getShardIdFromMeta(uint256 meta) internal pure returns (uint8 shardId) {
/// @audit function `getCallerShardIdFromMeta()` called only once
263: function getCallerShardIdFromMeta(uint256 meta) internal pure returns (uint8 callerShardId) {
/// @audit function `getCodeShardIdFromMeta()` called only once
272: function getCodeShardIdFromMeta(uint256 meta) internal pure returns (uint8 codeShardId) {
/// @audit function `getCallFlags()` called only once
296: function getCallFlags() internal view returns (uint256 callFlags) {
```
[148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L148) | [203](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L203) | [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L227) | [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L237) | [246](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L246) | [254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L254) | [263](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L263) | [272](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L272) | [296](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L296)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

/// @audit function `systemCall()` called only once
76: function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {
/// @audit function `systemCallWithReturndata()` called only once
123: function systemCallWithReturndata(
        uint32 gasLimit,
        address to,
        uint128 value,
        bytes memory data
    ) internal returns (bool success, bytes memory returnData) {
/// @audit function `getFarCallABI()` called only once
214: function getFarCallABI(
        uint32 dataOffset,
        uint32 memoryPage,
        uint32 dataStart,
        uint32 dataLength,
        uint32 gasPassed,
        uint8 shardId,
        CalldataForwardingMode forwardingMode,
        bool isConstructorCall,
        bool isSystemCall
    ) internal pure returns (uint256 farCallAbi) {
/// @audit function `getFarCallABIWithEmptyFatPointer()` called only once
250: function getFarCallABIWithEmptyFatPointer(
        uint32 gasPassed,
        uint8 shardId,
        CalldataForwardingMode forwardingMode,
        bool isConstructorCall,
        bool isSystemCall
    ) internal pure returns (uint256 farCallAbiWithEmptyFatPtr) {
```
[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L76) | [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L123) | [214](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L214) | [250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L250)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

/// @audit function `_encodeHashEIP712Transaction()` called only once
118: function _encodeHashEIP712Transaction(Transaction calldata _transaction) private view returns (bytes32) {
/// @audit function `_encodeHashLegacyTransaction()` called only once
147: function _encodeHashLegacyTransaction(Transaction calldata _transaction) private view returns (bytes32) {
/// @audit function `_encodeHashEIP2930Transaction()` called only once
219: function _encodeHashEIP2930Transaction(Transaction calldata _transaction) private view returns (bytes32) {
/// @audit function `_encodeHashEIP1559Transaction()` called only once
289: function _encodeHashEIP1559Transaction(Transaction calldata _transaction) private view returns (bytes32) {
```
[118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L118) | [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L147) | [219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L219) | [289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L289)

```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

/// @audit function `bytecodeLenInWords()` called only once
44: function bytecodeLenInWords(bytes32 _bytecodeHash) internal pure returns (uint256 codeLengthInWords) {
/// @audit function `constructedBytecodeHash()` called only once
71: function constructedBytecodeHash(bytes32 _bytecodeHash) internal pure returns (bytes32) {
```
[44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L44) | [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L71)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

/// @audit function `_deployL2Token()` called only once
109: function _deployL2Token(address _l1Token, bytes calldata _data) internal returns (address) {
/// @audit function `_getL1WithdrawMessage()` called only once
138: function _getL1WithdrawMessage(
        address _to,
        address _l1Token,
        uint256 _amount
    ) internal pure returns (bytes memory) {
/// @audit function `_deployBeaconProxy()` called only once
164: function _deployBeaconProxy(bytes32 salt) internal returns (BeaconProxy proxy) {
```
[109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L109) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L138) | [164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L164)

```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

/// @audit function `safeCastToU32()` called only once
27: function safeCastToU32(uint256 _x) internal pure returns (uint32) {
/// @audit function `systemCall()` called only once
37: function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {
/// @audit function `getFarCallABI()` called only once
95: function getFarCallABI(
        uint32 dataOffset,
        uint32 memoryPage,
        uint32 dataStart,
        uint32 dataLength,
        uint32 gasPassed,
        uint8 shardId,
        CalldataForwardingMode forwardingMode,
        bool isConstructorCall,
        bool isSystemCall
    ) internal pure returns (uint256 farCallAbi) {
/// @audit function `getFarCallABIWithEmptyFatPointer()` called only once
121: function getFarCallABIWithEmptyFatPointer(
        uint32 gasPassed,
        uint8 shardId,
        CalldataForwardingMode forwardingMode,
        bool isConstructorCall,
        bool isSystemCall
    ) internal pure returns (uint256 farCallAbiWithEmptyFatPtr) {
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L27) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L37) | [95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L95) | [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L121)
</details>

### [G-82] Inefficient Use of String Constants

In Solidity, if data can fit into 32 bytes, it's more efficient to use the bytes32 datatype instead of bytes or strings.

This is because the bytes32 datatype is cheaper in terms of gas usage.

<details>
<summary><i>5 issue instances in 5 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

26: string public constant override getName = "ValidatorTimelock";
```
[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

20: string public constant override getName = "AdminFacet";
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

27: string public constant override getName = "ExecutorFacet";
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

25: string public constant override getName = "GettersFacet";
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

35: string public constant override getName = "MailboxFacet";
```
[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35)
</details>

### [G-83] Consider using OZ EnumerateSet in place of nested mappings

Nested mappings and multi-dimensional arrays in Solidity operate through a process of double hashing, wherein the original storage slot and the first key are concatenated and hashed, and then this hash is again concatenated with the second key and hashed. This process can be quite gas expensive due to the double-hashing operation and subsequent storage operation (sstore).

A possible optimization involves manually concatenating the keys followed by a single hash operation and an sstore. However, this technique introduces the risk of storage collision, especially when there are other nested hash maps in the contract that use the same key types. Because Solidity is unaware of the number and structure of nested hash maps in a contract, it follows a conservative approach in computing the storage slot to avoid possible collisions.

OpenZeppelin's EnumerableSet provides a potential solution to this problem. It creates a data structure that combines the benefits of set operations with the ability to enumerate stored elements, which is not natively available in Solidity. EnumerableSet handles the element uniqueness internally and can therefore provide a more gas-efficient and collision-resistant alternative to nested mappings or multi-dimensional arrays in certain scenarios.

<details>
<summary><i>13 issue instances in 6 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

27: mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
        public isWithdrawalFinalized;
32: mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
        public depositAmount;
51: mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;
27: mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
        public isWithdrawalFinalized;
32: mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
        public depositAmount;
51: mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27) | [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L32) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L51) | [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27) | [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L32) | [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L51)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

52: mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
        public
        override depositHappened;
57: mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
        public isWithdrawalFinalized;
65: mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;
```
[52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L52) | [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57) | [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L65)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

50: mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

114: mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;
```
[114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L114)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

21: mapping(uint256 contractAddress => mapping(uint256 index => bytes32 value)) internal immutableDataStorage;
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L21)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

41: mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L41)
</details>

### [G-84] Declare `immutable` as `private` to save gas

Using `private` instead of `public` for immutables saves gas.

The compiler doesn't need to create non-payable getter functions for deployment calldata, store the bytes of the value outside of where it's used, or add another entry to the method ID table, saving 3406-3606 gas in deployment.

<details>
<summary><i>6 issue instances in 3 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

23: IL1SharedBridge public immutable override sharedBridge;
23: IL1SharedBridge public immutable override sharedBridge;
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L23) | [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L23)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

34: address public immutable override l1WethAddress;
37: IBridgehub public immutable override bridgehub;
40: IL1ERC20Bridge public immutable override legacyBridge;
```
[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L34) | [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L37) | [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L40)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

27: address public immutable bridgehub;
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L27)
</details>

### [G-85] State variables should be cached in stack rather than re-reading them from storage

Caching state variables in local variables can optimize gas usage, as accessing the stack is cheaper than accessing storage.

The instances below point to the second+ access of a state variable within a function.

<details>
<summary><i>15 issue instances in 4 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

/// @audit function acceptAdmin() uses state variable `pendingAdmin` 3 times
61: address currentPendingAdmin = pendingAdmin;
66: delete pendingAdmin;
69: emit NewAdmin(previousAdmin, pendingAdmin);
/// @audit function createNewChain() uses state variable `sharedBridge` 2 times
130: require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
140: address(sharedBridge),
```
[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L61) | [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L66) | [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69) | [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130) | [140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L140)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

/// @audit function acceptAdmin() uses state variable `pendingAdmin` 3 times
120: address currentPendingAdmin = pendingAdmin;
125: delete pendingAdmin;
128: emit NewAdmin(previousAdmin, pendingAdmin);
/// @audit function _setChainIdUpgrade() uses state variable `protocolVersion` 3 times
192: nonce: protocolVersion,
216: newProtocolVersion: protocolVersion
227: emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
```
[120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L120) | [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L125) | [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L128) | [192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L192) | [216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L216) | [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

/// @audit function _processL2ToL1Log() uses state variable `numberOfLogsToProcess` 2 times
108: logIdInMerkleTree = numberOfLogsToProcess;
109: numberOfLogsToProcess++;
```
[108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L108) | [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L109)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

/// @audit function getCurrentPubdataSpent() uses state variable `basePubdataSpent` 2 times
119: return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;
119: return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;
```
[119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L119) | [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L119)
</details>

### [G-86] Division by powers of two should use bit shifting

When dividing by powers of two (e.g., 2, 4, 8), it is more efficient to use bit shifting.

`<x> / 2` can be replaced with `<x> >> 1`, as both operations use the SHR opcode in the compiler.
However, the division approach incurs an additional 20 gas overhead due to jumps to and from a compiler utility function that introduces checks.

This overhead can be avoided by using `unchecked` around the division by powers of two.

<details>
<summary><i>5 issue instances in 4 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

25: uint256 bytecodeLenInWords = _bytecode.length / 32;
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

23: uint256 mapValue = _map.map[_index / 8];
43: uint256 mapIndex = _index / 8;
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L23) | [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L43)

```solidity
File: code/system-contracts/contracts/Compressor.sol

57: dictionary.length / 8 <= encodedData.length / 2,
```
[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L57)

```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

86: uint256 lengthInWords = _bytecode.length / 32;
```
[86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L86)
</details>

### [G-87] Optimize names to save gas

Function names for public and external methods, as well as public state variable names, can be optimized to achieve gas savings.
By renaming functions to generate method IDs with two leading zero bytes, you can save 128 gas during contract deployment.
Further, renaming functions for lower method IDs can conserve 22 gas per call for each sorted position shifted.

Optimizing function names for gas efficiency can result in significant savings, especially for frequently called functions or heavily deployed contracts. 
Reference: [Solidity Gas Optimizations - Function Name](https://blog.emn178.cc/en/post/solidity-gas-optimization-function-name/)

<details>
<summary><i>59 issue instances in 57 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

19: contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {
19: contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {
```
[19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L19) | [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L19)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

30: contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {
```
[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L30)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

15: contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {
```
[15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L15)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

20: contract Governance is IGovernance, Ownable2Step {
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L20)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

25: contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L25)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

22: contract ValidatorTimelock is IExecutor, Ownable2Step {
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L22)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

17: contract DiamondInit is ZkSyncStateTransitionBase, IDiamondInit {
```
[17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L17)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

10: contract DiamondProxy {
```
[10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L10)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

18: contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {
```
[18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L18)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

22: contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L22)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

20: contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L20)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

30: contract MailboxFacet is ZkSyncStateTransitionBase, IMailbox {
```
[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L30)

```solidity
File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

11: contract ZkSyncStateTransitionBase is ReentrancyGuard {
```
[11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L11)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

44: abstract contract BaseZkSyncUpgrade is ZkSyncStateTransitionBase {
```
[44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L44)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

17: abstract contract BaseZkSyncUpgradeGenesis is BaseZkSyncUpgrade {
```
[17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L17)

```solidity
File: code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

10: contract DefaultUpgrade is BaseZkSyncUpgrade {
```
[10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L10)

```solidity
File: code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

11: contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {
```
[11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L11)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

10: library L2ContractHelper {
```
[10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L10)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol

10: library UncheckedMath {
```
[10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L10)

```solidity
File: code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol

18: library UnsafeBytes {
```
[18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L18)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

11: library Diamond {
```
[11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L11)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

8: library LibMap {
```
[8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L8)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

9: library Merkle {
```
[9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L9)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

20: library PriorityQueue {
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L20)

```solidity
File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

13: library TransactionValidator {
```
[13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L13)

```solidity
File: code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

25: abstract contract ReentrancyGuard {
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L25)

```solidity
File: code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

20: library AddressAliasHelper {
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L20)

```solidity
File: code/system-contracts/contracts/AccountCodeStorage.sol

22: contract AccountCodeStorage is IAccountCodeStorage {
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L22)

```solidity
File: code/system-contracts/contracts/BootloaderUtilities.sol

16: contract BootloaderUtilities is IBootloaderUtilities {
```
[16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L16)

```solidity
File: code/system-contracts/contracts/ComplexUpgrader.sol

14: contract ComplexUpgrader is IComplexUpgrader {
```
[14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L14)

```solidity
File: code/system-contracts/contracts/Compressor.sol

22: contract Compressor is ICompressor, ISystemContract {
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L22)

```solidity
File: code/system-contracts/contracts/ContractDeployer.sol

23: contract ContractDeployer is IContractDeployer, ISystemContract {
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L23)

```solidity
File: code/system-contracts/contracts/DefaultAccount.sol

19: contract DefaultAccount is IAccount {
```
[19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L19)

```solidity
File: code/system-contracts/contracts/EmptyContract.sol

10: contract EmptyContract {
```
[10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/EmptyContract.sol#L10)

```solidity
File: code/system-contracts/contracts/ImmutableSimulator.sol

18: contract ImmutableSimulator is IImmutableSimulator {
```
[18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L18)

```solidity
File: code/system-contracts/contracts/KnownCodesStorage.sol

18: contract KnownCodesStorage is IKnownCodesStorage, ISystemContract {
```
[18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L18)

```solidity
File: code/system-contracts/contracts/L1Messenger.sol

25: contract L1Messenger is IL1Messenger, ISystemContract {
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L25)

```solidity
File: code/system-contracts/contracts/L2BaseToken.sol

18: contract L2BaseToken is IBaseToken, ISystemContract {
```
[18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L18)

```solidity
File: code/system-contracts/contracts/MsgValueSimulator.sol

19: contract MsgValueSimulator is ISystemContract {
```
[19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L19)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

27: contract NonceHolder is INonceHolder, ISystemContract {
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L27)

```solidity
File: code/system-contracts/contracts/PubdataChunkPublisher.sol

16: contract PubdataChunkPublisher is IPubdataChunkPublisher, ISystemContract {
```
[16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L16)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

17: contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract {
```
[17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L17)

```solidity
File: code/system-contracts/contracts/GasBoundCaller.sol

15: contract GasBoundCaller {
```
[15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L15)

```solidity
File: code/system-contracts/contracts/libraries/EfficientCall.sol

32: library EfficientCall {
```
[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L32)

```solidity
File: code/system-contracts/contracts/libraries/RLPEncoder.sol

10: library RLPEncoder {
```
[10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L10)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractHelper.sol

41: library SystemContractHelper {
```
[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L41)

```solidity
File: code/system-contracts/contracts/libraries/SystemContractsCaller.sol

68: library SystemContractsCaller {
```
[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L68)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

78: library TransactionHelper {
```
[78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L78)

```solidity
File: code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol

18: library UnsafeBytesCalldata {
```
[18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L18)

```solidity
File: code/system-contracts/contracts/libraries/Utils.sol

11: library Utils {
```
[11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L11)

```solidity
File: code/system-contracts/contracts/interfaces/ISystemContract.sol

17: abstract contract ISystemContract {
```
[17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L17)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

23: contract L2SharedBridge is IL2SharedBridge, Initializable {
```
[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L23)

```solidity
File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

15: contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {
```
[15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L15)

```solidity
File: code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol

20: library AddressAliasHelper {
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L20)

```solidity
File: code/contracts/zksync/contracts/ForceDeployUpgrader.sol

10: contract ForceDeployUpgrader {
```
[10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L10)

```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

83: library L2ContractHelper {
```
[83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L83)

```solidity
File: code/contracts/zksync/contracts/SystemContractsCaller.sol

25: library Utils {
36: library SystemContractsCaller {
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L25) | [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L36)
</details>

### [G-88] Avoid updating storage when the value hasn't changed

A check regarding whether the current value and the new value are the same should be added.
This helps prevent unnecessary state changes and events in case the new value is the same as the current value.

<details>
<summary><i>22 issue instances in 7 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

/// @audit Missing `_newPendingAdmin` check before state change
55: pendingAdmin = _newPendingAdmin;
```
[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55)

```solidity
File: code/contracts/ethereum/contracts/governance/Governance.sol

/// @audit Missing `_newDelay` check before state change
251: minDelay = _newDelay;
/// @audit Missing `_newSecurityCouncil` check before state change
258: securityCouncil = _newSecurityCouncil;
```
[251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L251) | [258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L258)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

/// @audit Missing `_newPendingAdmin` check before state change
114: pendingAdmin = _newPendingAdmin;
/// @audit Missing `_validatorTimelock` check before state change
133: validatorTimelock = _validatorTimelock;
/// @audit Missing `_newProtocolVersion` check before state change
148: protocolVersion = _newProtocolVersion;
```
[114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L114) | [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L133) | [148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L148)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

/// @audit Missing `_stateTransitionManager` check before state change
74: stateTransitionManager = _stateTransitionManager;
/// @audit Missing `_executionDelay` check before state change
97: executionDelay = _executionDelay;
```
[74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L74) | [97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L97)

```solidity
File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

/// @audit Missing `_bootloaderHash` check before state change
172: _setL2BootloaderBytecodeHash(_bootloaderHash);
/// @audit Missing `_defaultAccountHash` check before state change
173: _setL2DefaultAccountBytecodeHash(_defaultAccountHash);
```
[172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L172) | [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L173)

```solidity
File: code/system-contracts/contracts/NonceHolder.sol

/// @audit Missing `_value` check before state change
93: nonceValues[addressAsKey][_key] = _value;
```
[93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L93)

```solidity
File: code/system-contracts/contracts/SystemContext.sol

/// @audit Missing `_newChainId` check before state change
85: chainId = _newChainId;
/// @audit Missing `_newOrigin` check before state change
100: origin = _newOrigin;
/// @audit Missing `_gasPrice` check before state change
106: gasPrice = _gasPrice;
/// @audit Missing `_basePubdataSpent` check before state change
113: basePubdataSpent = _basePubdataSpent;
/// @audit Missing `_gasPerPubdataByte` check before state change
114: gasPerPubdataByte = _gasPerPubdataByte;
/// @audit Missing `_prevL2BlockHash` check before state change
319: _setL2BlockHash(_l2BlockNumber - 1, _prevL2BlockHash);
/// @audit Missing `_expectedPrevL2BlockHash` check before state change
365: _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);
/// @audit Missing `_expectedPrevL2BlockHash` check before state change
392: _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);
/// @audit Missing `_l2BlockTimestamp` check before state change
397: _setVirtualBlock(_l2BlockNumber, _maxVirtualBlocksToCreate, _l2BlockTimestamp);
/// @audit Missing `_prevBatchHash` check before state change
455: batchHashes[previousBatchNumber] = _prevBatchHash;
/// @audit Missing `_baseFee` check before state change
462: baseFee = _baseFee;
```
[85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L85) | [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L100) | [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L106) | [113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L113) | [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L114) | [319](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L319) | [365](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L365) | [392](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L392) | [397](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L397) | [455](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L455) | [462](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L462)
</details>

### [G-89] Optimize External Calls with Assembly for Memory Efficiency

Using interfaces to make external contract calls in Solidity is convenient but can be inefficient in terms of memory utilization.
Each such call involves creating a new memory location to store the data being passed, thus incurring memory expansion costs. 

Inline assembly allows for optimized memory usage by re-using already allocated memory spaces or using the scratch space for smaller datasets.
This can result in notable gas savings, especially for contracts that make frequent external calls.

Additionally, using inline assembly enables important safety checks like verifying if the target address has code deployed to it using `extcodesize(addr)` before making the call, mitigating risks associated with contract interactions.

<details>
<summary><i>39 issue instances in 8 files:</i></summary>

```solidity
File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

65: uint256 amount = IERC20(_token).balanceOf(address(this));
67: IERC20(_token).safeTransfer(address(sharedBridge), amount);
189: sharedBridge.claimFailedDepositLegacyErc20Bridge(
            _depositSender,
            _l1Token,
            amount,
            _l2TxHash,
            _l2BatchNumber,
            _l2MessageIndex,
            _l2TxNumberInBatch,
            _merkleProof
        );
218: (address l1Receiver, address l1Token, uint256 amount) = sharedBridge.finalizeWithdrawalLegacyErc20Bridge(
            _l2BatchNumber,
            _l2MessageIndex,
            _l2TxNumberInBatch,
            _message,
            _merkleProof
        );
65: uint256 amount = IERC20(_token).balanceOf(address(this));
67: IERC20(_token).safeTransfer(address(sharedBridge), amount);
189: sharedBridge.claimFailedDepositLegacyErc20Bridge(
            _depositSender,
            _l1Token,
            amount,
            _l2TxHash,
            _l2BatchNumber,
            _l2MessageIndex,
            _l2TxNumberInBatch,
            _merkleProof
        );
218: (address l1Receiver, address l1Token, uint256 amount) = sharedBridge.finalizeWithdrawalLegacyErc20Bridge(
            _l2BatchNumber,
            _l2MessageIndex,
            _l2TxNumberInBatch,
            _message,
            _merkleProof
        );
```
[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65) | [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67) | [189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L189) | [218](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L218) | [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65) | [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67) | [189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L189) | [218](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L218)

```solidity
File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

127: uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
128: uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
130: IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);
131: uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
138: require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");
195: require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");
316: bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
                _chainId,
                _l2TxHash,
                _l2BatchNumber,
                _l2MessageIndex,
                _l2TxNumberInBatch,
                _merkleProof,
                TxStatus.Failure
            );
362: IERC20(_l1Token).safeTransfer(_depositSender, _amount);
396: require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");
423: bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
                _l2BatchNumber,
                _l2MessageIndex
            );
452: IERC20(l1Token).safeTransfer(l1Receiver, amount);
467: bool baseTokenWithdrawal = (l1Token == bridgehub.baseToken(_chainId));
477: bool success = bridgehub.proveL2MessageInclusion(
            _chainId,
            _messageParams.l2BatchNumber,
            _messageParams.l2MessageIndex,
            l2ToL1Message,
            _merkleProof
        );
508: l1Token = bridgehub.baseToken(_chainId);
```
[127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127) | [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L128) | [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L130) | [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131) | [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138) | [195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195) | [316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L316) | [362](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L362) | [396](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L396) | [423](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L423) | [452](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L452) | [467](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L467) | [477](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L477) | [508](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L508)

```solidity
File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

137: IStateTransitionManager(_stateTransitionManager).createNewChain(
            _chainId,
            _baseToken,
            address(sharedBridge),
            _admin,
            _initData
        );
160: return IZkSyncStateTransition(stateTransition).proveL2MessageInclusion(_batchNumber, _index, _message, _proof);
172: return IZkSyncStateTransition(stateTransition).proveL2LogInclusion(_batchNumber, _index, _log, _proof);
187: IZkSyncStateTransition(stateTransition).proveL1ToL2TransactionStatus(
                _l2TxHash,
                _l2BatchNumber,
                _l2MessageIndex,
                _l2TxNumberInBatch,
                _merkleProof,
                _status
            );
206: IZkSyncStateTransition(stateTransition).l2TransactionBaseCost(
                _gasPrice,
                _l2GasLimit,
                _l2GasPerPubdataByteLimit
            );
238: canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction(
            BridgehubL2TransactionRequest({
                sender: msg.sender,
                contractL2: _request.l2Contract,
                mintValue: _request.mintValue,
                l2Value: _request.l2Value,
                l2Calldata: _request.l2Calldata,
                l2GasLimit: _request.l2GasLimit,
                l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
                factoryDeps: _request.factoryDeps,
                refundRecipient: refundRecipient
            })
        );
304: canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction(
            BridgehubL2TransactionRequest({
                sender: _request.secondBridgeAddress,
                contractL2: outputRequest.l2Contract,
                mintValue: _request.mintValue,
                l2Value: _request.l2Value,
                l2Calldata: outputRequest.l2Calldata,
                l2GasLimit: _request.l2GasLimit,
                l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
                factoryDeps: outputRequest.factoryDeps,
                refundRecipient: refundRecipient
            })
        );
```
[137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L137) | [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L160) | [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L172) | [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L187) | [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L206) | [238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L238) | [304](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L304)

```solidity
File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

226: IAdmin(_chainContract).executeUpgrade(cutData);
```
[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L226)

```solidity
File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62: require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");
226: address contractAddress = stateTransitionManager.stateTransition(_chainId);
```
[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62) | [226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L226)

```solidity
File: code/system-contracts/contracts/libraries/TransactionHelper.sol

377: uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);
382: IERC20(token).safeApprove(paymaster, 0);
383: IERC20(token).safeApprove(paymaster, minAllowance);
```
[377](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377) | [382](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L382) | [383](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L383)

```solidity
File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

66: l2TokenBeacon.transferOwnership(_aliasedOwner);
104: IL2StandardToken(expectedL2Token).bridgeMint(_l2Receiver, _amount);
126: IL2StandardToken(_l2Token).bridgeBurn(msg.sender, _amount);
```
[66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L66) | [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L104) | [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L126)

```solidity
File: code/contracts/zksync/contracts/L2ContractHelper.sol

91: return L2_MESSENGER.sendToL1(_message);
```
[91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L91)
</details>

