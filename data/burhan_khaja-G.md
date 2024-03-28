| ID    | TITLE                                                                                                                           |
| ----- | ------------------------------------------------------------------------------------------------------------------------------- |
|G-01 | Making constructor payable saves deployment gas costs                                                                           
|G-02 | Deployment size can be reduced by optimizing the IPFS hash to have more zeros (or using the --no-cbor-metadata compiler option) 
|G-03 | Using yul's selfbalance() is cheaper than address(this).balance                                                                 
|G-04 | Using bytes32 and assembly for storing strings under 32 bytes  saves gas                                                        
|G-05 | Do-While loops are cheaper than for loops                                                                                     
|G-06 | Test if a number is even or odd by checking the last bit instead of using a modulo operator 
|G-07 | Use inline assembly for gas effective zero address checks
|G-08 | Using assembly to revert with an error message is cheaper than any other method, (further advanced optimization to 4naly3er-report.md GAS-6)

## G-01 - Making constructor payable saves deployment gas cost
In solidity, non-payable constructor and functions have an implicit require(msg.value == 0) inserted in them to prevent accidental eth loss. But unfortunately it increases deployment gas costs by 200. 

Since we assume experienced users are going to deploy the contracts who won't accidently send eth, marking constructors payable will be highly gas effiective for your codebase as there will be fewer bytecodes at deploy time which eventually means less gas costs due to smaller calldata.

**There are 10 instances that require this gas optimization in your codebase:**

*10 * 200 = 2000*

Therefore, you saved deployment gas by `2000`

**Instances:**

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L41

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L40

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L41

## G-02 - Deployment size can be reduced by optimizing the IPFS hash to have more zeros (or using the --no-cbor-metadata compiler option) 

The Solidity compiler appends 51 bytes of metadata to the actual smart contract code. Since each deployment byte costs 200 gas, removing them can take over 10,000 gas cost off of deployment.

You can read more about it here := https://www.rareskills.io/post/solidity-metadata

Imagine saving 10000 * (no_of_inscope_contracts) gas


## G-03 - Using yul's selfbalance() is cheaper than address(this).balance
The solidity code address(this).balance can sometimes be done more efficiently with the selfbalance() function from yul
Using yul's `selfbalance()` function is gas effective than solidity's `address(this).balance`

**Here is the example of using selfbalance() in one of many instance in your codebase:**


https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41
```diff
  function transferEthToSharedBridge() external onlyBaseTokenBridge {
        ...

- 41 :    uint256 amount = address(this).balance;
+ 41 :    uint256 contractBalance;
+ 42 :     assembly {
+ 43 :         contractBalance := selfbalance()   
+ 44 :     }
+ 45 :    uint256 amount = contractBalance;
        ...
    }
```

**Instances:**

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L100


## G-04 - Using bytes32 and assembly for storing strings under 32 bytes  saves gas
If the length of a string is less than 32 bytes, it’s always efficient to store it in a bytes32 variable and use assembly to store and retrieve its data.

Remember in solidity, if a string is less than 32 bytes, the length * 2 is stored at the least significant byte of it’s storage slot and the actual data of the string is stored starting from the most significant byte in the slot in which it is defined.

