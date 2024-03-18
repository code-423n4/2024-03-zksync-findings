# GAS OPTIMIZATIONS

##

## [G-1] l2BridgeAddress[_chainId] mapping can be cached 

 ``l2BridgeAddress[_chainId]`` is a mapping that is accessed multiple times within a function.Caching this mapping could indeed be beneficial for optimizing gas usage. Saves ``100 GAS`` , ``1 LOAD``

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

