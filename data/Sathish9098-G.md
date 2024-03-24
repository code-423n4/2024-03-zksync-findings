# GAS OPTIMIZATIONS

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



### [G-1.1] ``securityCouncil`` and ``minDelay`` can be packed same Slot 

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

## [G-1.2] ``genesisUpgrade`` and ``protocolVersion`` can be packed with same slot 

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

### ``chainId`` and ``origin`` can be packed same slot : Saves 2000 GAS 

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

## [G-1] l2BridgeAddress[_chainId] , l2BridgeAddress[ERA_CHAIN_ID] , ``chainBalance[_chainId][_l1Token]``  mappings can be cached 

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

address l2BridgeAddress_ = l2BridgeAddress[_chainId] ; 
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

## [G-1] State variables should be cached with stack variable

The instances below point to the second+ access of a state variable within a function. Caching of a state variable replace each Gwarmaccess (100 gas) with a much cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses. Most of the times this if statement will be true and we will save 100 gas at a small possibility of 3 gas loss ,

### [G-]  Cache ``sharedBridge`` Storage variable to reduce redundant access

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

### [G-] basePubdataSpent should be cached  : Saves ``100 GAS`` , ``1 SLOD``

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

## [G-] Don't cache state variable only used once

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

## [G-] Parameter validation prior to storage Validations for better gas efficiency 

Function parameters should be checked before storage variables

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



## [G-] Avoid updating storage when the value hasn't changed

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

## [G-] Don't emit state variables when stack variable available 

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

## [G-] Using storage instead of memory for structs/arrays saves gas

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

## [G-] Don't declare the variables inside the loop

The variables selector and oldFacet are declared outside of the for-loop to avoid redundant declarations on each iteration. This optimization reduces the cost associated with variable declaration and memory allocation during the loop execution.

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/state-transition/libraries
/Diamond.sol

137: uint256 selectorsLength = _selectors.length;
        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
            bytes4 selector = _selectors[i];
            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
            require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists

            _addOneFunction(_facet, selector, _isFacetFreezable);
        }

158: for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
            bytes4 selector = _selectors[i];
            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
            require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address


178:  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
            bytes4 selector = _selectors[i];
            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
            require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet


```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L137-L144

##

## [G-] Optimizing gas consumption by utilizing ``calldata`` for read-Only external function parameters

calldata must be used when declaring an external function's dynamic parameters

When a function with a memory array is called externally, the abi.decode ()  step has to use a for-loop to copy each index of the calldata to the memory index. Each iteration of this for-loop costs at least 60 gas (i.e. 60 * <mem_array>.length). Using calldata directly, obliviates the need for such a loop in the contract code and runtime execution. 

```solidity

```

##

## [G-] Consolidating multiple mappings into a single struct mapping for gas Optimization

Saves a storage slot for the mapping. Depending on the circumstances and sizes of types, can avoid a Gsset (20000 gas) per mapping combined. Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Finally, if both fields are accessed in the same function, can save ~42 gas per access due to not having to recalculate the key’s keccak256 hash (Gkeccak256 - 30 gas) and that calculation’s associated stack operations.


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

## [G-] Consolidating multiple event emissions into a single event : Saves ``375 GAS``

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

[G-] The result of function calls should be cached rather than re-calling the function 

The instances below point to the second+ call of the function within a single function




