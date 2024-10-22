# GAS OPTIMIZATIONS

| Count | Issue                                                                                   | Gas Saved (Estimate) |
|-------|-------------------------------------------------------------------------------------------|----------------------|
| G-1   | State variables can be packed into fewer storage slots                                    | 8000 GAS             |
| G-1.1 | `stateTransitionManager` and `executionDelay` can be packed in the same slot            | 2000 GAS, 1 SLOT     |
| G-1.2 | `securityCouncil` and `minDelay` can be packed in the same slot                          | -                    |
| G-1.3 | `genesisUpgrade` and `protocolVersion` can be packed with the same slot                  | 2000 GAS, 1 SLOT     |
| G-1.4 | `chainId` and `origin` can be packed in the same slot                                    | 2000 GAS             |
| G-2   | `l2BridgeAddress[_chainId]`, `l2BridgeAddress[ERA_CHAIN_ID]`, `chainBalance...` mappings can be cached | 400 GAS, 4 SLOAD     |
| G-3   | State variables should be cached with stack variable                                     | 100 GAS, 1 SLOAD     |
| G-3.1 | Cache `sharedBridge` storage variable to reduce redundant access                         | 100 GAS, 1 SLOAD     |
| G-3.2 | `basePubdataSpent` should be cached                                                      | 100 GAS, 1 SLOAD     |
| G-4   | `AddressAliasHelper.undoL1ToL2Alias(msg.sender)` function value should be cached         | 2000 GAS             |
| G-5   | Don't cache the `_refundRecipient` as it's already a memory variable                     | 35 GAS               |
| G-6   | Parameter validation prior to storage validations for better gas efficiency              | -                    |
| G-7   | Don't emit state variables when a stack variable is available                            | 375 GAS              |
| G-8   | Using storage instead of memory for structs/arrays saves gas                             | -                    |
| G-9   | Consolidating multiple mappings into a single struct mapping for gas optimization         | -                    |
| G-10  | Consolidating multiple event emissions into a single event saves gas                     | 375 GAS              |
| G-11  | Updating storage while emitting events                                                   | 21 GAS               |
| G-12  | Assigning state variables directly with named struct constructors wastes gas             | -                    |
| G-13  | Consider using alternatives to OpenZeppelin                                              | -                    |
| G-14  | Using assembly to revert with an error message                                           | 300 GAS              |
| G-15  | Invert if-else statements that have a negation                                           | -                    |
| G-16  | The check `require(block.timestamp >= commitBatchTimestamp + delay, "5c")` is redundant when `commitBatchTimestamp` is 0 | 50 GAS              |
| G-17  | `hashL2Bytecode()` can be more gas optimized                                             | 100+ GAS             |
| G-18  | Skip the shifting process by optimizing `extractNumberFromMeta()`                        | -                    |
| G-19  | Don't cache state variable only used once                                                | -                    |
| G-20  | Avoid updating storage when the value hasn't changed                                     | -                    |
| G-21  | `_l2BlockNumber - 1` Subtraction results should be cached                                | -                |
| G-22  | ``dictionary.length`` and ``encodedData.length``  length should be cached                                | -                |
| G-23  | Optimizing Uint32 Storage Updates by Eliminating XOR Misuse                               | -                |

##

## [G-1] State variables can be packed into fewer storage slots

The EVM works with 32 byte words. Variables less than 32 bytes can be declared next to each other in storage and this will pack the values together into a single 32 byte storage slot (if the values combined are <= 32 bytes). If the variables packed together are retrieved together in functions we will effectively save ~2000 gas with every subsequent SLOAD for that storage slot. This is due to us incurring a Gwarmaccess (100 gas) versus a Gcoldsload (2100 gas).

### [G-1.1] ``stateTransitionManager`` and ``executionDelay`` can be packed same slot : Saves ``2000 GAS`` , ``1 SLOT``

If we rearrange the ``stateTransitionManager`` and ``executionDelay`` order we can save ``1 SLOT`` and ``2000 GAS`` 

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 /// @notice Error for when an address is not a validator.
    error ValidatorDoesNotExist(uint256 _chainId);

    /// @dev The stateTransitionManager smart contract.
    IStateTransitionManager public stateTransitionManager;

