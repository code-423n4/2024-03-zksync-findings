
# Gas Optimizations

| Number | Issue | Instences |
|--------|-------|-----------|
|[G-01]| Don’t make variables public unless necessary | 4 |
|[G-02]| Use assembly to emit an event | 75 | 
|[G-03]| Use of memory instead of storage for struct/array state variables | 10 | 
|[G-04]| Optimal Struct Variable Order | 14 | 
|[G-05]| Consider using OpenZeppelin's EnumerateSet instead of nested mappings | 4 |
|[G-06]| Constructors can be marked payable | 7 | 
|[G-07]| Avoid Unnecessary Use of Storage | 5 |
|[G-08]| Use assembly to validate msg.sender | 34 | 
|[G-09]| abi.encode() is less efficient than abi.encodePacked() | 32 |
|[G-10]| Using bytes32 is cheaper than using string | 5 |
|[G-11]| Consider pre-calculating the address of address(this) | 20 |
|[G-12]| Counting down in for statements is more gas efficient | 18 |
|[G-13]| Do not calculate constants | 60 |
|[G-14]| do-while is cheaper than for-loops when the initial check can be skipped | 18 |
|[G-15]| Packing of storage variables | 4 |
|[G-16]| Use Mappings Instead of Arrays | 1 |
|[G-17]| Cache state variables outside of loop to avoid reading storage on every iteration | 5 |
|[G-18]| Use uint8 Can Increase Gas Cost | 31 |
|[G-19]| Use of emit inside a loop | 3 |
|[G-20]| Use assembly to write address storage values | 3 |
|[G-21]| Store Data in calldata Instead of Memory for Certain Function Parameters  | 45 |
|[G-22]| Cache storage variables: write and read storage variables exactly once | 10 |
|[G-23]| State variables which are not modified within functions should be set as constant or immutable for values set at deployment | 3 |
|[G-24]| Use selfdestruct in the constructor if the contract is one-time use | 7 |
|[G-25]| Use fallback or receive instead of deposit() when transferring Ether | 5 |
|[G-26]| Using assembly to revert with an error message |  258 |
|[G-27]| Use inline assembly to check for address(0) | 30 |
|[G-28]| selfbalance is cheaper than address(this).balance (more efficient in certain scenarios) | 4 |
|[G-29]| Change Constant to Immutable for keccak Variables |  2  |
|[G-30]| Use Double Require/if Instead of Operator && | 13  |
|[G-31]| Precompute Off-Chain When Possible | 19 |
|[G-32]| Don't initialize Variables with Default Values: | 17 |
|[G-33]| Use of memory instead of calldata for immutable arguments | 24 |
|[G-34]| Use uint256(1)/uint256(2) instead of true/false to save gas for changes | 1 |
|[G-35]| Cache multiple accesses of a mapping/array | 19 |
|[G-36]| Empty Block | 6 |
|[G-37]| Emitting constants wastes gas | 2 |
|[G-38]| Inline modifiers that are only used once, to save gas | 15 |
|[G-39]| Use assembly to calculate hashes | 53 |
|[G-40]| Use assembly in place of abi.decode to extract calldata values more efficiently | 7 |


## [G-01] Don’t make variables public unless necessary

Issue Description - Making variables public comes with some overhead costs that can be avoided in many cases. A public variable implicitly creates a public getter function of the same name, increasing the contract size.

Proposed Optimization - Only mark variables as public if their values truly need to be readable by external contracts/users. Otherwise, use private or internal visibility.

Estimated Gas Savings - The savings from avoiding unnecessary public variables are small per transaction, around 5-10 gas. However, this adds up over many transactions targeting a contract with public state variables that don’t need to be public.
```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

23   IL1SharedBridge public immutable override sharedBridge;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L23

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

37   IBridgehub public immutable override bridgehub;

40   IL1ERC20Bridge public immutable override legacyBridge;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L37

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
 
27   address public immutable bridgehub;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L27

## [G-02] Use assembly to emit an event

To efficiently emit events, it's possible to utilize assembly by making use of scratch space and the free memory pointer. This approach has the advantage of potentially avoiding the costs associated with memory expansion.

However, it's important to note that in order to safely optimize this process, it is preferable to cache and restore the free memory pointer.
A good example of such practice can be seen in Solady's https://github.com/Vectorized/solady/blob/main/src/tokens/ERC1155.sol#L167 codebase.

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

155  emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);

199  emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);

225  emit WithdrawalFinalized(l1Receiver, l1Token, amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L155


```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

168  emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);

227  emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);

239  emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);

367  emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);

454  emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);

602  emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L168

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

56  emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

68  emit NewPendingAdmin(currentPendingAdmin, address(0));

69  emit NewAdmin(previousAdmin, pendingAdmin);

145 emit NewChain(_chainId, _stateTransitionManager, _admin);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L56

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

47  emit ChangeSecurityCouncil(address(0), _securityCouncil);

50  emit ChangeMinDelay(0, _minDelay);

132 emit TransparentOperationScheduled(id, _delay, _operation);

144 emit ShadowOperationScheduled(_id, _delay);

157 emit OperationCancelled(_id);

180 emit OperationExecuted(id);

199 emit OperationExecuted(id);

250 emit ChangeMinDelay(minDelay, _newDelay);

257 emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L47

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

115  emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

127  emit NewPendingAdmin(currentPendingAdmin, address(0));

128  emit NewAdmin(previousAdmin, pendingAdmin);

227  emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);

235  emit StateTransitionNewChain(_chainId, _stateTransitionContract);

287  emit StateTransitionNewChain(_chainId, stateTransitionAddress);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L115

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

83  emit ValidatorAdded(_chainId, _newValidator);

92  emit ValidatorRemoved(_chainId, _validator);

98  emit NewExecutionDelay(_executionDelay);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L83

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

28  emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

40  emit NewPendingAdmin(pendingAdmin, address(0));

41  emit NewAdmin(previousAdmin, pendingAdmin);

47  emit ValidatorStatusUpdate(_validator, _active);

54  emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);

63  emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);

75  emit NewFeeParams(oldFeeParams, _newFeeParams);

86  emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator);

92  emit ValidiumModeStatusUpdate(_validiumMode);

115 emit ExecuteUpgrade(_diamondCut);

125 emit ExecuteUpgrade(_diamondCut);

139 emit Freeze();

149 emit Unfreeze();

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L28

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

