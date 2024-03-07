
### Consider implementing two-step procedure for updating protocol addresses
Implementing a two-step procedure for updating protocol addresses adds an extra layer of security. In such a system, the first step initiates the change, and the second step, after a predefined delay, confirms and finalizes it. This delay allows stakeholders or monitoring tools to observe and react to unintended or malicious changes. If an unauthorized change is detected, corrective actions can be taken before the change is finalized. To achieve this, introduce a "proposed address" state variable and a "delay period". Upon an update request, set the "proposed address". After the delay, if not contested, the main protocol address can be updated.

```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

114:        pendingAdmin = _newPendingAdmin;	// @audit-issue

133:        validatorTimelock = _validatorTimelock;	// @audit-issue

234:        stateTransition[_chainId] = _stateTransitionContract;	// @audit-issue
```
[114](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L114-L114), [133](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L133-L133), [234](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L234-L234), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

74:        stateTransitionManager = _stateTransitionManager;	// @audit-issue
```
[74](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L74-L74), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

27:        s.pendingAdmin = _newPendingAdmin;	// @audit-issue
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L27-L27), 


```solidity
Path: ./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

136:        s.verifier = _newVerifier;	// @audit-issue
```
[136](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L136-L136), 


```solidity
Path: ./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

55:        pendingAdmin = _newPendingAdmin;	// @audit-issue

109:        sharedBridge = IL1SharedBridge(_sharedBridge);	// @audit-issue

134:        stateTransitionManager[_chainId] = _stateTransitionManager;	// @audit-issue

135:        baseToken[_chainId] = _baseToken;	// @audit-issue
```
[55](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55-L55), [109](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L109-L109), [134](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134-L134), [135](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L135-L135), 


```solidity
Path: ./code/contracts/ethereum/contracts/governance/Governance.sol

258:        securityCouncil = _newSecurityCouncil;	// @audit-issue
```
[258](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L258-L258), 


```solidity
Path: ./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

133:            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;	// @audit-issue

143:        l2BridgeAddress[_chainId] = _l2BridgeAddress;	// @audit-issue
```
[133](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133-L133), [143](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L143-L143), 


```solidity
Path: ./code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

52:        l2Bridge = _l2Bridge;	// @audit-issue

53:        l1Address = _l1Address;	// @audit-issue
```
[52](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L52-L52), [53](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L53-L53), 


```solidity
Path: ./code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

52:        l1Address = _l1Address;	// @audit-issue
```
[52](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L52-L52), 


```solidity
Path: ./code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

99:            l1TokenAddress[expectedL2Token] = _l1Token;	// @audit-issue
```
[99](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L99-L99), 


```solidity
Path: ./code/system-contracts/contracts/SystemContext.sol

100:        origin = _newOrigin;	// @audit-issue
```
[100](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L100-L100), 


#### Recommendation

Introduce two state variables in your contract: one to hold the proposed new address (`address public proposedAddress`) and another to timestamp the proposal (`uint public addressChangeInitiated`). Implement two functions: one to propose a new address, recording the current timestamp, and another to finalize the address change after the delay period has elapsed.



### Missing checks for `address(0)`
In Solidity, the Ethereum address `0x0000000000000000000000000000000000000000` is known as the "zero address". This address has significance because it's the default value for uninitialized address variables and is often used to represent an invalid or non-existent address. The "
Missing zero address control" issue arises when a Solidity smart contract does not properly check or prevent interactions with the zero address, leading to unintended behavior.
For instance, a contract might allow tokens to be sent to the zero address without any checks, which essentially burns those tokens as they become irretrievable. While sometimes this is intentional, without proper control or checks, accidental transfers could occur.    
        

```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

59:        bridgehub = _bridgehub;	// @audit-issue
```
[59](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L59-L59), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

30:        s.chainId = _initializeData.chainId;	// @audit-issue

31:        s.bridgehub = _initializeData.bridgehub;	// @audit-issue

32:        s.stateTransitionManager = _initializeData.stateTransitionManager;	// @audit-issue

33:        s.baseToken = _initializeData.baseToken;	// @audit-issue

34:        s.baseTokenBridge = _initializeData.baseTokenBridge;	// @audit-issue

35:        s.protocolVersion = _initializeData.protocolVersion;	// @audit-issue

37:        s.verifier = _initializeData.verifier;	// @audit-issue

38:        s.admin = _initializeData.admin;	// @audit-issue

41:        s.storedBatchHashes[0] = _initializeData.storedBatchZero;	// @audit-issue

42:        s.verifierParams = _initializeData.verifierParams;	// @audit-issue

43:        s.l2BootloaderBytecodeHash = _initializeData.l2BootloaderBytecodeHash;	// @audit-issue

44:        s.l2DefaultAccountBytecodeHash = _initializeData.l2DefaultAccountBytecodeHash;	// @audit-issue

45:        s.priorityTxMaxGasLimit = _initializeData.priorityTxMaxGasLimit;	// @audit-issue

46:        s.feeParams = _initializeData.feeParams;	// @audit-issue

47:        s.blobVersionedHashRetriever = _initializeData.blobVersionedHashRetriever;	// @audit-issue
```
[30](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L30-L30), [31](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L31-L31), [32](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L32-L32), [33](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L33-L33), [34](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L34-L34), [35](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L35-L35), [37](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L37-L37), [38](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L38-L38), [41](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L41-L41), [42](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L42-L42), [43](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L43-L43), [44](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L44-L44), [45](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L45-L45), [46](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L46-L46), [47](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L47-L47), 


```solidity
Path: ./code/contracts/ethereum/contracts/governance/Governance.sol

46:        securityCouncil = _securityCouncil;	// @audit-issue
```
[46](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L46-L46), 


```solidity
Path: ./code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

56:        sharedBridge = _sharedBridge;	// @audit-issue
```
[56](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L56-L56), 


```solidity
Path: ./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

96:        l1WethAddress = _l1WethAddress;	// @audit-issue

97:        bridgehub = _bridgehub;	// @audit-issue

98:        legacyBridge = _legacyBridge;	// @audit-issue
```
[96](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L96-L96), [97](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L97-L97), [98](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L98-L98), 