+   uint32 public executionDelay;

    /// @dev The mapping of L2 chainId => batch number => timestamp when it was committed.
    mapping(uint256 => LibMap.Uint32Map) internal committedBatchTimestamp;

    /// @dev The address that can commit/revert/validate/execute batches.
    mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;

    /// @dev The delay between committing and executing batches.
-    uint32 public executionDelay;

    constructor(address _initialOwner, uint32 _executionDelay) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L40-L53



### [G-1.2] ``securityCouncil`` and ``minDelay`` can be packed same Slot 

A ``uint96`` variable can hold values up to ``2^96 - 1``, which is a significantly large number. Specifically, it can represent up to over ``79 billion years``. Given that this range is far beyond any practical ``delay duration`` for any process or mechanism, uint96 provides more than sufficient capacity for a ``delay timer`` in ``seconds``. So packing ``securityCouncil`` and ``minDelay`` within same slot is perfectly safe.

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/governance
/Governance.sol

contract Governance is IGovernance, Ownable2Step {
    /// @notice A constant representing the timestamp for completed operations.
    uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1);

    /// @notice The address of the security council.
    /// @dev It is supposed to be multisig contract.
    address public securityCouncil;

+    uint96 public minDelay;

    /// @notice A mapping to store timestamps when each operation will be ready for execution.
    /// @dev - 0 means the operation is not created.
    /// @dev - 1 (EXECUTED_PROPOSAL_TIMESTAMP) means the operation is already executed.
    /// @dev - any other value means timestamp in seconds when the operation will be ready for execution.
    mapping(bytes32 operationId => uint256 executionTimestamp) public timestamps;

    /// @notice The minimum delay in seconds for operations to be ready for execution.
-    uint256 public minDelay;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L26-L35

##

## [G-1.3] ``genesisUpgrade`` and ``protocolVersion`` can be packed with same slot 

``protocolVersion`` as ``uint96``: uint256 is the default integer type in Solidity, occupying a full 32 bytes (256 bits). Using ``uint96`` (which is significantly smaller but still offers a large maximum value) could be more efficient in terms of storage, especially if it can be packed with other variables. ``uint96`` allows for values up to roughly ``79 quintillion``, which is ample for version numbering and most other conceivable uses. Saves ``2000 GAS`` , ``1 SLOT``

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition
/StateTransitionManager.sol

 /// @dev genesisUpgrade contract address, used to setChainId
    address public genesisUpgrade;

    /// @dev current protocolVersion
-    uint256 public protocolVersion;
+    uint96 public protocolVersion;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L42

### [G-1.4] ``chainId`` and ``origin`` can be packed same slot : Saves 2000 GAS 

chainId (type uint256) typically doesn't use the full range of a 256-bit number since chain IDs are much smaller integers. For most practical purposes, chain IDs like Ethereum's (1), Binance Smart Chain's (56), etc., are well below 2^96 (which is over 4 billion), meaning they could be represented with a uint96 without losing information.

