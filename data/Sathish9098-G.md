# GAS OPTIMIZATIONS

##

## [G-] State variables can be packed into fewer storage slots

The EVM works with 32 byte words. Variables less than 32 bytes can be declared next to each other in storage and this will pack the values together into a single 32 byte storage slot (if the values combined are <= 32 bytes). If the variables packed together are retrieved together in functions we will effectively save ~2000 gas with every subsequent SLOAD for that storage slot. This is due to us incurring a Gwarmaccess (100 gas) versus a Gcoldsload (2100 gas).

### ``securityCouncil`` and ``minDelay`` can be packed same Slot 

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

##

## [G-]  Cache ``sharedBridge`` Storage variable to reduce redundant access

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

##