Here is the dummy example of using bytes32 and assembly for storing strings under 32bytes
[LINK TO GIST](https://gist.github.com/burhankhaja/20d2e14a12e378137dc52277fc50b539)

**Here are all the instances in your codebase that need this optimization:**

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35

## G-05 - Do-While loops are cheaper than for loops

In Solidity, do-while loops are more gas efficient than for loops, even if you add an if-condition check for the case where the loop doesn’t execute at all.

**Lets take example of one of the many instances of for loop in your codebase:**
```diff
File: contracts/ethereum/contracts/governance/Governance.sol

function _execute(Call[] calldata _calls) internal {
-        for (uint256 i = 0; i < _calls.length; ++i) {
-            (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls-[i].data);
-            if (!success) {
-                // Propagate an error if the call fails.
-                assembly {
-                    revert(add(returnData, 0x20), mload(returnData))
-                }
-            }
-       }


+ uint256 i;
+  do {
+     (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls-[i].data);
+     if (!success) {
+         // Propagate an error if the call fails.
+         assembly {
+             revert(add(returnData, 0x20), mload(returnData))
+         }
+     }
+     unchecked {
+           ++i;
+      }
+  } while (i < _calls.length) ;

}

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L224-L234)

**Here are the rest of instances of for-loops in your codebase that when replaced with do-whiles will save significant amounts of gas:**

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

135:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

185:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

209:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol)

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

633:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol)

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol)

```solidity
File: system-contracts/contracts/ContractDeployer.sol

270:         for (uint256 i = 0; i < deploymentsLength; ++i) {

275:         for (uint256 i = 0; i < deploymentsLength; ++i) {

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol)

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

38:             for (uint256 i = 0; i < immutablesLength; ++i) {

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol)

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

30:             for (uint256 i = 0; i < hashesLen; ++i) {

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol)

```solidity
File: system-contracts/contracts/L1Messenger.sol

210:         for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

222:         for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

228:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

240:         for (uint256 i = 0; i < numberOfMessages; ++i) {

258:         for (uint256 i = 0; i < numberOfBytecodes; ++i) {

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol)

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol

36:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol)

## G-06 - Test if a number is even or odd by checking the last bit instead of using a modulo operator 

The conventional way to check if a number is even or odd is to do x % 2 == 0 where x is the number in question. You can instead check if x & uint256(1) == 0. where x is assumed to be a uint256. 

`Bitwise and` is cheaper than the modulo op code. In binary, the rightmost bit represents "1" whereas all the bits to the are multiples of 2, which are even. Adding "1" to an even number causes it to be odd.

**Instances:**

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L88

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L78

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L27

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L30

## G-07 - Use inline assembly for gas effective zero address checks

we can manipulate memory directly and use fewer opcodes instead of leaving it to the Solidity compiler by utilizing inline assembly for zero address checks and can save lot of gas doing so.

**Here is the simple demonstration of this optimization technique on one of the many zero address checks across the codebase:**

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L55

```diff
 function initialize(
        address _l1Bridge,
        address _l1LegecyBridge,
        bytes32 _l2TokenProxyBytecodeHash,
        address _aliasedOwner
    ) external reinitializer(2) {
-        require(_l1Bridge != address(0), "bf");
+        assembly {
+            if iszero(_l1Bridge) {
+                mstore(0x00, 0x20)
+                mstore(0x20, 0x0c)
+                mstore(0x40, 0x5a65726f20416464726573730000000000000000000000000000000000000000) // load hex of "Zero Address" to memory
+                revert(0x00, 0x60)
+            }
+        }
        ...
        ...
}
```

**Instances:**
- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L57

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L68

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L96

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L129

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L141

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L161

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L181

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L108

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L188

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L42

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L26

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51

- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L82

## G-08 - Using assembly to revert with an error message is cheaper than any other method, (further advanced optimization to 4naly3er-report.md GAS-6)

GAS-6 from [4nalyzer report](https://github.com/code-423n4/2024-03-zksync/blob/main/4naly3er-report.md#gas-6-use-custom-errors-instead-of-revert-strings-to-save-gas) flags that it is better to use custom errors rather than requires for reverting.

Luckily, there is lot more efficient way of doing it and that is using assembly for reverting. By applying this method you will save >300 amount of execution gas costs.

**Instances:**
```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

64:         require(msg.sender == address(sharedBridge), "Not shared bridge");

66:         require(amount == _amount, "Incorrect amount");

141:         require(_amount != 0, "0T"); // empty deposit

143:         require(amount == _amount, "3T"); // The token has non-standard transfer logic

186:         require(amount != 0, "2T"); // empty deposit

215:         require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol)

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

69:         require(msg.sender == address(bridgehub), "ShB not BH");

84:         require(msg.sender == address(legacyBridge), "ShB not legacy bridge");

108:         require(_owner != address(0), "ShB owner 0");

122:             require(amount > 0, "ShB: 0 amount to transfer");

125:             require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");

132:         require(msg.sender == ERA_DIAMOND_PROXY, "ShB: not era diamond proxy");

150:             require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");

153:             require(msg.value == 0, "ShB m.v > 0 b d.it");

156:             require(amount == _amount, "3T"); // The token has non-standard transfer logic

183:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

189:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");

190:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

195:             require(_depositAmount == 0, "ShB wrong withdraw amount");

197:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");

201:             require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic

203:         require(amount != 0, "6T"); // empty deposit amount

232:         require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");

320:             require(proofValid, "yn");

322:         require(_amount > 0, "y1");

337:                 require(dataHash == txDataHash, "ShB: d.it not hap");

344:             require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");

355:             require(callSuccess, "ShB: claimFailedDeposit failed");

391:             require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");

412:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");

422:             require(!alreadyFinalized, "Withdrawal is already finalized 2");

434:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds

444:             require(callSuccess, "ShB: withdraw failed");

479:         require(success, "ShB withd w proof"); // withdrawal wrong proof

496:         require(_l2ToL1message.length >= 56, "ShB wrong msg len"); // wrong messsage length

512:             require(_l2ToL1message.length == 76, "ShB wrong msg len 2");

517:             revert("ShB Incorrect message function selector");

558:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

559:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol)

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