```diff
FILE: 2024-03-zksync/code/system-contracts/contracts/SystemContext.sol

/// @notice The chainId of the network. It is set at the genesis.
-    uint256 public chainId;
+    uint96 public chainId;

    /// @notice The `tx.origin` in the current transaction.
    /// @dev It is updated before each transaction by the bootloader
    address public origin;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L26


##

## [G-2] l2BridgeAddress[_chainId] , l2BridgeAddress[ERA_CHAIN_ID] , ``chainBalance[_chainId][_l1Token]``  mappings can be cached 

 ``l2BridgeAddress[_chainId]``, ``l2BridgeAddress[ERA_CHAIN_ID]`` , ``chainBalance[_chainId][_l1Token]`` mappings that is accessed multiple times within a function. Caching this mapping could indeed be beneficial for optimizing gas usage. Saves ``400 GAS`` , ``4 SLOAD``

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1SharedBridge.sol

/// @notice Initiates a deposit transaction within Bridgehub, used by `requestL2TransactionTwoBridges`.
    function bridgehubDeposit(
        uint256 _chainId,
        address _prevMsgSender,
        uint256, // l2Value, needed for Weth deposits in the future
        bytes calldata _data
    ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {

+ address l2BridgeAddress_ = l2BridgeAddress[_chainId] ; 
-        require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
+        require(l2BridgeAddress_ != address(0), "ShB l2 bridge not deployed");

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
-                l2Contract: l2BridgeAddress[_chainId],
+                l2Contract: l2BridgeAddress_,
                l2Calldata: l2TxCalldata,
                factoryDeps: new bytes[](0),
                txDataHash: txDataHash
            });
        }
        emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188-L221

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1SharedBridge.sol

function depositLegacyErc20Bridge(
        address _prevMsgSender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte,
        address _refundRecipient
    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
+ address l2BridgeAddress_ = l2BridgeAddress[ERA_CHAIN_ID] ; 
-        require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
+        require(l2BridgeAddress_ != address(0), "ShB b. n dep");
        require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");

        // Note that funds have been transferred to this contract in the legacy ERC20 bridge.
        if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {
            chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
        }

        bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);

        {
            // If the refund recipient is not specified, the refund will be sent to the sender of the transaction.
            // Otherwise, the refund will be sent to the specified address.
            // If the recipient is a contract on L1, the address alias will be applied.
            address refundRecipient = _refundRecipient;
            if (_refundRecipient == address(0)) {
                refundRecipient = _prevMsgSender != tx.origin
                    ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
                    : _prevMsgSender;
            }

            L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
                chainId: ERA_CHAIN_ID,
-                l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
+                l2Contract: l2BridgeAddress_ ,
                mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
                l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
                l2Calldata: l2TxCalldata,
                l2GasLimit: _l2TxGasLimit,
                l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
                factoryDeps: new bytes[](0),
                refundRecipient: refundRecipient
            });
            l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
        }

        bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
        // Save the deposited amount to claim funds on L1 if the deposit failed on L2
        depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;

        emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
    }

```

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1SharedBridge.sol

if (!hyperbridgingEnabled[_chainId]) {
            // check that the chain has sufficient balance
+    uint256 chainBalanceAmount_ = chainBalance[_chainId][_l1Token] ;
-            require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
+            require(chainBalanceAmount_ >= _amount, "ShB n funds");
-            chainBalance[_chainId][_l1Token] -= _amount;
+            chainBalance[_chainId][_l1Token] = chainBalanceAmount_ - _amount;
        }


437: if (!hyperbridgingEnabled[_chainId]) {
            // Check that the chain has sufficient balance
+    uint256 chainBalanceAmount_ = chainBalance[_chainId][_l1Token] ;
-           require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds
+           require(chainBalanceAmount_ >= amount, "ShB not enough funds 2"); // not enought funds
-            chainBalance[_chainId][l1Token] -= amount;
+            chainBalance[_chainId][_l1Token] = chainBalanceAmount_ - _amount;
        }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L349-L350

##

## [G-3] State variables should be cached with stack variable

The instances below point to the second+ access of a state variable within a function. Caching of a state variable replace each Gwarmaccess (100 gas) with a much cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses. Most of the times this if statement will be true and we will save 100 gas at a small possibility of 3 gas loss ,

### [G-3.1]  Cache ``sharedBridge`` Storage variable to reduce redundant access

sharedBridge variable implies that instead of directly accessing this storage variable multiple times within a single function or transaction (which would repeatedly read from blockchain storage), the value should be read once and stored in a local variable (memory). This local variable is then used for subsequent operations within the function. Saves ``100 GAS`` , ``1 SLOD``

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridgehub
/Bridgehub.sol

