
# Gas Optimization Of Zksync Era Contest

# SUMMARY
|      |  issue  |  instance  |
|------|---------|------------|
|[G‑01]|Use calldata instead of memory for function arguments that do not get mutated|17|
|[G‑02]|Using storage instead of `memory` for structs/arrays saves gas|15|
|[G‑03]|State variables that are used multiple times in a function should be cached in stack variables|4|
|[G‑04]|Multiple address/ID mappings can be combined into a single mapping of an address/ID to a struct, where appropriate|8|
|[G‑05]|Use inline assembly to check for address(0)|50|
|[G‑06]|Structs can be packed into fewer storage slots|4|
|[G‑07]|Constructors can be marked payable|10|
|[G‑08]|State variable read in a loop|5|
|[G‑09]|Consider using OZ EnumerateSet in place of nested mappings|8|
|[G‑10]|Multiple accesses of a mapping/array should use a local variable cache|40|
|[G‑11]|Internal functions only called once can be inlined to save gas|53|
|[G‑12]|Use assembly to write address storage values|13|
|[G‑13]|Use assembly to calculate hashes to save gas|59|
|[G‑14]|REQUIRE()/REVERT() STRINGS LONGER THAN 32 BYTES COST EXTRA GAS|66|
|[G‑15]|Sort Solidity operations using short-circuit mode|2|
|[G‑16]|Avoid emitting storage values|12|
|[G‑17]|Can Make The Variable Outside The Loop To Save Gas|20|
|[G‑18]|A modifier used only once and not being inherited should be inlined to save gas|7|
|[G‑19]|Refactor external/internal function to avoid unnecessary External Calls|3|
|[G‑20]|Avoid updating storage when the value hasn't changed|31|
|[G‑21]|Use assembly to emit an event|77|
|[G‑22]|Do-While loops are cheaper than for loops|6|
|[G‑23]|Initializers can be marked payable|8|
|[G‑24]|require() or revert() statements that check input arguments should be at the top of the function|6|
|[G‑25]|Use nested if statements instead of &&|10|
|[G‑26]|Amounts should be checked for 0 before calling a transfer|3|
|[G‑27]|abi.encode() is less efficient than abi.encodePacked()|17|
|[G‑28]|Do not calculate constants|2|
|[G‑29]|Delete variables that you don't need|2|
|[G‑30]|Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead|20|
|[G‑31]|Storage Slot Reduction via Variable Resizing|2|
|[G‑32]|Avoid fetching a low-level call's return data by using assembly|3|
|[G‑33]|Use hardcode address instead address(this)|5|
|[G‑34]|Duplicated `require()`/`revert()` checks should be refactored to a modifier or function|3|
|[G‑35]|Unused named return variables without optimizer waste gas|4|
|[G‑36]|Stack variable used as a cheaper cache for a state variable is only used once|13|
|[G‑37]|Use of emit inside a loop|3|
|[G‑38]|Structs should group like types together to save gas|11|
|[G‑39]|Don't compare boolean expressions to boolean literals|1|
|[G‑40]|Use selfbalance() instead of address(this).balance|4|
|[G‑41]|Use assembly in place of abi.decode to extract calldata values more efficiently|10|
|[G‑42]|"" has the same value as new bytes(0) but costs less gas|8|
|[G‑43]|State variables only set in their definitions should be declared constant|3|
|[G‑44]|Fewer storage slots can be used by storing timestamps in types smaller than uint256|3|
|[G‑45]|Storage re-read via storage pointer|2|
|[G‑46]|`keccak256()` should only need to be called on a specific string literal once|4|
|[G‑47]|Private functions used once can be inlined|6|
|[G‑48]|>=/<= costs less gas than >/<|3|
|[G‑49]|Assigning state variables directly with named struct constructors wastes gas|1|
|[G‑50]|Most important: avoid zero to one storage writes where possible|2|
|[G‑51]|Instead of counting down in for statements, count up|~|



## [G-01] Use calldata instead of memory for function arguments that do not get mutated
Mark data types as `calldata` instead of `memory` where possible. This makes it so that the data is not automatically loaded into memory. If the data passed into the function does not need to be changed (like updating values in an array), it can be passed in as `calldata`. The one exception to this is if the argument must later be passed into another function that takes an argument that specifies `memory` storage.

🔴 Affected code:
There are 17 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol
168             L2Log memory _log,
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L168:168

```solidity
File: contracts/ethereum/contracts/bridgehub/IBridgehub.sol
85    L2Log memory _log,
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L85:85

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
200             StoredBatchInfo memory _lastCommittedBatchData,

209             StoredBatchInfo memory _lastCommittedBatchData,
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L209:209

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
67              L2Log memory _log,

57              L2Message memory _message,

48              BridgehubL2TransactionRequest memory _request
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L48:48

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol
34              L2Log memory _log,
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L34:34

```solidity
File: contracts/zksync/contracts/L2ContractHelper.sol
65          function withdrawWithMessage(address _l1Receiver, bytes memory _additionalData) external payable;

22          function sendToL1(bytes memory _message) external returns (bytes32);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L22:22

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol
114             string memory _newSymbol,

178         function decodeString(bytes memory _input) external pure returns (string memory result) {

183         function decodeUint8(bytes memory _input) external pure returns (uint8 result) {

50          function bridgeInitialize(address _l1Address, bytes memory _data) external initializer {

113             string memory _newName,
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L113:113

```solidity
File: system-contracts/contracts/L2BaseToken.sol
85          function withdrawWithMessage(address _l1Receiver, bytes memory _additionalData) external payable override {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L85:85

```solidity
File: system-contracts/contracts/interfaces/IL1Messenger.sol
49          function sendToL1(bytes memory _message) external returns (bytes32);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IL1Messenger.sol#L49:49


## [G-02] Using storage instead of `memory` for structs/arrays saves gas
When fetching data from a storage location, assigning the data to a memory variable causes all fields of the struct/array to be read from storage, which incurs a Gcoldsload (2100 gas) for each field of the struct/array. If the fields are read from the new memory variable, they incur an additional MLOAD rather than a cheap stack read. Instead of declearing the variable with the memory keyword, declaring the variable with the storage keyword and caching any fields that need to be re-read in stack variables, will be much cheaper, only incuring the Gcoldsload for the fields actually read. The only time it makes sense to read the whole struct/array into a memory variable, is if the full struct/array is being returned by the function, is being passed to a function that requires memory, or if the array/struct is being read from another memory array/struct


🔴 Affected code:
There are 15 instances of this issue:

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol
27              Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L27:27

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol
72              FeeParams memory oldFeeParams = s.feeParams;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L72:72

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
396             VerifierParams memory verifierParams = s.verifierParams;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L396:396

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol
210                 Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L210:210

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
157             FeeParams memory feeParams = s.feeParams;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L157:157

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
140                 SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

160                 SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

180                 SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L180:180

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
155             VerifierParams memory oldVerifierParams = s.verifierParams;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L155:155

```solidity
File: system-contracts/contracts/ContractDeployer.sol
41              AccountInfo memory info = accountInfo[_address];

75              AccountInfo memory currentInfo = accountInfo[msg.sender];
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L75:75

```solidity
File: system-contracts/contracts/SystemContext.sol
135             VirtualBlockUpgradeInfo memory currentVirtualBlockUpgradeInfo = virtualBlockUpgradeInfo;

173             BlockInfo memory batchInfo = currentBatchInfo;

181             BlockInfo memory blockInfo = currentL2BlockInfo;

275             BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L275:275


## [G-03] State variables that are used multiple times in a function should be cached in stack variables

🔴 Affected code:
There are 4 instances of this issue:

### Cache State variables in bridgehubDeposit Function

**Original Code**
```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol
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
        require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

        require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

        stateTransitionManager[_chainId] = _stateTransitionManager;
        baseToken[_chainId] = _baseToken;

        IStateTransitionManager(_stateTransitionManager).createNewChain(
            _chainId,
            _baseToken,
            address(sharedBridge),
            _admin,
            _initData
        );

        emit NewChain(_chainId, _stateTransitionManager, _admin);
        return _chainId;
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114-L148

**Description:**
In the `createNewChain` function of `Bridgehub`, the multiple accesses to `sharedBridge` State variable are optimized by caching the State variable to local variable to avoid redundant lookups, thus saving gas.

**Optimized Code**
```diff
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
+       IL1SharedBridge _sharedBridge = sharedBridge;
        require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");
-       require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
+       require(address(_sharedBridge) != address(0), "Bridgehub: weth bridge not set");

        require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

        stateTransitionManager[_chainId] = _stateTransitionManager;
        baseToken[_chainId] = _baseToken;

        IStateTransitionManager(_stateTransitionManager).createNewChain(
            _chainId,
            _baseToken,
-           address(sharedBridge),
+           address(_sharedBridge),
            _admin,
            _initData
        );

        emit NewChain(_chainId, _stateTransitionManager, _admin);
        return _chainId;
    }

```



### Cache State variables in _setChainIdUpgrade Function

**Original Code**
```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
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
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177-L228

**Description:**
In the `_setChainIdUpgrade` function of `StateTransitionManager`, the multiple accesses to `protocolVersion` State variable are optimized by caching the State variable to local variable to avoid redundant lookups, thus saving gas.

**Optimized Code**
```diff
function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
        bytes memory systemContextCalldata = abi.encodeCall(ISystemContext.setChainId, (_chainId));
        uint256[] memory uintEmptyArray;
        bytes[] memory bytesEmptyArray;
+       uint256 _protocolVersion = protocolVersion;
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
-           nonce: protocolVersion,
+           nonce: _protocolVersion,
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
-           newProtocolVersion: protocolVersion
+           newProtocolVersion: _protocolVersion
        });

        Diamond.FacetCut[] memory emptyArray;
        Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({
            facetCuts: emptyArray,
            initAddress: genesisUpgrade,
            initCalldata: abi.encodeCall(IDefaultUpgrade.upgrade, (proposedUpgrade))
        });

        IAdmin(_chainContract).executeUpgrade(cutData);
-       emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
+       emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, _protocolVersion);
    }
```


### Cache State variables in getCurrentPubdataSpent Function
**Original Code**
```solidity
File: system-contracts/contracts/SystemContext.sol
    function getCurrentPubdataSpent() public view returns (uint256) {
        uint256 pubdataPublished = SystemContractHelper.getZkSyncMeta().pubdataPublished;
        return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L117-L120

**Description:**
In the `getCurrentPubdataSpent` function of `SystemContext`, the multiple accesses to `basePubdataSpent` State variable are optimized by caching the State variable to local variable to avoid redundant lookups, thus saving gas.

**Optimized Code**
```diff
    function getCurrentPubdataSpent() public view returns (uint256) {
        uint256 _basePubdataSpent = basePubdataSpent;
        uint256 pubdataPublished = SystemContractHelper.getZkSyncMeta().pubdataPublished;
-       return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;
+       return pubdataPublished > _basePubdataSpent ? pubdataPublished - _basePubdataSpent : 0;
    }
```

```solidity
File: system-contracts/contracts/SystemContext.sol
275             BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;

277             if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L277:277


```diff
    function _setVirtualBlock(
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

-       if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
+       if (virtualBlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {    

```


## [G-04] Multiple address/ID mappings can be combined into a single mapping of an address/ID to a struct, where appropriate
Saves a storage slot for the mapping. Depending on the circumstances and sizes of types, can avoid a Gsset (20000 gas) per mapping combined. Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Finally, if both fields are accessed in the same function, can save ~42 gas per access due to not having to recalculate the key's keccak256 hash (Gkeccak256 - 30 gas) and that calculation's associated stack operations.

🔴 Affected code:
There are 8 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol
32          mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))

45          mapping(address => uint256) private __DEPRECATED_lastWithdrawalLimitReset;
46      
47          /// @dev Deprecated storage variable related to withdrawal limitations.
48          mapping(address => uint256) private __DEPRECATED_withdrawnAmountInWindow;
49      
50          /// @dev Deprecated storage variable related to deposit limitations.
51          mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L45:51

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
48          mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;
49      
50          /// @dev A mapping chainId => L2 deposit transaction hash => keccak256(abi.encode(account, tokenAddress, amount))
51          /// @dev Tracks deposit transactions from L2 to enable users to claim their funds if a deposit fails.
52          mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))