43:         require(msg.sender == deployer || msg.sender == owner(), "Bridgehub: not owner or deployer");

82:         require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

102:         require(_chainId != 0, "Bridgehub: chainId cannot be 0");

103:         require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");

109:         require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");

110:         require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

112:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

203:                 require(msg.value == _request.mintValue, "Bridgehub: msg.value mismatch 1");

205:                 require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");

255:                 require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3");

276:         require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol)

```solidity
File: contracts/ethereum/contracts/common/ReentrancyGuard.sol

58:         require(lockSlotOldValue == 0, "1B");

75:         require(_status == _NOT_ENTERED, "r1");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol)

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

23:         require(_bytecode.length % 32 == 0, "pq");

26:         require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words

27:         require(bytecodeLenInWords % 2 == 1, "ps"); // bytecode length in words must be odd

41:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash

43:         require(_bytecodeLen(_bytecodeHash) % 2 == 1, "uy"); // Code length in words must be odd

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol)

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

42:         require(_admin != address(0), "Admin should be non zero address");

59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

65:         require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

155:         require(isOperationPending(_id), "Operation must be pending");

172:         require(isOperationReady(id), "Operation must be ready before execution");

177:         require(isOperationReady(id), "Operation must be ready after execution");

191:         require(isOperationPending(id), "Operation must be pending before execution");

196:         require(isOperationPending(id), "Operation must be pending after execution");

216:         require(!isOperation(_id), "Operation with this proposal id already exists");

217:         require(_delay >= minDelay, "Proposed delay is less than minimum delay");

240:         require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol)

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

58:         require(msg.sender == bridgehub, "StateTransition: only bridgehub");

70:         require(_initializeData.governor != address(0), "StateTransition: governor zero");

204:         require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol)

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

68:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");

195:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

217:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol)

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

25:         require(address(_initializeData.verifier) != address(0), "vt");

26:         require(_initializeData.admin != address(0), "vy");

27:         require(_initializeData.validatorTimelock != address(0), "hc");

28:         require(_initializeData.priorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "vu");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol)

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

14:         require(_chainId == block.chainid, "pr");

25:         require(msg.data.length >= 4 || msg.data.length == 0, "Ut");

30:         require(facetAddress != address(0), "F"); // Proxy has no facet for this selector

31:         require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol)

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

34:         require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights

59:         require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");

70:         require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");

130:         require(!diamondStorage.isFrozen, "a9"); // diamond proxy is frozen already

140:         require(diamondStorage.isFrozen, "a7"); // diamond proxy is not frozen

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol)

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

36:         require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f"); // only commit next batch

39:         require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us");

69:         require(_previousBatch.batchHash == logOutput.previousBatchHash, "l");

71:         require(logOutput.chainedPriorityTxsHash == _newBatch.priorityOperationsHash, "t");

73:         require(logOutput.numberOfLayer1Txs == _newBatch.numberOfLayer1Txs, "ta");

105:         require(batchTimestamp == _expectedBatchTimestamp, "tb");

109:         require(_previousBatchTimestamp < batchTimestamp, "h3");

117:         require(block.timestamp - COMMIT_TIMESTAMP_NOT_OLDER <= batchTimestamp, "h1"); // New batch timestamp is too small

118:         require(lastL2BlockTimestamp <= block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA, "h2"); // The last L2 block timestamp is too big

144:             require(!_checkBit(processedLogs, uint8(logKey)), "kp");

149:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");

152:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");

155:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");

158:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");

161:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");

164:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bl");

167:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bk");

170:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");

173:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");

176:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bu");

177:                 require(_expectedSystemContractUpgradeTxHash == logValue, "ut");

179:                 revert("ul");

187:             require(processedLogs == 511, "b7");

189:             require(processedLogs == 1023, "b8");

226:         require(_newBatchesData.length == 1, "e4");

228:         require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data

279:         require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");

318:         require(currentBatchNumber == s.totalBatchesExecuted + _executedBatchIdx + 1, "k"); // Execute batches in order

325:         require(priorityOperationsHash == _storedBatch.priorityOperationsHash, "x"); // priority operations hash does not match to expected

353:         require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.

397:         require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");

416:         require(currentTotalBatchesVerified <= s.totalBatchesCommitted, "q");

437:         require(proofPublicInput.length == 1, "t4");

444:         require(successVerifyProof, "p"); // Proof verification fail

477:         require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch

478:         require(_newLastBatch >= s.totalBatchesExecuted, "v2"); // Already executed batches cannot be reverted

530:         require(_batch.systemLogs.length <= MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES, "pu");

582:         require(success, "failed to call point evaluation precompile");

584:         require(result == BLS_MODULUS, "precompile unexpected output");

597:         require(_pubdataCommitments.length > 0, "pl");

598:         require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");

599:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");

605:             require(blobVersionedHash != bytes32(0), "vh");

629:         require(versionedHash == bytes32(0), "lh");

647:         require(success, "vc");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol)

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

182:         require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol)

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

39:         require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");

48:         require(callSuccess, "ShB: transferEthToSharedBridge failed");

115:         require(_batchNumber <= s.totalBatchesExecuted, "xx");

122:         require(hashedLog != L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH, "tw");

163:         require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

190:         require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");

211:         require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for eth base token");

248:         require(_request.l2GasPerPubdataByteLimit == REQUIRED_L2_GAS_PRICE_PER_PUBDATA, "qp");

276:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj");

284:         require(_mintValue >= baseCost + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol)

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

16:         require(msg.sender == s.admin, "StateTransition Chain: not admin");

22:         require(s.validators[msg.sender], "StateTransition Chain: not validator");

27:         require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

32:         require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

53:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol)

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

107:             require(selectors.length > 0, "B"); // no functions for diamond cut

116:                 revert("C"); // undefined diamond cut action

132:         require(_facet.code.length > 0, "G");

141:             require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists

155:         require(_facet.code.length > 0, "K");

161:             require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

175:         require(_facet == address(0), "a1"); // facet address must be zero

181:             require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet

215:             require(_isSelectorFreezable == ds.selectorToFacet[selector0].isFreezable, "J1");

280:             require(_calldata.length == 0, "H"); // Non-empty calldata for zero address

287:                     revert("I"); // delegatecall failed

297:             require(data.length == 32, "lp");

298:             require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol)

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

24:         require(pathLength > 0, "xc");

25:         require(pathLength < 256, "bt");

26:         require(_index < (1 << pathLength), "px");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol)

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

65:         require(!_queue.isEmpty(), "D"); // priority queue is empty

73:         require(!_queue.isEmpty(), "s"); // priority queue is empty

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol)

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

115:         require(_totalGasLimit >= overhead, "my"); // provided gas limit doesn't cover transaction overhead

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol)

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

72:         require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

190:         require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");

223:         require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");

224:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");

249:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol)

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

33:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

52:         require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol)

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol

26:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

37:         require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");

48:         require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");

57:         require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol)

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol

37:             revert("Unsupported tx type");

92:             require(vInt == 27 || vInt == 28, "Invalid v value");

191:             require(vInt == 27 || vInt == 28, "Invalid v value");

286:             require(vInt == 27 || vInt == 28, "Invalid v value");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol)

```solidity
File: system-contracts/contracts/ComplexUpgrader.sol