```solidity
Path: ./code/system-contracts/contracts/test-contracts/SystemCaller.sol

16:        to = _to;	// @audit-issue
```
[16](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/test-contracts/SystemCaller.sol#L16-L16), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

114:        pendingAdmin = _newPendingAdmin;	// @audit-issue

133:        validatorTimelock = _validatorTimelock;	// @audit-issue

234:        stateTransition[_chainId] = _stateTransitionContract;	// @audit-issue
```
[114](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L114-L114), [133](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L133-L133), [234](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L234-L234), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

74:        stateTransitionManager = _stateTransitionManager;	// @audit-issue
```
[74](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L74-L74), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

27:        s.pendingAdmin = _newPendingAdmin;	// @audit-issue
```
[27](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L27-L27), 


```solidity
Path: ./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

55:        pendingAdmin = _newPendingAdmin;	// @audit-issue

109:        sharedBridge = IL1SharedBridge(_sharedBridge);	// @audit-issue

134:        stateTransitionManager[_chainId] = _stateTransitionManager;	// @audit-issue

135:        baseToken[_chainId] = _baseToken;	// @audit-issue
```
[55](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55-L55), [109](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L109-L109), [134](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134-L134), [135](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L135-L135), 


```solidity
Path: ./code/contracts/ethereum/contracts/governance/Governance.sol

258:        securityCouncil = _newSecurityCouncil;	// @audit-issue
```
[258](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L258-L258), 


```solidity
Path: ./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

143:        l2BridgeAddress[_chainId] = _l2BridgeAddress;	// @audit-issue
```
[143](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L143-L143), 


```solidity
Path: ./code/system-contracts/contracts/SystemContext.sol

100:        origin = _newOrigin;	// @audit-issue
```
[100](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L100-L100), 

#### Recommendation

It is strongly recommended to implement checks to prevent the zero address from being set during the initialization of contracts. This can be achieved by adding require statements that ensure address parameters are not the zero address. 

### Do not allow fees to be set to `100%`
It is recommended from a risk perspective to disallow setting 100% fees at all. A reasonable fee maximum should be checked for instead.

```solidity
Path: ./code/system-contracts/contracts/SystemContext.sol

463:        baseFee = _baseFee;	// @audit-issue

479:        baseFee = _baseFee;	// @audit-issue
```
[463](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L463-L463), [479](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L479-L479), 


#### Recommendation

Implement strict validation checks in your smart contract's fee-setting functions to ensure that fees cannot be configured to 100%. Define a maximum allowable fee percentage that preserves the contract's functionality and user experience, such as 10% or 20%, depending on your project's specific requirements and economic model. For example:
```solidity
function setTransactionFee(uint256 newFeePercentage) public onlyOwner {
    require(newFeePercentage <= 20, "Fee cannot exceed 20%");
    transactionFee = newFeePercentage;
}
```

### Gas griefing/theft is possible on an unsafe external call
A low-level call will copy any amount of bytes to local memory. When bytes are copied from returndata to memory, the memory expansion cost is paid.

This means that when using a standard solidity call, the callee can 'returnbomb' the caller, imposing an arbitrary gas cost.

Because this gas is paid by the caller and in the caller's context, it can cause the caller to run out of gas and halt execution.

Consider replacing all unsafe `call` with `excessivelySafeCall` from this [repository](https://github.com/nomad-xyz/ExcessivelySafeCall).


```solidity
Path: ./code/contracts/ethereum/contracts/dev-contracts/ConstructorForwarder.sol

10:        (bool success, ) = payable(to).call{value: msg.value}(data);	// @audit-issue
```
[10](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/dev-contracts/ConstructorForwarder.sol#L10-L10), 


```solidity
Path: ./code/contracts/ethereum/contracts/dev-contracts/Forwarder.sol

11:        (success, returnValue) = payable(to).call{value: msg.value}(data);	// @audit-issue
```
[11](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/dev-contracts/Forwarder.sol#L11-L11), 


```solidity
Path: ./code/contracts/zksync/contracts/TestnetPaymaster.sol

63:            (bool success, ) = payable(BOOTLOADER_ADDRESS).call{value: requiredETH}("");	// @audit-issue
```
[63](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/zksync/contracts/TestnetPaymaster.sol#L63-L63), 


```solidity
Path: ./code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

108:        (bool success, ) = _to.call{value: _amount}("");	// @audit-issue
```
[108](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L108-L108), 


```solidity
Path: ./code/system-contracts/contracts/MsgValueSimulator.sol

63:            (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call(	// @audit-issue
```
[63](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/MsgValueSimulator.sol#L63-L63), 


```solidity
Path: ./code/system-contracts/contracts/GasBoundCaller.sol

57:        bytes memory returnData = EfficientCall.call(gasleft(), _to, msg.value, _data, false);	// @audit-issue
```
[57](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/GasBoundCaller.sol#L57-L57), 


```solidity
Path: ./code/system-contracts/contracts/openzeppelin/utils/Address.sol

66:        (bool success, ) = recipient.call{value: amount}("");	// @audit-issue

159:        (bool success, bytes memory returndata) = target.call{value: value}(	// @audit-issue
```
[66](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/openzeppelin/utils/Address.sol#L66-L66), [159](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/openzeppelin/utils/Address.sol#L159-L159), 


#### Recommendation

Mitigate the risk of gas griefing by replacing direct low-level calls (`call`, `delegatecall`, etc.) with `excessivelySafeCall`, a utility that limits the amount of gas used for copying return data, thereby preventing return bombing. The `excessivelySafeCall` function, available in certain security-focused repositories such as [nomad-xyz/ExcessivelySafeCall](https://github.com/nomad-xyz/ExcessivelySafeCall), implements additional checks to ensure that the callee cannot impose arbitrary gas costs on the caller. To incorporate this into your contract:

1. Review your contract for external calls to untrusted contracts.
2. Import or implement an `excessivelySafeCall` utility in your contract.
3. Replace unsafe external calls with `excessivelySafeCall`, specifying limits on return data size as appropriate for your application.

Example usage:
```solidity
// Assuming excessivelySafeCall is available in your contract
(bool success, ) = target.excessivelySafeCall(gasLimit, callData, maxReturnSize);
require(success, "External call failed");

This approach not only protects against gas griefing attacks but also enhances the overall security posture of your contract by ensuring that external interactions do not lead to unexpected execution halts or excessive gas consumption. Always perform thorough testing after integrating `excessivelySafeCall` to ensure compatibility and intended functionality.


### Use Of `transfer` or `send` Instead Of `call` To Send Native Assets
The use of `transfer()` in the contracts may have unintended outcomes on the native asset being sent to the receiver. The transaction will fail when:

- The receiver address is a smart contract that does not implement a payable function.
- The receiver address is a smart contract that implements a payable fallback function which uses more than 2300 gas units.
- The receiver address is a smart contract that implements a payable fallback function that needs less than 2300 gas units but is called through proxy, raising the call's gas usage above 2300.
- Additionally, using a gas value higher than 2300 might be mandatory for some multi-signature wallets.




```solidity
Path: ./code/contracts/ethereum/contracts/dev-contracts/WETH9.sol

33:        payable(msg.sender).transfer(wad);	// @audit-issue
```
[33](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/dev-contracts/WETH9.sol#L33-L33), 


```solidity
Path: ./code/system-contracts/contracts/test-contracts/TransferTest.sol

12:        to.transfer(amount);	// @audit-issue

21:        bool success = to.send(amount);	// @audit-issue
```
[12](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/test-contracts/TransferTest.sol#L12-L12), [21](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/test-contracts/TransferTest.sol#L21-L21), 


#### Recommendation


To transfer, a native asset is recommended to either use:

- `<receiver>.call.value(amount)`
- [OpenZeppelin Address.sendValue()](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v2.5.1/contracts/utils/Address.sol#L63-L69)

In both cases, care must be taken not to create reentrancy vulnerabilities. Consider using ReentrancyGuard or the [Check-Effects-Interactions pattern](https://docs.soliditylang.org/en/latest/security-considerations.html#use-the-checks-effects-interactions-pattern).



### Use of `ecrecover` is susceptible to signature malleability
The built-in EVM precompile `ecrecover` is susceptible to signature malleability, which could lead to [replay attacks](https://medium.com/cryptronics/signature-replay-vulnerabilities-in-smart-contracts-3b6f7596df57).

Consider using OpenZeppelin’s [ECDSA library](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/cryptography/ECDSA.sol#L125-L128) instead of the built-in function.

```solidity
Path: ./code/system-contracts/contracts/DefaultAccount.sol

186:        address recoveredAddress = ecrecover(_hash, v, r, s);	// @audit-issue
```
[186](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/DefaultAccount.sol#L186-L186), 


#### Recommendation

To enhance the security of your Solidity smart contracts and mitigate the risk of signature malleability attacks, it is advisable to use OpenZeppelin's [ECDSA library](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/cryptography/ECDSA.sol#L125-L128) instead of the built-in `ecrecover` function. The ECDSA library provides robust and reliable signature verification, reducing the vulnerability to replay attacks and ensuring the integrity of your contract interactions.


### Division in comparison
To ensure accuracy in comparisons within programming, especially when dealing with integers, it's often more efficient to use multiplication rather than division. This approach stems from the fact that division operations are generally slower and more complex than multiplication. And in the context of solidity they can cause precision errors.

Suppose you want to compare if a/b is greater than c/d (where a, b, c, and d are integers). Instead of performing division, which is prone to precision errors, you can cross-multiply to avoid division. The comparison a/b > c/d is equivalent to ad > bc. This way, you only use multiplication, which is faster and avoids potential inaccuracies or complexities associated with division.

```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

30:        require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");	// @audit-issue
```
[30](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L30-L30), 


#### Recommendation

When comparing ratios or fractions in Solidity, avoid direct division operations within the comparison. Instead, cross-multiply to maintain precision and reduce computational complexity. For example, to compare if `a/b` is greater than `c/d`, where `a`, `b`, `c`, and `d` are integers, reframe the comparison as `a * d > b * c`. This approach avoids the division entirely, eliminating the risk of precision loss due to integer division truncation. Additionally, this method is more gas-efficient, as multiplication operations are cheaper than division. Apply this strategy in all relevant comparisons to enhance the accuracy and performance of your smart contracts. Always test thoroughly to ensure that the logic remains correct after the transformation.


### Ownership Irrevocability Vulnerability
The smart contract under inspection inherits from the `Ownable` library, which provides basic authorization control functions, simplifying the implementation of user permissions. However, the contract does not provide a mechanism to transfer ownership to another address or account, and it retains the default `renounceOwnership` function from `Ownable`.  
Given this, once the owner renounces ownership using the `renounceOwnership` function, the contract becomes ownerless. As evidenced in the provided transaction logs, after the `renounceOwnership` function is called, attempts to call functions that require owner permissions fail with the error message: `"Ownable: caller is not the owner."`  
This state renders the contract's adjustable parameters immutable and potentially makes the contract useless for any future administrative changes that might be necessary.

```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

25:contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {	// @audit-issue
```
[25](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L25-L25), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

22:contract ValidatorTimelock is IExecutor, Ownable2Step {	// @audit-issue
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L22-L22), 


```solidity
Path: ./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

16:contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {	// @audit-issue
```
[16](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L16-L16), 


```solidity
Path: ./code/contracts/ethereum/contracts/governance/Governance.sol

20:contract Governance is IGovernance, Ownable2Step {	// @audit-issue
```
[20](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L20-L20), 


```solidity
Path: ./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

30:contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {	// @audit-issue
```
[30](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L30-L30), 


#### Recommendation


To mitigate this vulnerability:
* Override the renounceOwnership function to revert transactions: By overriding this function to simply revert any transaction, it will become impossible for the contract owner to unintentionally (or intentionally) render the contract ownerless and thus immutable.
* Implement an ownership transfer function: While the Ownable library does provide a transferOwnership function, if this is not present or has been removed from the current contract, it should be re-implemented to ensure there is a way to transfer ownership in future scenarios.


### Unused import
The identifier is imported but never used within the file.

```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

19:import {REQUIRED_L2_GAS_PRICE_PER_PUBDATA, L2_TO_L1_LOG_SERIALIZE_SIZE, DEFAULT_L2_LOGS_TREE_ROOT_HASH, EMPTY_STRING_KECCAK, SYSTEM_UPGRADE_L2_TX_TYPE, ERA_DIAMOND_PROXY, ERA_CHAIN_ID} from "../common/Config.sol";	// @audit-issue: ERA_DIAMOND_PROXY not used in the contract.

19:import {REQUIRED_L2_GAS_PRICE_PER_PUBDATA, L2_TO_L1_LOG_SERIALIZE_SIZE, DEFAULT_L2_LOGS_TREE_ROOT_HASH, EMPTY_STRING_KECCAK, SYSTEM_UPGRADE_L2_TX_TYPE, ERA_DIAMOND_PROXY, ERA_CHAIN_ID} from "../common/Config.sol";	// @audit-issue: ERA_CHAIN_ID not used in the contract.
```
[19](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L19-L19), [19](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L19-L19), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol

5:import {L2CanonicalTransaction} from "../../common/Messaging.sol";	// @audit-issue: L2CanonicalTransaction not used in the contract.
```
[5](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L5-L5), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol

9:import {Verifier} from "../Verifier.sol";	// @audit-issue: Verifier not used in the contract.

10:import {VerifierParams} from "./IVerifier.sol";	// @audit-issue: VerifierParams not used in the contract.
```
[9](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L9-L9), [10](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L10-L10), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

7:import {FeeParams} from "./ZkSyncStateTransitionStorage.sol";	// @audit-issue: FeeParams not used in the contract.

10:import {VerifierParams} from "../chain-interfaces/IVerifier.sol";	// @audit-issue: VerifierParams not used in the contract.
```
[7](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L7-L7), [10](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L10-L10), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

13:import {IZkSyncStateTransitionBase} from "../../chain-interfaces/IZkSyncStateTransitionBase.sol";	// @audit-issue: IZkSyncStateTransitionBase not used in the contract.
```
[13](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L13-L13), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

17:import {IZkSyncStateTransitionBase} from "../../chain-interfaces/IZkSyncStateTransitionBase.sol";	// @audit-issue: IZkSyncStateTransitionBase not used in the contract.
```
[17](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L17-L17), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

15:import {IZkSyncStateTransitionBase} from "../../chain-interfaces/IZkSyncStateTransitionBase.sol";	// @audit-issue: IZkSyncStateTransitionBase not used in the contract.
```
[15](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L15-L15), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

14:import {UnsafeBytes} from "../../../common/libraries/UnsafeBytes.sol";	// @audit-issue: UnsafeBytes not used in the contract.

19:import {L2_BOOTLOADER_ADDRESS, L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, L2_BASE_TOKEN_SYSTEM_CONTRACT_ADDR} from "../../../common/L2ContractAddresses.sol";	// @audit-issue: L2_BASE_TOKEN_SYSTEM_CONTRACT_ADDR not used in the contract.

21:import {IBridgehub} from "../../../bridgehub/IBridgehub.sol";	// @audit-issue: IBridgehub not used in the contract.

25:import {IZkSyncStateTransitionBase} from "../../chain-interfaces/IZkSyncStateTransitionBase.sol";	// @audit-issue: IZkSyncStateTransitionBase not used in the contract.
```
[14](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L14-L14), [19](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L19-L19), [21](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L21-L21), [25](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L25-L25), 


```solidity
Path: ./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

6:import {IMailbox} from "../state-transition/chain-interfaces/IMailbox.sol";	// @audit-issue: IMailbox not used in the contract.
```
[6](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L6-L6), 


```solidity
Path: ./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

11:import {MAX_NEW_FACTORY_DEPS, SYSTEM_UPGRADE_L2_TX_TYPE, MAX_ALLOWED_PROTOCOL_VERSION_DELTA} from "../common/Config.sol";	// @audit-issue: MAX_NEW_FACTORY_DEPS not used in the contract.

11:import {MAX_NEW_FACTORY_DEPS, SYSTEM_UPGRADE_L2_TX_TYPE, MAX_ALLOWED_PROTOCOL_VERSION_DELTA} from "../common/Config.sol";	// @audit-issue: SYSTEM_UPGRADE_L2_TX_TYPE not used in the contract.
```
[11](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L11-L11), [11](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L11-L11), 


```solidity
Path: ./code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

15:import {L2ContractHelper, DEPLOYER_SYSTEM_CONTRACT, L2_BASE_TOKEN_ADDRESS, IContractDeployer} from "../L2ContractHelper.sol";	// @audit-issue: L2_BASE_TOKEN_ADDRESS not used in the contract.

17:import {ERA_CHAIN_ID, ERA_WETH_ADDRESS} from "../Config.sol";	// @audit-issue: ERA_WETH_ADDRESS not used in the contract.
```
[15](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L15-L15), [17](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L17-L17), 


```solidity
Path: ./code/system-contracts/contracts/Compressor.sol

10:import {L1_MESSENGER_CONTRACT, INITIAL_WRITE_STARTING_POSITION, COMPRESSED_INITIAL_WRITE_SIZE, STATE_DIFF_ENTRY_SIZE, STATE_DIFF_ENUM_INDEX_OFFSET, STATE_DIFF_FINAL_VALUE_OFFSET, STATE_DIFF_DERIVED_KEY_OFFSET, DERIVED_KEY_LENGTH, VALUE_LENGTH, ENUM_INDEX_LENGTH, KNOWN_CODE_STORAGE_CONTRACT} from "./Constants.sol";	// @audit-issue: INITIAL_WRITE_STARTING_POSITION not used in the contract.

10:import {L1_MESSENGER_CONTRACT, INITIAL_WRITE_STARTING_POSITION, COMPRESSED_INITIAL_WRITE_SIZE, STATE_DIFF_ENTRY_SIZE, STATE_DIFF_ENUM_INDEX_OFFSET, STATE_DIFF_FINAL_VALUE_OFFSET, STATE_DIFF_DERIVED_KEY_OFFSET, DERIVED_KEY_LENGTH, VALUE_LENGTH, ENUM_INDEX_LENGTH, KNOWN_CODE_STORAGE_CONTRACT} from "./Constants.sol";	// @audit-issue: COMPRESSED_INITIAL_WRITE_SIZE not used in the contract.

10:import {L1_MESSENGER_CONTRACT, INITIAL_WRITE_STARTING_POSITION, COMPRESSED_INITIAL_WRITE_SIZE, STATE_DIFF_ENTRY_SIZE, STATE_DIFF_ENUM_INDEX_OFFSET, STATE_DIFF_FINAL_VALUE_OFFSET, STATE_DIFF_DERIVED_KEY_OFFSET, DERIVED_KEY_LENGTH, VALUE_LENGTH, ENUM_INDEX_LENGTH, KNOWN_CODE_STORAGE_CONTRACT} from "./Constants.sol";	// @audit-issue: STATE_DIFF_ENUM_INDEX_OFFSET not used in the contract.

10:import {L1_MESSENGER_CONTRACT, INITIAL_WRITE_STARTING_POSITION, COMPRESSED_INITIAL_WRITE_SIZE, STATE_DIFF_ENTRY_SIZE, STATE_DIFF_ENUM_INDEX_OFFSET, STATE_DIFF_FINAL_VALUE_OFFSET, STATE_DIFF_DERIVED_KEY_OFFSET, DERIVED_KEY_LENGTH, VALUE_LENGTH, ENUM_INDEX_LENGTH, KNOWN_CODE_STORAGE_CONTRACT} from "./Constants.sol";	// @audit-issue: STATE_DIFF_FINAL_VALUE_OFFSET not used in the contract.

10:import {L1_MESSENGER_CONTRACT, INITIAL_WRITE_STARTING_POSITION, COMPRESSED_INITIAL_WRITE_SIZE, STATE_DIFF_ENTRY_SIZE, STATE_DIFF_ENUM_INDEX_OFFSET, STATE_DIFF_FINAL_VALUE_OFFSET, STATE_DIFF_DERIVED_KEY_OFFSET, DERIVED_KEY_LENGTH, VALUE_LENGTH, ENUM_INDEX_LENGTH, KNOWN_CODE_STORAGE_CONTRACT} from "./Constants.sol";	// @audit-issue: STATE_DIFF_DERIVED_KEY_OFFSET not used in the contract.

10:import {L1_MESSENGER_CONTRACT, INITIAL_WRITE_STARTING_POSITION, COMPRESSED_INITIAL_WRITE_SIZE, STATE_DIFF_ENTRY_SIZE, STATE_DIFF_ENUM_INDEX_OFFSET, STATE_DIFF_FINAL_VALUE_OFFSET, STATE_DIFF_DERIVED_KEY_OFFSET, DERIVED_KEY_LENGTH, VALUE_LENGTH, ENUM_INDEX_LENGTH, KNOWN_CODE_STORAGE_CONTRACT} from "./Constants.sol";	// @audit-issue: DERIVED_KEY_LENGTH not used in the contract.

10:import {L1_MESSENGER_CONTRACT, INITIAL_WRITE_STARTING_POSITION, COMPRESSED_INITIAL_WRITE_SIZE, STATE_DIFF_ENTRY_SIZE, STATE_DIFF_ENUM_INDEX_OFFSET, STATE_DIFF_FINAL_VALUE_OFFSET, STATE_DIFF_DERIVED_KEY_OFFSET, DERIVED_KEY_LENGTH, VALUE_LENGTH, ENUM_INDEX_LENGTH, KNOWN_CODE_STORAGE_CONTRACT} from "./Constants.sol";	// @audit-issue: VALUE_LENGTH not used in the contract.

10:import {L1_MESSENGER_CONTRACT, INITIAL_WRITE_STARTING_POSITION, COMPRESSED_INITIAL_WRITE_SIZE, STATE_DIFF_ENTRY_SIZE, STATE_DIFF_ENUM_INDEX_OFFSET, STATE_DIFF_FINAL_VALUE_OFFSET, STATE_DIFF_DERIVED_KEY_OFFSET, DERIVED_KEY_LENGTH, VALUE_LENGTH, ENUM_INDEX_LENGTH, KNOWN_CODE_STORAGE_CONTRACT} from "./Constants.sol";	// @audit-issue: ENUM_INDEX_LENGTH not used in the contract.
```
[10](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L10-L10), [10](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L10-L10), [10](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L10-L10), [10](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L10-L10), [10](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L10-L10), [10](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L10-L10), [10](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L10-L10), [10](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L10-L10), 


```solidity
Path: ./code/system-contracts/contracts/PubdataChunkPublisher.sol

6:import {L1_MESSENGER_CONTRACT, BLOB_SIZE_BYTES, MAX_NUMBER_OF_BLOBS} from "./Constants.sol";	// @audit-issue: L1_MESSENGER_CONTRACT not used in the contract.

7:import {EfficientCall} from "./libraries/EfficientCall.sol";	// @audit-issue: EfficientCall not used in the contract.
```
[6](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/PubdataChunkPublisher.sol#L6-L6), [7](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/PubdataChunkPublisher.sol#L7-L7), 


```solidity
Path: ./code/system-contracts/contracts/Constants.sol

5:import {IAccountCodeStorage} from "./interfaces/IAccountCodeStorage.sol";	// @audit-issue: IAccountCodeStorage not used in the contract.

6:import {INonceHolder} from "./interfaces/INonceHolder.sol";	// @audit-issue: INonceHolder not used in the contract.

7:import {IContractDeployer} from "./interfaces/IContractDeployer.sol";	// @audit-issue: IContractDeployer not used in the contract.

8:import {IKnownCodesStorage} from "./interfaces/IKnownCodesStorage.sol";	// @audit-issue: IKnownCodesStorage not used in the contract.

9:import {IImmutableSimulator} from "./interfaces/IImmutableSimulator.sol";	// @audit-issue: IImmutableSimulator not used in the contract.

10:import {IBaseToken} from "./interfaces/IBaseToken.sol";	// @audit-issue: IBaseToken not used in the contract.

11:import {IL1Messenger} from "./interfaces/IL1Messenger.sol";	// @audit-issue: IL1Messenger not used in the contract.

12:import {ISystemContext} from "./interfaces/ISystemContext.sol";	// @audit-issue: ISystemContext not used in the contract.

13:import {ICompressor} from "./interfaces/ICompressor.sol";	// @audit-issue: ICompressor not used in the contract.

14:import {IComplexUpgrader} from "./interfaces/IComplexUpgrader.sol";	// @audit-issue: IComplexUpgrader not used in the contract.

15:import {IBootloaderUtilities} from "./interfaces/IBootloaderUtilities.sol";	// @audit-issue: IBootloaderUtilities not used in the contract.

16:import {IPubdataChunkPublisher} from "./interfaces/IPubdataChunkPublisher.sol";	// @audit-issue: IPubdataChunkPublisher not used in the contract.
```
[5](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Constants.sol#L5-L5), [6](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Constants.sol#L6-L6), [7](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Constants.sol#L7-L7), [8](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Constants.sol#L8-L8), [9](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Constants.sol#L9-L9), [10](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Constants.sol#L10-L10), [11](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Constants.sol#L11-L11), [12](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Constants.sol#L12-L12), [13](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Constants.sol#L13-L13), [14](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Constants.sol#L14-L14), [15](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Constants.sol#L15-L15), [16](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Constants.sol#L16-L16), 


```solidity
Path: ./code/system-contracts/contracts/L1Messenger.sol

10:import {SystemLogKey, SYSTEM_CONTEXT_CONTRACT, KNOWN_CODE_STORAGE_CONTRACT, COMPRESSOR_CONTRACT, STATE_DIFF_ENTRY_SIZE, MAX_ALLOWED_PUBDATA_PER_BATCH, L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, PUBDATA_CHUNK_PUBLISHER, COMPUTATIONAL_PRICE_FOR_PUBDATA} from "./Constants.sol";	// @audit-issue: KNOWN_CODE_STORAGE_CONTRACT not used in the contract.
```
[10](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/L1Messenger.sol#L10-L10), 


```solidity
Path: ./code/system-contracts/contracts/ContractDeployer.sol

7:import {CREATE2_PREFIX, CREATE_PREFIX, NONCE_HOLDER_SYSTEM_CONTRACT, ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT, FORCE_DEPLOYER, MAX_SYSTEM_CONTRACT_ADDRESS, KNOWN_CODE_STORAGE_CONTRACT, BASE_TOKEN_SYSTEM_CONTRACT, IMMUTABLE_SIMULATOR_SYSTEM_CONTRACT, COMPLEX_UPGRADER_CONTRACT, KECCAK256_SYSTEM_CONTRACT} from "./Constants.sol";	// @audit-issue: KECCAK256_SYSTEM_CONTRACT not used in the contract.
```
[7](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/ContractDeployer.sol#L7-L7), 


```solidity
Path: ./code/system-contracts/contracts/libraries/SystemContractHelper.sol

7:import {SystemContractsCaller, CalldataForwardingMode, CALLFLAGS_CALL_ADDRESS, CODE_ADDRESS_CALL_ADDRESS, EVENT_WRITE_ADDRESS, EVENT_INITIALIZE_ADDRESS, GET_EXTRA_ABI_DATA_ADDRESS, LOAD_CALLDATA_INTO_ACTIVE_PTR_CALL_ADDRESS, META_CODE_SHARD_ID_OFFSET, META_CALLER_SHARD_ID_OFFSET, META_SHARD_ID_OFFSET, META_AUX_HEAP_SIZE_OFFSET, META_HEAP_SIZE_OFFSET, META_GAS_PER_PUBDATA_BYTE_OFFSET, MIMIC_CALL_BY_REF_CALL_ADDRESS, META_CALL_ADDRESS, MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT, PTR_CALLDATA_CALL_ADDRESS, PTR_ADD_INTO_ACTIVE_CALL_ADDRESS, PTR_SHRINK_INTO_ACTIVE_CALL_ADDRESS, PTR_PACK_INTO_ACTIVE_CALL_ADDRESS, RAW_FAR_CALL_BY_REF_CALL_ADDRESS, PRECOMPILE_CALL_ADDRESS, SET_CONTEXT_VALUE_CALL_ADDRESS, SYSTEM_CALL_BY_REF_CALL_ADDRESS, TO_L1_CALL_ADDRESS} from "./SystemContractsCaller.sol";	// @audit-issue: SystemContractsCaller not used in the contract.

7:import {SystemContractsCaller, CalldataForwardingMode, CALLFLAGS_CALL_ADDRESS, CODE_ADDRESS_CALL_ADDRESS, EVENT_WRITE_ADDRESS, EVENT_INITIALIZE_ADDRESS, GET_EXTRA_ABI_DATA_ADDRESS, LOAD_CALLDATA_INTO_ACTIVE_PTR_CALL_ADDRESS, META_CODE_SHARD_ID_OFFSET, META_CALLER_SHARD_ID_OFFSET, META_SHARD_ID_OFFSET, META_AUX_HEAP_SIZE_OFFSET, META_HEAP_SIZE_OFFSET, META_GAS_PER_PUBDATA_BYTE_OFFSET, MIMIC_CALL_BY_REF_CALL_ADDRESS, META_CALL_ADDRESS, MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT, PTR_CALLDATA_CALL_ADDRESS, PTR_ADD_INTO_ACTIVE_CALL_ADDRESS, PTR_SHRINK_INTO_ACTIVE_CALL_ADDRESS, PTR_PACK_INTO_ACTIVE_CALL_ADDRESS, RAW_FAR_CALL_BY_REF_CALL_ADDRESS, PRECOMPILE_CALL_ADDRESS, SET_CONTEXT_VALUE_CALL_ADDRESS, SYSTEM_CALL_BY_REF_CALL_ADDRESS, TO_L1_CALL_ADDRESS} from "./SystemContractsCaller.sol";	// @audit-issue: CalldataForwardingMode not used in the contract.

7:import {SystemContractsCaller, CalldataForwardingMode, CALLFLAGS_CALL_ADDRESS, CODE_ADDRESS_CALL_ADDRESS, EVENT_WRITE_ADDRESS, EVENT_INITIALIZE_ADDRESS, GET_EXTRA_ABI_DATA_ADDRESS, LOAD_CALLDATA_INTO_ACTIVE_PTR_CALL_ADDRESS, META_CODE_SHARD_ID_OFFSET, META_CALLER_SHARD_ID_OFFSET, META_SHARD_ID_OFFSET, META_AUX_HEAP_SIZE_OFFSET, META_HEAP_SIZE_OFFSET, META_GAS_PER_PUBDATA_BYTE_OFFSET, MIMIC_CALL_BY_REF_CALL_ADDRESS, META_CALL_ADDRESS, MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT, PTR_CALLDATA_CALL_ADDRESS, PTR_ADD_INTO_ACTIVE_CALL_ADDRESS, PTR_SHRINK_INTO_ACTIVE_CALL_ADDRESS, PTR_PACK_INTO_ACTIVE_CALL_ADDRESS, RAW_FAR_CALL_BY_REF_CALL_ADDRESS, PRECOMPILE_CALL_ADDRESS, SET_CONTEXT_VALUE_CALL_ADDRESS, SYSTEM_CALL_BY_REF_CALL_ADDRESS, TO_L1_CALL_ADDRESS} from "./SystemContractsCaller.sol";	// @audit-issue: MIMIC_CALL_BY_REF_CALL_ADDRESS not used in the contract.

7:import {SystemContractsCaller, CalldataForwardingMode, CALLFLAGS_CALL_ADDRESS, CODE_ADDRESS_CALL_ADDRESS, EVENT_WRITE_ADDRESS, EVENT_INITIALIZE_ADDRESS, GET_EXTRA_ABI_DATA_ADDRESS, LOAD_CALLDATA_INTO_ACTIVE_PTR_CALL_ADDRESS, META_CODE_SHARD_ID_OFFSET, META_CALLER_SHARD_ID_OFFSET, META_SHARD_ID_OFFSET, META_AUX_HEAP_SIZE_OFFSET, META_HEAP_SIZE_OFFSET, META_GAS_PER_PUBDATA_BYTE_OFFSET, MIMIC_CALL_BY_REF_CALL_ADDRESS, META_CALL_ADDRESS, MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT, PTR_CALLDATA_CALL_ADDRESS, PTR_ADD_INTO_ACTIVE_CALL_ADDRESS, PTR_SHRINK_INTO_ACTIVE_CALL_ADDRESS, PTR_PACK_INTO_ACTIVE_CALL_ADDRESS, RAW_FAR_CALL_BY_REF_CALL_ADDRESS, PRECOMPILE_CALL_ADDRESS, SET_CONTEXT_VALUE_CALL_ADDRESS, SYSTEM_CALL_BY_REF_CALL_ADDRESS, TO_L1_CALL_ADDRESS} from "./SystemContractsCaller.sol";	// @audit-issue: MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT not used in the contract.

7:import {SystemContractsCaller, CalldataForwardingMode, CALLFLAGS_CALL_ADDRESS, CODE_ADDRESS_CALL_ADDRESS, EVENT_WRITE_ADDRESS, EVENT_INITIALIZE_ADDRESS, GET_EXTRA_ABI_DATA_ADDRESS, LOAD_CALLDATA_INTO_ACTIVE_PTR_CALL_ADDRESS, META_CODE_SHARD_ID_OFFSET, META_CALLER_SHARD_ID_OFFSET, META_SHARD_ID_OFFSET, META_AUX_HEAP_SIZE_OFFSET, META_HEAP_SIZE_OFFSET, META_GAS_PER_PUBDATA_BYTE_OFFSET, MIMIC_CALL_BY_REF_CALL_ADDRESS, META_CALL_ADDRESS, MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT, PTR_CALLDATA_CALL_ADDRESS, PTR_ADD_INTO_ACTIVE_CALL_ADDRESS, PTR_SHRINK_INTO_ACTIVE_CALL_ADDRESS, PTR_PACK_INTO_ACTIVE_CALL_ADDRESS, RAW_FAR_CALL_BY_REF_CALL_ADDRESS, PRECOMPILE_CALL_ADDRESS, SET_CONTEXT_VALUE_CALL_ADDRESS, SYSTEM_CALL_BY_REF_CALL_ADDRESS, TO_L1_CALL_ADDRESS} from "./SystemContractsCaller.sol";	// @audit-issue: RAW_FAR_CALL_BY_REF_CALL_ADDRESS not used in the contract.

7:import {SystemContractsCaller, CalldataForwardingMode, CALLFLAGS_CALL_ADDRESS, CODE_ADDRESS_CALL_ADDRESS, EVENT_WRITE_ADDRESS, EVENT_INITIALIZE_ADDRESS, GET_EXTRA_ABI_DATA_ADDRESS, LOAD_CALLDATA_INTO_ACTIVE_PTR_CALL_ADDRESS, META_CODE_SHARD_ID_OFFSET, META_CALLER_SHARD_ID_OFFSET, META_SHARD_ID_OFFSET, META_AUX_HEAP_SIZE_OFFSET, META_HEAP_SIZE_OFFSET, META_GAS_PER_PUBDATA_BYTE_OFFSET, MIMIC_CALL_BY_REF_CALL_ADDRESS, META_CALL_ADDRESS, MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT, PTR_CALLDATA_CALL_ADDRESS, PTR_ADD_INTO_ACTIVE_CALL_ADDRESS, PTR_SHRINK_INTO_ACTIVE_CALL_ADDRESS, PTR_PACK_INTO_ACTIVE_CALL_ADDRESS, RAW_FAR_CALL_BY_REF_CALL_ADDRESS, PRECOMPILE_CALL_ADDRESS, SET_CONTEXT_VALUE_CALL_ADDRESS, SYSTEM_CALL_BY_REF_CALL_ADDRESS, TO_L1_CALL_ADDRESS} from "./SystemContractsCaller.sol";	// @audit-issue: SYSTEM_CALL_BY_REF_CALL_ADDRESS not used in the contract.
```
[7](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/libraries/SystemContractHelper.sol#L7-L7), [7](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/libraries/SystemContractHelper.sol#L7-L7), [7](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/libraries/SystemContractHelper.sol#L7-L7), [7](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/libraries/SystemContractHelper.sol#L7-L7), [7](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/libraries/SystemContractHelper.sol#L7-L7), [7](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/libraries/SystemContractHelper.sol#L7-L7), 


#### Recommendation

Regularly review your Solidity code to remove unused imports. This practice declutters the codebase, making it easier to understand and maintain. In addition, consider using tools or IDE features that can automatically detect and highlight unused imports for cleanup. Keeping imports limited to only what is necessary helps maintain a clear understanding of the contract's dependencies and reduces potential confusion for developers working on or reviewing the code.



### Consider using `safePermit()`
The [Anyswap hack](https://media.dedaub.com/phantom-functions-and-the-billion-dollar-no-op-c56f062ae49f#ef54) occurred because the `permit()` function didn't really exist, but the fallback function that took its place did not complain. Consider using [`safePermit()`](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/5229b75785213541e93fb0a466a3d102a3bf5dbe/contracts/token/ERC20/utils/SafeERC20.sol#L89-L105) which ensures that the permit actually went through.

```solidity
Path: ./code/system-contracts/contracts/openzeppelin/token/ERC20/utils/SafeERC20.sol

120:        token.permit(owner, spender, value, deadline, v, r, s);	// @audit-issue
```
[120](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/openzeppelin/token/ERC20/utils/SafeERC20.sol#L120-L120), 


#### Recommendation

Consider replacing the use of the `permit()` function with `safePermit()` from OpenZeppelin's SafeERC20 library or a similar safe implementation. `safePermit()` provides additional safety checks to ensure that the permit transaction is executed securely, reducing the risk of potential vulnerabilities.


### Event is not properly `indexed`
Index event fields make the field more quickly accessible [to off-chain tools](https://ethereum.stackexchange.com/questions/40396/can-somebody-please-explain-the-concept-of-event-indexing) that parse events. This is especially useful when it comes to filtering based on an address. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Where applicable, each `event` should use three `indexed` fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three applicable fields, all of the applicable fields should be `indexed`.

```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

32:    event ValidatorAdded(uint256 _chainId, address _addedValidator);	// @audit-issue

35:    event ValidatorRemoved(uint256 _chainId, address _removedValidator);	// @audit-issue
```
[32](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L32-L32), [35](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L35-L35), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

24:    event DiamondCut(FacetCut[] facetCuts, address initAddress, bytes initCalldata);	// @audit-issue
```
[24](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L24-L24), 


```solidity
Path: ./code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol

133:    event NewChain(uint256 indexed chainId, address stateTransitionManager, address indexed chainGovernance);	// @audit-issue
```
[133](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L133-L133), 


```solidity
Path: ./code/contracts/ethereum/contracts/governance/IGovernance.sol

77:    event ChangeSecurityCouncil(address _securityCouncilBefore, address _securityCouncilAfter);	// @audit-issue
```
[77](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/IGovernance.sol#L77-L77), 


```solidity
Path: ./code/contracts/ethereum/contracts/dev-contracts/EventOnFallback.sol

9:    event Called(address msgSender, uint256 value, bytes data);	// @audit-issue
```
[9](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/dev-contracts/EventOnFallback.sol#L9-L9), 


```solidity
Path: ./code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

31:    event BridgehubDepositBaseTokenInitiated(	// @audit-issue
32:        uint256 indexed chainId,
33:        address indexed from,
34:        address l1Token,
35:        uint256 amount
36:    );
```
[31](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L31-L36), 


#### Recommendation

Enhance smart contract efficiency post-deployment by utilizing indexed events. This approach aids in efficiently tracking contract activities, significantly contributing to the reduction of gas costs.


### Use `increaseAllowance()`/`decreaseAllowance()` instead of `approve()`/`safeApprove()`
Changing an allowance with `approve()` brings the risk that someone may use both the old and the new allowance by unfortunate transaction ordering. [Refer to ERC20 API: An Attack Vector on the Approve/TransferFrom Methods](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM/edit#heading=h.m9fhqynw2xvt). It is recommended to use the `increaseAllowance()`/`decreaseAllowance()` to avoid ths problem.

```solidity
Path: ./code/system-contracts/contracts/libraries/TransactionHelper.sol

382:                IERC20(token).safeApprove(paymaster, 0);	// @audit-issue

383:                IERC20(token).safeApprove(paymaster, minAllowance);	// @audit-issue
```
[382](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/libraries/TransactionHelper.sol#L382-L382), [383](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/libraries/TransactionHelper.sol#L383-L383), 


#### Recommendation

To enhance the security of your Solidity smart contracts and avoid potential issues related to transaction ordering, it is advisable to use the `increaseAllowance()` and `decreaseAllowance()` functions instead of `approve()` or `safeApprove()`. These functions provide a safer and more atomic way to modify allowances and mitigate the risk associated with potential attack vectors like those described in the [ERC20 API: An Attack Vector on the Approve/TransferFrom Methods](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM/edit#heading=h.m9fhqynw2xvt) document.