/// @notice register new chain
    /// @notice for Eth the baseToken address is 1
    function createNewChain(
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
+   address  sharedBridge_ =  address(sharedBridge) ;    
-  require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
+  require(address(sharedBridge_) != address(0), "Bridgehub: weth bridge not set");
        require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

        stateTransitionManager[_chainId] = _stateTransitionManager;
        baseToken[_chainId] = _baseToken;

        IStateTransitionManager(_stateTransitionManager).createNewChain(
            _chainId,
            _baseToken,
-            address(sharedBridge),
+            sharedBridge_,
            _admin,
            _initData
        );

        emit NewChain(_chainId, _stateTransitionManager, _admin);
        return _chainId;
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130

### [G-3.2] basePubdataSpent should be cached  : Saves ``100 GAS`` , ``1 SLOD``

```diff
FILE: 2024-03-zksync/code/system-contracts/contracts
/SystemContext.sol

function getCurrentPubdataSpent() public view returns (uint256) {
        uint256 pubdataPublished = SystemContractHelper.getZkSyncMeta().pubdataPublished;
        return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L117-L120

##

## [G-4] AddressAliasHelper.undoL1ToL2Alias(msg.sender) function value should be cached 

AddressAliasHelper.undoL1ToL2Alias(msg.sender) is stored in a local variable senderAlias. This approach minimizes the need to repeatedly execute the same external call, thus reducing the gas cost. The require statement then uses senderAlias for its conditions, eliminating the need for a second external function call. Saves ``2000 GAS``

```diff
FILE: 2024-03-zksync/code/contracts/zksync/contracts/bridge
/L2SharedBridge.sol

function finalizeDeposit(
        address _l1Sender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        bytes calldata _data
    ) external payable override {
        // Only the L1 bridge counterpart can initiate and finalize the deposit.

+  address senderAlias = AddressAliasHelper.undoL1ToL2Alias(msg.sender);
-        require(
            AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
                AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
            "mq"
        );
+        require(
            senderAlias  == l1Bridge ||
                senderAlias  == l1LegacyBridge,
            "mq"
        );
        require(msg.value == 0, "Value should be 0 for ERC20 bridge");


```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L79-L92



##

## [G-5] Don't cache the ``_refundRecipient`` its already memory variable 

The reassignment of _refundRecipient to refundRecipient is unnecessary since _refundRecipient is already a memory variable and its value can be used directly within the function. This redundancy does not contribute to efficiency or clarity and could be streamlined for better readability and gas efficiency. Saves ``35 GAS``

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1SharedBridge.sol

577: address refundRecipient = _refundRecipient;
578: if (_refundRecipient == address(0)) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L577



##

## [G-6] Parameter validation prior to storage Validations for better gas efficiency 

Function parameters should be checked before storage variables.

```diff
FILE: 2024-03-zksync/code/contracts/zksync/contracts/bridge
/L2SharedBridge.sol

 ) external payable override {
+        require(msg.value == 0, "Value should be 0 for ERC20 bridge");
        // Only the L1 bridge counterpart can initiate and finalize the deposit.
        require(
            AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
                AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
            "mq"
        );
-        require(msg.value == 0, "Value should be 0 for ERC20 bridge");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92



```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1SharedBridge.sol

 function depositLegacyErc20Bridge(
        address _prevMsgSender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte,
        address _refundRecipient
    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
-        require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
        require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
+        require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L554-L564


##

## [G-7] Don't emit state variables when stack variable available 

Replace s.totalBatchesCommitted with _newLastBatch in the emit statement to use the stack variable instead of the state variable. This adjustment conserves gas as reading from the stack is cheaper than accessing state variables. 

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 s.totalBatchesCommitted = _newLastBatch;

        // Reset the batch number of the executed system contracts upgrade transaction if the batch
        // where the system contracts upgrade was committed is among the reverted batches.
        if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) {
            delete s.l2SystemContractsUpgradeBatchNumber;
        }

-        emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
+        emit BlocksRevert(_newLastBatch, s.totalBatchesVerified, s.totalBatchesExecuted);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496

##

## [G-8] Using storage instead of memory for structs/arrays saves gas

When fetching data from a storage location, assigning the data to a memory variable causes all fields of the struct/array to be read from storage, which incurs a Gcoldsload (2100 gas) for each field of the struct/array. If the fields are read from the new memory variable, they incur an additional MLOAD rather than a cheap stack read. Instead of declearing the variable with the memory keyword, declaring the variable with the storage keyword and caching any fields that need to be re-read in stack variables, will be much cheaper, only incuring the Gcoldsload for the fields actually read. The only time it makes sense to read the whole struct/array into a memory variable, is if the full struct/array is being returned by the function, is being passed to a function that requires memory, or if the array/struct is being read from another memory array/struct.

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition/libraries
/Diamond.sol

140: SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
160: SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
180:  SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L140


##

## [G-9] Consolidating multiple mappings into a single struct mapping for gas Optimization

Saves a storage slot for the mapping. Depending on the circumstances and sizes of types, can avoid a Gsset (20000 gas) per mapping combined. Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Finally, if both fields are accessed in the same function, can save ~42 gas per access due to not having to recalculate the key’s keccak256 hash (Gkeccak256 - 30 gas) and that calculation’s associated stack operations.

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition/chain-deps
/ZkSyncStateTransitionStorage.sol

85: /// @dev Stored hashed StoredBatch for batch number
86:    mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
87:    /// @dev Stored root hashes of L2 -> L1 logs
88:    mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L85-L88


```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1SharedBridge.sol

+ struct BridgeInfo {
+    address l2Bridge; // Address of the bridge proxy
+    bool hyperbridgingEnabled; // Indicates if hyperbridging is enabled for the chain
+ }

+ mapping(uint256 => BridgeInfo) public bridgeInfos;

- 48: mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;

- 60: /// @dev Indicates whether the hyperbridging is enabled for a given chain.
- 61:    mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L48

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridgehub
/Bridgehub.sol

/// @notice chainID => StateTransitionManager contract address, storing StateTransitionManager
    mapping(uint256 _chainId => address) public stateTransitionManager;

    /// @notice chainID => baseToken contract address, storing baseToken
    mapping(uint256 _chainId => address) public baseToken;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L25-L29

##

## [G-10] Consolidating multiple event emissions into a single event : Saves ``375 GAS``

Emitting an event has a fixed gas cost plus a variable cost based on the size of the data emitted. The fixed cost is mainly due to the use of the LOG operation in the Ethereum Virtual Machine (EVM), which is around 375 gas for a LOG operation itself (LOG0, emitting a log with no topics).

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/governance
/Governance.sol

+ event ConfigurationChanged(address indexed oldSecurityCouncil, address indexed newSecurityCouncil, uint oldMinDelay, uint newMinDelay);



  securityCouncil = _securityCouncil;
-        emit ChangeSecurityCouncil(address(0), _securityCouncil);

        minDelay = _minDelay;
-        emit ChangeMinDelay(0, _minDelay);

+  emit ConfigurationChanged(address(0), _securityCouncil, 0, _minDelay);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L46-L50

##

## [G-11] via updating storage while emitting events

Via doing so ``21gas`` can be saved with each emit

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition
/StateTransitionManager.sol

/// @inheritdoc IStateTransitionManager
    function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
-        // Save previous value into the stack to put it into the event later
-        address oldPendingAdmin = pendingAdmin;
-        // Change pending admin
-        pendingAdmin = _newPendingAdmin;
-        emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
+        emit NewPendingAdmin(pendingAdmin , pendingAdmin = _newPendingAdmin);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L109-L116

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

66: /// @inheritdoc IAdmin
    function changeFeeParams(FeeParams calldata _newFeeParams) external onlyAdminOrStateTransitionManager {
        // Double checking that the new fee params are valid, i.e.
        // the maximal pubdata per batch is not less than the maximal pubdata per priority transaction.
        require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");

-        FeeParams memory oldFeeParams = s.feeParams;
-        s.feeParams = _newFeeParams;

-        emit NewFeeParams(oldFeeParams, _newFeeParams);
+        emit NewFeeParams(s.feeParams, s.feeParams = _newFeeParams);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L66-L76

##

## [G-12] Assigning state variables directly with named struct constructors wastes gas

Using named arguments for struct means that the compiler needs to organize the fields in memory before doing the assignment, which wastes gas. Set each field directly in storage (use dot-notation), or use the unnamed version of the constructor. Using named arguments for struct constructors can lead to additional gas costs compared to other methods of struct initialization. This is due to the way the Solidity compiler handles memory and storage, especially with respect to struct assignment. 

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1SharedBridge.sol

430: MessageParams memory messageParams = MessageParams({
            l2BatchNumber: _l2BatchNumber,
            l2MessageIndex: _l2MessageIndex,
            l2TxNumberInBatch: _l2TxNumberInBatch
        });


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
            });

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L430-L434

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition
/StateTransitionManager.sol

182: L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
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
        });