22:         require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");

24:         require(_delegateTo.code.length > 0, "Delegatee is an EOA");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol)

```solidity
File: system-contracts/contracts/Compressor.sol

63:                 require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

68:                 require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");

119:         require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");

140:             require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");

156:         require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");

171:             require(enumIndex == compressedEnumIndex, "rw: enum key mismatch");

187:         require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");

230:                 require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");

242:                 revert("unsupported operation");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol)

```solidity
File: system-contracts/contracts/ContractDeployer.sol

29:         require(msg.sender == address(this), "Callable only by self");

273:         require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");

286:         require(_bytecodeHash != bytes32(0x0), "BytecodeHash cannot be zero");

287:         require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

295:         require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied");

325:         require(knownCodeMarker > 0, "The code hash is not known");

372:             require(value == 0, "The value must be zero if we do not call the constructor");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol)

```solidity
File: system-contracts/contracts/DefaultAccount.sol

100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

160:         require(_signature.length == 65, "Signature length is incorrect");

173:         require(v == 27 || v == 28, "v is neither 27 nor 28");

184:         require(uint256(s) <= 0x7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF5D576E7357A4501DDFE92F46681B20A0, "Invalid s");

202:         require(success, "Failed to pay the fee to the operator");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol)

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

35:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol)

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

20:         require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");

76:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");

78:         require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol)

```solidity
File: system-contracts/contracts/L1Messenger.sol