57          mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
58              public isWithdrawalFinalized;
59      
60          /// @dev Indicates whether the hyperbridging is enabled for a given chain.
61          mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;
62      
63          /// @dev Maps token balances for each chain to prevent unauthorized spending across hyperchains.
64          /// This serves as a security measure until hyperbridging is implemented.
65          mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57:65

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol
21    mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;
22    /// @notice we store registered tokens (for arbitrary base token)
23    mapping(address _token => bool) public tokenIsRegistered;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21-L23

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol
26          mapping(uint256 _chainId => address) public stateTransitionManager;
27      
28          /// @notice chainID => baseToken contract address, storing baseToken
29          mapping(uint256 _chainId => address) public baseToken;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L26:29

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
30          mapping(uint256 => address) public stateTransition;
31      
32          /// @dev Batch hash zero, calculated at initialization
33          bytes32 public storedBatchZero;
34      
35          /// @dev Stored cutData for diamond cut
36          bytes32 public initialCutHash;
37      
38          /// @dev genesisUpgrade contract address, used to setChainId
39          address public genesisUpgrade;
40      
41          /// @dev current protocolVersion
42          uint256 public protocolVersion;
43      
44          /// @dev validatorTimelock contract address, used to setChainId
45          address public validatorTimelock;
46      
47          /// @dev Stored cutData for upgrade diamond cut. protocolVersion => cutHash
48          mapping(uint256 => bytes32) public upgradeCutHash;
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L30:48

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
47          mapping(uint256 => LibMap.Uint32Map) internal committedBatchTimestamp;
48      
49          /// @dev The address that can commit/revert/validate/execute batches.
50          mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L47:50

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol
86          mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
87          /// @dev Stored root hashes of L2 -> L1 logs
88          mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;

114         mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L86:114


```solidity
File: system-contracts/contracts/NonceHolder.sol
36          mapping(uint256 account => uint256 packedMinAndDeploymentNonce) internal rawNonces;
37      
38          /// Mapping of values under nonces for accounts.
39          /// The main key of the mapping is the 256-bit address of the account, while the
40          /// inner mapping is a mapping from a nonce to the value stored there.
41          mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L36:41



## [G-05] Use inline assembly to check for address(0)
Writing contracts in inline assembly is generally considered gas optimized. we can manipulate memory directly and use fewer opcodes instead of leaving it to the Solidity compiler.
Authentication mechanism is one example where using inline assembly is good, like implementing address zero check.

Here’s an example below:
```js
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

🔴 Affected code:
There are 50 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
108             require(_owner != address(0), "ShB owner 0");

188             require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

563             require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

578                 if (_refundRecipient == address(0)) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L578:578

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol
130             require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

132             require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

326             if (_refundRecipient == address(0)) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L326:326

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol
41              require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L41:41

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol
42              require(_admin != address(0), "Admin should be non zero address");

240             require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L240:240

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
82              require(_initializeData.governor != address(0), "StateTransition: governor zero");

246             if (stateTransition[_chainId] != address(0)) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L246:246

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol
25              require(address(_initializeData.verifier) != address(0), "vt");

26              require(_initializeData.admin != address(0), "vy");