220: Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({
            facetCuts: emptyArray,
            initAddress: genesisUpgrade,
            initCalldata: abi.encodeCall(IDefaultUpgrade.upgrade, (proposedUpgrade))
        });

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L182

##

## [G-13] Consider using alternatives to OpenZeppelin

OpenZeppelin is a great and popular smart contract library, but there are other alternatives that are worth considering. These alternatives offer better gas efficiency and have been tested and recommended by developers.

Two examples of such alternatives are [Solmate](https://github.com/transmissions11/solmate) and [Solady](https://github.com/Vectorized/solady).

Solmate is a library that provides a number of gas-efficient implementations of common smart contract patterns. Solady is another gas-efficient library that places a strong emphasis on using assembly.

```
FILE: package.json

 "@openzeppelin/contracts": "4.9.5",
    "@openzeppelin/contracts-upgradeable": "4.9.5",

```

##

## [G-14] Using assembly to revert with an error message

When reverting in solidity code, it is common practice to use a require or revert statement to revert execution with an error message. This can in most cases be further optimized by using assembly to revert with the error message. Saves around 300 GAS per message 

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1ERC20Bridge.sol

64: require(msg.sender == address(sharedBridge), "Not shared bridge");
66: require(amount == _amount, "Incorrect amount");
141: require(_amount != 0, "0T"); // empty deposit
143: require(amount == _amount, "3T"); // The token has non-standard transfer logic
186: require(amount != 0, "2T"); // empty deposit

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1SharedBridge.sol

69: require(msg.sender == address(bridgehub), "ShB not BH");
75: require(
            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
            "L1SharedBridge: not bridgehub or era chain"
        );
84: require(msg.sender == address(legacyBridge), "ShB not legacy bridge");

108: require(_owner != address(0), "ShB owner 0");
129: require(amount > 0, "ShB: 0 amount to transfer");
132: require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
138: require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");
155: require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69C9-L69C65

##

## [G-15] Invert if-else statements that have a negation

 In theory, the extra ! increases the computational cost. Also should benchmark both methods because the compiler is can sometimes optimize this.

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1SharedBridge.sol

164: if (!hyperbridgingEnabled[_chainId]) {

211: if (!hyperbridgingEnabled[_chainId]) {

347: if (!hyperbridgingEnabled[_chainId]) {

437: if (!hyperbridgingEnabled[_chainId]) {

567: if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L164


```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/governance
/Governance.sol

227: if (!success) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L227


```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition
/ValidatorTimelock.sol

88: if (!validators[_chainId][_validator]) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L88

##

## [G-16] This check ``require(block.timestamp >= commitBatchTimestamp + delay, "5c")`` is redundant when ``commitBatchTimestamp`` is 0 

The optimization introduces a conditional check that evaluates if commitBatchTimestamp is not 0 before executing the require statement. This ensures that the gas-consuming operation of checking block.timestamp >= commitBatchTimestamp + delay is skipped when commitBatchTimestamp is 0, as under this condition, the require statement's condition would always be true. Saves ``50 Gas`` in every iterations.

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition
/ValidatorTimelock.sol

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

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195

##

## [G-17] hashL2Bytecode() can be more gas optimized 

The optimizations reduce EVM opcode execution through calldata access minimization, merge conditional JUMPI operations, consolidate bitwise manipulations into a single execution step, and streamline computational pathways to decrease execution cost and bytecode size. Saves more than ``100 GAS``

```solidity
FILE: 2024-03-zksync/code/system-contracts/contracts/libraries
/Utils.sol

 function hashL2Bytecode(bytes calldata _bytecode) internal view returns (bytes32 hashedBytecode) {
        // Note that the length of the bytecode must be provided in 32-byte words.
        require(_bytecode.length % 32 == 0, "po");

        uint256 lengthInWords = _bytecode.length / 32;
        require(lengthInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words
        require(lengthInWords % 2 == 1, "pr"); // bytecode length in words must be odd
        hashedBytecode =
            EfficientCall.sha(_bytecode) &
            0x00000000FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF;
        // Setting the version of the hash
        hashedBytecode = (hashedBytecode | bytes32(uint256(1 << 248)));
        // Setting the length
        hashedBytecode = hashedBytecode | bytes32(lengthInWords << 224);
    }



```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L82-L96

### Optimized Code

```solidity

function hashL2Bytecode(bytes calldata _bytecode) internal view returns (bytes32 hashedBytecode) {
    uint256 length = _bytecode.length;
    require(length % 32 == 0, "po");

    uint256 lengthInWords = length / 32;
    // Combine conditions to reduce the number of require statements
    require(lengthInWords < 2 ** 16 && lengthInWords % 2 == 1, "Bytecode format invalid");

    hashedBytecode = EfficientCall.sha(_bytecode) &
        0x00000000FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF;

    // Combine bitwise operations into a single operation to optimize gas
    hashedBytecode |= bytes32(uint256(1) << 248) | bytes32(lengthInWords << 224);
}

```

##

## [G-18] Skip the shifting process by optimizing ``extractNumberFromMeta() ``

Direct Extraction: The optimized version skips the two-step shifting process. Instead, it directly shifts the meta right by offset bits to position the desired number at the right end of the uint256.

Masking: It then applies a bitmask to isolate the size bits of interest. The mask is created with (1 << size) - 1, which generates a uint256 where the rightmost size bits are 1 and the rest are 0. This efficiently masks out any bits beyond the size of interest.

### Original Code

```solidity
FILE: 2024-03-zksync/code/system-contracts/contracts/libraries
/SystemContractHelper.sol

function extractNumberFromMeta(uint256 meta, uint256 offset, uint256 size) internal pure returns (uint256 result) {
        // Firstly, we delete all the bits after the field
        uint256 shifted = (meta << (256 - size - offset));
        // Then we shift everything back
        result = (shifted >> (256 - size));
    }

```

### Optimized Version

```solidity

function extractNumberFromMeta(uint256 meta, uint256 offset, uint256 size) internal pure returns (uint256) {
    return (meta >> offset) & ((1 << size) - 1);
}

```

##

## [G-19] Don't cache state variable only used once

``dataHash`` is read from ``depositHappened[_chainId][_l2TxHash]`` and used exactly once in the require statement. This usage adheres to the principle as it does not unnecessarily cache the state variable into a local variable for multiple uses; instead, it uses the value directly where needed. Similarly, txDataHash is computed and used immediately, aligning with the principle as it's not caching but direct usage. 

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1SharedBridge.sol

 if (notCheckedInLegacyBridgeOrWeCanCheckDeposit) {
-                bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
-                bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));
-                require(dataHash == txDataHash, "ShB: d.it not hap");
+                require(depositHappened[_chainId][_l2TxHash] == keccak256(abi.encode(_depositSender, _l1Token, _amount)), "ShB: d.it not hap");
                delete depositHappened[_chainId][_l2TxHash];
            }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L339-L344


##

## [G-20] Avoid updating storage when the value hasn't changed

If the old value is equal to the new value, not re-storing the value will avoid a Gsreset (2900 gas), potentially at the expense of a Gcoldsload (2100 gas) or a Gwarmaccess (100 gas)

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

/// @inheritdoc IAdmin
    function setValidator(address _validator, bool _active) external onlyStateTransitionManager {
        s.validators[_validator] = _active;
        emit ValidatorStatusUpdate(_validator, _active);
    }

    /// @inheritdoc IAdmin
    function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {
        // Change the porter availability
        s.zkPorterIsAvailable = _zkPorterIsAvailable;
        emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L44-L55


##

## [G-21] ``_l2BlockNumber - 1`` Subtraction results should be cached 

The subtraction in second time is redundant 

```solidity
FILE: 2024-03-zksync/code/system-contracts/contracts
/SystemContext.sol

unchecked {
            bytes32 correctPrevBlockHash = _calculateLegacyL2BlockHash(_l2BlockNumber - 1);
            require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");

            // Whenever we'll be queried about the hashes of the blocks before the upgrade,
            // we'll use batches' hashes, so we don't need to store 256 previous hashes.
            // However, we do need to store the last previous hash in order to be able to correctly calculate the
            // hash of the new L2 block.
            _setL2BlockHash(_l2BlockNumber - 1, correctPrevBlockHash);
        }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L255

## 

## [G-22] ``dictionary.length`` and ``encodedData.length``  length should be cached

Instead of calculating length every time caching length reusing is more gas efficient 

```solidity
FILE: 2024-03-zksync/code/system-contracts/contracts
/Compressor.sol

 require(
                dictionary.length / 8 <= encodedData.length / 2,
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



```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L56-L69

##

## [G-23] Optimizing Uint32 Storage Updates by Eliminating XOR Misuse

Correct Value Setting: The approach uses a mask to clear the specific uint32 area within the storage slot before setting the new value. This method is more straightforward and efficient than using XOR for this purpose.
Clear and Set: It first creates a mask with all bits set to 1 except the bits corresponding to the target uint32 value, which are cleared (0). Then, it applies this mask to the original slot value to clear the old uint32 value. Finally, it uses the bitwise OR operation to set the new uint32 value in its correct position.
Mask Construction: The clearMask is constructed to have 0 bits in the position of the target uint32 and 1 bits elsewhere. This ensures only the target uint32 is affected when the mask is applied.

### Original Code

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition/libraries
/LibMap.sol

/// @dev Updates the uint32 value at `_index` in `map`.
    /// @param _map The Uint32Map instance containing the packed uint32 values.
    /// @param _index The index of the uint32 value to set.
    /// @param _value The new value at the specified index.
    function set(Uint32Map storage _map, uint256 _index, uint32 _value) internal {
        unchecked {
            // Each storage slot can store 256 bits of data.
            // As uint32 is 32 bits long, 8 uint32s can be packed into one storage slot.
            // Hence, `_index / 8` is done to find the storage slot that contains the required uint32.
            uint256 mapIndex = _index / 8;
            uint256 mapValue = _map.map[mapIndex];

            // First three bits of the original `_index` denotes the position of the uint32 in that slot.
            // So, '(_index & 7) * 32' is done to find the bit position of the uint32 in that storage slot.
            uint256 bitOffset = (_index & 7) * 32;

            // XORing a value A with B, and then with A again, gives the original value B.
            // We will use this property to update the uint32 value in the slot.

            // Shift the bits to the right and retrieve the uint32 value.
            uint32 oldValue = uint32(mapValue >> bitOffset);

            // Calculate the XOR of the new value and the existing value.
            uint256 newValueXorOldValue = uint256(oldValue ^ _value);

            // Finally, we XOR the slot with the XOR of the new value and the existing value,
            // shifted to its proper position. The XOR operation will effectively replace the old value with the new value.
            _map.map[mapIndex] = (newValueXorOldValue << bitOffset) ^ mapValue;
        }

```

### Optimized Code

```solidity

function set(Uint32Map storage _map, uint256 _index, uint32 _value) internal {
    unchecked {
        uint256 mapIndex = _index / 8; // Determine the storage slot index.
        uint256 mapValue = _map.map[mapIndex]; // Fetch the current storage slot value.

        uint256 bitOffset = (_index & 7) * 32; // Calculate the bit position of the target uint32 within the slot.

        // Clear the target uint32 value in the slot by applying a mask, then set the new value.
        uint256 clearMask = ~(uint256(0xFFFFFFFF) << bitOffset);
        _map.map[mapIndex] = (mapValue & clearMask) | (uint256(_value) << bitOffset);
    }
}

``` 