205:         require(numberOfL2ToL1Logs <= L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, "Too many L2->L1 logs");

302:         require(calldataPtr <= MAX_ALLOWED_PUBDATA_PER_BATCH, "L1 Messenger pubdata is too long");

319:         require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol)

```solidity
File: system-contracts/contracts/L2BaseToken.sol

41:         require(fromBalance >= _amount, "Transfer amount exceeds balance");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol)

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol

43:         require(to != address(this), "MsgValueSimulator calls itself");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol)

```solidity
File: system-contracts/contracts/NonceHolder.sol

66:         require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");

85:         require(_value != 0, "Nonce value cannot be set to 0");

89:             require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");

115:         require(oldMinNonce == _expectedNonce, "Incorrect nonce");

170:             revert("Reusing the same nonce twice");

172:             revert("The nonce was not set as used");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol)

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol

22:         require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol)

```solidity
File: system-contracts/contracts/SystemContext.sol

219:         require(_isFirstInBatch, "Upgrade transaction must be first");

222:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

226:             require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");

264:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

332:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

344:             require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");

345:             require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");

350:             require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");

362:             require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");

371:             revert("Invalid new L2 block number");

390:         require(currentBatchNumber > 0, "The current batch number must be greater than 0");

428:         require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");

429:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");

```
[Link to code](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol)