27              require(_initializeData.validatorTimelock != address(0), "hc");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27:27

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol
30              require(facetAddress != address(0), "F"); // Proxy has no facet for this selector
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30:30

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
191             if (_expectedSystemContractUpgradeTxHash == bytes32(0)) {

237             if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {

639                 require(blobVersionedHash != bytes32(0), "vh");

663             require(versionedHash == bytes32(0), "lh");

669                     (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||

669                     (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||

670                         (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),

670                         (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670:670

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol
183             require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183:183

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
275             address refundRecipient = _params.refundRecipient == address(0) ? _params.sender : _params.refundRecipient;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L275:275

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
141                 require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists

161                 require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

175             require(_facet == address(0), "a1"); // facet address must be zero

181                 require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet

279             if (_init == address(0)) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L279:279

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
93              if (_l2DefaultAccountBytecodeHash == bytes32(0)) {

110             if (_l2BootloaderBytecodeHash == bytes32(0)) {

148                 _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) &&

149                 _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) &&

150                 _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)

249             require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L249:249

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol
33              require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33:33

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol
55              require(_l1Bridge != address(0), "bf");

56              require(_l2TokenProxyBytecodeHash != bytes32(0), "df");

57              require(_aliasedOwner != address(0), "sf");

58              require(_l2TokenProxyBytecodeHash != bytes32(0), "df");

68                  require(_l1LegecyBridge != address(0), "bf2");

96              if (currentL1Token == address(0)) {

129             require(l1Token != address(0), "yh");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L129:129

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol
51              require(_l1Address != address(0), "in6"); // Should be non-zero address
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51:51

```solidity
File: system-contracts/contracts/DefaultAccount.sol
94              bytes32 txHash = _suggestedSignedHash != bytes32(0) ? _suggestedSignedHash : _transaction.encodeHash();

188             return recoveredAddress == address(this) && recoveredAddress != address(0);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L188:188

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol
76              require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L76:76

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol
406             if (address(uint160(_transaction.paymaster)) != address(0)) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L406:406




## [G-06] Structs can be packed into fewer storage slots
Each slot saved can avoid an extra Gsset (20000 gas) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings

🔴 Affected code:
There are 4 instances of this issue:

```solidity
File: contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol
15      struct StateTransitionManagerInitializeData {
16          address governor;
17          address validatorTimelock;
18          address genesisUpgrade;
19          bytes32 genesisBatchHash;
20          uint64 genesisIndexRepeatedStorageChanges;
21          bytes32 genesisBatchCommitment;
22          Diamond.DiamondCutData diamondCut;
23          uint256 protocolVersion;
24      }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L15:24

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol
66      struct ZkSyncStateTransitionStorage {
67          /// @dev Storage of variables needed for deprecated diamond cut facet
68          uint256[7] __DEPRECATED_diamondCutStorage;
69          /// @notice Address which will exercise critical changes to the Diamond Proxy (upgrades, freezing & unfreezing). Replaced by STM
70          address __DEPRECATED_governor;
71          /// @notice Address that the governor proposed as one that will replace it
72          address __DEPRECATED_pendingGovernor;
73          /// @notice List of permitted validators
74          mapping(address validatorAddress => bool isValidator) validators;
75          /// @dev Verifier contract. Used to verify aggregated proof for batches
76          IVerifier verifier;
77          /// @notice Total number of executed batches i.e. batches[totalBatchesExecuted] points at the latest executed batch
78          /// (batch 0 is genesis)
79          uint256 totalBatchesExecuted;
80          /// @notice Total number of proved batches i.e. batches[totalBatchesProved] points at the latest proved batch
81          uint256 totalBatchesVerified;
82          /// @notice Total number of committed batches i.e. batches[totalBatchesCommitted] points at the latest committed
83          /// batch
84          uint256 totalBatchesCommitted;
85          /// @dev Stored hashed StoredBatch for batch number
86          mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
87          /// @dev Stored root hashes of L2 -> L1 logs
88          mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;
89          /// @dev Container that stores transactions requested from L1
90          PriorityQueue.Queue priorityQueue;
91          /// @dev The smart contract that manages the list with permission to call contract functions
92          address __DEPRECATED_allowList;
93          /// @notice Part of the configuration parameters of ZKP circuits. Used as an input for the verifier smart contract
94          VerifierParams verifierParams;
95          /// @notice Bytecode hash of bootloader program.
96          /// @dev Used as an input to zkp-circuit.
97          bytes32 l2BootloaderBytecodeHash;
98          /// @notice Bytecode hash of default account (bytecode for EOA).
99          /// @dev Used as an input to zkp-circuit.
100         bytes32 l2DefaultAccountBytecodeHash;
101         /// @dev Indicates that the porter may be touched on L2 transactions.
102         /// @dev Used as an input to zkp-circuit.
103         bool zkPorterIsAvailable;
104         /// @dev The maximum number of the L2 gas that a user can request for L1 -> L2 transactions
105         /// @dev This is the maximum number of L2 gas that is available for the "body" of the transaction, i.e.
106         /// without overhead for proving the batch.
107         uint256 priorityTxMaxGasLimit;
108         /// @dev Storage of variables needed for upgrade facet
109         UpgradeStorage __DEPRECATED_upgrades;
110         /// @dev A mapping L2 batch number => message number => flag.
111         /// @dev The L2 -> L1 log is sent for every withdrawal, so this mapping is serving as
112         /// a flag to indicate that the message was already processed.
113         /// @dev Used to indicate that eth withdrawal was already processed
114         mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;
115         /// @dev The most recent withdrawal time and amount reset
116         uint256 __DEPRECATED_lastWithdrawalLimitReset;
117         /// @dev The accumulated withdrawn amount during the withdrawal limit window
118         uint256 __DEPRECATED_withdrawnAmountInWindow;
119         /// @dev A mapping user address => the total deposited amount by the user
120         mapping(address => uint256) __DEPRECATED_totalDepositedAmountPerUser;
121         /// @dev Stores the protocol version. Note, that the protocol version may not only encompass changes to the
122         /// smart contracts, but also to the node behavior.
123         uint256 protocolVersion;
124         /// @dev Hash of the system contract upgrade transaction. If 0, then no upgrade transaction needs to be done.
125         bytes32 l2SystemContractsUpgradeTxHash;
126         /// @dev Batch number where the upgrade transaction has happened. If 0, then no upgrade transaction has happened
127         /// yet.
128         uint256 l2SystemContractsUpgradeBatchNumber;
129         /// @dev Address which will exercise non-critical changes to the Diamond Proxy (changing validator set & unfreezing)
130         address admin;
131         /// @notice Address that the admin proposed as one that will replace admin role
132         address pendingAdmin;
133         /// @dev Fee params used to derive gasPrice for the L1->L2 transactions. For L2 transactions,
134         /// the bootloader gives enough freedom to the operator.
135         FeeParams feeParams;
136         /// @dev Address of the blob versioned hash getter smart contract used for EIP-4844 versioned hashes.
137         address blobVersionedHashRetriever;
138         /// new fields
139         /// @dev The chainId of the chain
140         uint256 chainId;
141         /// @dev The address of the bridgehub
142         address bridgehub;
143         /// @dev The address of the StateTransitionManager
144         address stateTransitionManager;
145         /// @dev The address of the baseToken contract. Eth is address(1)
146         address baseToken;
147         /// @dev The address of the baseTokenbridge. Eth also uses the shared bridge
148         address baseTokenBridge;
149         /// @notice gasPriceMultiplier for each baseToken, so that each L1->L2 transaction pays for its transaction on the destination
150         /// we multiply by the nominator, and divide by the denominator
151         uint128 baseTokenGasPriceMultiplierNominator;
152         uint128 baseTokenGasPriceMultiplierDenominator;
153     }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L66:153

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol
83          struct StoredBatchInfo {
84              uint64 batchNumber;
85              bytes32 batchHash;
86              uint64 indexRepeatedStorageChanges;
87              uint256 numberOfLayer1Txs;
88              bytes32 priorityOperationsHash;
89              bytes32 l2LogsTreeRoot;
90              uint256 timestamp;
91              bytes32 commitment;
92          }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L83:92

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
62          struct FacetCut {
63              address facet;
64              Action action;
65              bool isFreezable;
66              bytes4[] selectors;
67          }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L62:67



## [G-07] Constructors can be marked payable
Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided. A constructor can safely be marked as payable, since only the deployer would be able to pass funds, and the project itself would not pass any funds.


🔴 Affected code:
There are 10 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol
55          constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
56              sharedBridge = _sharedBridge;
57          }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55:57

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
90          constructor(
91              address _l1WethAddress,
92              IBridgehub _bridgehub,
93              IL1ERC20Bridge _legacyBridge
94          ) reentrancyGuardInitializer {
95              _disableInitializers();
96              l1WethAddress = _l1WethAddress;
97              bridgehub = _bridgehub;
98              legacyBridge = _legacyBridge;
99          }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90:99

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol
38          constructor() reentrancyGuardInitializer {}
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38:38

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol
41          constructor(address _admin, address _securityCouncil, uint256 _minDelay) {
42              require(_admin != address(0), "Admin should be non zero address");
43      
44              _transferOwnership(_admin);
45      
46              securityCouncil = _securityCouncil;
47              emit ChangeSecurityCouncil(address(0), _securityCouncil);
48      
49              minDelay = _minDelay;
50              emit ChangeMinDelay(0, _minDelay);
51          }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L41:51

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
58          constructor(address _bridgehub) reentrancyGuardInitializer {
59              bridgehub = _bridgehub;
60          }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58:60

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
55          constructor(address _initialOwner, uint32 _executionDelay) {
56              _transferOwnership(_initialOwner);
57              executionDelay = _executionDelay;
58          }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55:58

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol
19          constructor() reentrancyGuardInitializer {}
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19:19

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol
11          constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
12              // Check that the contract is deployed on the expected chain.
13              // Thus, the contract deployed by the same Create2 factory on the different chain will have different addresses!
14              require(_chainId == block.chainid, "pr");
15              Diamond.diamondCut(_diamondCut);
16          }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11:16

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol
41          constructor() {
42              _disableInitializers();
43          }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L41:43

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol
40          constructor() {
41              // Disable initialization to prevent Parity hack.
42              _disableInitializers();
43          }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L40:43



## [G-08] State variable read in a loop

The state variable should be cached in and read from a local variable, or accumulated in a local variable then written to storage once outside of the loop, rather than reading/updating it on every iteration of the loop, which will replace each Gwarmaccess (100 gas) with a much cheaper stack read.

🔴 Affected code:
There are 5 instances of this issue:

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
117                     committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);

136                     committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);

186                     uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(

210                     uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L210:210

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol
41       immutableDataStorage[uint256(uint160(_dest))][index] = value;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L41:41


## [G-09] Consider using OZ EnumerateSet in place of nested mappings             
Nested mappings and multi-dimensional arrays in Solidity operate through a process of double hashing, wherein the original storage slot and the first key are concatenated and hashed, and then this hash is again concatenated with the second key and hashed. This process can be quite gas expensive due to the double-hashing operation and subsequent storage operation (sstore).
A possible optimization involves manually concatenating the keys followed by a single hash operation and an sstore. However, this technique introduces the risk of storage collision, especially when there are other nested hash maps in the contract that use the same key types. Because Solidity is unaware of the number and structure of nested hash maps in a contract, it follows a conservative approach in computing the storage slot to avoid possible collisions.
OpenZeppelin's EnumerableSet provides a potential solution to this problem. It creates a data structure that combines the benefits of set operations with the ability to enumerate stored elements, which is not natively available in Solidity. EnumerableSet handles the element uniqueness internally and can therefore provide a more gas-efficient and collision-resistant alternative to nested mappings or multi-dimensional arrays in certain scenarios.

🔴 Affected code:
There are 8 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol
27  mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
        public isWithdrawalFinalized;

32  mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
        public depositAmount;     

51   mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;           
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27-L28


```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
52  mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
        public
        override depositHappened;

57    mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
        public isWithdrawalFinalized;

65   mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;                
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L52


```solidity
File: system-contracts/contracts/ImmutableSimulator.sol
21   mapping(uint256 contractAddress => mapping(uint256 index => bytes32 value)) internal immutableDataStorage;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L21


```solidity
File: system-contracts/contracts/NonceHolder.sol
41  mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L41


## [G-10] Multiple accesses of a mapping/array should use a local variable cache
The instances below point to the second+ access of a value inside a mapping/array, within a function. Caching a mapping's value in a local storage or calldata variable when the value is accessed multiple times, saves ~42 gas per access due to not having to recalculate the key's keccak256 hash (Gkeccak256 - 30 gas) and that calculation's associated stack operations. Caching an array's struct avoids recalculating the array offsets into memory/calldata


🔴 Affected code:
There are 40 instances of this issue:


### Cache Mapping Result in bridgehubDeposit Function

**Original Code**
```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
function bridgehubDeposit(
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
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188-L228


**Description:**
In the `bridgehubDeposit` function of `L1SharedBridge`, the multiple accesses to `l2BridgeAddress[_chainId]` mapping are optimized by caching the mapping result to avoid redundant lookups, thus saving gas.

**Optimized Code**
```diff
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
function bridgehubDeposit(
        uint256 _chainId,
        address _prevMsgSender,
        uint256, // l2Value, needed for Weth deposits in the future
        bytes calldata _data
    ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
+       address _l2BridgeAddress = l2BridgeAddress[_chainId];
        require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
        require(_l2BridgeAddress != address(0), "ShB l2 bridge not deployed");

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
-               l2Contract: l2BridgeAddress[_chainId],
+               l2Contract: _l2BridgeAddress,
                l2Calldata: l2TxCalldata,
                factoryDeps: new bytes[](0),
                txDataHash: txDataHash
            });
        }
        emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);
    }
```

### Cache Mapping Result in `L1SharedBridge::depositLegacyErc20Bridge` Function

**Original Code**
```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
function depositLegacyErc20Bridge(
        address _prevMsgSender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte,
        address _refundRecipient
    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
        require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
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
                l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
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
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L554-L603


**Description:**
In the `depositLegacyErc20Bridge` function of `L1SharedBridge`, the multiple accesses to `l2BridgeAddress[ERA_CHAIN_ID]` mapping are optimized by caching the mapping result to avoid redundant lookups, thus saving gas.

**Optimized Code**
```diff
function depositLegacyErc20Bridge(
        address _prevMsgSender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte,
        address _refundRecipient
    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
+       address _l2BridgeAddress = l2BridgeAddress[ERA_CHAIN_ID];
-       require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
+       require(_l2BridgeAddress != address(0), "ShB b. n dep");
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
-               l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
+               l2Contract: _l2BridgeAddress,
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


```solidity
File: contracts/ethereum/contracts/governance/Governance.sol
226                (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L226:226

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
66                  blobHashes[0] = logOutput.blob1Hash;

333             s.l2LogsRootHashes[currentBatchNumber] = _storedBatch.l2LogsTreeRoot;

353                 emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

408                     _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],

412                 bytes32 currentBatchCommitment = _committedBatches[i].commitment;

670                         (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),

670                         (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670:670

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol
170                 bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];

184             return ds.selectorToFacet[_selector].isFreezable;
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L184:184

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
105                 bytes4[] memory selectors = facetCuts[i].selectors;

195                 ds.facetToSelectors[_facet].facetPosition = ds.facets.length.toUint16();

223             ds.facetToSelectors[_facet].selectors.push(_selector);

247             delete ds.selectorToFacet[_selector];

244             ds.facetToSelectors[_facet].selectors.pop();
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L244:244

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/LibMap.sol
61                  _map.map[mapIndex] = (newValueXorOldValue << bitOffset) ^ mapValue;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L61:61

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol
32                      : _efficientHash(_path[i], currentHash);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L32:32

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol
79              delete _queue.data[head];
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L79:79

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol
99                  l1TokenAddress[expectedL2Token] = _l1Token;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L99:99

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol
96                  if (_transaction.reserved[0] != 0) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L96:96

```solidity
File: system-contracts/contracts/Compressor.sol
174                 uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L174:174

```solidity
File: system-contracts/contracts/ContractDeployer.sol
254                 this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L254:254

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol
40                      bytes32 value = _immutables[i].value;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L40:40

```solidity
File: system-contracts/contracts/L1Messenger.sol
225                     l2ToL1LogsTreeArray[i] = keccak256(

289             uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L289:289

```solidity
File: system-contracts/contracts/L2BaseToken.sol
43                  balance[_from] = fromBalance - _amount;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L43:43

```solidity
File: system-contracts/contracts/NonceHolder.sol
72                  rawNonces[addressAsKey] = (oldRawNonce + _value);

118                 rawNonces[addressAsKey] = oldRawNonce + 1;

144                 rawNonces[addressAsKey] = (oldRawNonce + DEPLOY_NONCE_MULTIPLIER);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L144:144

```solidity
File: system-contracts/contracts/libraries/RLPEncoder.so
34                      encoded[0] = bytes1(uint8(hbs + 0x81));

69                      encoded[0] = bytes1(uint8(_offset + hbs + 56));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L69:69

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol
184             if (_transaction.reserved[0] != 0) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L184:184


## [G-11] Internal functions only called once can be inlined to save gas
Not inlining costs 20 to 40 gas because of two extra JUMP instructions and additional stack operations needed for function calls.


🔴 Affected code:
There are 53 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol
160         function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160:160

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
254         function _getERC20Getters(address _token) internal view returns (bytes memory) {

458         function _checkWithdrawal(

487         function _parseL2WithdrawalMessage(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L487:487


```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
177         function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177:177

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
130         function _processL2Logs(

625         function _verifyBlobInformation(

103         function _verifyBatchTimestamp(

500         function _createBatchCommitment(

592         function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

597         function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {

253         function _commitBatchesWithoutSystemContractsUpgrade(

273         function _commitBatchesWithSystemContractsUpgrade(

308         function _collectOperationsFromPriorityQueue(uint256 _nPriorityOps) internal returns (bytes32 concatHash) {

321         function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {

453         function _getBatchProofPublicInput(

515         function _batchPassThroughData(CommitBatchInfo calldata _batch) internal pure returns (bytes memory) {

525         function _batchMetaParameters() internal view returns (bytes memory) {

537         function _batchAuxiliaryOutput(

561         function _encodeBlobAuxilaryOutput(

605         function _pointEvaluationPrecompile(
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L605:605

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
130         function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {

258         function _requestL2Transaction(

316         function _writePriorityOp(

353         function _hashFactoryDeps(bytes[] memory _factoryDeps) internal pure returns (uint256[] memory hashedFactoryDeps) {

289         function _serializeL2Transaction(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L289:289


```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
163         function _upgradeVerifier(address _newVerifier, VerifierParams calldata _verifierParams) internal {

171         function _setBaseSystemContracts(bytes32 _bootloaderHash, bytes32 _defaultAccountHash) internal {

180         function _setL2SystemContractUpgrade(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L180:180


```solidity
File: contracts/zksync/contracts/SystemContractsCaller.sol
95          function getFarCallABI(

37          function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

121         function getFarCallABIWithEmptyFatPointer(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L121:121

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol
109         function _deployL2Token(address _l1Token, bytes calldata _data) internal returns (address) {

164         function _deployBeaconProxy(bytes32 salt) internal returns (BeaconProxy proxy) {

138         function _getL1WithdrawMessage(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L138:138

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol
44          function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {

229         function encodeEIP1559TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {

139         function encodeEIP2930TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L139:139

```solidity
File: system-contracts/contracts/Compressor.sol
197         function _decodeRawBytecode(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L197:197

```solidity
File: system-contracts/contracts/ContractDeployer.sol
283         function _performDeployOnAddress(

309         function _storeConstructingByteCodeHashOnAddress(address _newAddress, bytes32 _bytecodeHash) internal {
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L309:309

```solidity
File: system-contracts/contracts/DefaultAccount.sol
78          function _validateTransaction(

159         function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {

131         function _execute(Transaction calldata _transaction) internal {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L131:131

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol
74          function _validateBytecode(bytes32 _bytecodeHash) internal pure {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L74:74

```solidity
File: system-contracts/contracts/L1Messenger.sol
61          function sha256GasCost(uint256 _length) internal pure returns (uint256) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L61:61

```solidity
File: system-contracts/contracts/L2BaseToken.sol
112         function _getL1WithdrawMessage(address _to, uint256 _amount) internal pure returns (bytes memory) {

117         function _getExtendedWithdrawMessage(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L117:117

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol
25          function _getAbiParams() internal view returns (uint256 value, bool isSystemCall, address to) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L25:25

```solidity
File: system-contracts/contracts/SystemContext.sol
233         function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {

241         function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {

221         function _calculateL2BlockHash(

263         function _setVirtualBlock(

427         function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L427:427


## [G-12] Use assembly to write address storage values
By using assembly to write to address storage values, you can bypass some of these operations and lower the gas cost of writing to storage. Assembly code allows you to directly access the Ethereum Virtual Machine (EVM) and perform low-level operations that are not possible in Solidity.

example of using assembly to write to address storage values:
```
contract MyContract {
    address private myAddress;
    
    function setAddressUsingAssembly(address newAddress) public {
        assembly {
            sstore(0, newAddress)
        }
    }
}
```
🔴 Affected code:
There are 13 instances of this issue:

```solidity
File:  contracts/ethereum/contracts/bridgehub/Bridgehub.sol
55  pendingAdmin = _newPendingAdmin;

65  admin = currentPendingAdmin;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55


```solidity
File:  contracts/ethereum/contracts/governance/Governance.sol
46   securityCouncil = _securityCouncil;

258   securityCouncil = _newSecurityCouncil;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L46


```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
85  genesisUpgrade = _initializeData.genesisUpgrade;

87  validatorTimelock = _initializeData.validatorTimelock;

133 validatorTimelock = _validatorTimelock;

114 pendingAdmin = _newPendingAdmin;

124 admin = currentPendingAdmin;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L85

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol
60   l1Bridge = _l1Bridge;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L60


```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol
52  l1Address = _l1Address;

54  l2Bridge = msg.sender;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L52


```solidity
File: system-contracts/contracts/SystemContext.sol
100   origin = _newOrigin;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L100


## [G-13] Use assembly to calculate hashes to save gas
Using assembly to calculate hashes can save 80 gas per instance


🔴 Affected code:
There are 59 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol
76              bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76:76

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
210             bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));

341                     bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));

598             bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L598:598

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol
12          bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");

67              bytes32 data = keccak256(
68                  bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
69              );
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L67:69

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol
205             return keccak256(abi.encode(_operation));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L205:205

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
100             storedBatchZero = keccak256(abi.encode(batchZero));

102             initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

138             initialCutHash = keccak256(abi.encode(_diamondCut));

147             upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

156             upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

255             bytes32 cutHashInput = keccak256(_diamondCut);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L255:255

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol
104             bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104:104

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
63                          keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),

313                 concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));

460                     keccak256(
461                         abi.encodePacked(
462                             _prevBatchCommitment,
463                             _currentBatchCommitment,
464                             _verifierParams.recursionNodeLevelVkHash,
465                             _verifierParams.recursionLeafLevelVkHash
466                         )
467                     )

506             bytes32 passThroughDataHash = keccak256(_batchPassThroughData(_newBatchData));

507             bytes32 metadataHash = keccak256(_batchMetaParameters());

508             bytes32 auxiliaryOutputHash = keccak256(
509                 _batchAuxiliaryOutput(_newBatchData, _stateDiffHash, _blobCommitments, _blobHashes)
510             );

512             return keccak256(abi.encode(passThroughDataHash, metadataHash, auxiliaryOutputHash));

545             bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs);

588             return keccak256(abi.encode(_storedBatchInfo));

654                 blobCommitments[versionedHashIndex] = keccak256(
655                     abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
656                 );

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L654:656

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
112             bytes32 hashedLog = keccak256(
113                 abi.encodePacked(_log.l2ShardId, _log.isService, _log.txNumberInBatch, _log.sender, _log.key, _log.value)
114             );

138                     value: keccak256(_message.data)

332             canonicalTxHash = keccak256(transactionEncoding);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L332:332

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
212             bytes32 l2ProtocolUpgradeTxHash = keccak256(encodedTransaction);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L212:212

```solidity
File: contracts/zksync/contracts/L2ContractHelper.sol
85          bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");

108             bytes32 data = keccak256(
109                 bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
110             );
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L108:110

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol
150             bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150:150

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol
29                  txHash = keccak256(bytes.concat(signedTxHash, EfficientCall.keccak(_transaction.signature)));

120                 keccak256(
121                     bytes.concat(
122                         encodedListLength,
123                         encodedNonce,
124                         encodedGasParam,
125                         encodedTo,
126                         encodedValue,
127                         encodedDataLength,
128                         _transaction.data,
129                         vEncoded,
130                         rEncoded,
131                         sEncoded
132                     )
133                 );

211                 keccak256(
212                     bytes.concat(
213                         "\x01",
214                         encodedListLength,
215                         encodedFixedLengthParams,
216                         encodedDataLength,
217                         _transaction.data,
218                         encodedAccessListLength,
219                         vEncoded,
220                         rEncoded,
221                         sEncoded
222                     )
223                 );

306                 keccak256(
307                     bytes.concat(
308                         "\x02",
309                         encodedListLength,
310                         encodedFixedLengthParams,
311                         encodedDataLength,
312                         _transaction.data,
313                         encodedAccessListLength,
314                         vEncoded,
315                         rEncoded,
316                         sEncoded
317                     )
318                 );
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L306:318

```solidity
File: system-contracts/contracts/ContractDeployer.sol
105             bytes32 hash = keccak256(
106                 bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, constructorInputHash)
107             );

121             bytes32 hash = keccak256(
122                 bytes.concat(CREATE_PREFIX, bytes32(uint256(uint160(_sender))), bytes32(_senderNonce))
123             );
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L121:123

```solidity
File: system-contracts/contracts/L1Messenger.sol
95              bytes32 hashedLog = keccak256(
96                  abi.encodePacked(
97                      _l2ToL1Log.l2ShardId,
98                      _l2ToL1Log.isService,
99                      _l2ToL1Log.txNumberInBlock,
100                     _l2ToL1Log.sender,
101                     _l2ToL1Log.key,
102                     _l2ToL1Log.value
103                 )
104             );

106             chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

122             chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

164             chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

212                 reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));

225                     l2ToL1LogsTreeArray[i] = keccak256(
226                         abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
227                     );

243                 reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));

259                 reconstructedChainedL1BytecodesRevealDataHash = keccak256(
260                     abi.encode(
261                         reconstructedChainedL1BytecodesRevealDataHash,
262                         Utils.hashL2Bytecode(
263                             _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
264                         )
265                     )
266                 );
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L259:266

```solidity
File: system-contracts/contracts/SystemContext.sol
159                 hash = keccak256(abi.encode(_block));

227             return keccak256(abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash));

234             return keccak256(abi.encodePacked(uint32(_blockNumber)));

403             currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L403:403

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol
85              keccak256(
86                  "Transaction(uint256 txType,uint256 from,uint256 to,uint256 gasLimit,uint256 gasPerPubdataByteLimit,uint256 maxFeePerGas,uint256 maxPriorityFeePerGas,uint256 paymaster,uint256 nonce,uint256 value,bytes data,bytes32[] factoryDeps,bytes paymasterInput)"
87              );

119             bytes32 structHash = keccak256(
120                 abi.encode(
121                     EIP712_TRANSACTION_TYPE_HASH,
122                     _transaction.txType,
123                     _transaction.from,
124                     _transaction.to,
125                     _transaction.gasLimit,
126                     _transaction.gasPerPubdataByteLimit,
127                     _transaction.maxFeePerGas,
128                     _transaction.maxPriorityFeePerGas,
129                     _transaction.paymaster,
130                     _transaction.nonce,
131                     _transaction.value,
132                     EfficientCall.keccak(_transaction.data),
133                     keccak256(abi.encodePacked(_transaction.factoryDeps)),
134                     EfficientCall.keccak(_transaction.paymasterInput)
135                 )
136             );

133                     keccak256(abi.encodePacked(_transaction.factoryDeps)),

138             bytes32 domainSeparator = keccak256(
139                 abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
140             );

139                 abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

139                 abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

142             return keccak256(abi.encodePacked("\x19\x01", domainSeparator, structHash));

203                 keccak256(
204                     bytes.concat(
205                         encodedListLength,
206                         encodedNonce,
207                         encodedGasParam,
208                         encodedTo,
209                         encodedValue,
210                         encodedDataLength,
211                         _transaction.data,
212                         encodedChainId
213                     )
214                 );

275                 keccak256(
276                     bytes.concat(
277                         "\x01",
278                         encodedListLength,
279                         encodedFixedLengthParams,
280                         encodedDataLength,
281                         _transaction.data,
282                         encodedAccessListLength
283                     )
284                 );

347                 keccak256(
348                     bytes.concat(
349                         "\x02",
350                         encodedListLength,
351                         encodedFixedLengthParams,
352                         encodedDataLength,
353                         _transaction.data,
354                         encodedAccessListLength
355                     )
356                 );
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L347:356



## [G-14] REQUIRE()/REVERT() STRINGS LONGER THAN 32 BYTES COST EXTRA GAS
require(msg.sender == destination, "when these strings get longer than 32 bytes, they cost more gas");

🔴 Affected code:
There are 66 instances of this issue:
```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");

require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

require(!alreadyFinalized, "Withdrawal is already finalized 2");

require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564:564

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225:225

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol


require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

require(isOperationReady(id), "Operation must be ready before execution");

require(isOperationReady(id), "Operation must be ready after execution");

require(isOperationPending(id), "Operation must be pending before execution");

require(isOperationPending(id), "Operation must be pending after execution");

require(!isOperation(_id), "Operation with this proposal id already exists");

require(_delay >= minDelay, "Proposed delay is less than minimum delay");

require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L240:240

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L256:256

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68:68

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol
require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90:90

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
require(success, "failed to call point evaluation precompile");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616:616

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");

require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");

require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L206:206

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol
require(s.validators[msg.sender], "StateTransition Chain: not validator");

require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53:53

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");

require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L249:249

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol
require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33:33

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol
require(msg.value == 0, "Value should be 0 for ERC20 bridge");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92:92

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol
require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");

require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");

require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L57:57

```solidity
File: system-contracts/contracts/ComplexUpgrader.sol
require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22:22

```solidity
File: system-contracts/contracts/Compressor.sol
require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");

require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");

require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");

require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");

require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L230:230

```solidity
File: system-contracts/contracts/ContractDeployer.sol
require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");

require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

require(value == 0, "The value must be zero if we do not call the constructor");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L350:350

```solidity
File: system-contracts/contracts/DefaultAccount.sol
require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

require(success, "Failed to pay the fee to the operator");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L202:202

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol
require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35:35

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol
require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L76:76

```solidity
File: system-contracts/contracts/L1Messenger.sol
require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L315:315

```solidity
File: system-contracts/contracts/NonceHolder.sol
require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L66:66

```solidity
File: system-contracts/contracts/SystemContext.sol

require(_isFirstInBatch, "Upgrade transaction must be first");

require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");

require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");

require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");

require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");

require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");

require(currentBatchNumber > 0, "The current batch number must be greater than 0");

require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L452:452
```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol
require(index < 10, "There are only 10 accessible registers");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319:319

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol
require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L363:363


## [G-15] Sort Solidity operations using short-circuit mode
Short-circuiting is a solidity contract development model that uses OR/AND logic to sequence different cost operations. It puts low gas cost operations in the front and high gas cost operations in the back, so that if the front is low If the cost operation is feasible, you can skip (short-circuit) the subsequent high-cost Ethereum virtual machine operation.

```
//f(x) is a low gas cost operation 
//g(y) is a high gas cost operation 
//Sort operations with different gas costs as follows 
f(x) || g(y) 
f(x) && g(y)
```
🔴 Affected code:
There are 2 instances of this issue:

- `accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential` is a high gas cost operation then `_key != 0`.
```solidity
File: system-contracts/contracts/NonceHolder.sol
88  if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L88

`currentVirtualL2BlockInfo.number` is storage read high gas cost then `virtualBlockInfo.timestamp == 0`.
```solidity
File: system-contracts/contracts/SystemContext.sol
277  if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L277


## [G-16] Avoid emitting storage values
Caching of a state variable replaces each Gwarmaccess (100 gas) with a much cheaper stack read. We can avoid unecessary SLOADs by caching storage values that were previously accessed and emitting those cached values


🔴 Affected code:
There are 12 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

69              emit NewAdmin(previousAdmin, pendingAdmin);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69:69

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol
250             emit ChangeMinDelay(minDelay, _newDelay);

257             emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L257:257

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

128             emit NewAdmin(previousAdmin, pendingAdmin);

227             emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227:227

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
436             emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

496             emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);

496             emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);

496             emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496:496

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol
101             emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);

126             emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);

126             emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126:126


## [G-17] Can Make The Variable Outside The Loop To Save Gas 
When you declare a variable inside a loop, Solidity creates a new instance of the variable for each iteration of the loop. This can lead to unnecessary gas costs, especially if the loop is executed frequently or iterates over a large number of elements.

By declaring the variable outside the loop, you can avoid the creation of multiple instances of the variable and reduce the gas cost of your contract. Here's an example:

```
contract MyContract {
    function sum(uint256[] memory values) public pure returns (uint256) {
        uint256 total = 0;
        
        for (uint256 i = 0; i < values.length; i++) {
            total += values[i];
        }
        
        return total;
    }
}
```

🔴 Affected code:
There are 20 instances of this issue:

```solidity
File:  contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
186  uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(

210  uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);    
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L186


```solidity
File:  contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
637  bytes32 blobVersionedHash = _getBlobVersionedHash(versionedHashIndex);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L637


```solidity
File:  contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol
209  address facetAddr = ds.facets[i];
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L209


```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
357  bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L357


```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
103         address facet = facetCuts[i].facet;
            bool isFacetFreezable = facetCuts[i].isFreezable;
            bytes4[] memory selectors = facetCuts[i].selectors;

139  bytes4 selector = _selectors[i];

159  bytes4 selector = _selectors[i];

179  bytes4 selector = _selectors[i];
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L103-L105


```solidity
File:  system-contracts/contracts/Compressor.sol
160         bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
            uint64 enumIndex = stateDiff.readUint64(84);

166         uint256 initValue = stateDiff.readUint256(92);
            uint256 finalValue = stateDiff.readUint256(124);
            uint256 compressedEnumIndex = _sliceToUint256(            
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L160


```solidity
File: system-contracts/contracts/ImmutableSimulator.sol
39              uint256 index = _immutables[i].index;
                bytes32 value = _immutables[i].value;

                
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L39-L40


```solidity
File: system-contracts/contracts/L1Messenger.sol
207  bytes32 hashedLog = EfficientCall.keccak(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L207


```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol
37  uint256 start = BLOB_SIZE_BYTES * i;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L37


## [G-18] A modifier used only once and not being inherited should be inlined to save gas

When you use a modifier in Solidity, Solidity generates code to check the conditions of the modifier and execute the modified function if the conditions are met. This generated code can consume gas, especially if the modifier is used frequently or if the modified function is called multiple times.
By inlining a modifier that is used only once and not being inherited, you can eliminate the overhead of the generated code and reduce the gas cost of your contract.

🔴 Affected code:

There are 7 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
73   modifier onlyBridgehubOrEra(uint256 _chainId) {
        require(
            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
            "L1SharedBridge: not bridgehub or era chain"
        );
        _;
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L73-L80


```solidity
File: contracts/ethereum/contracts/governance/Governance.sol
64    modifier onlySecurityCouncil() {
        require(msg.sender == securityCouncil, "Only security council is allowed to call this function");
        _;
    }

70  modifier onlyOwnerOrSecurityCouncil() {
        require(
            msg.sender == owner() || msg.sender == securityCouncil,
            "Only the owner and security council are allowed to call this function"
        );
        _;
    }    
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L64-L70


```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
63   modifier onlyBridgehub() {
        require(msg.sender == bridgehub, "StateTransition: only bridgehub");
        _;
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L63-L66


```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol
134 modifier onlyNextVersion(uint8 _version) {
        // The version should be incremented by 1. Otherwise, the governor risks disabling
        // future reinitialization of the token by providing too large a version.
        require(_version == _getInitializedVersion() + 1, "v");
        _;
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L134-L139


```solidity
File: system-contracts/contracts/ContractDeployer.sol
28  modifier onlySelf() {
        require(msg.sender == address(this), "Callable only by self");
        _;
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L28


```solidity
File: system-contracts/contracts/KnownCodesStorage.sol
19    modifier onlyCompressor() {
        require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");
        _;
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L19

## [G-19] Refactor external/internal function to avoid unnecessary External Calls
The functions below perform external calls that are previously performed in the functions that invoke them. We can refactor the external/internal functions so we could pass the cached external calls into them and avoid the extra external calls that would otherwise take place in the internal functions.

🔴 Affected code:

There are 3 instances of this issue:

### Cache External Call in L1SharedBridge's transferFundsFromLegacy Function
**Original Code**
```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
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


**Description:**
In the `transferFundsFromLegacy` function of `L1SharedBridge`, the external call `IERC20(_token)` is optimized by caching its result to avoid multiple external calls, thus saving gas.

**Optimized Code**
```diff
    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
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
+           IERC20 _IERC20 = IERC20(_token);
-           uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
+           uint256 balanceBefore = _IERC20.balanceOf(address(this));
-           uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
+           uint256 amount = _IERC20.balanceOf(address(legacyBridge));
            require(amount > 0, "ShB: 0 amount to transfer");
            IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);
-           uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
+           uint256 balanceAfter = _IERC20.balanceOf(address(this));
            require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
        }
    }
```

## [G-20] Avoid updating storage when the value hasn't changed
If the old value is equal to the new value, not re-storing the value will avoid a Gsreset (**2900 gas**), potentially at the expense of a Gcoldsload (**2100 gas**) or a Gwarmaccess (**100 gas**).

🔴 Affected code:
There are 31 instances of this issue:
```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
104         function initialize(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L104:104

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol
60          function acceptAdmin() external {

51          function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

108         function setSharedBridge(address _sharedBridge) external onlyOwner {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108:108

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol
256         function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {

249         function updateDelay(uint256 _newDelay) external onlySelf {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L249:249

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
142         function setNewVersionUpgrade(

132         function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {

119         function acceptAdmin() external {

110         function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {

137         function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {

79          function initialize(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L79:79

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
96          function setExecutionDelay(uint32 _executionDelay) external onlyOwner {

73          function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L73:73

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol
49          function initialize(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L49:49

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol
50          function bridgeInitialize(address _l1Address, bytes memory _data) external initializer {

111         function reinitializeToken(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L111:111

```solidity
File: system-contracts/contracts/L1Messenger.sol
94          function _processL2ToL1Log(L2ToL1Log memory _l2ToL1Log) internal returns (uint256 logIdInMerkleTree) {

194         function publishPubdataAndClearState(

161         function requestBytecodeL1Publication(

116         function sendToL1(bytes calldata _message) external override returns (bytes32 hash) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L116:116

```solidity
File: system-contracts/contracts/SystemContext.sol
84          function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {

486         function resetTxNumberInBatch() external onlyCallFromBootloader {

402         function appendTransactionToCurrentL2Block(bytes32 _txHash) external onlyCallFromBootloader {

263         function _setVirtualBlock(

99          function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {

112         function setPubdataInfo(uint256 _gasPerPubdataByte, uint256 _basePubdataSpent) external onlyCallFromBootloader {

444         function setNewBatch(

105         function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {

314         function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal {

471         function unsafeOverrideBatch(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L471:471


## [G-21] Use assembly to emit an event
To efficiently emit events, it's possible to utilize assembly by making use of scratch space and the free memory pointer. This approach has the advantage of potentially avoiding the costs associated with memory expansion.

However, it's important to note that in order to safely optimize this process, it is preferable to cache and restore the free memory pointer.

A good example of such practice can be seen in [Solady's](https://github.com/Vectorized/solady/blob/main/src/tokens/ERC1155.sol#L167) codebase.

[Reffrence](https://gist.github.com/CloudEllie/05fda0fdecba2ed7d85f68c709e46c8d#gas-17-use-assembly-to-emit-an-event)


🔴 Affected code:
There are 77 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol
155             emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);

199             emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);

225             emit WithdrawalFinalized(l1Receiver, l1Token, amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L225:225

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
168             emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);

227             emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);

239             emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);

367             emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);

454             emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);

602             emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L602:602

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol
56              emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

68              emit NewPendingAdmin(currentPendingAdmin, address(0));

69              emit NewAdmin(previousAdmin, pendingAdmin);

145             emit NewChain(_chainId, _stateTransitionManager, _admin);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L145:145

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol
47              emit ChangeSecurityCouncil(address(0), _securityCouncil);

50              emit ChangeMinDelay(0, _minDelay);

132             emit TransparentOperationScheduled(id, _delay, _operation)

144             emit ShadowOperationScheduled(_id, _delay);

157             emit OperationCancelled(_id);

180             emit OperationExecuted(id);

199             emit OperationExecuted(id);

250             emit ChangeMinDelay(minDelay, _newDelay);

257             emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L257:257

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
115             emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

127             emit NewPendingAdmin(currentPendingAdmin, address(0));

128             emit NewAdmin(previousAdmin, pendingAdmin);

227             emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
235             emit StateTransitionNewChain(_chainId, _stateTransitionContract);

287             emit StateTransitionNewChain(_chainId, stateTransitionAddress);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L287:287

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
83              emit ValidatorAdded(_chainId, _newValidator);

92              emit ValidatorRemoved(_chainId, _validator);

98              emit NewExecutionDelay(_executionDelay);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98:98

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol
28              emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

40              emit NewPendingAdmin(pendingAdmin, address(0));

41              emit NewAdmin(previousAdmin, pendingAdmin);

47              emit ValidatorStatusUpdate(_validator, _active);

54              emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);

63              emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);

75              emit NewFeeParams(oldFeeParams, _newFeeParams);

86              emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator);

92              emit ValidiumModeStatusUpdate(_validiumMode);

115             emit ExecuteUpgrade(_diamondCut);

125             emit ExecuteUpgrade(_diamondCut);

139             emit Freeze();

149             emit Unfreeze();
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L149:149

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
261                 emit BlockCommit(
262                     _lastCommittedBatchData.batchNumber,
263                     _lastCommittedBatchData.batchHash,
264                     _lastCommittedBatchData.commitment
265                 );

299                 emit BlockCommit(
300                     _lastCommittedBatchData.batchNumber,
301                     _lastCommittedBatchData.batchHash,
302                     _lastCommittedBatchData.commitment
303                 );

353                 emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

436             emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

496             emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496:496

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
343             emit NewPriorityRequest(
344                 _priorityOpParams.txId,
345                 canonicalTxHash,
346                 _priorityOpParams.expirationTimestamp,
347                 transaction,
348                 _factoryDeps
349             );
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L343:349

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
121             emit DiamondCut(facetCuts, initAddress, initCalldata);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L121:121

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
87              emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);

104             emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);

121             emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);

137             emit NewVerifier(address(oldVerifier), address(_newVerifier));

157             emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

256             emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L256:256

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol
40              emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);

67              emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L67:67

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol
105             emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);

134             emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L134:134

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol
101             emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);

126             emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);

147             emit BridgeMint(_to, _amount);

156             emit BridgeBurn(_from, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L156:156

```solidity
File: system-contracts/contracts/ContractDeployer.so
68              emit AccountVersionUpdated(msg.sender, _version);

86              emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);

355             emit ContractDeployed(_sender, _bytecodeHash, _newAddress);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L355:355

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol
59                  emit MarkedAsKnown(_bytecodeHash, _shouldSendToL1);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L59:59

```solidity
File: system-contracts/contracts/L1Messenger.sol
111             emit L2ToL1LogSent(_l2ToL1Log);

156             emit L1MessageSent(msg.sender, hash, _message);

181             emit BytecodeL1PublicationRequested(_bytecodeHash);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L181:181

```solidity
File: system-contracts/contracts/L2BaseToken.sol
49              emit Transfer(_from, _to, _amount);

67              emit Mint(_account, _amount);

79              emit Withdrawal(msg.sender, _l1Receiver, amount);

92              emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L92:92

```solidity
File: system-contracts/contracts/NonceHolder.sol
96              emit ValueSetUnderNonce(msg.sender, _key, _value);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L96:96


## [G-22] Do-While loops are cheaper than for loops
If you want to push optimization at the expense of creating slightly unconventional code, Solidity do-while loops are more gas efficient than for loops, even if you add an if-condition check for the case where the loop doesn’t execute at all.
```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.20;

// times == 10 in both tests
contract Loop1 {
    function loop(uint256 times) public pure {
        for (uint256 i; i < times;) {
            unchecked {
                ++i;
            }
        }
    }
}

contract Loop2 {
    function loop(uint256 times) public pure {
        if (times == 0) {
            return;
        }

        uint256 i;

        do {
            unchecked {
                ++i;
            }
        } while (i < times);
    }
}
```
🔴 Affected code:
There are 6 instances of this issue:


- `require(_pubdataCommitments.length > 0, "pl");` condition in line 631

- `MAX_NUMBER_OF_BLOBS` is constant.
```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
636  for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {

667  for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {    
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636

- `require(pathLength > 0, "xc");` condition in line 24
```solidity
File:  contracts/ethereum/contracts/state-transition/libraries/Merkle.sol
29  for (uint256 i; i < pathLength; i = i.uncheckedInc()) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L29

`require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");`.
```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
226   for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226


```solidity
File: system-contracts/contracts/L1Messenger.sol
218  for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L218

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol
36   for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36

## [G-23] Initializers can be marked payable
Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided. An initializer can safely be marked as payable, since only the deployer would be able to pass funds, and the project itself would not pass any funds.


🔴 Affected code:
There are 8 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol
60          function initialize() external reentrancyGuardInitializer {}
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L60:60

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
104         function initialize(
105             address _owner,
106             uint256 _eraFirstPostUpgradeBatch
107         ) external reentrancyGuardInitializer initializer {
108             require(_owner != address(0), "ShB owner 0");
109             _transferOwnership(_owner);
110     
111             eraFirstPostUpgradeBatch = _eraFirstPostUpgradeBatch;
112             l2BridgeAddress[ERA_CHAIN_ID] = ERA_ERC20_BRIDGE_ADDRESS;
113         }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L104:113

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol
41          function initialize(address _owner) external reentrancyGuardInitializer {
42              _transferOwnership(_owner);
43          }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L41:43

```solidity
File: contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol
65          function initialize(StateTransitionManagerInitializeData calldata _initalizeData) external;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L65:65

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
79          function initialize(
80              StateTransitionManagerInitializeData calldata _initializeData
81          ) external reentrancyGuardInitializer {
82              require(_initializeData.governor != address(0), "StateTransition: governor zero");
83              _transferOwnership(_initializeData.governor);
84      
85              genesisUpgrade = _initializeData.genesisUpgrade;
86              protocolVersion = _initializeData.protocolVersion;
87              validatorTimelock = _initializeData.validatorTimelock;
88      
89              // We need to initialize the state hash because it is used in the commitment of the next batch
90              IExecutor.StoredBatchInfo memory batchZero = IExecutor.StoredBatchInfo(
91                  0,
92                  _initializeData.genesisBatchHash,
93                  _initializeData.genesisIndexRepeatedStorageChanges,
94                  0,
95                  EMPTY_STRING_KECCAK,
96                  DEFAULT_L2_LOGS_TREE_ROOT_HASH,
97                  0,
98                  _initializeData.genesisBatchCommitment
99              );
100             storedBatchZero = keccak256(abi.encode(batchZero));
101     
102             initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));
103     
104             // While this does not provide a protection in the production, it is needed for local testing
105             // Length of the L2Log encoding should not be equal to the length of other L2Logs' tree nodes preimages
106             assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
107         }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L79:107

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol
24          function initialize(InitializeData calldata _initializeData) external reentrancyGuardInitializer returns (bytes32) {
25              require(address(_initializeData.verifier) != address(0), "vt");
26              require(_initializeData.admin != address(0), "vy");
27              require(_initializeData.validatorTimelock != address(0), "hc");
28              require(_initializeData.priorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "vu");
29      
30              s.chainId = _initializeData.chainId;
31              s.bridgehub = _initializeData.bridgehub;
32              s.stateTransitionManager = _initializeData.stateTransitionManager;
33              s.baseToken = _initializeData.baseToken;
34              s.baseTokenBridge = _initializeData.baseTokenBridge;
35              s.protocolVersion = _initializeData.protocolVersion;
36      
37              s.verifier = _initializeData.verifier;
38              s.admin = _initializeData.admin;
39              s.validators[_initializeData.validatorTimelock] = true;
40      
41              s.storedBatchHashes[0] = _initializeData.storedBatchZero;
42              s.verifierParams = _initializeData.verifierParams;
43              s.l2BootloaderBytecodeHash = _initializeData.l2BootloaderBytecodeHash;
44              s.l2DefaultAccountBytecodeHash = _initializeData.l2DefaultAccountBytecodeHash;
45              s.priorityTxMaxGasLimit = _initializeData.priorityTxMaxGasLimit;
46              s.feeParams = _initializeData.feeParams;
47              s.blobVersionedHashRetriever = _initializeData.blobVersionedHashRetriever;
48      
49              // While this does not provide a protection in the production, it is needed for local testing
50              // Length of the L2Log encoding should not be equal to the length of other L2Logs' tree nodes preimages
51              assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
52      
53              return Diamond.DIAMOND_INIT_SUCCESS_RETURN_VALUE;
54          }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L24:54

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol
62          function initialize(InitializeData calldata _initData) external returns (bytes32);
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L62:62

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol
49          function initialize(
50              address _l1Bridge,
51              address _l1LegecyBridge,
52              bytes32 _l2TokenProxyBytecodeHash,
53              address _aliasedOwner
54          ) external reinitializer(2) {
55              require(_l1Bridge != address(0), "bf");
56              require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
57              require(_aliasedOwner != address(0), "sf");
58              require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
59      
60              l1Bridge = _l1Bridge;
61              l2TokenProxyBytecodeHash = _l2TokenProxyBytecodeHash;
62      
63              if (block.chainid != ERA_CHAIN_ID) {
64                  address l2StandardToken = address(new L2StandardERC20{salt: bytes32(0)}());
65                  l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(l2StandardToken);
66                  l2TokenBeacon.transferOwnership(_aliasedOwner);
67              } else {
68                  require(_l1LegecyBridge != address(0), "bf2");
69                  // l2StandardToken and l2TokenBeacon are already deployed on ERA, and stored in the proxy
70              }
71          }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L49:71


## [G-24] require() or revert() statements that check input arguments should be at the top of the function

Checks that involve constants should come before checks that involve state variables, function calls, and calculations. By doing these checks first, the function is able to revert before wasting a Gcoldsload (2100 gas*) in a function that may ultimately revert in the unhappy case.


🔴 Affected code:
There are 6 instances of this issue:

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol
25              require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25:25

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
631             require(_pubdataCommitments.length > 0, "pl");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631:631

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
155             require(_facet.code.length > 0, "K");

132             require(_facet.code.length > 0, "G");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132:132

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
205             require(
206                 _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
207                 "The new protocol version should be included in the L2 system upgrade tx"
208             );
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L205:208

```solidity
File: system-contracts/contracts/NonceHolder.sol
85              require(_value != 0, "Nonce value cannot be set to 0");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L85:85












## [G-25] Use nested if statements instead of &&
If the if statement has a logical AND and is not followed by an else statement, it can be replaced with 2 if statements.

```
contract NestedIfTest {

    //Execution cost: 22334 gas
    function funcBad(uint256 input) public pure returns (string memory) { 
       if (input<10 && input>0 && input!=6){ 
           return "If condition passed";
       } 

   }

    //Execution cost: 22294 gas
    function funcGood(uint256 input) public pure returns (string memory) { 
    if (input<10) { 
        if (input>0){
            if (input!=6){
                return "If condition passed";
            }
        }
    }
   }
}
   
```

🔴 Affected code:

There are 10 instances of this issue:


```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
361      if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L361:361

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
148                 _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) &&
149                 _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) &&
150                 _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L148:150

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol
102             if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {

131             if (
132                 uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS &&
133                 codeHash != 0x00 &&
134                 !Utils.isContractConstructing(codeHash)
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L131:134

```solidity
File: system-contracts/contracts/ContractDeployer.sol
47            if (
48                  _address > address(MAX_SYSTEM_CONTRACT_ADDRESS) &&
49                  ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getRawCodeHash(_address) == 0
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L47:49

```solidity
File: system-contracts/contracts/DefaultAccount.sol
139  if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L139:139

```solidity
File: system-contracts/contracts/NonceHolder.sol
88              if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {


169             if (isUsed && !_shouldBeUsed) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L171:171

```solidity
File: system-contracts/contracts/SystemContext.sol
277             if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {

360             if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L360:360










## [G-26] Amounts should be checked for 0 before calling a transfer
Checking non-zero transfer values can avoid an expensive external call and save gas.

🔴 Affected code:
There are 3 instances of this issue:

- inside the function no check > 0 amount.
```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol
67  IERC20(_token).safeTransfer(address(sharedBridge), amount);

162 _token.safeTransferFrom(_from, address(sharedBridge), _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67

- inside the function no check > 0 amount.
```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
175  _token.safeTransferFrom(_from, address(this), _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175


## [G-27] abi.encode() is less efficient than abi.encodePacked()
In terms of efficiency, abi.encodePacked() is generally considered to be more gas-efficient than abi.encode(), because it skips the step of adding function signatures and other metadata to the encoded data. However, this comes at the cost of reduced safety, as abi.encodePacked() does not perform any type checking or padding of data.


🔴 Affected code:
There are 17 instances of this issue:


Note: I collect instances where 'abi.encodePacked' is used, ensuring there are no occurrences of collision.

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol
76  bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76


```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
210  bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));

258  bytes memory decimals = abi.encode(uint8(18));
259  return abi.encode(name, symbol, decimals);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L210


```solidity
File: contracts/ethereum/contracts/governance/Governance.sol
205   return keccak256(abi.encode(_operation));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L205

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
100  storedBatchZero = keccak256(abi.encode(batchZero));

102  initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

138  initialCutHash = keccak256(abi.encode(_diamondCut));

147  upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

156  upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100


```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol
104  bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104


```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol
150  bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""));

171  (salt, l2TokenProxyBytecodeHash, abi.encode(address(l2TokenBeacon), ""))
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L171


```solidity
File: system-contracts/contracts/L1Messenger.sol
106   chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

122   chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

164   chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

212  reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L106



## [G-28] Do not calculate constants
Due to how constant variables are implemented (replacements at compile-time), an expression assigned to a constant variable is recomputed each time that the variable is used, which wastes some gas
[Reffrence](https://code4rena.com/reports/2022-07-golom#g-24-do-not-calculate-constants)

🔴 Affected code:
There are 2 instances of this issue:

```solidity
File: system-contracts/contracts/NonceHolder.sol
28          uint256 private constant DEPLOY_NONCE_MULTIPLIER = 2 ** 128;

31          uint256 private constant MAXIMAL_MIN_NONCE_INCREMENT = 2 ** 32;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L31:31


## [G-29] Delete variables that you don't need
In Ethereum, you get a gas refund for freeing up storage space.
Deleting a variable refund 15,000 gas up to a maximum of half the gas cost of the transaction. Deleting with the delete keyword is equivalent to assigning the initial value for the data type, such as 0 for integers.

🔴 Affected code:
There are 2 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol
66   delete pendingAdmin;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L66


```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
125   delete pendingAdmin;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L125


## [G-30] Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead
> When using elements that are smaller than 32 bytes, your contractâ€™s gas usage may be higher. This is because the EVM operates on 32 bytes at a time. Therefore, if the element is smaller than that, the EVM must use more operations in order to reduce the size of the element from 32 bytes to the desired size.https://docs.soliditylang.org/en/v0.8.11/internals/layout_in_storage.htmlEach operation involving a `uint8` costs an extra [**22-28 gas**](https://gist.github.com/IllIllI000/9388d20c70f9a4632eb3ca7836f54977) (depending on whether the other operand is also a variable of type `uint8`) as compared to ones involving `uint256`, due to the compiler having to clear the higher bits of the memory word before operating on the `uint8`, as well as the associated stack operations of doing so. Use a larger size then downcast where needed.


🔴 Affected code:
There are 20 instances of this issue:

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol
40              uint8 version = uint8(_bytecodeHash[0]);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L40:40

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
39              uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L39:39

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/LibMap.sol
54                  uint32 oldValue = uint32(mapValue >> bitOffset);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L54:54

```solidity
File: system-contracts/contracts/Compressor.sol
65                      uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);
66                      uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

161                 uint64 enumIndex = stateDiff.readUint64(84);

174                 uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

177                 uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L177:177

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol
75              uint8 version = uint8(_bytecodeHash[0]);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L75:75

```solidity
File: system-contracts/contracts/L1Messenger.sol
200             uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

233             uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

237                 uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

251             uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

255                 uint32 currentBytecodeLength = uint32(

286             uint24 compressedStateDiffSize = uint24(bytes3(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 3]));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L286:286

```solidity
File: system-contracts/contracts/SystemContext.sol
278                 uint128 currentBatchNumber = currentBatchInfo.number;

409             (uint128 currentBatchNumber, uint128 currentBatchTimestamp) = getBatchNumberAndTimestamp();

428             uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp;

450             (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();

450             (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L450:450


## [G-31] Storage Slot Reduction via Variable Resizing
The Ethereum Virtual Machine (EVM) operates with 32-byte words in storage. Variables smaller than 32 bytes can be packed together into a single storage slot, which saves gas costs when retrieving these variables together. In this contract, `minDelay` is currently declared as a `uint256`, taking up a full storage slot on its own.

🔴 Affected code:
There are 2 instances of this issue:

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol
contract Governance is IGovernance, Ownable2Step {
    /// @notice A constant representing the timestamp for completed operations.
    uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1);

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
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L20-L35

note:  `minDelay` no need should be 256 bits.
**Issue Summary:**
the `minDelay` variable is declared as a `uint256`, occupying its own storage slot. By changing its type to `uint64`, it can be packed with the `securityCouncil` address variable into a single storage slot, thus saving one storage slot and reducing gas costs.

**Code Change:**
```diff
contract Governance is IGovernance, Ownable2Step {
    /// @notice A constant representing the timestamp for completed operations.
    uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1);

    /// @notice The address of the security council.
    /// @dev It is supposed to be multisig contract.
    address public securityCouncil;
+   uint64 public minDelay; // Changed type to uint64
    /// @notice A mapping to store timestamps when each operation will be ready for execution.
    /// @dev - 0 means the operation is not created.
    /// @dev - 1 (EXECUTED_PROPOSAL_TIMESTAMP) means the operation is already executed.
    /// @dev - any other value means timestamp in seconds when the operation will be ready for execution.
    mapping(bytes32 operationId => uint256 executionTimestamp) public timestamps;

    /// @notice The minimum delay in seconds for operations to be ready for execution.
-   uint256 public minDelay; // Removed previous declaration
```


- Affected code:
```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
42   uint256 public protocolVersion;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L42


- In the StateTransitionManager contract, the `protocolVersion` variable is declared as a `uint256`, occupying a full storage slot. However, considering that it is solely used for versioning purposes, downsizing it to a `uint64` can save on storage slot.
**Note:**
This adjustment enables packing it alongside an address variable into a single storage slot.

```diff
- uint256 public protocolVersion;
+ uint64 public protocolVersion;
```



## [G-32] Avoid fetching a low-level call's return data by using assembly
Even if you don't assign the call's second return value, it still gets copied to memory. Use assembly instead to prevent this and save 159 gas.

🔴 Affected code:
There are 3 instances of this issue:

```solidity
File: contracts/GasBoundCaller.sol
57   bytes memory returnData = EfficientCall.call(gasleft(), _to, msg.value, _data, false);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L57:57

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol
226     (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L226:226

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol
63                  (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call(
64                      abi.encodeCall(REAL_BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo, (msg.sender, to, value))
65                  );
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L63:65


## [G-33] Use hardcode address instead address(this)
it can be more gas-efficient to use a hardcoded address instead of the address(this) expression, especially if you need to use the same address multiple times in your contract.

🔴 Affected code:
There are 5 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
127  uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

131  uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

174     uint256 balanceBefore = _token.balanceOf(address(this));
        _token.safeTransferFrom(_from, address(this), _amount);
        uint256 balanceAfter = _token.balanceOf(address(this));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127


## [G-34] Duplicated `require()`/`revert()` checks should be refactored to a modifier or function

Saves deployment costs.

🔴 Affected code:
There are 3 instances of this issue:

- `require(block.timestamp >= commitBatchTimestamp + delay, "5c");` also use in line number 217
```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
195    require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195:195

- `require(_l2TokenProxyBytecodeHash != bytes32(0), "df");` also use in line number 58
- i think it should be remove it redundat check.
```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol
56     require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L56:56

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol
92     require(vInt == 27 || vInt == 28, "Invalid v value");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L92:92


## [G-35] Unused named return variables without optimizer waste gas
Consider changing the variable to be an unnamed one, since the variable is never assigned, nor is it returned by name. If the optimizer is not turned on, leaving the code as it is will also waste gas for the stack variable.

🔴 Affected code:
There are 4 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol
121         ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L121:121

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
87          function getDiamondStorage() internal pure returns (DiamondStorage storage diamondStorage) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L87:87

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol
44          function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L44:44

```solidity
File: system-contracts/contracts/ContractDeployer.sol
34          function getAccountInfo(address _address) external view returns (AccountInfo memory info) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L34:34










## [G-36] Stack variable used as a cheaper cache for a state variable is only used once
If the variable is only accessed once, it's cheaper to use the state variable directly that one time, and save the 3 gas the extra stack assignment would spend.


🔴 Affected code:
There are 13 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
342            require(dataHash == txDataHash, "ShB: d.it not hap");

325            require(proofValid, "yn");

484            require(success, "ShB withd w proof"); // withdrawal wrong proof
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L484:484

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol
56              emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

69              emit NewAdmin(previousAdmin, pendingAdmin);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69:69

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
115             emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

128             emit NewAdmin(previousAdmin, pendingAdmin);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L128:128

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
195                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

195                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

217                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

217                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L217:217

```solidity
File: system-contracts/contracts/SystemContext.sol
352                _l2BlockTimestamp >= currentBatchTimestamp,

430                 _newTimestamp > currentBlockTimestamp,
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L430:430

## [G-37] Use of emit inside a loop
Emitting an event inside a loop performs a LOG op N times, where N is the loop length. Consider refactoring the code to emit the event only once at the end of loop. Gas savings should be multiplied by the average loop length.

🔴 Affected code:
There are 3 instances of this issue:

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
261                 emit BlockCommit(

299                 emit BlockCommit(

353                 emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353:353





## [G-38] Structs should group like types together to save gas
Structs can be more gas-efficient by grouping together members of the same type. This ordering can potentially save gas.


🔴 Affected code:
There are 11 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridgehub/IBridgehub.sol
10      struct L2TransactionRequestDirect {
11          uint256 chainId;
12          uint256 mintValue;
13          address l2Contract;
14          uint256 l2Value;
15          bytes l2Calldata;
16          uint256 l2GasLimit;
17          uint256 l2GasPerPubdataByteLimit;
18          bytes[] factoryDeps;
19          address refundRecipient;
20      }

22      struct L2TransactionRequestTwoBridgesOuter {
23          uint256 chainId;
24          uint256 mintValue;
25          uint256 l2Value;
26          uint256 l2GasLimit;
27          uint256 l2GasPerPubdataByteLimit;
28          address refundRecipient;
29          address secondBridgeAddress;
30          uint256 secondBridgeValue;
31          bytes secondBridgeCalldata;
32      }

34      struct L2TransactionRequestTwoBridgesInner {
35          bytes32 magicValue;
36          address l2Contract;
37          bytes l2Calldata;
38          bytes[] factoryDeps;
39          bytes32 txDataHash;
40      }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L34:40

```solidity
File: contracts/ethereum/contracts/common/Messaging.sol
55      struct WritePriorityOpParams {
56          address sender;
57          uint256 txId;
58          uint256 l2Value;
59          address contractAddressL2;
60          uint64 expirationTimestamp;
61          uint256 l2GasLimit;
62          uint256 l2GasPrice;
63          uint256 l2GasPricePerPubdata;
64          uint256 valueToMint;
65          address refundRecipient;
66      }

127     struct BridgehubL2TransactionRequest {
128         address sender;
129         address contractL2;
130         uint256 mintValue;
131         uint256 l2Value;
132         bytes l2Calldata;
133         uint256 l2GasLimit;
134         uint256 l2GasPerPubdataByteLimit;
135         bytes[] factoryDeps;
136         address refundRecipient;
137     }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L127:137

```solidity
File: contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol
15      struct StateTransitionManagerInitializeData {
16          address governor;
17          address validatorTimelock;
18          address genesisUpgrade;
19          bytes32 genesisBatchHash;
20          uint64 genesisIndexRepeatedStorageChanges;
21          bytes32 genesisBatchCommitment;
22          Diamond.DiamondCutData diamondCut;
23          uint256 protocolVersion;
24      }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L15:24

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol
66      struct ZkSyncStateTransitionStorage {
67          /// @dev Storage of variables needed for deprecated diamond cut facet
68          uint256[7] __DEPRECATED_diamondCutStorage;
69          /// @notice Address which will exercise critical changes to the Diamond Proxy (upgrades, freezing & unfreezing). Replaced by STM
70          address __DEPRECATED_governor;
71          /// @notice Address that the governor proposed as one that will replace it
72          address __DEPRECATED_pendingGovernor;
73          /// @notice List of permitted validators
74          mapping(address validatorAddress => bool isValidator) validators;
75          /// @dev Verifier contract. Used to verify aggregated proof for batches
76          IVerifier verifier;
77          /// @notice Total number of executed batches i.e. batches[totalBatchesExecuted] points at the latest executed batch
78          /// (batch 0 is genesis)
79          uint256 totalBatchesExecuted;
80          /// @notice Total number of proved batches i.e. batches[totalBatchesProved] points at the latest proved batch
81          uint256 totalBatchesVerified;
82          /// @notice Total number of committed batches i.e. batches[totalBatchesCommitted] points at the latest committed
83          /// batch
84          uint256 totalBatchesCommitted;
85          /// @dev Stored hashed StoredBatch for batch number
86          mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
87          /// @dev Stored root hashes of L2 -> L1 logs
88          mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;
89          /// @dev Container that stores transactions requested from L1
90          PriorityQueue.Queue priorityQueue;
91          /// @dev The smart contract that manages the list with permission to call contract functions
92          address __DEPRECATED_allowList;
93          /// @notice Part of the configuration parameters of ZKP circuits. Used as an input for the verifier smart contract
94          VerifierParams verifierParams;
95          /// @notice Bytecode hash of bootloader program.
96          /// @dev Used as an input to zkp-circuit.
97          bytes32 l2BootloaderBytecodeHash;
98          /// @notice Bytecode hash of default account (bytecode for EOA).
99          /// @dev Used as an input to zkp-circuit.
100         bytes32 l2DefaultAccountBytecodeHash;
101         /// @dev Indicates that the porter may be touched on L2 transactions.
102         /// @dev Used as an input to zkp-circuit.
103         bool zkPorterIsAvailable;
104         /// @dev The maximum number of the L2 gas that a user can request for L1 -> L2 transactions
105         /// @dev This is the maximum number of L2 gas that is available for the "body" of the transaction, i.e.
106         /// without overhead for proving the batch.
107         uint256 priorityTxMaxGasLimit;
108         /// @dev Storage of variables needed for upgrade facet
109         UpgradeStorage __DEPRECATED_upgrades;
110         /// @dev A mapping L2 batch number => message number => flag.
111         /// @dev The L2 -> L1 log is sent for every withdrawal, so this mapping is serving as
112         /// a flag to indicate that the message was already processed.
113         /// @dev Used to indicate that eth withdrawal was already processed
114         mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;
115         /// @dev The most recent withdrawal time and amount reset
116         uint256 __DEPRECATED_lastWithdrawalLimitReset;
117         /// @dev The accumulated withdrawn amount during the withdrawal limit window
118         uint256 __DEPRECATED_withdrawnAmountInWindow;
119         /// @dev A mapping user address => the total deposited amount by the user
120         mapping(address => uint256) __DEPRECATED_totalDepositedAmountPerUser;
121         /// @dev Stores the protocol version. Note, that the protocol version may not only encompass changes to the
122         /// smart contracts, but also to the node behavior.
123         uint256 protocolVersion;
124         /// @dev Hash of the system contract upgrade transaction. If 0, then no upgrade transaction needs to be done.
125         bytes32 l2SystemContractsUpgradeTxHash;
126         /// @dev Batch number where the upgrade transaction has happened. If 0, then no upgrade transaction has happened
127         /// yet.
128         uint256 l2SystemContractsUpgradeBatchNumber;
129         /// @dev Address which will exercise non-critical changes to the Diamond Proxy (changing validator set & unfreezing)
130         address admin;
131         /// @notice Address that the admin proposed as one that will replace admin role
132         address pendingAdmin;
133         /// @dev Fee params used to derive gasPrice for the L1->L2 transactions. For L2 transactions,
134         /// the bootloader gives enough freedom to the operator.
135         FeeParams feeParams;
136         /// @dev Address of the blob versioned hash getter smart contract used for EIP-4844 versioned hashes.
137         address blobVersionedHashRetriever;
138         /// new fields
139         /// @dev The chainId of the chain
140         uint256 chainId;
141         /// @dev The address of the bridgehub
142         address bridgehub;
143         /// @dev The address of the StateTransitionManager
144         address stateTransitionManager;
145         /// @dev The address of the baseToken contract. Eth is address(1)
146         address baseToken;
147         /// @dev The address of the baseTokenbridge. Eth also uses the shared bridge
148         address baseTokenBridge;
149         /// @notice gasPriceMultiplier for each baseToken, so that each L1->L2 transaction pays for its transaction on the destination
150         /// we multiply by the nominator, and divide by the denominator
151         uint128 baseTokenGasPriceMultiplierNominator;
152         uint128 baseTokenGasPriceMultiplierDenominator;
153     }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L66:153

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol
25      struct InitializeData {
26          uint256 chainId;
27          address bridgehub;
28          address stateTransitionManager;
29          uint256 protocolVersion;
30          address admin;
31          address validatorTimelock;
32          address baseToken;
33          address baseTokenBridge;
34          bytes32 storedBatchZero;
35          IVerifier verifier;
36          VerifierParams verifierParams;
37          bytes32 l2BootloaderBytecodeHash;
38          bytes32 l2DefaultAccountBytecodeHash;
39          uint256 priorityTxMaxGasLimit;
40          FeeParams feeParams;
41          address blobVersionedHashRetriever;
42      }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L25:42

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol
27      struct LogProcessingOutput {
28          uint256 numberOfLayer1Txs;
29          bytes32 chainedPriorityTxsHash;
30          bytes32 previousBatchHash;
31          bytes32 pubdataHash;
32          bytes32 stateDiffHash;
33          bytes32 l2LogsTreeRoot;
34          uint256 packedBatchAndL2BlockTimestamp;
35          bytes32 blob1Hash;
36          bytes32 blob2Hash;
37      }

83          struct StoredBatchInfo {
84              uint64 batchNumber;
85              bytes32 batchHash;
86              uint64 indexRepeatedStorageChanges;
87              uint256 numberOfLayer1Txs;
88              bytes32 priorityOperationsHash;
89              bytes32 l2LogsTreeRoot;
90              uint256 timestamp;
91              bytes32 commitment;
92          }

112         struct CommitBatchInfo {
113             uint64 batchNumber;
114             uint64 timestamp;
115             uint64 indexRepeatedStorageChanges;
116             bytes32 newStateRoot;
117             uint256 numberOfLayer1Txs;
118             bytes32 priorityOperationsHash;
119             bytes32 bootloaderHeapInitialContentsHash;
120             bytes32 eventsQueueStateHash;
121             bytes systemLogs;
122             bytes pubdataCommitments;
123         }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L112:123



## [G-39] Don't compare boolean expressions to boolean literals

For cases of: `if (<x> == true)`, use `if (<x>)` instead. For cases of: `if (<x> == false)`, use `if (!<x>)` instead.

🔴 Affected code:
There are 1 instances of this issue:
```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol
68              require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68:68


## [G-40] Use selfbalance() instead of address(this).balance
it's recommended to use the selfbalance() function instead of address(this).balance. The selfbalance() function is a built-in Solidity function that returns the balance of the current contract in Wei and is considered more gas-efficient and secure.

🔴 Affected code:
There are 4 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
118  uint256 balanceBefore = address(this).balance;

120  uint256 balanceAfter = address(this).balance;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118


```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
41  uint256 amount = address(this).balance;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41


```solidity
File: system-contracts/contracts/DefaultAccount.sol
100  require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100



## [G-41] Use assembly in place of abi.decode to extract calldata values more efficiently
Instead of using abi.decode, we can use assembly to decode our desired calldata values directly. This will allow us to avoid decoding calldata values that we will not use.
[Reffrence](https://code4rena.com/reports/2023-05-juicebox#g-04-use-assembly-in-place-of-abidecode-to-extract-calldata-values-more-efficiently)

🔴 Affected code:
There are 10 instances of this issue:

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol
190  (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L190


```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
252   Diamond.DiamondCutData memory diamondCut = abi.decode(_diamondCut, (Diamond.DiamondCutData));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L252


```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol
617  (, uint256 result) = abi.decode(data, (uint256, uint256));

682   versionedHash = abi.decode(data, (bytes32));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L617


```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
292  require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L292


```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol
177  proxy = BeaconProxy(abi.decode(returndata, (address)));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L177


```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol
57  (bytes memory nameBytes, bytes memory symbolBytes, bytes memory decimalsBytes) = abi.decode(

179  (result) = abi.decode(_input, (string));

184   (result) = abi.decode(_input, (uint8));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L57


```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol
337  (address token, uint256 minAllowance) = abi.decode(_transaction.paymasterInput[4:68], (address, uint256));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L337



## [G‑42] "" has the same value as new bytes(0) but costs less gas
In Solidity, new bytes(0) and "" both represent an empty byte array. However, "" is more gas-efficient than new bytes(0) This is because "" is a literal and is stored in the code, whereas new bytes(0) is a dynamic allocation that requires the creation of a new memory location at runtime

🔴 Affected code:
There are 8 instances of this issue:

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
196                 signature: new bytes(0),

198                 paymasterInput: new bytes(0),

199                 reservedDynamic: new bytes(0)

213                 l1ContractsUpgradeCalldata: new bytes(0),

214                 postUpgradeCalldata: new bytes(0),
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L214:214

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol
308                 signature: new bytes(0),

310                 paymasterInput: new bytes(0),

311                 reservedDynamic: new bytes(0)
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L311:311


## [G-43] State variables only set in their definitions should be declared constant
Avoids a Gsset (20000 gas) at deployment, and replaces the first access in each transaction (Gcoldsload - 2100 gas) and each access thereafter (Gwarmacces - 100 gas) with a PUSH32 (3 gas).

🔴 Affected code:
There are 3 instances of this issue:

```solidity
File: system-contracts/contracts/SystemContext.sol
37          uint256 public blockGasLimit = type(uint32).max;

41          address public coinbase = BOOTLOADER_FORMAL_ADDRESS;

44          uint256 public difficulty = 2.5e15;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L44:44


## [G-44] Fewer storage slots can be used by storing timestamps in types smaller than uint256
Ethereum's block.timestamp can be stored in a type smaller than uint256.   A uint32 variable can store a timestamp until year 2106.

🔴 Affected code:
There are 3 instances of this issue:

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol
34          uint256 packedBatchAndL2BlockTimestamp;

90              uint256 timestamp;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L90:90

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
37          uint256 upgradeTimestamp;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L37:37


## [G-45] Storage re-read via storage pointer
The instances below point to the second+ access of a state variable, via a storage pointer, within a function. Caching the value replaces each Gwarmaccess (100 gas) with a much cheaper stack read.

🔴 Affected code:
There are 2 instances of this issue:

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol
91              return state == OperationState.Waiting || state == OperationState.Ready;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L91:91

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
113                 } else if (action == Action.Remove) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L113:113

## [G-46] `keccak256()` should only need to be called on a specific string literal once
It should be saved to an immutable variable, and the variable used instead. If the hash is being used as a part of a function selector, the cast to `bytes4` should also only be done once.


🔴 Affected code:
There are 4 instances of this issue:

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol
85              keccak256(
86                  "Transaction(uint256 txType,uint256 from,uint256 to,uint256 gasLimit,uint256 gasPerPubdataByteLimit,uint256 maxFeePerGas,uint256 maxPriorityFeePerGas,uint256 paymaster,uint256 nonce,uint256 value,bytes data,bytes32[] factoryDeps,bytes paymasterInput)"
87              );

85              keccak256(
86                  "Transaction(uint256 txType,uint256 from,uint256 to,uint256 gasLimit,uint256 gasPerPubdataByteLimit,uint256 maxFeePerGas,uint256 maxPriorityFeePerGas,uint256 paymaster,uint256 nonce,uint256 value,bytes data,bytes32[] factoryDeps,bytes paymasterInput)"
87              );

139                 abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

139                 abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139:139


## [G-47] Private functions used once can be inlined

Private functions used once can be inlined to save GAS


🔴 Affected code:
There are 6 instances of this issue:

```solidity
File: contracts/ethereum/contracts/common/ReentrancyGuard.sol
46          function _initializeReentrancyGuard() private {
47              uint256 lockSlotOldValue;
48      
49              // Storing an initial non-zero value makes deployment a bit more
50              // expensive but in exchange every call to nonReentrant
51              // will be cheaper.
52              assembly {
53                  lockSlotOldValue := sload(LOCK_FLAG_ADDRESS)
54                  sstore(LOCK_FLAG_ADDRESS, _NOT_ENTERED)
55              }
56      
57              // Check that storage slot for reentrancy guard is empty to rule out possibility of slot conflict
58              require(lockSlotOldValue == 0, "1B");
59          }
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L46:59

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
92          function _setL2DefaultAccountBytecodeHash(bytes32 _l2DefaultAccountBytecodeHash) private {
93              if (_l2DefaultAccountBytecodeHash == bytes32(0)) {
94                  return;
95              }
96      
97              L2ContractHelper.validateBytecodeHash(_l2DefaultAccountBytecodeHash);
98      
99              // Save previous value into the stack to put it into the event later
100             bytes32 previousDefaultAccountBytecodeHash = s.l2DefaultAccountBytecodeHash;
101     
102             // Change the default account bytecode hash
103             s.l2DefaultAccountBytecodeHash = _l2DefaultAccountBytecodeHash;
104             emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);
105         }


109         function _setL2BootloaderBytecodeHash(bytes32 _l2BootloaderBytecodeHash) private {
110             if (_l2BootloaderBytecodeHash == bytes32(0)) {
111                 return;
112             }
113     
114             L2ContractHelper.validateBytecodeHash(_l2BootloaderBytecodeHash);
115     
116             // Save previous value into the stack to put it into the event later
117             bytes32 previousBootloaderBytecodeHash = s.l2BootloaderBytecodeHash;
118     
119             // Change the bootloader bytecode hash
120             s.l2BootloaderBytecodeHash = _l2BootloaderBytecodeHash;
121             emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);
122         }


126         function _setVerifier(IVerifier _newVerifier) private {
127             // An upgrade to the verifier must be done carefully to ensure there aren't batches in the committed state
128             // during the transition. If verifier is upgraded, it will immediately be used to prove all committed batches.
129             // Batches committed expecting the old verifier will fail. Ensure all commited batches are finalized before the
130             // verifier is upgraded.
131             if (_newVerifier == IVerifier(address(0))) {
132                 return;
133             }
134     
135             IVerifier oldVerifier = s.verifier;
136             s.verifier = _newVerifier;
137             emit NewVerifier(address(oldVerifier), address(_newVerifier));
138         }


142         function _setVerifierParams(VerifierParams calldata _newVerifierParams) private {
143             // An upgrade to the verifier params must be done carefully to ensure there aren't batches in the committed state
144             // during the transition. If verifier is upgraded, it will immediately be used to prove all committed batches.
145             // Batches committed expecting the old verifier params will fail. Ensure all commited batches are finalized before the
146             // verifier is upgraded.
147             if (
148                 _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) &&
149                 _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) &&
150                 _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)
151             ) {
152                 return;
153             }
154     
155             VerifierParams memory oldVerifierParams = s.verifierParams;
156             s.verifierParams = _newVerifierParams;
157             emit NewVerifierParams(oldVerifierParams, _newVerifierParams);
158         }


222         function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure {
223             require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");
224             require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");
225     
226             for (uint256 i = 0; i < _factoryDeps.length; ++i) {
227                 require(
228                     L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
229                     "Wrong factory dep hash"
230                 );
231             }
232         }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L222:232


## [G-48] >=/<= costs less gas than >/<
The compiler uses opcodes GT and ISZERO for code that uses >, but only requires LT for >=. A similar behaviour applies for >, which uses opcodes LT and ISZERO, but only requires GT for <=.
[Reffrence](https://gist.github.com/CloudEllie/05fda0fdecba2ed7d85f68c709e46c8d#gas-18--costs-less-gas-than-)

🔴 Affected code:
There are 3 instances of this issue:

```solidity
File: contracts/GasBoundCaller.sol
49              uint256 pubdataAllowance = _maxTotalGas > expectedForCompute ? _maxTotalGas - expectedForCompute : 0;

63              uint256 pubdataSpent = pubdataPublishedAfter > pubdataPublishedBefore
64                  ? pubdataPublishedAfter - pubdataPublishedBefore
65                  : 0;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L63:65

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol
53              uint256 userGas = gasInContext > MSG_VALUE_SIMULATOR_STIPEND_GAS
54                  ? gasInContext - MSG_VALUE_SIMULATOR_STIPEND_GAS
55                  : 0;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L53:55


## [G-49] Assigning state variables directly with named struct constructors wastes gas
Using named arguments for struct means that the compiler needs to organize the fields in memory before doing the assignment, which wastes gas. Set each field directly in storage (use dot-notation), or use the unnamed version of the constructor.

🔴 Affected code:
There are 1 instances of this issue:

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
218             ds.selectorToFacet[_selector] = SelectorToFacet({
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L218:218


## [G-50] Most important: avoid zero to one storage writes where possible
Initializing a storage variable is one of the most expensive operations a contract can do.
When a storage variable goes from zero to non-zero, the user must pay 22,100 gas total (20,000 gas for a zero to non-zero write and 2,100 for a cold storage access).
This is why the Openzeppelin reentrancy guard registers functions as active or not with 1 and 2 rather than 0 and 1. It only costs 5,000 gas to alter a storage variable from non-zero to non-zero.

🔴 Affected code:
There are 2 instances of this issue:

```solidity
File: system-contracts/contracts/L1Messenger.sol
330  numberOfLogsToProcess = 0;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L330

```solidity
File: system-contracts/contracts/SystemContext.sol
487   txNumberInBlock = 0;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L487


## [G-51] Instead of counting down in for statements, count up
Counting down is more gas efficient than counting up because neither we are making zero variable to non-zero variable and also we will get gas refund in the last transaction when making non-zero to zero variable.