| ID    | TITLE                                                                                                                           |
| ----- | ------------------------------------------------------------------------------------------------------------------------------- |
|G-01 | Making constructor payable saves deployment gas costs                                                                           
|G-02 | Deployment size can be reduced by optimizing the IPFS hash to have more zeros (or using the --no-cbor-metadata compiler option) 
|G-03 | Using yul's selfbalance() is cheaper than address(this).balance                                                                 
|G-04 | Using bytes32 and assembly for storing strings under 32 bytes  saves gas                                                        
|G-05 | Do-While loops are cheaper than for loops                                                                                     
|G-06 | Test if a number is even or odd by checking the last bit instead of using a modulo operator 
|G-07 | Use inline assembly for gas effective zero address checks

## G-01 - Making constructor payable saves deployment gas cost
In solidity, non-payable constructor and functions have an implicit require(msg.value == 0) inserted in them to prevent accidental eth loss. But unfortunately it increases deployment gas costs by 200. 

Since we assume experienced users are going to deploy the contracts who won't accidently send eth, marking constructors payable will be highly gas effiective for your codebase as there will be fewer bytecodes at deploy time which eventually means less gas costs due to smaller calldata.

**There are 10 instances that require this gas optimization in your codebase:**

*10 * 200 = 2000*

Therefore, you saved deployment gas by `2000`

`instances`

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L41

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L40

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L41

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

**The rest of instances that need this optimization are:**

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L100


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