261  emit BlockCommit(

299  emit BlockCommit(

353  emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

436  emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

496  emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

343  emit NewPriorityRequest(

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L343

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

121  emit DiamondCut(facetCuts, initAddress, initCalldata);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L121

```solidity
file: blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

87   emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);

104  emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);

121  emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);

137  emit NewVerifier(address(oldVerifier), address(_newVerifier));

157  emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

256  emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L87


```solidity
file: blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

40   emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);

67   emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L40

```solidity
file: blob/main/code/system-contracts/contracts/ContractDeployer.sol

68  emit AccountVersionUpdated(msg.sender, _version);

86  emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);

355 emit ContractDeployed(_sender, _bytecodeHash, _newAddress);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L68

```solidity 
file: blob/main/code/system-contracts/contracts/KnownCodesStorage.sol

59   emit MarkedAsKnown(_bytecodeHash, _shouldSendToL1);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L59

```solidity
file: blob/main/code/system-contracts/contracts/L1Messenger.sol

111  emit L2ToL1LogSent(_l2ToL1Log);

156  emit L1MessageSent(msg.sender, hash, _message);

181  emit BytecodeL1PublicationRequested(_bytecodeHash);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L111

```solidity
file: blob/main/code/system-contracts/contracts/L2BaseToken.sol

49  emit Transfer(_from, _to, _amount);

67  emit Mint(_account, _amount);

79  emit Withdrawal(msg.sender, _l1Receiver, amount);

92  emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L49

```solidity
file: blob/main/code/system-contracts/contracts/NonceHolder.sol

96   emit ValueSetUnderNonce(msg.sender, _key, _value);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L96

## [G-03] Use of memory instead of storage for struct/array state variables

When fetching data from storage, using the memory keyword to assign it to a variable reads all fields of the struct/array and incurs a Gcoldsload (2100 gas) for each field.

This can be avoided by declaring the variable with the storage keyword and caching the necessary fields in stack variables.

The memory keyword should only be used if the entire struct/array is being returned or passed to a function that requires memory, or if it is being read from another memory array/struct.


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

46   bytes32[] memory blobCommitments = new bytes32[](MAX_NUMBER_OF_BLOBS);

47   bytes32[] memory blobHashes = new bytes32[](MAX_NUMBER_OF_BLOBS);

399  uint256[] memory proofPublicInput = new uint256[](committedBatchesLength);


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L46

```solidity
file: blob/main/code/system-contracts/contracts/L1Messenger.sol
 
204  bytes32[] memory l2ToL1LogsTreeArray = new bytes32[](L2_TO_L1_LOGS_MERKLE_TREE_LEAVES);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L204


```solidity
file: blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol

24   bytes32[] memory blobHashes = new bytes32[](MAX_NUMBER_OF_BLOBS);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L24

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

140  SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

160  SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

180  SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L140

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

97  FacetCut[] memory facetCuts = _diamondCut.facetCuts;

105 bytes4[] memory selectors = facetCuts[i].selectors;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L97

## [G-04] Optimal Struct Variable Order

Detect optimal variable order in struct definitions to decrease the number of slots used. Each storage slot used can cost at least 5,000 gas for each write operation, and potentially up to 20,000 gas if you’re turning a zero value into a non-zero value. Hence, optimizing storage usage can result in significant gas savings. The real-world savings could vary depending on your contract’s specific logic and the state of the Ethereum network.


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

66 struct ZkSyncStateTransitionStorage {
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
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L66-L153


```solidity
file:  blob/main/code/system-contracts/contracts/ContractDeployer.sol

197 struct ForceDeployment {
        // The bytecode hash to put on an address
        bytes32 bytecodeHash;
        // The address on which to deploy the bytecodehash to
        address newAddress;
        // Whether to run the constructor on the force deployment
        bool callConstructor;
        // The value with which to initialize a contract
        uint256 value;
        // The constructor calldata
        bytes input;
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L197-L208

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol

10 struct L2TransactionRequestDirect {
    uint256 chainId;
    uint256 mintValue;
    address l2Contract;
    uint256 l2Value;
    bytes l2Calldata;
    uint256 l2GasLimit;
    uint256 l2GasPerPubdataByteLimit;
    bytes[] factoryDeps;
    address refundRecipient;
}

22 struct L2TransactionRequestTwoBridgesOuter {
    uint256 chainId;
    uint256 mintValue;
    uint256 l2Value;
    uint256 l2GasLimit;
    uint256 l2GasPerPubdataByteLimit;
    address refundRecipient;
    address secondBridgeAddress;
    uint256 secondBridgeValue;
    bytes secondBridgeCalldata;
}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L10-L20

```solidity
file: blob/main/code/contracts/ethereum/contracts/common/Messaging.sol

55  struct WritePriorityOpParams {
    address sender;
    uint256 txId;
    uint256 l2Value;
    address contractAddressL2;
    uint64 expirationTimestamp;
    uint256 l2GasLimit;
    uint256 l2GasPrice;
    uint256 l2GasPricePerPubdata;
    uint256 valueToMint;
    address refundRecipient;
}

127  struct BridgehubL2TransactionRequest {
    address sender;
    address contractL2;
    uint256 mintValue;
    uint256 l2Value;
    bytes l2Calldata;
    uint256 l2GasLimit;
    uint256 l2GasPerPubdataByteLimit;
    bytes[] factoryDeps;
    address refundRecipient;
}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L55-L66

```solidity
file: blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol

16  struct ForceDeployment {
        bytes32 bytecodeHash;
        address newAddress;
        bool callConstructor;
        uint256 value;
        bytes input;
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L16-L22

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol

25  struct Call {
        address target;
        uint256 value;
        bytes data;
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L25-L29

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol

25  struct InitializeData {
    uint256 chainId;
    address bridgehub;
    address stateTransitionManager;
    uint256 protocolVersion;
    address admin;
    address validatorTimelock;
    address baseToken;
    address baseTokenBridge;
    bytes32 storedBatchZero;
    IVerifier verifier;
    VerifierParams verifierParams;
    bytes32 l2BootloaderBytecodeHash;
    bytes32 l2DefaultAccountBytecodeHash;
    uint256 priorityTxMaxGasLimit;
    FeeParams feeParams;
    address blobVersionedHashRetriever;
}

51 struct InitializeDataNewChain {
    IVerifier verifier;
    VerifierParams verifierParams;
    bytes32 l2BootloaderBytecodeHash;
    bytes32 l2DefaultAccountBytecodeHash;
    uint256 priorityTxMaxGasLimit;
    FeeParams feeParams;
    address blobVersionedHashRetriever;
}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L25-L42

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

27  struct LogProcessingOutput {
    uint256 numberOfLayer1Txs;
    bytes32 chainedPriorityTxsHash;
    bytes32 previousBatchHash;
    bytes32 pubdataHash;
    bytes32 stateDiffHash;
    bytes32 l2LogsTreeRoot;
    uint256 packedBatchAndL2BlockTimestamp;
    bytes32 blob1Hash;
    bytes32 blob2Hash;
}

83 struct StoredBatchInfo {
        uint64 batchNumber;
        bytes32 batchHash;
        uint64 indexRepeatedStorageChanges;
        uint256 numberOfLayer1Txs;
        bytes32 priorityOperationsHash;
        bytes32 l2LogsTreeRoot;
        uint256 timestamp;
        bytes32 commitment;
    }

112 struct CommitBatchInfo {
        uint64 batchNumber;
        uint64 timestamp;
        uint64 indexRepeatedStorageChanges;
        bytes32 newStateRoot;
        uint256 numberOfLayer1Txs;
        bytes32 priorityOperationsHash;
        bytes32 bootloaderHeapInitialContentsHash;
        bytes32 eventsQueueStateHash;
        bytes systemLogs;
        bytes pubdataCommitments;
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L27-L37

```solidity
file: blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol

25  struct Transaction {
    // The type of the transaction.
    uint256 txType;
    // The caller.
    uint256 from;
    // The callee.
    uint256 to;
    // The gasLimit to pass with the transaction.
    // It has the same meaning as Ethereum's gasLimit.
    uint256 gasLimit;
    // The maximum amount of gas the user is willing to pay for a byte of pubdata.
    uint256 gasPerPubdataByteLimit;
    // The maximum fee per gas that the user is willing to pay.
    // It is akin to EIP1559's maxFeePerGas.
    uint256 maxFeePerGas;
    // The maximum priority fee per gas that the user is willing to pay.
    // It is akin to EIP1559's maxPriorityFeePerGas.
    uint256 maxPriorityFeePerGas;
    // The transaction's paymaster. If there is no paymaster, it is equal to 0.
    uint256 paymaster;
    // The nonce of the transaction.
    uint256 nonce;
    // The value to pass with the transaction.
    uint256 value;
    // In the future, we might want to add some
    // new fields to the struct. The `txData` struct
    // is to be passed to account and any changes to its structure
    // would mean a breaking change to these accounts. In order to prevent this,
    // we should keep some fields as "reserved".
    // It is also recommended that their length is fixed, since
    // it would allow easier proof integration (in case we will need
    // some special circuit for preprocessing transactions).
    uint256[4] reserved;
    // The transaction's calldata.
    bytes data;
    // The signature of the transaction.
    bytes signature;
    // The properly formatted hashes of bytecodes that must be published on L1
    // with the inclusion of this transaction. Note, that a bytecode has been published
    // before, the user won't pay fees for its republishing.
    bytes32[] factoryDeps;
    // The input to the paymaster.
    bytes paymasterInput;
    // Reserved dynamic type for the future use-case. Using it should be avoided,
    // But it is still here, just in case we want to enable some additional functionality.
    bytes reservedDynamic;
}


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L25-L71

## [G-05] Consider using OpenZeppelin's EnumerateSet instead of nested mappings

Nested mappings and multi-dimensional arrays in Solidity operate through a process of double hashing, wherein the original storage slot and the first key are concatenated and hashed, and then this hash is again concatenated with the second key and hashed. This process can be quite gas expensive due to the double-hashing operation and subsequent storage operation (sstore).

OpenZeppelin's EnumerableSet provides a potential solution to this problem. It creates a data structure that combines the benefits of set operations with the ability to enumerate stored elements, which is not natively available in Solidity. EnumerableSet handles the element uniqueness internally and can therefore provide a more gas-efficient and collision-resistant alternative to nested mappings or multi-dimensional arrays in certain scenarios.

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

27   mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
        public isWithdrawalFinalized;

32   mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
        public depositAmount;
    
51   mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27-L29

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

52   mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))

57   mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
        public isWithdrawalFinalized;

65   mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L52


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

50    mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

114  mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L114



```solidity
file: blob/main/code/system-contracts/contracts/ImmutableSimulator.sol

21   mapping(uint256 contractAddress => mapping(uint256 index => bytes32 value)) internal immutableDataStorage;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L21


```solidity
file: blob/main/code/system-contracts/contracts/NonceHolder.sol

41  mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L41

## [G-06] Constructors can be marked payable
 
Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided. A constructor can safely be marked as payable, since only the deployer would be able to pass funds, and the project itself would not pass any funds.

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

55   constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55


```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

90   constructor(

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

38  constructor() reentrancyGuardInitializer {}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

58  constructor(address _bridgehub) reentrancyGuardInitializer {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

55  constructor(address _initialOwner, uint32 _executionDelay) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

19  constructor() reentrancyGuardInitializer {}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

11   constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11


## [G-07] Avoid Unnecessary Use of Storage

Writing data to storage is one of the most expensive operations in Solidity. Reduce gas costs by avoiding unnecessary writes. For example, move constant values to memory:

<details> 

```solidity
// Expensive
string public constant NAME = "MyContract"; 

// Cheaper
string memory NAME = "MyContract";

```

</details>

Also be careful about storing large pieces of data on-chain. Use alternative patterns like IPFS for larger data.

Storing data costs 20,000 gas versus 3 gas for memory.
Minimize storage by using memory for fixed constants and temporary values.
Store large data like files off-chain (IPFS) and put hash on-chain.

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

26   string public constant override getName = "ValidatorTimelock";

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

20   string public constant override getName = "AdminFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

27  string public constant override getName = "ExecutorFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

25  string public constant override getName = "GettersFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

35  string public constant override getName = "MailboxFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35


## [G-08] Use assembly to validate msg.sender

It is possible to use assembly to efficiently validate msg.sender with the least amount of opcodes. For more details check the following report. https://code4rena.com/reports/2023-05-juicebox#g-06-use-assembly-to-validate-msgsender

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

64   require(msg.sender == address(sharedBridge), "Not shared bridge");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

69  require(msg.sender == address(bridgehub), "ShB not BH");

75  require(
            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
            "L1SharedBridge: not bridgehub or era chain"
        );

84  require(msg.sender == address(legacyBridge), "ShB not legacy bridge");
        _;
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol
 
46   require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

62   require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

59  require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

65  require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

71  require(
            msg.sender == owner() || msg.sender == securityCouncil,
            "Only the owner and security council are allowed to call this function"
        );

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

64  require(msg.sender == bridgehub, "StateTransition: only bridgehub");

70  require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

121 require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62  require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

68  require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

34   require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

16  require(msg.sender == s.admin, "StateTransition Chain: not admin");

22  require(s.validators[msg.sender], "StateTransition Chain: not validator");

27  require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

32  require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

37  require(
            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by admin or state transition manager"
        );

45  require(
            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by validator or state transition manager"
        );

53  require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16

```solidity
file: blob/main/code/system-contracts/contracts/AccountCodeStorage.sol

26  require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L26

```solidity
file: blob/main/code/system-contracts/contracts/ComplexUpgrader.sol

22  require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22


```solidity
file: blob/main/code/system-contracts/contracts/ContractDeployer.sol

29   require(msg.sender == address(this), "Callable only by self");

239  require(
            msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
            "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
        );

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29


```solidity
file: blob/main/code/system-contracts/contracts/DefaultAccount.sol

29  if (msg.sender != BOOTLOADER_FORMAL_ADDRESS) {

222  assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L29

```solidity
file: blob/main/code/system-contracts/contracts/ImmutableSimulator.sol

35   require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35

```solidity 
file: blob/main/code/system-contracts/contracts/KnownCodesStorage.sol

20  require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L20


```solidity 
file: blob/main/code/system-contracts/contracts/L2BaseToken.sol

33  require(
            msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
                msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
                msg.sender == BOOTLOADER_FORMAL_ADDRESS,
            "Only system contracts with special access can call this method"
        );

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L33-L38

```solidity
file: blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol

41   require(msg.sender == caller, "Inappropriate caller");

48   require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");

55   require(msg.sender == FORCE_DEPLOYER);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L41

## [G-09] abi.encode() is less efficient than abi.encodePacked()

See for more information: https://github.com/ConnorBlockchain/Solidity-Encode-Gas-Comparison

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

76   bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76


```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

210  bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));

258  bytes memory decimals = abi.encode(uint8(18));

259  return abi.encode(name, symbol, decimals); 

265  return abi.encode(data1, data2, data3);

341  bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));

598  bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L210

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

205    return keccak256(abi.encode(_operation));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L205

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

100  storedBatchZero = keccak256(abi.encode(batchZero));

102  initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

138  initialCutHash = keccak256(abi.encode(_diamondCut));

147  upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

156  upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

104  bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

313  concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));

512  return keccak256(abi.encode(passThroughDataHash, metadataHash, auxiliaryOutputHash));

588  return keccak256(abi.encode(_storedBatchInfo));

680  (bool success, bytes memory data) = s.blobVersionedHashRetriever.staticcall(abi.encode(_index));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
 
323  bytes memory transactionEncoding = abi.encode(transaction);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L323

```solidity
file: blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

192  bytes memory encodedTransaction = abi.encode(_l2ProtocolUpgradeTx);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L192


```solidity
file: blob/main/code/system-contracts/contracts/L1Messenger.sol

106  chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

122  chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

164  chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

212  reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));

226  abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])

243  reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));

260  abi.encode(

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L106


```solidity
file: blob/main/code/system-contracts/contracts/SystemContext.sol

159   hash = keccak256(abi.encode(_block));

227   return keccak256(abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash));

403   currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L159

```solidity
file: blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol

120   abi.encode(

139   abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L120

## [G-10] Using bytes32 is cheaper than using string. 

Storing and manipulating data in bytes32 is more gas-efficient than using string, which involves dynamic storage allocation. bytes32 is a fixed-size type, whereas string can have variable length, resulting in higher gas costs.

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

26   string public constant override getName = "ValidatorTimelock";

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

20   string public constant override getName = "AdminFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

27  string public constant override getName = "ExecutorFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

25  string public constant override getName = "GettersFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

35  string public constant override getName = "MailboxFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35

## [G-11] Consider pre-calculating the address of address(this)

It can be more gas-efficient to use a hardcoded address instead of the address(this) expression, especially if you need to use the same address multiple times in your contract.

The reason for this, is that using address(this) requires an additional EXTCODESIZE operation to retrieve the contract’s address from its bytecode, which can increase the gas cost of your contract. By pre-calculating and using a hardcoded address, you can avoid this additional operation and reduce the overall gas cost of your contract.

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

65   uint256 amount = IERC20(_token).balanceOf(address(this));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

118  uint256 balanceBefore = address(this).balance;

120  uint256 balanceAfter = address(this).balance;

127  uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

131  uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

174  uint256 balanceBefore = _token.balanceOf(address(this))

175  _token.safeTransferFrom(_from, address(this), _amount);

176  uint256 balanceAfter = _token.balanceOf(address(this));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

59   require(msg.sender == address(this), 

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

265   bytes32(uint256(uint160(address(this)))),

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L265

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

41  uint256 amount = address(this).balance;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41

```solidity
file: blob/main/code/system-contracts/contracts/ContractDeployer.sol

29   require(msg.sender == address(this), "Callable only by self");

333  BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo(address(this), _newAddress, value);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29


```solidity
file: blob/main/code/system-contracts/contracts/DefaultAccount.sol
 
47   if (codeAddress != address(this)) {

100  require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

188   return recoveredAddress == address(this) && recoveredAddress != address(0);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L47

```solidity 
file: blob/main/code/system-contracts/contracts/L1Messenger.sol

129  sender: address(this),

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#129

```solidity
file: blob/main/code/system-contracts/contracts/L2BaseToken.sol

106    balance[address(this)] -= amount;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L106


```solidity
file: blob/main/code/system-contracts/contracts/MsgValueSimulator.sol

60  require(to != address(this), "MsgValueSimulator calls itself");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#60


```solidity
file: blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol

377  uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377

## [G-12] Counting down in for statements is more gas efficient

Counting down is more gas efficient than counting up because neither we are making zero variable to non-zero variable and also we will get gas refund in the last transaction when making non-zero to zero variable. https://solodit.xyz/auth?next=/issues/g-02-counting-down-in-for-statements-is-more-gas-efficient-code4rena-pooltogether-pooltogether-git

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

25   for (uint256 i = 0; i < _calls.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L25


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

135  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

185  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

209  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

580   for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

667   for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580

```solidity
file: blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226   for (uint256 i = 0; i < _factoryDeps.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226


```solidity
file: blob/main/code/system-contracts/contracts/ContractDeployer.sol

248    for (uint256 i = 0; i < deploymentsLength; ++i) {

253    for (uint256 i = 0; i < deploymentsLength; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L248

```solidity
file:  blob/main/code/system-contracts/contracts/ImmutableSimulator.sol
 
38   for (uint256 i = 0; i < immutablesLength; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L38

```solidity
file: blob/main/code/system-contracts/contracts/KnownCodesStorage.sol

30  for (uint256 i = 0; i < hashesLen; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L30


```solidity
file: blob/main/code/system-contracts/contracts/L1Messenger.sol

206   for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

218   for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

224   for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

236   for (uint256 i = 0; i < numberOfMessages; ++i) {

254   for (uint256 i = 0; i < numberOfBytecodes; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206


```solidity
file: blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol

36   for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36

## [G-13] Do not calculate constants

Due to how constant variables are implemented (replacements at compile-time), an expression assigned to a constant variable is recomputed each time that the variable is used, which wastes some gas.

```solidity
file: blob/main/code/system-contracts/contracts/NonceHolder.sol

28  uint256 private constant DEPLOY_NONCE_MULTIPLIER = 2 ** 128;

32   uint256 private constant MAXIMAL_MIN_NONCE_INCREMENT = 2 ** 32;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L28


```solidity
fille: blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol

41   uint256 constant META_GAS_PER_PUBDATA_BYTE_OFFSET = 0 * 8;

42   uint256 constant META_HEAP_SIZE_OFFSET = 8 * 8;

43   uint256 constant META_AUX_HEAP_SIZE_OFFSET = 12 * 8;

44   uint256 constant META_SHARD_ID_OFFSET = 28 * 8;

45   uint256 constant META_CALLER_SHARD_ID_OFFSET = 29 * 8;

46   uint256 constant META_CODE_SHARD_ID_OFFSET = 30 * 8;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L41

```solidity
file: blob/main/code/contracts/ethereum/contracts/common/Config.sol

14   uint256 constant MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES = 4 + L2_TO_L1_LOG_SERIALIZE_SIZE * 512;

112  bytes32 constant TWO_BRIDGES_MAGIC_VALUE = bytes32(uint256(keccak256("TWO_BRIDGES_MAGIC_VALUE")) - 1);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L14


```solidity
file: blob/main/code/system-contracts/contracts/Constants.sol

48  address payable constant BOOTLOADER_FORMAL_ADDRESS = payable(address(SYSTEM_CONTRACTS_OFFSET + 0x01));
IAccountCodeStorage constant ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT = IAccountCodeStorage(
    address(SYSTEM_CONTRACTS_OFFSET + 0x02)
);
INonceHolder constant NONCE_HOLDER_SYSTEM_CONTRACT = INonceHolder(address(SYSTEM_CONTRACTS_OFFSET + 0x03));
IKnownCodesStorage constant KNOWN_CODE_STORAGE_CONTRACT = IKnownCodesStorage(address(SYSTEM_CONTRACTS_OFFSET + 0x04));
IImmutableSimulator constant IMMUTABLE_SIMULATOR_SYSTEM_CONTRACT = IImmutableSimulator(
    address(SYSTEM_CONTRACTS_OFFSET + 0x05)
);
IContractDeployer constant DEPLOYER_SYSTEM_CONTRACT = IContractDeployer(address(SYSTEM_CONTRACTS_OFFSET + 0x06));

// A contract that is allowed to deploy any codehash
// on any address. To be used only during an upgrade.
address constant FORCE_DEPLOYER = address(SYSTEM_CONTRACTS_OFFSET + 0x07);
IL1Messenger constant L1_MESSENGER_CONTRACT = IL1Messenger(address(SYSTEM_CONTRACTS_OFFSET + 0x08));
address constant MSG_VALUE_SYSTEM_CONTRACT = address(SYSTEM_CONTRACTS_OFFSET + 0x09);

IBaseToken constant BASE_TOKEN_SYSTEM_CONTRACT = IBaseToken(address(SYSTEM_CONTRACTS_OFFSET + 0x0a));
IBaseToken constant REAL_BASE_TOKEN_SYSTEM_CONTRACT = IBaseToken(address(REAL_SYSTEM_CONTRACTS_OFFSET + 0x0a));

// Hardcoded because even for tests we should keep the address. (Instead `SYSTEM_CONTRACTS_OFFSET + 0x10`)
// Precompile call depends on it.
// And we don't want to mock this contract.
address constant KECCAK256_SYSTEM_CONTRACT = address(0x8010);

ISystemContext constant SYSTEM_CONTEXT_CONTRACT = ISystemContext(payable(address(SYSTEM_CONTRACTS_OFFSET + 0x0b)));
ISystemContext constant REAL_SYSTEM_CONTEXT_CONTRACT = ISystemContext(payable(address(REAL_SYSTEM_CONTRACTS_OFFSET + 0x0b)));

IBootloaderUtilities constant BOOTLOADER_UTILITIES = IBootloaderUtilities(address(SYSTEM_CONTRACTS_OFFSET + 0x0c));

// It will be a different value for tests, while shouldn't. But for now, this constant is not used by other contracts, so that's fine.
address constant EVENT_WRITER_CONTRACT = address(SYSTEM_CONTRACTS_OFFSET + 0x0d);

ICompressor constant COMPRESSOR_CONTRACT = ICompressor(address(SYSTEM_CONTRACTS_OFFSET + 0x0e));

IComplexUpgrader constant COMPLEX_UPGRADER_CONTRACT = IComplexUpgrader(address(SYSTEM_CONTRACTS_OFFSET + 0x0f));

IPubdataChunkPublisher constant PUBDATA_CHUNK_PUBLISHER = IPubdataChunkPublisher(
    address(SYSTEM_CONTRACTS_OFFSET + 0x11)
);

/// @dev If the bitwise AND of the extraAbi[2] param when calling the MSG_VALUE_SIMULATOR
/// is non-zero, the call will be assumed to be a system one.
uint256 constant MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT = 1;

/// @dev The maximal msg.value that context can have
uint256 constant MAX_MSG_VALUE = 2 ** 128 - 1;

/// @dev Prefix used during derivation of account addresses using CREATE2
/// @dev keccak256("zksyncCreate2")
bytes32 constant CREATE2_PREFIX = 0x2020dba91b30cc0006188af794c2fb30dd8520db7e2c088b7fc7c103c00ca494;
/// @dev Prefix used during derivation of account addresses using CREATE
/// @dev keccak256("zksyncCreate")
bytes32 constant CREATE_PREFIX = 0x63bae3a9951d38e8a3fbb7b70909afc1200610fc5bc55ade242f815974674f23;

/// @dev Each state diff consists of 156 bytes of actual data and 116 bytes of unused padding, needed for circuit efficiency.
uint256 constant STATE_DIFF_ENTRY_SIZE = 272;

/// @dev While the "real" amount of pubdata that can be sent rarely exceeds the BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, it is better to
/// allow the operator to provide any reasonably large value in order to avoid unneeded constraints on the operator.
uint256 constant MAX_ALLOWED_PUBDATA_PER_BATCH = 520000;

enum SystemLogKey {
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

/// @dev The number of leaves in the L2->L1 log Merkle tree.
/// While formally a tree of any length is acceptable, the node supports only a constant length of 4096 leaves.
uint256 constant L2_TO_L1_LOGS_MERKLE_TREE_LEAVES = 4096;

/// @dev The length of the derived key in bytes inside compressed state diffs.
uint256 constant DERIVED_KEY_LENGTH = 32;
/// @dev The length of the enum index in bytes inside compressed state diffs.
uint256 constant ENUM_INDEX_LENGTH = 8;
/// @dev The length of value in bytes inside compressed state diffs.
uint256 constant VALUE_LENGTH = 32;

/// @dev The length of the compressed initial storage write in bytes.
uint256 constant COMPRESSED_INITIAL_WRITE_SIZE = DERIVED_KEY_LENGTH + VALUE_LENGTH;
/// @dev The length of the compressed repeated storage write in bytes.
uint256 constant COMPRESSED_REPEATED_WRITE_SIZE = ENUM_INDEX_LENGTH + VALUE_LENGTH;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L48-L137


```solidity
file: blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol

12  address constant TO_L1_CALL_ADDRESS = address((1 << 16) - 1);
address constant CODE_ADDRESS_CALL_ADDRESS = address((1 << 16) - 2);
address constant PRECOMPILE_CALL_ADDRESS = address((1 << 16) - 3);
address constant META_CALL_ADDRESS = address((1 << 16) - 4);
address constant MIMIC_CALL_CALL_ADDRESS = address((1 << 16) - 5);
address constant SYSTEM_MIMIC_CALL_CALL_ADDRESS = address((1 << 16) - 6);
address constant MIMIC_CALL_BY_REF_CALL_ADDRESS = address((1 << 16) - 7);
address constant SYSTEM_MIMIC_CALL_BY_REF_CALL_ADDRESS = address((1 << 16) - 8);
address constant RAW_FAR_CALL_CALL_ADDRESS = address((1 << 16) - 9);
address constant RAW_FAR_CALL_BY_REF_CALL_ADDRESS = address((1 << 16) - 10);
address constant SYSTEM_CALL_CALL_ADDRESS = address((1 << 16) - 11);
address constant SYSTEM_CALL_BY_REF_CALL_ADDRESS = address((1 << 16) - 12);
address constant SET_CONTEXT_VALUE_CALL_ADDRESS = address((1 << 16) - 13);
address constant SET_PUBDATA_PRICE_CALL_ADDRESS = address((1 << 16) - 14);
address constant INCREMENT_TX_COUNTER_CALL_ADDRESS = address((1 << 16) - 15);
address constant PTR_CALLDATA_CALL_ADDRESS = address((1 << 16) - 16);
address constant CALLFLAGS_CALL_ADDRESS = address((1 << 16) - 17);
address constant PTR_RETURNDATA_CALL_ADDRESS = address((1 << 16) - 18);
address constant EVENT_INITIALIZE_ADDRESS = address((1 << 16) - 19);
address constant EVENT_WRITE_ADDRESS = address((1 << 16) - 20);
address constant LOAD_CALLDATA_INTO_ACTIVE_PTR_CALL_ADDRESS = address((1 << 16) - 21);
address constant LOAD_LATEST_RETURNDATA_INTO_ACTIVE_PTR_CALL_ADDRESS = address((1 << 16) - 22);
address constant PTR_ADD_INTO_ACTIVE_CALL_ADDRESS = address((1 << 16) - 23);
address constant PTR_SHRINK_INTO_ACTIVE_CALL_ADDRESS = address((1 << 16) - 24);
address constant PTR_PACK_INTO_ACTIVE_CALL_ADDRESS = address((1 << 16) - 25);
address constant MULTIPLICATION_HIGH_ADDRESS = address((1 << 16) - 26);
address constant GET_EXTRA_ABI_DATA_ADDRESS = address((1 << 16) - 27);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L12-L38



## [G-14] do-while is cheaper than for-loops when the initial check can be skipped

Using do-while loops instead of for loops can be more gas-efficient. Even if you add an if condition to account for the case where the loop doesn't execute at all, a do-while loop can still be cheaper in terms of gas.

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

25   for (uint256 i = 0; i < _calls.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L25


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

135  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

185  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

209  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

580   for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

667   for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580

```solidity
file: blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226   for (uint256 i = 0; i < _factoryDeps.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226


```solidity
file: blob/main/code/system-contracts/contracts/ContractDeployer.sol

248    for (uint256 i = 0; i < deploymentsLength; ++i) {

253    for (uint256 i = 0; i < deploymentsLength; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L248

```solidity
file:  blob/main/code/system-contracts/contracts/ImmutableSimulator.sol
 
38   for (uint256 i = 0; i < immutablesLength; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L38

```solidity
file: blob/main/code/system-contracts/contracts/KnownCodesStorage.sol

30  for (uint256 i = 0; i < hashesLen; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L30


```solidity
file: blob/main/code/system-contracts/contracts/L1Messenger.sol

206   for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

218   for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

224   for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

236   for (uint256 i = 0; i < numberOfMessages; ++i) {

254   for (uint256 i = 0; i < numberOfBytecodes; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206


```solidity
file: blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol

36   for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36


## [G-15] Packing of storage variables

Pack variables in one slot by defining them in a lower data type. Packing only helps when multiple variables of the packed slot are being accessed in the same call. If not done correctly, it increases gas costs instead, due to shifts required.

<details>

```solidity
Before:

contract MyContract {
  uint32  x; // Storage slot 0
  uint256 y; // Storage slot 1
  uint32  z; // Storage slot 2
}
After:

contract MyContract {
  uint32 x;  // Storage slot 0
  uint32 z;  // Storage slot 0
  uint256 y; // Storage slot 1
}

```
</details>


```solidity
file: blob/main/code/system-contracts/contracts/L1Messenger.sol

28      bytes32 internal chainedLogsHash;

    /// @notice Number of logs sent in the current block.
    /// @dev Will be reset at the end of the block to zero value.
    uint256 internal numberOfLogsToProcess;

    /// @notice Sequential hash of hashes of the messages sent in the current block.
    /// @dev Will be reset at the end of the block to zero value.
    bytes32 internal chainedMessagesHash;

    /// @notice Sequential hash of bytecode hashes that needs to published
    /// according to the current block execution invariant.
    /// @dev Will be reset at the end of the block to zero value.
    bytes32 internal chainedL1BytecodesRevealDataHash;

    /// The gas cost of processing one keccak256 round.
    uint256 internal constant KECCAK_ROUND_GAS_COST = 40;

    /// The number of bytes processed in one keccak256 round.
    uint256 internal constant KECCAK_ROUND_NUMBER_OF_BYTES = 136;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L28-L47



```solidity
file:  blob/main/code/system-contracts/contracts/SystemContext.sol

23     uint256 internal constant MINIBLOCK_HASHES_TO_STORE = 257;

    /// @notice The chainId of the network. It is set at the genesis.
    uint256 public chainId;

    /// @notice The `tx.origin` in the current transaction.
    /// @dev It is updated before each transaction by the bootloader
    address public origin;

    /// @notice The `tx.gasPrice` in the current transaction.
    /// @dev It is updated before each transaction by the bootloader
    uint256 public gasPrice;

    /// @notice The current block's gasLimit.
    uint256 public blockGasLimit = type(uint32).max;

    /// @notice The `block.coinbase` in the current transaction.
    /// @dev For the support of coinbase, we will use the bootloader formal address for now
    address public coinbase = BOOTLOADER_FORMAL_ADDRESS;

    /// @notice Formal `block.difficulty` parameter.
    uint256 public difficulty = 2.5e15;

    /// @notice The `block.basefee`.
    /// @dev It is currently a constant.
    uint256 public baseFee;

    /// @notice The number and the timestamp of the current L1 batch stored packed.
    BlockInfo internal currentBatchInfo;

    /// @notice The hashes of batches.
    /// @dev It stores batch hashes for all previous batches.
    mapping(uint256 batchNumber => bytes32 batchHash) internal batchHashes;

    /// @notice The number and the timestamp of the current L2 block.
    BlockInfo internal currentL2BlockInfo;

    /// @notice The rolling hash of the transactions in the current L2 block.
    bytes32 internal currentL2BlockTxsRollingHash;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L23-L61

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol
 
22    uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1);

    /// @notice The address of the security council.
    /// @dev It is supposed to be multisig contract.
    address public securityCouncil;

    /// @notice A mapping to store timestamps when each operation will be ready for execution.
    /// @dev - 0 means the operation is not created.
    /// @dev - 1 (EXECUTED_PROPOSAL_TIMESTAMP) means the operation is already executed.
    /// @dev - any other value means timestamp in seconds when the operation will be ready for execution.
    mapping(bytes32 operationId => uint256 executionTimestamp) public timestamps;

    /// @notice The minimum delay in seconds for operations to be ready for execution.
    uint256 public minDelay;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L22-L35


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

27      address public immutable bridgehub;

    /// @notice chainId => chainContract
    mapping(uint256 => address) public stateTransition;

    /// @dev Batch hash zero, calculated at initialization
    bytes32 public storedBatchZero;

    /// @dev Stored cutData for diamond cut
    bytes32 public initialCutHash;

    /// @dev genesisUpgrade contract address, used to setChainId
    address public genesisUpgrade;

    /// @dev current protocolVersion
    uint256 public protocolVersion;

    /// @dev validatorTimelock contract address, used to setChainId
    address public validatorTimelock;

    /// @dev Stored cutData for upgrade diamond cut. protocolVersion => cutHash
    mapping(uint256 => bytes32) public upgradeCutHash;

    /// @dev used to manage non critical updates
    address public admin;

    /// @dev used to accept the admin role
    address private pendingAdmin;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L27-L54

## [G-16] Use Mappings Instead of Arrays

There are two data types to describe lists of data in Solidity, arrays and maps, and their syntax and structure are quite different, allowing each to serve a distinct purpose. While arrays are packable and iterable, mappings are less expensive.

```solidity
file: blob/main/code/system-contracts/contracts/SystemContext.sol

70    bytes32[MINIBLOCK_HASHES_TO_STORE] internal l2BlockHash;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L70

## [G-17] Cache state variables outside of loop to avoid reading storage on every iteration

Reading from storage should always try to be avoided within loops. In the following instances, we are able to cache state variables outside of the loop to save a Gwarmaccess (100 gas) per loop iteration.

### Cache committedBatchTimestamp[ERA_CHAIN_ID] outside the loop

```solidity 
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116  for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);
            }

135  for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);
            }

185   for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
                    _newBatchesData[i].batchNumber
                );

                // Note: if the `commitBatchTimestamp` is zero, that means either:
                // * The batch was committed, but not through this contract.
                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
                // We allow executing such batches.

                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
            }
209   for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);

                // Note: if the `commitBatchTimestamp` is zero, that means either:
                // * The batch was committed, but not through this contract.
                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
                // We allow executing such batches.

                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
            }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116-L119



### Cache immutableDataStorage outside the loop


```solidity
file: blob/main/code/system-contracts/contracts/ImmutableSimulator.sol

38  for (uint256 i = 0; i < immutablesLength; ++i) {
                uint256 index = _immutables[i].index;
                bytes32 value = _immutables[i].value;
                immutableDataStorage[uint256(uint160(_dest))][index] = value;
            }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L38-L42

## [G-18] Use uint8 Can Increase Gas Cost

A smart contract's gas consumption can be higher if developers use items that are less than 32 bytes in size because the Ethereum Virtual Machine can only handle 32 bytes at a time. In order to increase the element's size to the necessary size, the EVM has to perform additional operations. 


```solidity
file: blob/main/code/contracts/ethereum/contracts/common/Messaging.sol

24  uint8 l2ShardId;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L24

```solidity
file: blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

40  uint8 version = uint8(_bytecodeHash[0]);

50  codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3]));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L40


```solidity
file: blob/main/code/system-contracts/contracts/Compressor.sol

143  uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

145  uint8 operation = metadata & OPERATION_BITMASK;

146  uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

174  uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

176  uint8 operation = metadata & OPERATION_BITMASK;

177  uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L143

```solidity
file: blob/main/code/system-contracts/contracts/DefaultAccount.sol

161   uint8 v;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L161

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

39   uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));

40   require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us");

592  function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

597  function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L39


```solidity
file: blob/main/code/system-contracts/contracts/KnownCodesStorage.sol

75   uint8 version = uint8(_bytecodeHash[0]);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L75

```solidity
file: blob/main/code/system-contracts/contracts/L1Messenger.sol

289   uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L289


```solidity
file: blob/main/code/system-contracts/contracts/interfaces/ICompressor.sol

6  uint8 constant OPERATION_BITMASK = 7;
// The number of bits shifting the compressed state diff metadata by which we retrieve its length.
8  uint8 constant LENGTH_BITS_OFFSET = 3;
// The maximal length in bytes that an enumeration index can have.
10 uint8 constant MAX_ENUMERATION_INDEX_SIZE = 8;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ICompressor.sol#L6

```solidity
file: blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol

19   uint8 shardId;

20   uint8 callerShardId;

21   uint8 codeShardId;

254  function getShardIdFromMeta(uint256 meta) internal pure returns (uint8 shardId) {

263  function getCallerShardIdFromMeta(uint256 meta) internal pure returns (uint8 callerShardId) {

272  function getCodeShardIdFromMeta(uint256 meta) internal pure returns (uint8 codeShardId) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L19


```solidity
file: blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol

220  uint8 shardId,

252  uint8 shardId,

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L220


```solidity
file: blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol

15  uint8 constant EIP_712_TX_TYPE = 0x71;

/// @dev The type id of legacy transactions.
16  uint8 constant LEGACY_TX_TYPE = 0x0;
/// @dev The type id of legacy transactions.
17  uint8 constant EIP_2930_TX_TYPE = 0x01;
/// @dev The type id of EIP1559 transactions.
18  uint8 constant EIP_1559_TX_TYPE = 0x02;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L15

## [G-19] Use of emit inside a loop

Emitting an event inside a loop performs a LOG op N times, where N is the loop length. This can lead to significant gas costs.

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

261  emit BlockCommit(
                _lastCommittedBatchData.batchNumber,
                _lastCommittedBatchData.batchHash,
                _lastCommittedBatchData.commitment
            );
299  emit BlockCommit(
                _lastCommittedBatchData.batchNumber,
                _lastCommittedBatchData.batchHash,
                _lastCommittedBatchData.commitment
            );

353  emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
        }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261-L265

## [G-20] Use assembly to write address storage values

Using assembly { sstore(state.slot, addr) instead of state = addr can save gas.

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

55   pendingAdmin = _newPendingAdmin;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

114  pendingAdmin = _newPendingAdmin;

133  validatorTimelock = _validatorTimelock;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L114

## [G-21] Store Data in calldata Instead of Memory for Certain Function Parameters 

Instead of copying variables to memory, it is typically more cost-effective to load them immediately from calldata. If all you need to do is read data, you can conserve gas by saving the data in calldata.
Because the values in calldata cannot be changed while the function is being executed, if the variable needs to be updated when calling a function, use memory instead.

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

440  function _verifyProof(uint256[] memory proofPublicInput, ProofInput calldata _proof) internal view {

203  bytes32[] memory _blobCommitments,

204  bytes32[] memory _blobHashes

540  bytes32[] memory _blobCommitments,

541  bytes32[] memory _blobHashes

562  bytes32[] memory _blobCommitments,

563  bytes32[] memory _blobHashes

627  bytes32[] memory _blobHashes

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L440


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

126  function _addFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {

149  function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {

172  function _removeFunctions(address _facet, bytes4[] memory _selectors) private {

278  function _initializeDiamondCut(address _init, bytes memory _calldata) private {
    
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L126

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

48   BridgehubL2TransactionRequest memory _request

57   L2Message memory _message,

67   L2Log memory _log,

107  L2Log memory _log,

130  function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {

229  BridgehubL2TransactionRequest memory _request

260  WritePriorityOpParams memory _params,

261  bytes memory _calldata,

262  bytes[] memory _factoryDeps

290  WritePriorityOpParams memory _priorityOpParams,

291  bytes memory _calldata,

292  bytes[] memory _factoryDeps

317  WritePriorityOpParams memory _priorityOpParams,

318  bytes memory _calldata,

319  bytes[] memory _factoryDeps

353  function _hashFactoryDeps(bytes[] memory _factoryDeps) internal pure returns (uint256[] memory hashedFactoryDeps) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L48


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

33   StoredBatchInfo memory _previousBatch,

200  StoredBatchInfo memory _lastCommittedBatchData,

209  StoredBatchInfo memory _lastCommittedBatchData,

216  StoredBatchInfo memory _lastCommittedBatchData,

254  StoredBatchInfo memory _lastCommittedBatchData,

274  StoredBatchInfo memory _lastCommittedBatchData,

321  function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {

456  VerifierParams memory _verifierParams

587  function _hashStoredBatchInfo(StoredBatchInfo memory _storedBatchInfo) internal pure returns (bytes32) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L33

```solidity
file: blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol

19  function readUint32(bytes memory _bytes, uint256 _start) internal pure returns (uint32 result, uint256 offset) {

26  function readAddress(bytes memory _bytes, uint256 _start) internal pure returns (address result, uint256 offset) {

33  function readUint256(bytes memory _bytes, uint256 _start) internal pure returns (uint256 result, uint256 offset) {

40  function readBytes32(bytes memory _bytes, uint256 _start) internal pure returns (bytes32 result, uint256 offset) 

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L19

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

20  L2CanonicalTransaction memory _transaction,

21  bytes memory _encoded,

46  function validateUpgradeTransaction(L2CanonicalTransaction memory _transaction) internal pure {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L20


```solidity
file: blob/main/code/system-contracts/contracts/DefaultAccount.sol

159  function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L159


## [G-22] Cache storage variables: write and read storage variables exactly once

You will see the following pattern frequently in efficient solidity code. Reading from a storage variable costs at least 100 gas as Solidity does not cache the storage read. Writes are considerably more expensive. Therefore, you should manually cache the variable to do exactly one storage read and exactly one storage write.

<details>

```solidity

// SPDX-License-Identifier: MIT
pragma solidity 0.8.20;

contract Counter1 {
    uint256 public number;

    function increment() public {
        require(number < 10);
        number = number + 1;
    }
}

contract Counter2 {
    uint256 public number;

    function increment() public {
        uint256 _number = number;
        require(_number < 10);
        number = _number + 1;
    }
}

```

</details>

The first function reads counter twice, the second code reads it once.

### Cache the securityCouncil state variable    

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

256  function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
        emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
        securityCouncil = _newSecurityCouncil;
    }
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L256

### Cache the genesisUpgrade,protocolVersion and validatorTimelock  state variables 

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

79      function initialize(
        StateTransitionManagerInitializeData calldata _initializeData
    ) external reentrancyGuardInitializer {
        require(_initializeData.governor != address(0), "StateTransition: governor zero");
        _transferOwnership(_initializeData.governor);

        genesisUpgrade = _initializeData.genesisUpgrade;
        protocolVersion = _initializeData.protocolVersion;
        validatorTimelock = _initializeData.validatorTimelock;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L79-L87

### Cache the protocolVersion state variable in function  _setChainIdUpgrade()

```solidity
file:  blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

177       function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
        bytes memory systemContextCalldata = abi.encodeCall(ISystemContext.setChainId, (_chainId));
        uint256[] memory uintEmptyArray;
        bytes[] memory bytesEmptyArray;

        L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
            txType: SYSTEM_UPGRADE_L2_TX_TYPE,
            from: uint256(uint160(L2_FORCE_DEPLOYER_ADDR)),
            to: uint256(uint160(L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR)),
            gasLimit: $(PRIORITY_TX_MAX_GAS_LIMIT),
            gasPerPubdataByteLimit: REQUIRED_L2_GAS_PRICE_PER_PUBDATA,
            maxFeePerGas: uint256(0),
            maxPriorityFeePerGas: uint256(0),
            paymaster: uint256(0),
            // Note, that the priority operation id is used as "nonce" for L1->L2 transactions
            nonce: protocolVersion,
            value: 0,
            reserved: [uint256(0), 0, 0, 0],
            data: systemContextCalldata,
            signature: new bytes(0),
            factoryDeps: uintEmptyArray,
            paymasterInput: new bytes(0),
            reservedDynamic: new bytes(0)
        });

        ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
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
        });

        Diamond.FacetCut[] memory emptyArray;
        Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({
            facetCuts: emptyArray,
            initAddress: genesisUpgrade,
            initCalldata: abi.encodeCall(IDefaultUpgrade.upgrade, (proposedUpgrade))
        });

        IAdmin(_chainContract).executeUpgrade(cutData);
        emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177-L227

### Cached variabl should be use instead of again get them from storage use oldPendingAdmin memory variable instead of pendingAdmin 

```solidity
file:

110  function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
        // Save previous value into the stack to put it into the event later
        address oldPendingAdmin = pendingAdmin;
        // Change pending admin
        pendingAdmin = _newPendingAdmin;
        emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
    }

119  function acceptAdmin() external {
        address currentPendingAdmin = pendingAdmin;
        require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

        address previousAdmin = admin;
        admin = currentPendingAdmin;
        delete pendingAdmin;

        emit NewPendingAdmin(currentPendingAdmin, address(0));
        emit NewAdmin(previousAdmin, pendingAdmin);
    }

```
### Cache the chainedLogsHash state variable 

```solidity
file: blob/main/code/system-contracts/contracts/L1Messenger.sol

106  chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L106

### Cache the numberOfLogsToProcess state variable 

```solidity
file: blob/main/code/system-contracts/contracts/L1Messenger.sol

108     logIdInMerkleTree = numberOfLogsToProcess;
        numberOfLogsToProcess++;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L108-L109

### Cache the chainedMessagesHash and chainedL1BytecodesRevealDataHash state variable 

```solidity
file: blob/main/code/system-contracts/contracts/L1Messenger.sol

122  chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

164   chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L122

### Cache the currentL2BlockTxsRollingHash state variable 

```solidity
file: blob/main/code/system-contracts/contracts/SystemContext.sol

403  currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L403

## [G-23] State variables which are not modified within functions should be set as constant or immutable for values set at deployment

Cache such variables and perform operations on them, if operations include modifications to the state variable(s) then remember to equate the state variable to it’s cached counterpart at the end

```solidity
file: blob/main/code/system-contracts/contracts/SystemContext.sol

37   uint256 public blockGasLimit = type(uint32).max;

    /// @notice The `block.coinbase` in the current transaction.
    /// @dev For the support of coinbase, we will use the bootloader formal address for now
41    address public coinbase = BOOTLOADER_FORMAL_ADDRESS;

    /// @notice Formal `block.difficulty` parameter.
44     uint256 public difficulty = 2.5e15;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L37

## [G-24] Use selfdestruct in the constructor if the contract is one-time use

Sometimes, contracts are used to deploy several contracts in one transaction, which necessitates doing it in the constructor.
If the contract’s only use is the code in the constructor, then selfdestructing at the end of the operation will save gas.
Although selfdestruct is set for removal in an upcoming hardfork, it will still be supported in the constructor per EIP 6780 https://eips.ethereum.org/EIPS/eip-6780

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

55   constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55


```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

90   constructor(

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

38  constructor() reentrancyGuardInitializer {}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

58  constructor(address _bridgehub) reentrancyGuardInitializer {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

55  constructor(address _initialOwner, uint32 _executionDelay) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

19  constructor() reentrancyGuardInitializer {}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

11   constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11


## [G-25] Use fallback or receive instead of deposit() when transferring Ether

Similar to above, you can “just transfer” ether to a contract and have it respond to the transfer instead of using a payable function. This of course, depends on the rest of the contract’s architecture.

Example Deposit in AAVE


<details>

```solidity

contract AddLiquidity{

    receive() external payable {
      IWETH(weth).deposit{msg.value}();
      AAVE.deposit(weth, msg.value, msg.sender, REFERRAL_CODE)
    }
}

```

</details>

The fallback function is capable of receiving bytes data which can be parsed with abi.decode. This servers as an alternative to supplying arguments to a deposit function.

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

26  function deposit(
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte,
        address _refundRecipient
    ) external payable returns (bytes32 txHash);

35  function deposit(
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte
    ) external payable returns (bytes32 txHash);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L26-L33

```solidity
file:  blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

128  function bridgehubDeposit(
        uint256 _chainId,
        address _prevMsgSender,
        uint256 _l2Value,
        bytes calldata _data
    ) external payable returns (L2TransactionRequestTwoBridgesInner memory request);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L128-L133

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

98  function deposit(
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte
    ) external payable returns (bytes32 l2TxHash) {
        l2TxHash = deposit(_l2Receiver, _l1Token, _amount, _l2TxGasLimit, _l2TxGasPerPubdataByte, address(0));
    }

133  function deposit(
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte,
        address _refundRecipient
    ) public payable nonReentrant returns (bytes32 l2TxHash) {
        require(_amount != 0, "0T"); // empty deposit
        uint256 amount = _depositFundsToSharedBridge(msg.sender, IERC20(_l1Token), _amount);
        require(amount == _amount, "3T"); // The token has non-standard transfer logic

        l2TxHash = sharedBridge.depositLegacyErc20Bridge{value: msg.value}(
            msg.sender,
            _l2Receiver,
            _l1Token,
            _amount,
            _l2TxGasLimit,
            _l2TxGasPerPubdataByte,
            _refundRecipient
        );
        depositAmount[msg.sender][_l1Token][l2TxHash] = _amount;
        emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L98-L106


## [G-26] Using assembly to revert with an error message

When reverting in solidity code, it is common practice to use a require or revert statement to revert execution with an error message. This can in most cases be further optimized by using assembly to revert with the error message.


Here’s an example;

<details>

```solidity
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

</details>

From the example above we can see that we get a gas saving of over 300 gas when reverting wth the same error message with assembly against doing so in solidity. This gas savings come from the memory expansion costs and extra type checks the solidity compiler does under the hood.

```solidity

File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

64:         require(msg.sender == address(sharedBridge), "Not shared bridge");

66:         require(amount == _amount, "Incorrect amount");

141:        require(_amount != 0, "0T"); // empty deposit

143:        require(amount == _amount, "3T"); // The token has non-standard transfer logic

186:        require(amount != 0, "2T"); // empty deposit

215:        require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64


```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

69:          require(msg.sender == address(bridgehub), "ShB not BH");

84:          require(msg.sender == address(legacyBridge), "ShB not legacy bridge");

108:         require(_owner != address(0), "ShB owner 0");

122:         require(amount > 0, "ShB: 0 amount to transfer");

125:         require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");

132:         require(msg.sender == ERA_DIAMOND_PROXY, "ShB: not era diamond proxy");

150:         require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");

153:         require(msg.value == 0, "ShB m.v > 0 b d.it");

156:         require(amount == _amount, "3T"); // The token has non-standard transfer logic

183:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

189:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");

190:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

195:         require(_depositAmount == 0, "ShB wrong withdraw amount");

197:         require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");

201:         require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic

203:         require(amount != 0, "6T"); // empty deposit amount

232:         require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");

320:         require(proofValid, "yn");

322:         require(_amount > 0, "y1");

337:         require(dataHash == txDataHash, "ShB: d.it not hap");

344:         require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");

355:         require(callSuccess, "ShB: claimFailedDeposit failed");

391:         require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");

412:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");

422:         require(!alreadyFinalized, "Withdrawal is already finalized 2");

434:         require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds

444:         require(callSuccess, "ShB: withdraw failed");

479:         require(success, "ShB withd w proof"); // withdrawal wrong proof

496:         require(_l2ToL1message.length >= 56, "ShB wrong msg len"); // wrong messsage length

512:         require(_l2ToL1message.length == 76, "ShB wrong msg len 2");

517:         revert("ShB Incorrect message function selector");

558:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

559:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

43:         require(msg.sender == deployer || msg.sender == owner(), "Bridgehub: not owner or deployer");

82:         require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

102:        require(_chainId != 0, "Bridgehub: chainId cannot be 0");

103:        require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");

109:        require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");

110:        require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

112:        require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

203:        require(msg.value == _request.mintValue, "Bridgehub: msg.value mismatch 1");

205:        require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");

255:        require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3");

276:        require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L43

```solidity
File: contracts/ethereum/contracts/common/ReentrancyGuard.sol

58:         require(lockSlotOldValue == 0, "1B");

75:         require(_status == _NOT_ENTERED, "r1");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L58

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

23:         require(_bytecode.length % 32 == 0, "pq");

26:         require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words

27:         require(bytecodeLenInWords % 2 == 1, "ps"); // bytecode length in words must be odd

41:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash

43:         require(_bytecodeLen(_bytecodeHash) % 2 == 1, "uy"); // Code length in words must be odd

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

42:         require(_admin != address(0), "Admin should be non zero address");

59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

65:         require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

155:        require(isOperationPending(_id), "Operation must be pending");

172:        require(isOperationReady(id), "Operation must be ready before execution");

177:        require(isOperationReady(id), "Operation must be ready after execution");

191:        require(isOperationPending(id), "Operation must be pending before execution");

196:        require(isOperationPending(id), "Operation must be pending after execution");

216:        require(!isOperation(_id), "Operation with this proposal id already exists");

217:        require(_delay >= minDelay, "Proposed delay is less than minimum delay");

240:        require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L42

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

58:         require(msg.sender == bridgehub, "StateTransition: only bridgehub");

70:         require(_initializeData.governor != address(0), "StateTransition: governor zero");

204:        require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

68:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");

195:        require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

217:        require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

25:         require(address(_initializeData.verifier) != address(0), "vt");

26:         require(_initializeData.admin != address(0), "vy");

27:         require(_initializeData.validatorTimelock != address(0), "hc");

28:         require(_initializeData.priorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "vu");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

14:         require(_chainId == block.chainid, "pr");

25:         require(msg.data.length >= 4 || msg.data.length == 0, "Ut");

30:         require(facetAddress != address(0), "F"); // Proxy has no facet for this selector

31:         require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L14

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

34:         require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights

59:         require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");

70:         require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");

130:        require(!diamondStorage.isFrozen, "a9"); // diamond proxy is frozen already

140:        require(diamondStorage.isFrozen, "a7"); // diamond proxy is not frozen

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

37:         require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f"); // only commit next batch

39:         require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us");

69:         require(_previousBatch.batchHash == logOutput.previousBatchHash, "l");

71:         require(logOutput.chainedPriorityTxsHash == _newBatch.priorityOperationsHash, "t");

73:         require(logOutput.numberOfLayer1Txs == _newBatch.numberOfLayer1Txs, "ta");

105:        require(batchTimestamp == _expectedBatchTimestamp, "tb");

109:        require(_previousBatchTimestamp < batchTimestamp, "h3");

117:        require(block.timestamp - COMMIT_TIMESTAMP_NOT_OLDER <= batchTimestamp, "h1"); // New batch timestamp is too small

118:        require(lastL2BlockTimestamp <= block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA, "h2"); // The last L2 block timestamp is too big

144:        require(!_checkBit(processedLogs, uint8(logKey)), "kp");

149:        require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");

152:        require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");

155:        require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");

158:        require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");

161:        require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");

164:        require(logSender == L2_BOOTLOADER_ADDRESS, "bl");

167:        require(logSender == L2_BOOTLOADER_ADDRESS, "bk");

170:        require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");

173:        require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");

176:        require(logSender == L2_BOOTLOADER_ADDRESS, "bu");

177:        require(_expectedSystemContractUpgradeTxHash == logValue, "ut");

179:        revert("ul");

187:        require(processedLogs == 511, "b7");

189:        require(processedLogs == 1023, "b8");

226:        require(_newBatchesData.length == 1, "e4");

228:        require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data

279:         require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");

318:         require(currentBatchNumber == s.totalBatchesExecuted + _executedBatchIdx + 1, "k"); // Execute batches in order

325:         require(priorityOperationsHash == _storedBatch.priorityOperationsHash, "x"); // priority operations hash does not match to expected

353:         require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.

397:         require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

416:         require(currentTotalBatchesVerified <= s.totalBatchesCommitted, "q");

437:         require(proofPublicInput.length == 1, "t4");

444:         require(successVerifyProof, "p"); // Proof verification fail

477:         require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch```solidity
file:


478:         require(_newLastBatch >= s.totalBatchesExecuted, "v2"); // Already executed batches cannot be reverted

530:         require(_batch.systemLogs.length <= MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES, "pu");

582:         require(success, "failed to call point evaluation precompile");

584:         require(result == BLS_MODULUS, "precompile unexpected output");

597:         require(_pubdataCommitments.length > 0, "pl");

598:         require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");

599:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");

605:         require(blobVersionedHash != bytes32(0), "vh");

629:         require(versionedHash == bytes32(0), "lh");

647:         require(success, "vc");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L37

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

182:         require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L182

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

39:         require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");

48:         require(callSuccess, "ShB: transferEthToSharedBridge failed");

115:        require(_batchNumber <= s.totalBatchesExecuted, "xx");

122:        require(hashedLog != L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH, "tw");

163:        require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

190:        require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");

211:        require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for eth base token");

248:        require(_request.l2GasPerPubdataByteLimit == REQUIRED_L2_GAS_PRICE_PER_PUBDATA, "qp");

276:        require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj");

284:        require(_mintValue >= baseCost + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

16:         require(msg.sender == s.admin, "StateTransition Chain: not admin");

22:         require(s.validators[msg.sender], "StateTransition Chain: not validator");

27:         require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

32:         require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

53:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

107:         require(selectors.length > 0, "B"); // no functions for diamond cut

116:         revert("C"); // undefined diamond cut action

132:         require(_facet.code.length > 0, "G");

141:         require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists

155:         require(_facet.code.length > 0, "K");

161:         require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

175:         require(_facet == address(0), "a1"); // facet address must be zero

181:         require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet

215:         require(_isSelectorFreezable == ds.selectorToFacet[selector0].isFreezable, "J1");

280:         require(_calldata.length == 0, "H"); // Non-empty calldata for zero address

287:         revert("I"); // delegatecall failed

297:         require(data.length == 32, "lp");

298:         require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

24:         require(pathLength > 0, "xc");

25:         require(pathLength < 256, "bt");

26:         require(_index < (1 << pathLength), "px");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

65:         require(!_queue.isEmpty(), "D"); // priority queue is empty

73:         require(!_queue.isEmpty(), "s"); // priority queue is empty

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L65

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

28:         require(l2GasForTxBody <= _priorityTxMaxGasLimit, "ui");

30:         require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");

48:         require(_transaction.from <= type(uint16).max, "ua");

49:         require(_transaction.to <= type(uint160).max, "ub");

50:         require(_transaction.paymaster == 0, "uc");

51:         require(_transaction.value == 0, "ud");

52:         require(_transaction.maxFeePerGas == 0, "uq");

53:         require(_transaction.maxPriorityFeePerGas == 0, "ux");

54:         require(_transaction.reserved[0] == 0, "ue");

55:         require(_transaction.reserved[1] <= type(uint160).max, "uf");

56:         require(_transaction.reserved[2] == 0, "ug");

57:         require(_transaction.reserved[3] == 0, "uo");

58:         require(_transaction.signature.length == 0, "uh");

59:         require(_transaction.paymasterInput.length == 0, "ul1");

60:         require(_transaction.reservedDynamic.length == 0, "um");

115:        require(_totalGasLimit >= overhead, "my"); // provided gas limit doesn't cover transaction overhead

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L28

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

72:         require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

190:        require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");

223:        require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");

224:        require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");

249:        require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L72

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

33:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

52:         require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol

26:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

37:         require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");

48:         require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");

57:         require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L26

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol

37:        revert("Unsupported tx type");

92:        require(vInt == 27 || vInt == 28, "Invalid v value");

191:       require(vInt == 27 || vInt == 28, "Invalid v value");

286:       require(vInt == 27 || vInt == 28, "Invalid v value");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L37

```solidity
File: system-contracts/contracts/ComplexUpgrader.sol

22:         require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");

24:         require(_delegateTo.code.length > 0, "Delegatee is an EOA");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22

```solidity
File: system-contracts/contracts/Compressor.sol

63:          require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

68:          require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");

119:         require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");

140:         require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");

156:         require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");

171:         require(enumIndex == compressedEnumIndex, "rw: enum key mismatch");

187:         require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");

230:         require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");

242:         revert("unsupported operation");


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L63

```solidity
File: system-contracts/contracts/ContractDeployer.sol

29:          require(msg.sender == address(this), "Callable only by self");

273:         require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");

286:         require(_bytecodeHash != bytes32(0x0), "BytecodeHash cannot be zero");

287:         require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

295:         require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied");

325:         require(knownCodeMarker > 0, "The code hash is not known");

372:         require(value == 0, "The value must be zero if we do not call the constructor");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29

```solidity
File: system-contracts/contracts/DefaultAccount.sol

100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

160:         require(_signature.length == 65, "Signature length is incorrect");

173:         require(v == 27 || v == 28, "v is neither 27 nor 28");

184:         require(uint256(s) <= 0x7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF5D576E7357A4501DDFE92F46681B20A0, "Invalid s");

202:         require(success, "Failed to pay the fee to the operator");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

35:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

20:         require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");

76:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");

78:         require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L20

```solidity
File: system-contracts/contracts/L1Messenger.sol

205:         require(numberOfL2ToL1Logs <= L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, "Too many L2->L1 logs");

302:         require(calldataPtr <= MAX_ALLOWED_PUBDATA_PER_BATCH, "L1 Messenger pubdata is too long");

319:         require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L205

```solidity
File: system-contracts/contracts/L2BaseToken.sol

41:         require(fromBalance >= _amount, "Transfer amount exceeds balance");
    
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L41


```solidity
File: system-contracts/contracts/NonceHolder.sol

66:         require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");

85:         require(_value != 0, "Nonce value cannot be set to 0");

89:         require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");

115:        require(oldMinNonce == _expectedNonce, "Incorrect nonce");

170:        revert("Reusing the same nonce twice");

172:        revert("The nonce was not set as used");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L66

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol

22:         require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L22

```solidity
File: system-contracts/contracts/SystemContext.sol

219:         require(_isFirstInBatch, "Upgrade transaction must be first");

222:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

226:         require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");

264:         require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

332:         require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

344:         require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");

345:         require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");

350:         require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");

362:         require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");

371:         revert("Invalid new L2 block number");

390:         require(currentBatchNumber > 0, "The current batch number must be greater than 0");

428:         require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");

429:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L219


## [G-27] Use inline assembly to check for address(0)

Writing contracts in inline assembly is generally considered gas optimized. we can manipulate memory directly and use fewer opcodes instead of leaving it to the Solidity compiler.


Authentication mechanism is one example where using inline assembly is good, like implementing address zero check.

Here’s an example below:

<details> 

```solidity

// SPDX-License-Identifier: MIT
pragma solidity 0.8.20;

contract NormalAddressZeroCheck {
    function check(address _caller) public pure returns (bool) {
        require(_caller != address(0x00), "Zero address");
        return true;
    }
}

contract AddressZeroCheckAssembly {
    // Saves about 90 gasfunction checkOptimized(address _caller) public pure returns (bool) {
        assembly {
            if iszero(_caller) {
                mstore(0x00, 0x20)
                mstore(0x20, 0x0c)
                mstore(0x40, 0x5a65726f20416464726573730000000000000000000000000000000000000000) // load hex of "Zero Address" to memory
                revert(0x00, 0x60)
            }
        }

        return true;
    }
}

```

</details>

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

108   require(_owner != address(0), "ShB owner 0");

188   require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

563   require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

578   if (_refundRecipient == address(0)) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L108

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

68  emit NewPendingAdmin(currentPendingAdmin, address(0));

130 require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

132 require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

326 if (_refundRecipient == address(0)) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol
 
42   require(_admin != address(0), "Admin should be non zero address");

47   emit ChangeSecurityCouncil(address(0), _securityCouncil);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L42


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

82  require(_initializeData.governor != address(0), "StateTransition: governor zero");

127 emit NewPendingAdmin(currentPendingAdmin, address(0));

207 verifier: address(0),

246 if (stateTransition[_chainId] != address(0)) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L82

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

25   require(address(_initializeData.verifier) != address(0), "vt");

26   require(_initializeData.admin != address(0), "vy");

27   require(_initializeData.validatorTimelock != address(0), "hc");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

30  require(facetAddress != address(0), "F"); // Proxy has no facet for this selector

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

40  emit NewPendingAdmin(pendingAdmin, address(0));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

183   require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

275   address refundRecipient = _params.refundRecipient == address(0) ? _params.sender : _params.refundRecipient;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L275

```solidity 
file: blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

141  require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists

161  require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

175  require(_facet == address(0), "a1"); // facet address must be zero

181  require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet

279  if (_init == address(0)) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L141


```solidity
file: blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
 
131  if (_newVerifier == IVerifier(address(0))) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L131

```solidity
file: blob/main/code/system-contracts/contracts/DefaultAccount.sol

188  return recoveredAddress == address(this) && recoveredAddress != address(0);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L188


```solidity
file: blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol

406  if (address(uint160(_transaction.paymaster)) != address(0)) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L406


## [G-28] selfbalance is cheaper than address(this).balance (more efficient in certain scenarios)

The solidity code address(this).balance can sometimes be done more efficiently with the selfbalance() function from yul, but be aware the compiler is sometimes smart enough to use this trick under the hood, so test both ways.

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

118  uint256 balanceBefore = address(this).balance;

120  uint256 balanceAfter = address(this).balance;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

41  uint256 amount = address(this).balance;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41


```solidity
file: blob/main/code/system-contracts/contracts/DefaultAccount.sol

100   require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100



## [G-29] Change Constant to Immutable for keccak Variables

The use of constant keccak variables results in extra hashing (and so gas). This results in the keccak operation being performed whenever the variable is used, increasing gas costs relative to just storing the output hash. Changing to immutable will only perform hashing on contract deployment which will save gas. You should use immutables until the referenced issues are implemented, then you only pay the gas costs for the computation at deploy time.

```solidity
file: blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol

82  bytes32 constant EIP712_DOMAIN_TYPEHASH = keccak256("EIP712Domain(string name,string version,uint256 chainId)");

82  bytes32 constant EIP712_TRANSACTION_TYPE_HASH =
        keccak256(
            "Transaction(uint256 txType,uint256 from,uint256 to,uint256 gasLimit,uint256 gasPerPubdataByteLimit,uint256 maxFeePerGas,uint256 maxPriorityFeePerGas,uint256 paymaster,uint256 nonce,uint256 value,bytes data,bytes32[] factoryDeps,bytes paymasterInput)"
        );

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L82

## [G-30] Use Double Require/if Instead of Operator &&

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

75  require(
            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
            "L1SharedBridge: not bridgehub or era chain"
        );

375  return (_chainId == ERA_CHAIN_ID) && (_l2BatchNumber < eraFirstPostUpgradeBatch);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75-L78

```solidity
file: blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

41  require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L41

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

361  if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {

668  require(
                (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
                    (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
                "bh"
            );

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L361

```solidity
file: blob/main/code/system-contracts/contracts/AccountCodeStorage.sol

102  if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L102

```solidity
file: blob/main/code/system-contracts/contracts/DefaultAccount.sol

139   if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) {
    
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L139


```solidity
file: blob/main/code/system-contracts/contracts/KnownCodesStorage.sol

76   require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L76

```solidity
file: blob/main/code/system-contracts/contracts/NonceHolder.sol

88  if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {

169  if (isUsed && !_shouldBeUsed) {

171  } else if (!isUsed && _shouldBeUsed) {
    
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L88


```solidity
file: blob/main/code/system-contracts/contracts/SystemContext.sol

277  if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {

360  if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L277


## [G-31] Precompute Off-Chain When Possible

Computing values in advance outside the blockchain is cheaper than doing it inside smart contracts:


<details>

```solidity

// On-chain computation
function verify(uint numA, uint numB) {
  require(numA * numB < 1000);
}

// Precomputed off-chain
function verify(uint result) {
  require(result < 1000); 
}

```

</details>

Do computations like hashes, signatures outside.
Pass in precomputed values to save on-chain gas.

```solidity
file: blob/main/code/system-contracts/contracts/Compressor.sol

51  require(
                encodedData.length * 4 == _bytecode.length,
                "Encoded data length should be 4 times shorter than the original bytecode"
            );

56   require(
                dictionary.length / 8 <= encodedData.length / 2,
                "Dictionary should have at most the same number of entries as the encoded data"
            );

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L51-L54


```solidity
file: blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

26   require(bytecodeLenInWords < 2 ** 16, "pp");

27   require(bytecodeLenInWords % 2 == 1, "ps");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L26

```solidity
file: blob/main/code/system-contracts/contracts/SystemContext.sol

144   if (blockNumber <= _block || blockNumber - _block > 256) {

374   } else if (currentL2BlockNumber + 1 == _l2BlockNumber) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L144


```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

132  require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132


```solidity
file: blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

23   require(_bytecode.length % 32 == 0, "pq");

43   require(bytecodeLen(_bytecodeHash) % 2 == 1, "uy")

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

195   require(block.timestamp >= commitBatchTimestamp + delay, "5c");

217   require(block.timestamp >= commitBatchTimestamp + delay, "5c");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

37   require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f"); 

61   require(
                logOutput.pubdataHash ==
                    keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),
                "wp"
            );
323   require(currentBatchNumber == s.totalBatchesExecuted + _executedBatchIdx + 1, "k");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L37

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

272   require(_mintValue >= baseCost + _params.l2Value, "mv");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L272

```solidity
file: blob/main/code/system-contracts/contracts/libraries/Utils.sol

84     require(_bytecode.length % 32 == 0, "po");

87     require(lengthInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words

88     require(lengthInWords % 2 == 1, "pr"); // bytecode length in words must be odd

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L84



## [G-32] Don't initialize Variables with Default Values:

If a variable is not set/initialized, it is assumed to have the default value . Explicitly initializing it with its default value is an anti-pattern and wastes gas


```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

25   for (uint256 i = 0; i < _calls.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L25


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

135  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

185  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

209  for (uint256 i = 0; i < _newBatchesData.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

580   for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

667   for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580

```solidity
file: blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226   for (uint256 i = 0; i < _factoryDeps.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226


```solidity
file: blob/main/code/system-contracts/contracts/ContractDeployer.sol

248    for (uint256 i = 0; i < deploymentsLength; ++i) {

253    for (uint256 i = 0; i < deploymentsLength; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L248

```solidity
file:  blob/main/code/system-contracts/contracts/ImmutableSimulator.sol
 
38   for (uint256 i = 0; i < immutablesLength; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L38

```solidity
file: blob/main/code/system-contracts/contracts/KnownCodesStorage.sol

30  for (uint256 i = 0; i < hashesLen; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L30


```solidity
file: blob/main/code/system-contracts/contracts/L1Messenger.sol

206   for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

224   for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

236   for (uint256 i = 0; i < numberOfMessages; ++i) {

254   for (uint256 i = 0; i < numberOfBytecodes; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206


```solidity
file: blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol

36   for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36


## [G-33] Use of memory instead of calldata for immutable arguments

Consider refactoring the function arguments from memory to calldata when they are immutable, as calldata is cheaper.

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

460  MessageParams memory _messageParams,

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L460


```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

168  L2Log memory _log,

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L168

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol

85   L2Log memory _log,

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L85

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

33   StoredBatchInfo memory _previousBatch,

200  StoredBatchInfo memory _lastCommittedBatchData,

209  StoredBatchInfo memory _lastCommittedBatchData,

216  StoredBatchInfo memory _lastCommittedBatchData,

254  StoredBatchInfo memory _lastCommittedBatchData,

274  StoredBatchInfo memory _lastCommittedBatchData,

321  function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {

456  VerifierParams memory _verifierParams

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L33

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

202 function facets() external view returns (Facet[] memory result) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L202

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

48   BridgehubL2TransactionRequest memory _request

57   L2Message memory _message,

67   L2Log memory _log,

130  function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {

229  BridgehubL2TransactionRequest memory _request

260  WritePriorityOpParams memory _params,

290  WritePriorityOpParams memory _priorityOpParams,

317  WritePriorityOpParams memory _priorityOpParams,

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L48


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

96   function diamondCut(DiamondCutData memory _diamondCut) internal {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L96


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

55   function pushBack(Queue storage _queue, PriorityOperation memory _operation) internal {

72   function popFront(Queue storage _queue) internal returns (PriorityOperation memory priorityOperation) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L55


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

20   L2CanonicalTransaction memory _transaction,

46   function validateUpgradeTransaction(L2CanonicalTransaction memory _transaction) internal pure {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L20


## [G-34] Use uint256(1)/uint256(2) instead of true/false to save gas for changes

Use uint256(1) and uint256(2) for true/false to avoid a Gsset (20000 gas) when changing from false to true, after having been true in the past. See source.

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

103  bool zkPorterIsAvailable;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L103


## [G-35] Cache multiple accesses of a mapping/array

Consider using a local storage or calldata variable when accessing a mapping/array value multiple times.

This can be useful to avoid recalculating the mapping hash and/or the array offsets.

### Some Gas Optimizations in ```L1SharedBridge.sol`` contract 


#### cache depositHappened[_chainId][_txHash] mapping in ```L1SharedBridge.bridgehubConfirmL2Transaction()``` function

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

232  function bridgehubConfirmL2Transaction(
        uint256 _chainId,
        bytes32 _txDataHash,
        bytes32 _txHash
    ) external override onlyBridgehub {
        require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");
        depositHappened[_chainId][_txHash] = _txDataHash;
        emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L232-L240
 

#### cache depositHappened[_chainId][_l2TxHash] mapping in ```L1SharedBridge._claimFailedDeposit()``` function

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

339  if (notCheckedInLegacyBridgeOrWeCanCheckDeposit) {
                bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
                bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));
                require(dataHash == txDataHash, "ShB: d.it not hap");
                delete depositHappened[_chainId][_l2TxHash];
            }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L339-L344

#### cache isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] mapping in ```L1SharedBridge._finalizeWithdrawal()``` function

```solidity
file:  blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

409     function _finalizeWithdrawal(
        uint256 _chainId,
        uint256 _l2BatchNumber,
        uint256 _l2MessageIndex,
        uint16 _l2TxNumberInBatch,
        bytes calldata _message,
        bytes32[] calldata _merkleProof
    ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
        require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");
        isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L409-L418



#### cache chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] and chainBalance[_targetChainId][_token] mapping in ```L1SharedBridge.transferFundsFromLegacy()``` function

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

116  function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
        if (_token == ETH_TOKEN_ADDRESS) {
            uint256 balanceBefore = address(this).balance;
            IMailbox(_target).transferEthToSharedBridge();
            uint256 balanceAfter = address(this).balance;
            require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");
            chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
                chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
                balanceAfter -
                balanceBefore;
        } else {
            uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
            uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
            require(amount > 0, "ShB: 0 amount to transfer");
            IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);
            uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
            require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
        }
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L116-L135

#### cache  chainBalance[_chainId][_l1Token]  mapping in ```L1SharedBridge._claimFailedDeposit()``` function

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

347  if (!hyperbridgingEnabled[_chainId]) {
            // check that the chain has sufficient balance
            require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
            chainBalance[_chainId][_l1Token] -= _amount;
        }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L347-L351

#### cache l2BridgeAddress[_chainId] mapping

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

182      function bridgehubDeposit(
        uint256 _chainId,
        address _prevMsgSender,
        uint256, // l2Value, needed for Weth deposits in the future
        bytes calldata _data
    ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
        require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

        (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
            _data,
            (address, uint256, address)
        );
        require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");
        require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

        uint256 amount;
        if (_l1Token == ETH_TOKEN_ADDRESS) {
            amount = msg.value;
            require(_depositAmount == 0, "ShB wrong withdraw amount");
        } else {
            require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
            amount = _depositAmount;

            uint256 withdrawAmount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount);
            require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic
        }
        require(amount != 0, "6T"); // empty deposit amount

        bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));
        if (!hyperbridgingEnabled[_chainId]) {
            chainBalance[_chainId][_l1Token] += amount;
        }

        {
            // Request the finalization of the deposit on the L2 side
            bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, amount);

            request = L2TransactionRequestTwoBridgesInner({
                magicValue: TWO_BRIDGES_MAGIC_VALUE,
                l2Contract: l2BridgeAddress[_chainId],
                l2Calldata: l2TxCalldata,
                factoryDeps: new bytes[](0),
                txDataHash: txDataHash
            });
        }
        emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L182-L228


### Some Gas Optimizations in ```Bridgehub.sol`` contract 

#### cache stateTransitionManagerIsRegistered[_stateTransitionManager] mapping in ```Bridgehub.addStateTransitionManager``` function 

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

82  function addStateTransitionManager(address _stateTransitionManager) external onlyOwner {
        require(
            !stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition already registered"
        );
        stateTransitionManagerIsRegistered[_stateTransitionManager] = true;
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L82-L88


#### cache stateTransitionManagerIsRegistered[_stateTransitionManager] mapping in ```Bridgehub.removeStateTransitionManager``` function 

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

92  function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner {
        require(
            stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition not registered yet"
        );
        stateTransitionManagerIsRegistered[_stateTransitionManager] = false;
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L92-L98

#### cache tokenIsRegistered[_token] mapping in ```Bridgehub.addToken``` function 

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

101  function addToken(address _token) external onlyOwner {
        require(!tokenIsRegistered[_token], "Bridgehub: token already registered");
        tokenIsRegistered[_token] = true;
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L101-L104


#### cache stateTransitionManager[_chainId] mapping in ```Bridgehub.createNewChain``` function 

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

132     require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

        stateTransitionManager[_chainId] = _stateTransitionManager;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132-L134


### Some Gas Optimizations in ```ValidatorTimelock.sol`` contract 

#### cache validators[_chainId][_newValidator] mapping in ```ValidatorTimelock.addValidator``` function 


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

78   function addValidator(uint256 _chainId, address _newValidator) external onlyChainAdmin(_chainId) {
        if (validators[_chainId][_newValidator]) {
            revert AddressAlreadyValidator(_chainId);
        }
        validators[_chainId][_newValidator] = true;
        emit ValidatorAdded(_chainId, _newValidator);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L78-L84

#### cache validators[_chainId][_validator] mapping in ```ValidatorTimelock.removeValidator``` function 

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

87  function removeValidator(uint256 _chainId, address _validator) external onlyChainAdmin(_chainId) {
        if (!validators[_chainId][_validator]) {
            revert ValidatorDoesNotExist(_chainId);
        }
        validators[_chainId][_validator] = false;
        emit ValidatorRemoved(_chainId, _validator);
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L87-L93


### Some Gas Optimizations in ```Diamond.sol`` contract 

#### cache facetToSelectors[_facet] mapping in _saveFacetIfNew,_addOneFunction and _removeOneFunction function 


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

189 function _saveFacetIfNew(address _facet) private {
        DiamondStorage storage ds = getDiamondStorage();

        uint256 selectorsLength = ds.facetToSelectors[_facet].selectors.length;
        // If there are no selectors associated with facet then save facet as new one
        if (selectorsLength == 0) {
            ds.facetToSelectors[_facet].facetPosition = ds.facets.length.toUint16();
            ds.facets.push(_facet);
        }
    }

205  function _addOneFunction(address _facet, bytes4 _selector, bool _isSelectorFreezable) private {
        DiamondStorage storage ds = getDiamondStorage();

        uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16();

        // if selectorPosition is nonzero, it means it is not a new facet
        // so the freezability of the first selector must be matched to _isSelectorFreezable
        // so all the selectors in a facet will have the same freezability
        if (selectorPosition != 0) {
            bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];
            require(_isSelectorFreezable == ds.selectorToFacet[selector0].isFreezable, "J1");
        }

        ds.selectorToFacet[_selector] = SelectorToFacet({
            facetAddress: _facet,
            selectorPosition: selectorPosition,
            isFreezable: _isSelectorFreezable
        });
        ds.facetToSelectors[_facet].selectors.push(_selector);
    }

228   function _removeOneFunction(address _facet, bytes4 _selector) private {
        DiamondStorage storage ds = getDiamondStorage();

        // Get index of `FacetToSelectors.selectors` of the selector and last element of array
        uint256 selectorPosition = ds.selectorToFacet[_selector].selectorPosition;
        uint256 lastSelectorPosition = ds.facetToSelectors[_facet].selectors.length - 1;

        // If the selector is not at the end of the array then move the last element to the selector position
        if (selectorPosition != lastSelectorPosition) {
            bytes4 lastSelector = ds.facetToSelectors[_facet].selectors[lastSelectorPosition];

            ds.facetToSelectors[_facet].selectors[selectorPosition] = lastSelector;
            ds.selectorToFacet[lastSelector].selectorPosition = selectorPosition.toUint16();
        }

        // Remove last element from the selectors array
        ds.facetToSelectors[_facet].selectors.pop();

        // Finally, clean up the association with facet
        delete ds.selectorToFacet[_selector];

        // If there are no selectors for facet then remove the facet from the list of known facets
        if (lastSelectorPosition == 0) {
            _removeFacet(_facet);
        }
    }


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L189-L198

### Some Gas Optimizations in ```L2BaseToken.sol`` contract 

#### cache facetToSelectors[_facet] mapping in ```L2BaseToken.transferFromTo``` function 

```solidity
file: blob/main/code/system-contracts/contracts/L2BaseToken.sol

32  function transferFromTo(address _from, address _to, uint256 _amount) external override {
        require(
            msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
                msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
                msg.sender == BOOTLOADER_FORMAL_ADDRESS,
            "Only system contracts with special access can call this method"
        );

        uint256 fromBalance = balance[_from];
        require(fromBalance >= _amount, "Transfer amount exceeds balance");
        unchecked {
            balance[_from] = fromBalance - _amount;
            // Overflow not possible: the sum of all balances is capped by totalSupply, and the sum is preserved by
            // decrementing then incrementing.
            balance[_to] += _amount;
        }

        emit Transfer(_from, _to, _amount);
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L32-L50



### Some Gas Optimizations in ```NonceHolder.sol`` contract 

#### cache facetToSelectors[_facet] mapping in increaseMinNonce,incrementMinNonceIfEquals and incrementDeploymentNonce function 

```solidity
file: blob/main/code/system-contracts/contracts/NonceHolder.sol

65  function increaseMinNonce(uint256 _value) public onlySystemCall returns (uint256 oldMinNonce) {
        require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");

        uint256 addressAsKey = uint256(uint160(msg.sender));
        uint256 oldRawNonce = rawNonces[addressAsKey];

        unchecked {
            rawNonces[addressAsKey] = (oldRawNonce + _value);
        }

        (, oldMinNonce) = _splitRawNonce(oldRawNonce);
    }

110   function incrementMinNonceIfEquals(uint256 _expectedNonce) external onlySystemCall {
        uint256 addressAsKey = uint256(uint160(msg.sender));
        uint256 oldRawNonce = rawNonces[addressAsKey];

        (, uint256 oldMinNonce) = _splitRawNonce(oldRawNonce);
        require(oldMinNonce == _expectedNonce, "Incorrect nonce");

        unchecked {
            rawNonces[addressAsKey] = oldRawNonce + 1;
        }
    }

135 function incrementDeploymentNonce(address _address) external returns (uint256 prevDeploymentNonce) {
        require(
            msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
            "Only the contract deployer can increment the deployment nonce"
        );
        uint256 addressAsKey = uint256(uint160(_address));
        uint256 oldRawNonce = rawNonces[addressAsKey];

        unchecked {
            rawNonces[addressAsKey] = (oldRawNonce + DEPLOY_NONCE_MULTIPLIER);
        }

        (prevDeploymentNonce, ) = _splitRawNonce(oldRawNonce);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L65-L76


## [G-36] Empty Block

The code should be refactored such that they no longer exist, or the block should do something useful, such as emitting an event or reverting. If the contract is meant to be extended, the contract should be abstract and the function signatures be added without any default implementation. If the block is an empty if-statement block to avoid doing subsequent checks in the else-if/else conditions, the else-if/else conditions should be nested under the negation of the if-statement, because they involve different classes of checks, which may lead to the introduction of errors when the code is later modified.

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

262  receive() external payable {}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L262

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

60  function initialize() external reentrancyGuardInitializer {}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L60

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

38  constructor() reentrancyGuardInitializer {}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol
 
19  constructor() reentrancyGuardInitializer {}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19


```solidity
file: blob/main/code/system-contracts/contracts/EmptyContract.sol

11  fallback() external payable {}

13  receive() external payable {}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/EmptyContract.sol#L11        


## [G-37] Emitting constants wastes gas

Every event parameter costs Glogdata (8 gas) per byte. You can avoid this extra cost, in cases where you're emitting a constant, by creating a second version of the event, which doesn't have the parameter (and have users look to the contract's variables for its value instead), and using the new event in the cases shown below.

```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

50   emit ChangeMinDelay(0, _minDelay);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L50

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

602  emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L602

## [G-38] Inline modifiers that are only used once, to save gas

Inline modifiers that are only used once, to save gas.

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

74  modifier onlyBridgehubOrEra(uint256 _chainId) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L74

```solidity
file: blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol

41  modifier reentrancyGuardInitializer() {

68  modifier nonReentrant() {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L41


```solidity
file:  blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

64  modifier onlySecurityCouncil() {

70  modifier onlyOwnerOrSecurityCouncil() {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L64

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

63  modifier onlyBridgehub() {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L63

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

15  modifier onlyAdmin() {

21  modifier onlyValidator() {

26  modifier onlyStateTransitionManager() {

31  modifier onlyBridgehub() {

36  modifier onlyAdminOrStateTransitionManager() {

44  modifier onlyValidatorOrStateTransitionManager() {

52  modifier onlyBaseTokenBridge() {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L15

```solidity
file: blob/main/code/system-contracts/contracts/ContractDeployer.sol

28  modifier onlySelf() {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L28

```solidity
file: blob/main/code/system-contracts/contracts/KnownCodesStorage.sol

19   modifier onlyCompressor() {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L19


## [G-40] Use assembly to calculate hashes

If the arguments to the encode call can fit into the scratch space (two words or fewer), then it's more efficient to use assembly to generate the hash (80 gas):

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

76   bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76


```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

210   bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));

341   bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));

598   bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L210


```solidity
file: blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

12  bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");

67  bytes32 data = keccak256(

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L12


```solidity
file: blob/main/code/contracts/ethereum/contracts/governance/Governance.sol

205  return keccak256(abi.encode(_operation));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L205


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

100   storedBatchZero = keccak256(abi.encode(batchZero));

102   initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

147   upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

156   upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

255   bytes32 cutHashInput = keccak256(_diamondCut);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

104  bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

63    keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),

313   concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));

460   keccak256(

506   bytes32 passThroughDataHash = keccak256(_batchPassThroughData(_newBatchData));

507   bytes32 metadataHash = keccak256(_batchMetaParameters());

508   bytes32 auxiliaryOutputHash = keccak256(

545   bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs);

588   return keccak256(abi.encode(_storedBatchInfo));

654   blobCommitments[versionedHashIndex] = keccak256(

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L63


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

112  bytes32 hashedLog = keccak256(

138  value: keccak256(_message.data)

332  canonicalTxHash = keccak256(transactionEncoding);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L112


```solidity
file: blob/main/code/system-contracts/contracts/BootloaderUtilities.sol

29    txHash = keccak256(bytes.concat(signedTxHash, EfficientCall.keccak(_transaction.signature)));

120   keccak256(

211   keccak256(

306   keccak256(

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L29


```solidity
file; blob/main/code/system-contracts/contracts/ContractDeployer.sol

105   bytes32 hash = keccak256(

121   bytes32 hash = keccak256(

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L105


```solidity
file: blob/main/code/system-contracts/contracts/L1Messenger.sol

95  bytes32 hashedLog = keccak256(

106 chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

122 chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

164 chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

212 reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));

225 l2ToL1LogsTreeArray[i] = keccak256(

243 reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));

259 reconstructedChainedL1BytecodesRevealDataHash = keccak256(

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L95

```solidity
file: blob/main/code/system-contracts/contracts/SystemContext.sol

159  hash = keccak256(abi.encode(_block));

227  return keccak256(abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash));

234  return keccak256(abi.encodePacked(uint32(_blockNumber)));

403  currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L159


```solidity
file: blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol

82  bytes32 constant EIP712_DOMAIN_TYPEHASH = keccak256("EIP712Domain(string name,string version,uint256 chainId)");

85  keccak256(
            "Transaction(uint256 txType,uint256 from,uint256 to,uint256 gasLimit,uint256 gasPerPubdataByteLimit,uint256 maxFeePerGas,uint256 maxPriorityFeePerGas,uint256 paymaster,uint256 nonce,uint256 value,bytes data,bytes32[] factoryDeps,bytes paymasterInput)"
        );

119  bytes32 structHash = keccak256(

133  keccak256(abi.encodePacked(_transaction.factoryDeps)),

138  bytes32 domainSeparator = keccak256(

139   abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

142  return keccak256(abi.encodePacked("\x19\x01", domainSeparator, structHash));

203  keccak256(

275  keccak256(

347  keccak256(
 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L82

## [G-41] Use assembly in place of abi.decode to extract calldata values more efficiently

Instead of using abi.decode, we can use assembly to decode our desired calldata values directly. This will allow us to avoid decoding calldata values that we will not use.

```solidity
file: blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

190   (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L190

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
 
252  Diamond.DiamondCutData memory diamondCut = abi.decode(_diamondCut, (Diamond.DiamondCutData));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L252

```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

617   (, uint256 result) = abi.decode(data, (uint256, uint256));

682   versionedHash = abi.decode(data, (bytes32));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L617


```solidity
file: blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

298  require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L298


```solidity
file: blob/main/code/system-contracts/contracts/ContractDeployer.sol

347  ImmutableData[] memory immutables = abi.decode(returnData, (ImmutableData[]));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L347

```solidity
file: blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol
 
374  (address token, uint256 minAllowance) = abi.decode(_transaction.paymasterInput[4:68], (address, uint256));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L374