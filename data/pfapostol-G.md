The content section shows only 10 examples, subsequent cases are listed as links.

### Gas Risk Issues

| |Issue|Instances| Gas Savings|
|-|:-|:-:|:-:|
| [[G-01](#g-01)] | Alternative Solady library can be used instead of OpenZeppelin to save gas | 8| 8000|
| [[G-02](#g-02)] | Setting the `constructor` to `payable` | 10| 130|
| [[G-03](#g-03)] | `array[index] += amount` is cheaper than `array[index] = array[index] + amount` (or related variants) | 1| 0|
| [[G-04](#g-04)] | Use assembly to check for `address(0)` | 47| 282|
| [[G-05](#g-05)] | `Internal` functions only called once can be inlined to save gas | 35| 1050|
| [[G-06](#g-06)] | `selfbalance()` is cheaper than `address(this).balance` | 3| 0|
| [[G-07](#g-07)] | Usage of `uint`/`int` smaller than 32 bytes (256 bits) incurs overhead | 97| 2134|
| [[G-08](#g-08)] | `>=` costs less gas than `>` | 14| 42|
| [[G-09](#g-09)] | Multiple mappings can be replaced with a single struct mapping | 17| 340000|
| [[G-10](#g-10)] | Structs can be packed into fewer storage slots | 3| 60000|
| [[G-11](#g-11)] | Using `storage` instead of `memory` for structs/arrays saves gas | 9| 37800|
| [[G-12](#g-12)] | State variables should be cached in stack variables rather than re-reading them from storage | 173| 16781|
| [[G-13](#g-13)] | `require()`/`revert()` strings longer than 32 bytes cost extra gas | 53| 159|
| [[G-14](#g-14)] | Stack variable used as a cheaper cache for a state variable is only used once | 91| 273|
| [[G-15](#g-15)] | State variables access within a loop | 8| 4240|
| [[G-16](#g-16)] | Newer versions of solidity are more gas efficient | 62| 0|
| [[G-17](#g-17)] | Consider activating `via-ir` for deploying | 1| 0|
| [[G-18](#g-18)] | Function calls should be cached instead of re-calling the function | 8| 384|
| [[G-19](#g-19)] | Add `unchecked` blocks for divisions where the operands cannot overflow | 8| 1272|
| [[G-20](#g-20)] | Consider pre-calculating the address of `address(this)` | 12| 31200|
| [[G-21](#g-21)] | Consider using `bytes32` rather than a `string` | 12| 1536|
| [[G-22](#g-22)] | Optimize Zero Checks Using Assembly | 99| 5742|
| [[G-23](#g-23)] | Consider using `assembly` to write address storage values if the address variable is mutable | 35| 0|
| [[G-24](#g-24)] | Consider Caching Multiple Accesses to Mappings/Arrays | 29| 2900|
| [[G-25](#g-25)] | Optimize Gas by Using Do-While Loops | 22| 5610|
| [[G-26](#g-26)] | Use Assembly for Efficient Event Emission | 65| 117000|
| [[G-27](#g-27)] | Optimize External Calls with Assembly for Memory Efficiency | 65| 14300|
| [[G-28](#g-28)] | Use Assembly for Hash Calculations | 29| 29145|
| [[G-29](#g-29)] | Consider Using Solady's Gas Optimized Lib for Math | 29| 0|
| [[G-30](#g-30)] | Trade-offs Between Modifiers and Internal Functions | 122| 1281000|
| [[G-31](#g-31)] | Consider Packing Small `uint` When it's Possible | 4| 83200|
| [[G-32](#g-32)] | Avoid Unnecessary Public Variables | 43| 946000|
| [[G-33](#g-33)] | Optimize by Using Assembly for Low-Level Calls' Return Data | 1| 159|
| [[G-34](#g-34)] | Avoid Zero Transfers to Save Gas | 4| 0|
| [[G-35](#g-35)] | Optimize Unsigned Integer Comparison With Zero | 13| 52|
| [[G-36](#g-36)] | Delete Unused State Variables | 18| 360000|
| [[G-37](#g-37)] | Optimize Gas by Using Only Named Returns | 187| 8228|
| [[G-38](#g-38)] | Use assembly in place of `abi.decode` to extract `calldata` values more efficiently | 9| 0|
| [[G-39](#g-39)] | Optimize Address Storage Value Management with `assembly` | 29| 0|
| [[G-40](#g-40)] | Use calldata instead of memory for function arguments that do not get mutated | 54| 0|
| [[G-41](#g-41)] | Gas savings can be achieved by changing the model for assigning value to the structure | 19| 4940|
| [[G-42](#g-42)] | Use `Array.unsafeAccess` to avoid repeated array length checks | 100| 210000|
| [[G-43](#g-43)] | Consider using OpenZeppelin's `EnumerateSet` instead of nested mappings | 10| 10000|
| [[G-44](#g-44)] | Counting down in `for` statements is more gas efficient | 8| 64|
| [[G-45](#g-45)] | Do not calculate constants | 1| 0|

### Gas Risk Issues

### [G-01]<a name="g-01"></a> Alternative Solady library can be used instead of OpenZeppelin to save gas

The following OpenZeppelin imports have a [Solady](https://github.com/Vectorized/solady) equivalent, as such they can be used to save GAS as Solady modules have been specifically designed to be as GAS efficient as possible.    

*There are 8 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
 // @audit `IERC20` has Solady alternative
7	import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";
...
 // @audit `SafeERC20` has Solady alternative
8	import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```

*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L7), [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L8)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
 // @audit `Initializable` has Solady alternative
7	import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
...
 // @audit `IERC20Metadata` has Solady alternative
10	import {IERC20Metadata} from "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";
...
 // @audit `IERC20` has Solady alternative
11	import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";
...
 // @audit `SafeERC20` has Solady alternative
12	import {SafeERC20} from "@openzeppelin/contracts/token/ERC20/utils/SafeERC20.sol";
```

*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L7), [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L10), [11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L11), [12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L12)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

```solidity
 // @audit `Initializable` has Solady alternative
7	import {Initializable} from "@openzeppelin/contracts/proxy/utils/Initializable.sol";
```

*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L7)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
 // @audit `draft-ERC20PermitUpgradeable` has Solady alternative
7	import {ERC20PermitUpgradeable} from "@openzeppelin/contracts-upgradeable/token/ERC20/extensions/draft-ERC20PermitUpgradeable.sol";
```

*GitHub* : [7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L7)

### [G-02]<a name="g-02"></a> Setting the `constructor` to `payable`

Saves ~13 gas per instance

*There are 10 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
57	    constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L57)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
92	    constructor(
93	        address _l1WethAddress,
94	        IBridgehub _bridgehub,
95	        IL1ERC20Bridge _legacyBridge
96	    ) reentrancyGuardInitializer {
```

*GitHub* : [92..96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L92-L96)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
40	    constructor() reentrancyGuardInitializer {}
```

*GitHub* : [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L40)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
43	    constructor(address _admin, address _securityCouncil, uint256 _minDelay) {
```

*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L43)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
60	    constructor(address _bridgehub) reentrancyGuardInitializer {
```

*GitHub* : [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L60)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
57	    constructor(address _initialOwner, uint32 _executionDelay) {
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

```solidity
21	    constructor() reentrancyGuardInitializer {}
```

*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L21)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

```solidity
13	    constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
```

*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L13)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

```solidity
43	    constructor() {
```

*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L43)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
42	    constructor() {
```

*GitHub* : [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L42)

### [G-03]<a name="g-03"></a> `array[index] += amount` is cheaper than `array[index] = array[index] + amount` (or related variants)

When updating a value in an array with arithmetic, using `array[index] += amount` is cheaper than `array[index] = array[index] + amount`.
This is because you avoid an additonal `mload` when the array is stored in memory, and an `sload` when the array is stored in storage.
This can be applied for any arithmetic operation including `+=`, `-=`,`/=`,`*=`,`^=`,`&=`, `%=`, `<<=`,`>>=`, and `>>>=`.
This optimization can be particularly significant if the pattern occurs during a loop.

*Saves 28 gas for a storage array, 38 for a memory array*


*There are 1 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
135	            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
```

*GitHub* : [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L135)

### [G-04]<a name="g-04"></a> Use assembly to check for `address(0)`



*There are 47 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
110	        require(_owner != address(0), "ShB owner 0");
...
190	        require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
...
565	        require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
...
580	            if (_refundRecipient == address(0)) {
```

*GitHub* : [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L110), [190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L190), [565](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L565), [580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L580)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
132	        require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
...
134	        require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");
...
328	        if (_refundRecipient == address(0)) {
```

*GitHub* : [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134), [328](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L328)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
44	        require(_admin != address(0), "Admin should be non zero address");
...
242	        require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");
```

*GitHub* : [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L44), [242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L242)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
84	        require(_initializeData.governor != address(0), "StateTransition: governor zero");
```

*GitHub* : [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L84), [248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L248)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L28), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol


*GitHub* : [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L32)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [193](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L193), [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L239), [639](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L639), [663](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L663), [669](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L669), [669](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L669), [670](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670), [670](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L185)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [277](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L277)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L95), [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L112), [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L133), [150](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L150), [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L151), [152](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L152), [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L251)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L35)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L143), [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L163), [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L177), [183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L183), [281](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L281)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L57), [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L58), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L59), [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L60), [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L70), [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L98), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L131)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L53)

### [G-05]<a name="g-05"></a> `Internal` functions only called once can be inlined to save gas



*There are 35 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
162	    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```

*GitHub* : [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L162)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
256	    function _getERC20Getters(address _token) internal view returns (bytes memory) {
...
460	    function _checkWithdrawal(
461	        uint256 _chainId,
462	        MessageParams memory _messageParams,
463	        bytes calldata _message,
464	        bytes32[] calldata _merkleProof
465	    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
...
489	    function _parseL2WithdrawalMessage(
490	        uint256 _chainId,
491	        bytes memory _l2ToL1message
492	    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
```

*GitHub* : [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L256), [460..465](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L460-L465), [489..492](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L489-L492)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
179	    function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
```

*GitHub* : [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L179)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
105	    function _verifyBatchTimestamp(
106	        uint256 _packedBatchAndL2BlockTimestamp,
107	        uint256 _expectedBatchTimestamp,
108	        uint256 _previousBatchTimestamp
109	    ) internal view {
...
255	    function _commitBatchesWithoutSystemContractsUpgrade(
256	        StoredBatchInfo memory _lastCommittedBatchData,
257	        CommitBatchInfo[] calldata _newBatchesData
258	    ) internal {
...
275	    function _commitBatchesWithSystemContractsUpgrade(
276	        StoredBatchInfo memory _lastCommittedBatchData,
277	        CommitBatchInfo[] calldata _newBatchesData,
278	        bytes32 _systemContractUpgradeTxHash
279	    ) internal {
...
310	    function _collectOperationsFromPriorityQueue(uint256 _nPriorityOps) internal returns (bytes32 concatHash) {
...
323	    function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {
```

*GitHub* : [105..109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L105-L109), [255..258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L255-L258), [275..279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L275-L279), [310](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L310), [323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L323), [440](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L440), [515](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515), [525](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525), [537..542](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542), [561..564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L561-L564), [592](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L592), [597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597), [605..609](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L605-L609), [625..628](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L625-L628)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L132), [260..265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L260-L265), [291..295](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L291-L295), [318..322](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L318-L322), [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L355)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L51)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol


*GitHub* : [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L28)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [71..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L71-L75), [111..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L111-L114), [130..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L130-L132)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L111), [140..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L140-L144)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39), [97..107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L97-L107), [123..129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L123-L129)

### [G-06]<a name="g-06"></a> `selfbalance()` is cheaper than `address(this).balance`



*There are 3 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
120	            uint256 balanceBefore = address(this).balance;
...
122	            uint256 balanceAfter = address(this).balance;
```

*GitHub* : [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L122)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
43	        uint256 amount = address(this).balance;
```

*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L43)

### [G-07]<a name="g-07"></a> Usage of `uint`/`int` smaller than 32 bytes (256 bits) incurs overhead

When using elements that are smaller than 32 bytes, your contract’s gas usage may be higher. This is because the EVM operates on 32 bytes at a time. Therefore, if the element is smaller than that, the EVM must use more operations in order to reduce the size of the element from 32 bytes to the desired size.

Each operation involving a uint8 costs an extra 22-28 gas (depending on whether the other operand is also a variable of type uint8) as compared to ones involving uint256, due to the compiler having to clear the higher bits of the memory word before operating on the uint8, as well as the associated stack operations of doing so. Use a larger size then downcast where needed.

https://docs.soliditylang.org/en/v0.8.11/internals/layout_in_storage.html

Use a larger size then downcast where needed.

*There are 97 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
184	        uint16 _l2TxNumberInBatch,
...
213	        uint16 _l2TxNumberInBatch,
```

*GitHub* : [184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L184), [213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L213)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
287	        uint16 _l2TxNumberInBatch,
...
314	        uint16 _l2TxNumberInBatch,
...
391	        uint16 _l2TxNumberInBatch,
...
406	        uint16 l2TxNumberInBatch;
...
415	        uint16 _l2TxNumberInBatch,
...
505	        (uint32 functionSignature, uint256 offset) = UnsafeBytes.readUint32(_l2ToL1message, 0);
...
620	        uint16 _l2TxNumberInBatch,
...
653	        uint16 _l2TxNumberInBatch,
```

*GitHub* : [287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L287), [314](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L314), [391](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L391), [406](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L406), [415](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L415), [505](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L505), [620](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L620), [653](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L653)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L183)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57), [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98), [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L117), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L136)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol


*GitHub* : [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L34), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L35), [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L56), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L57), [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L58), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L59), [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L60), [153](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L153), [154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L154)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L82), [83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L83), [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L81), [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L81)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L41), [592](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L592), [597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L69), [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L74)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L80), [183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L183)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L42)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol


*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L21)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L34), [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L43), [210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L210)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


*GitHub* : [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L20), [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L56), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L40)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L14), [15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L15)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L51), [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L58)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L83), [95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L95), [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L102), [111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L111)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L96)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L22)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L42), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L42), [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L86), [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L87), [88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L88), [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L89)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol


*GitHub* : [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L86), [88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L88), [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L115), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L116), [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L117)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol


*GitHub* : [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L114), [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L117)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L53), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L67), [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L128)


---

	 - code/contracts/ethereum/contracts/common/Messaging.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L26), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L28), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L40), [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L62)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L33), [95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L95), [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L117), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L136), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173), [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L185)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L14)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L15)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L8)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L29), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L42), [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L46), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39), [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L79), [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L81), [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L98), [99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L99), [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L100), [101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L101), [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L102), [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L103), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L124), [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L125)

### [G-08]<a name="g-08"></a> `>=` costs less gas than `>`

The compiler uses opcodes `GT` and `ISZERO` for solidity code that uses `>`, but only requires LT for `>=`, which saves 3 gas. Similarly for `<=`.

*There are 14 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
131	            require(amount > 0, "ShB: 0 amount to transfer");
...
329	        require(_amount > 0, "y1");
```

*GitHub* : [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131), [329](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L329)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
331	        } else if (_refundRecipient.code.length > 0) {
```

*GitHub* : [331](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L331)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
431	        if (_proof.serializedProof.length > 0) {
...
593	        return (_bitMap & (1 << _index)) > 0;
...
631	        require(_pubdataCommitments.length > 0, "pl");
```

*GitHub* : [431](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L431), [593](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L593), [631](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
160	        require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");
...
279	        if (refundRecipient.code.length > 0) {
```

*GitHub* : [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L160), [279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L279)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
109	            require(selectors.length > 0, "B"); // no functions for diamond cut
...
134	        require(_facet.code.length > 0, "G");
```

*GitHub* : [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L109), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L134), [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L157)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L26), [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L27)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L126)

### [G-09]<a name="g-09"></a> Multiple mappings can be replaced with a single struct mapping

Saves a storage slot for the mapping. Depending on the circumstances and sizes of types, can avoid a Gsset (20000 gas) per mapping combined. Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot.

*There are 17 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
34	    mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
35	        public depositAmount;
...
47	    mapping(address => uint256) private __DEPRECATED_lastWithdrawalLimitReset;
...
50	    mapping(address => uint256) private __DEPRECATED_withdrawnAmountInWindow;
...
53	    mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;
```

*GitHub* : [34..35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L34-L35), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L47), [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L50), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L53)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
50	    mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;
...
54	    mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
55	        public
56	        override depositHappened;
...
59	    mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
60	        public isWithdrawalFinalized;
...
63	    mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;
...
67	    mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;
```

*GitHub* : [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L50), [54..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L54-L56), [59..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L59-L60), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L63), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L67)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
23	    mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;
```

*GitHub* : [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L23), [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L25), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L28), [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L31)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L32), [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L50)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L49), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L52)

### [G-10]<a name="g-10"></a> Structs can be packed into fewer storage slots

Each slot saved can avoid an extra Gsset (20000 gas) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings

*There are 3 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
64	    struct FacetCut {
65	        address facet;
66	        Action action;
67	        bool isFreezable;
68	        bytes4[] selectors;
69	    }
```

*GitHub* : [64..69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L64-L69)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

```solidity
17	struct StateTransitionManagerInitializeData {
18	    address governor;
19	    address validatorTimelock;
20	    address genesisUpgrade;
21	    bytes32 genesisBatchHash;
22	    uint64 genesisIndexRepeatedStorageChanges;
23	    bytes32 genesisBatchCommitment;
24	    Diamond.DiamondCutData diamondCut;
25	    uint256 protocolVersion;
26	}
```

*GitHub* : [17..26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L17-L26)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

```solidity
85	    struct StoredBatchInfo {
86	        uint64 batchNumber;
87	        bytes32 batchHash;
88	        uint64 indexRepeatedStorageChanges;
89	        uint256 numberOfLayer1Txs;
90	        bytes32 priorityOperationsHash;
91	        bytes32 l2LogsTreeRoot;
92	        uint256 timestamp;
93	        bytes32 commitment;
94	    }
```

*GitHub* : [85..94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L85-L94)

### [G-11]<a name="g-11"></a> Using `storage` instead of `memory` for structs/arrays saves gas

When fetching data from a storage location, assigning the data to a `memory` variable causes all fields of the struct/array to be read from storage, which incurs a Gcoldsload (**2100 gas**) for *each* field of the struct/array. If the fields are read from the new memory variable, they incur an additional `MLOAD` rather than a cheap stack read. Instead of declearing the variable with the `memory` keyword, declaring the variable with the `storage` keyword and caching any fields that need to be re-read in stack variables, will be much cheaper, only incuring the Gcoldsload for the fields actually read. The only time it makes sense to read the whole struct/array into a `memory` variable, is if the full struct/array is being returned by the function, is being passed to a function that requires `memory`, or if the array/struct is being read from another `memory` array/struct

*There are 9 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

```solidity
29	        Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];
```

*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
74	        FeeParams memory oldFeeParams = s.feeParams;
```

*GitHub* : [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L74)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
398	        VerifierParams memory verifierParams = s.verifierParams;
```

*GitHub* : [398](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L398)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

```solidity
212	            Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];
```

*GitHub* : [212](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L212)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
159	        FeeParams memory feeParams = s.feeParams;
```

*GitHub* : [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L159)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

```solidity
157	        VerifierParams memory oldVerifierParams = s.verifierParams;
```

*GitHub* : [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L157)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
142	            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
...
162	            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
...
182	            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
```

*GitHub* : [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L142), [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L162), [182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L182)

### [G-12]<a name="g-12"></a> State variables should be cached in stack variables rather than re-reading them from storage

The instances below point to the second+ access of a state variable within a function. Caching of a state variable replaces each Gwarmaccess (**100 gas**) with a much cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses.

*There are 173 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
// @audit State variable `depositAmount` called 2 times in one function
187	        uint256 amount = depositAmount[_depositSender][_l1Token][_l2TxHash];
...
// @audit State variable `depositAmount` called 2 times in one function
189	        delete depositAmount[_depositSender][_l1Token][_l2TxHash];
```

*GitHub* : [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L187), [189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L189)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
// @audit State variable `chainBalance` called 4 times in one function
124	            chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
...
// @audit State variable `chainBalance` called 4 times in one function
125	                chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
...
// @audit State variable `chainBalance` called 4 times in one function
135	            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
...
// @audit State variable `chainBalance` called 4 times in one function
135	            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
```

*GitHub* : [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L124), [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L125), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L135), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L135)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
// @audit State variable `l2BridgeAddress` called 2 times in one function
190	        require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
...
// @audit State variable `l2BridgeAddress` called 2 times in one function
223	                l2Contract: l2BridgeAddress[_chainId],
```

*GitHub* : [190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L190), [223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L223)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
// @audit State variable `depositHappened` called 2 times in one function
239	        require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");
...
// @audit State variable `depositHappened` called 2 times in one function
240	        depositHappened[_chainId][_txHash] = _txDataHash;
```

*GitHub* : [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L239), [240](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L240)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol


*GitHub* : [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L351), [352](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L352), [342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L342), [345](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L345)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol


*GitHub* : [441](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L441), [442](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L442), [419](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L419), [420](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L420)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol


*GitHub* : [565](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L565), [588](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L588)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L57)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L66), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L67), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L63), [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L71)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L86), [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L89)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L96), [99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L99)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L104), [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L105)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132), [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L142), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L136)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [252](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L252), [253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L253)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L259), [260](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L260)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L114), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L116)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L125), [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L126), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L122), [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L127), [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L130)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [194](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L194), [218](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L218), [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L229)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L248), [284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L284)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L81), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L84)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L90), [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L93)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


*GitHub* : [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L32), [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L33), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L34), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L35), [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L36), [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L37), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L39), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L40), [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L41), [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L43), [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L44), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L45), [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L46), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L47), [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L48), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L49)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L27), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L35), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L38), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L39), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L63), [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L74), [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L75)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L82), [83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L83), [85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L85), [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L86)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92), [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L93)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L108), [113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L113), [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L119)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L229), [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L229), [235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L235), [235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L235), [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L237), [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L239), [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L249), [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L249)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [286](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L286), [289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289), [300](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L300)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [325](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L325), [327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L327), [335](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L335)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [358](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L358), [359](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L359), [360](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L360), [362](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L362), [364](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L364), [365](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L365)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [394](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L394), [398](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L398), [404](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L404), [410](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L410), [423](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L423), [436](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436), [437](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L437)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [482](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L482), [483](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L483), [485](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L485), [486](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L486), [488](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L488), [492](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L492), [493](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L493), [496](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496), [496](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496), [496](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [526](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L526), [529](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L529), [530](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L530)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41), [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L44)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L112), [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L126)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L159), [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L160), [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L161), [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L162)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L187), [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L188)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L208), [222](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L222), [223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L223)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [330](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L330), [331](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L331), [336](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L336)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L102), [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L105)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L119), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L122)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L137), [138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L138)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L157), [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L158)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [199](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L199), [200](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L200), [216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L216)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L239), [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L251), [253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L253), [257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L257)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L23), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L35), [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L37), [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L41)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L67), [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L68)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L97), [101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L101)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L97), [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L103)

### [G-13]<a name="g-13"></a> `require()`/`revert()` strings longer than 32 bytes cost extra gas

Each extra memory word of bytes past the original 32 [incurs an MSTORE](https://gist.github.com/hrkrshnn/ee8fabd532058307229d65dcd5836ddc#consider-having-short-revert-strings)

*There are 53 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
77	        require(
78	            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
79	            "L1SharedBridge: not bridgehub or era chain"
80	        );
...
157	            require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");
...
197	        require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");
...
429	            require(!alreadyFinalized, "Withdrawal is already finalized 2");
...
524	            revert("ShB Incorrect message function selector");
...
566	        require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
```

*GitHub* : [77..80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L77-L80), [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L157), [197](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L197), [429](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L429), [524](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L524), [566](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L566)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
85	        require(
86	            !stateTransitionManagerIsRegistered[_stateTransitionManager],
87	            "Bridgehub: state transition already registered"
88	        );
...
95	        require(
96	            stateTransitionManagerIsRegistered[_stateTransitionManager],
97	            "Bridgehub: state transition not registered yet"
98	        );
...
104	        require(!tokenIsRegistered[_token], "Bridgehub: token already registered");
...
127	        require(
128	            stateTransitionManagerIsRegistered[_stateTransitionManager],
129	            "Bridgehub: state transition not registered"
130	        );
```

*GitHub* : [85..88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L85-L88), [95..98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L95-L98), [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L104), [127..130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L127-L130), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134), [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L227), [302..305](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L302-L305)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L61), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L67), [73..76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L73-L76), [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L174), [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L179), [193](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L193), [198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L198), [218](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L218), [219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L219), [242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L242)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L258)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L64), [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L70)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92), [107..110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L107-L110), [112..115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L112-L115), [118..121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L118-L121)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [228..231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L228-L231), [616](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41), [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L160), [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L187), [208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L208)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol


*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L24), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L29), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L34), [39..42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L39-L42), [47..50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L47-L50), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L55)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L192), [207..210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L207-L210), [240..243](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L240-L243), [244..247](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L244-L247), [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L251), [252..255](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L252-L255)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [24..28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L24-L28), [29..32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L29-L32), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L35), [36..39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L36-L39)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L94)

### [G-14]<a name="g-14"></a> Stack variable used as a cheaper cache for a state variable is only used once

If the variable is only accessed once, it's cheaper to use the state variable directly that one time, and save the 3 gas the extra stack assignment would spend

*There are 91 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
77	    function l2TokenAddress(address _l1Token) external view returns (address) {
...
135	    function deposit(
136	        address _l2Receiver,
137	        address _l1Token,
138	        uint256 _amount,
139	        uint256 _l2TxGasLimit,
140	        uint256 _l2TxGasPerPubdataByte,
141	        address _refundRecipient
142	    ) public payable nonReentrant returns (bytes32 l2TxHash) {
...
162	    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
...
210	    function finalizeWithdrawal(
211	        uint256 _l2BatchNumber,
212	        uint256 _l2MessageIndex,
213	        uint16 _l2TxNumberInBatch,
214	        bytes calldata _message,
215	        bytes32[] calldata _merkleProof
216	    ) external nonReentrant {
```

*GitHub* : [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L77), [135..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L135-L142), [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L162), [210..216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L210-L216)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
118	    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
...
150	    function bridgehubDepositBaseToken(
151	        uint256 _chainId,
152	        address _prevMsgSender,
153	        address _l1Token,
154	        uint256 _amount
155	    ) external payable virtual onlyBridgehubOrEra(_chainId) {
...
175	    function _depositFunds(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
...
184	    function bridgehubDeposit(
185	        uint256 _chainId,
186	        address _prevMsgSender,
187	        uint256, // l2Value, needed for Weth deposits in the future
188	        bytes calldata _data
189	    ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
...
245	    function _getDepositL2Calldata(
246	        address _l1Sender,
247	        address _l2Receiver,
248	        address _l1Token,
249	        uint256 _amount
250	    ) internal view returns (bytes memory) {
...
256	    function _getERC20Getters(address _token) internal view returns (bytes memory) {
```

*GitHub* : [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118), [150..155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L150-L155), [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175), [184..189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L184-L189), [245..250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L245-L250), [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L256), [305..316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L305-L316), [411..418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L411-L418), [460..465](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L460-L465), [556..564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L556-L564)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L53), [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62), [154..160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L154-L160), [166..172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L166-L172), [178..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L178-L186), [200..205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L200-L205), [219..221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L219-L221), [264..266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L264-L266)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L226)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [81..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L81-L83), [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L112), [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L121), [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L179), [241..247](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L241-L247)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [110..113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L110-L113), [128..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L128-L132), [184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L184), [205..208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L205-L208)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L25), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34), [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L60), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L69), [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L81), [102..105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L102-L105)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [34..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L34-L38), [105..109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L105-L109), [275..279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L275-L279), [310](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L310), [323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L323), [388..392](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L388-L392), [440](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L440), [500..505](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L500-L505), [537..542](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542), [605..609](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L605-L609), [625..628](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L625-L628), [679](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L679)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L159), [165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L165), [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L204), [219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L219), [225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L225), [231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L231)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L40), [76..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L76-L83), [106..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L106-L111), [145..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L145-L149), [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158), [260..265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L260-L265)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L94), [111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L111), [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L128), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L144)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L49)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L41), [62..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L62-L67)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L98), [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L128), [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L151), [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L174), [191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L191), [207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L207), [280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L280)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


*GitHub* : [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L20), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L40)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [130..132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L130-L132)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L48)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [51..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L51-L56), [81..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L81-L87), [111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L111), [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L125), [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L151), [166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L166)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L52), [113..118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L113-L118)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [103..108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L103-L108)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39), [78..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L78-L83)

### [G-15]<a name="g-15"></a> State variables access within a loop

State variable reads and writes are more expensive than local variable reads and writes. Therefore, it is recommended to replace state variable reads and writes within loops with a local variable. Gas savings should be multiplied by the average loop length.

*There are 8 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
118	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
119	                committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);
120	            }
...
137	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
138	                committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);
139	            }
...
187	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
188	                uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
189	                    _newBatchesData[i].batchNumber
190	                );
191	
192	                // Note: if the `commitBatchTimestamp` is zero, that means either:
193	                // * The batch was committed, but not through this contract.
194	                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
195	                // We allow executing such batches.
196	
197	                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
198	            }
...
211	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
212	                uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
213	
214	                // Note: if the `commitBatchTimestamp` is zero, that means either:
215	                // * The batch was committed, but not through this contract.
216	                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
217	                // We allow executing such batches.
218	
219	                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
220	            }
```

*GitHub* : [118..120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L118-L120), [137..139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L137-L139), [187..198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L187-L198), [211..220](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L211-L220)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
259	        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
260	            _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));
261	
262	            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
263	            emit BlockCommit(
264	                _lastCommittedBatchData.batchNumber,
265	                _lastCommittedBatchData.batchHash,
266	                _lastCommittedBatchData.commitment
267	            );
268	        }
...
291	        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
292	            // The upgrade transaction must only be included in the first batch.
293	            bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
294	            _lastCommittedBatchData = _commitOneBatch(
295	                _lastCommittedBatchData,
296	                _newBatchesData[i],
297	                expectedUpgradeTxHash
298	            );
299	
300	            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
301	            emit BlockCommit(
302	                _lastCommittedBatchData.batchNumber,
303	                _lastCommittedBatchData.batchHash,
304	                _lastCommittedBatchData.commitment
305	            );
306	        }
...
313	        for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {
314	            PriorityOperation memory priorityOp = s.priorityQueue.popFront();
315	            concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));
316	        }
...
407	        for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {
408	            currentTotalBatchesVerified = currentTotalBatchesVerified.uncheckedInc();
409	            require(
410	                _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
411	                "o1"
412	            );
413	
414	            bytes32 currentBatchCommitment = _committedBatches[i].commitment;
415	            proofPublicInput[i] = _getBatchProofPublicInput(
416	                prevBatchCommitment,
417	                currentBatchCommitment,
418	                verifierParams
419	            );
420	
421	            prevBatchCommitment = currentBatchCommitment;
422	        }
```

*GitHub* : [259..268](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L259-L268), [291..306](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L291-L306), [313..316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313-L316), [407..422](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L407-L422)

### [G-16]<a name="g-16"></a> Newer versions of solidity are more gas efficient

The solidity language continues to pursue more efficient gas optimization schemes. Adopting a [newer version of solidity](https://github.com/ethereum/solc-js/tags) can be more gas efficient.

*There are 62 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
1	pragma solidity 0.8.20;
```

*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L1)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
1	pragma solidity 0.8.20;
```

*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L1)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
1	pragma solidity 0.8.20;
```

*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L1)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
1	pragma solidity 0.8.20;
```

*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
1	pragma solidity 0.8.20;
```

*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
1	pragma solidity 0.8.20;
```

*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

```solidity
1	pragma solidity 0.8.20;
```

*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

```solidity
1	pragma solidity 0.8.20;
```

*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

```solidity
1	pragma solidity 0.8.20;
```

*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
1	pragma solidity 0.8.20;
```

*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L1)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L1)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L1)


---

	 - code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L1)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L1)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L1)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L1)


---

	 - code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L1)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L1)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L1)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L1)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L1)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L1)


---

	 - code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L1)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L1)


---

	 - code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L1)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L1)


---

	 - code/contracts/ethereum/contracts/common/Config.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L1)


---

	 - code/contracts/ethereum/contracts/common/L2ContractAddresses.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L1)


---

	 - code/contracts/ethereum/contracts/common/Messaging.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L1)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L1)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L1)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L1)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L1)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L1)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L1)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L1)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L1)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L1)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L1)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L1)


---

	 - code/contracts/zksync/contracts/ForceDeployUpgrader.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L1)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L1)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [1](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L1)

### [G-17]<a name="g-17"></a> Consider activating `via-ir` for deploying

The IR-based code generator was developed to make code generation more performant by enabling optimization passes that can be applied across functions.

It is possible to activate the IR-based code generator through the command line by using the flag `--via-ir` or by including the option `{"viaIR": true}`.

Keep in mind that compiling with this option may take longer. However, you can simply test it before deploying your code. If you find that it provides better performance, you can add the `--via-ir` flag to your deploy command.

*There are 1 instance(s) of this issue:*

*GitHub* : [project\2024-03-zksync](https://github.com/code-423n4/2024-03-zksync/blob/main/#L0)

### [G-18]<a name="g-18"></a> Function calls should be cached instead of re-calling the function

Consider caching the result instead of re-calling the function when possible. Note: this also includes casts, which cost between 42-46 gas, depending on the type.

*There are 8 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
162	    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```

*GitHub* : [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L162)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
118	    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
...
175	    function _depositFunds(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
...
489	    function _parseL2WithdrawalMessage(
490	        uint256 _chainId,
491	        bytes memory _l2ToL1message
492	    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
```

*GitHub* : [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118), [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175), [489..492](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L489-L492)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
169	    function execute(Operation calldata _operation) external payable onlyOwnerOrSecurityCouncil {
...
188	    function executeInstant(Operation calldata _operation) external payable onlySecurityCouncil {
```

*GitHub* : [169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L169), [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L188)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
625	    function _verifyBlobInformation(
626	        bytes calldata _pubdataCommitments,
627	        bytes32[] memory _blobHashes
628	    ) internal view returns (bytes32[] memory blobCommitments) {
```

*GitHub* : [625..628](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L625-L628)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

```solidity
81	    function finalizeDeposit(
82	        address _l1Sender,
83	        address _l2Receiver,
84	        address _l1Token,
85	        uint256 _amount,
86	        bytes calldata _data
87	    ) external payable override {
```

*GitHub* : [81..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L81-L87)

### [G-19]<a name="g-19"></a> Add `unchecked` blocks for divisions where the operands cannot overflow

`uint` divisions can't overflow, while `int` divisions can overflow only in [one specific case](https://docs.soliditylang.org/en/latest/types.html#division).

Consider adding an `unchecked` block to have some [gas savings](https://gist.github.com/DadeKuma/3bc597338ae774b8b3bd43280d55271f).

*There are 8 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
161	        uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
162	            s.baseTokenGasPriceMultiplierDenominator;
...
170	            batchOverheadBaseToken /
171	            uint256(feeParams.maxPubdataPerBatch);
...
173	        uint256 l2GasPrice = feeParams.minimalL2GasPrice + batchOverheadBaseToken / uint256(feeParams.maxL2GasPerBatch);
...
174	        uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata;
```

*GitHub* : [161..162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L161-L162), [170..171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L170-L171), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L173), [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L174)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

```solidity
27	        uint256 bytecodeLenInWords = _bytecode.length / 32;
```

*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L27)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

```solidity
25	            uint256 mapValue = _map.map[_index / 8];
...
45	            uint256 mapIndex = _index / 8;
```

*GitHub* : [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L25), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L45)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

```solidity
32	        require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");
```

*GitHub* : [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L32)

### [G-20]<a name="g-20"></a> Consider pre-calculating the address of `address(this)`

It can be more gas-efficient to use a hardcoded address instead of the `address(this)` expression, especially if you need to use the same address multiple times in your contract.

The reason for this, is that using `address(this)` requires an additional `EXTCODESIZE` operation to retrieve the contract’s address from its bytecode, which can increase the gas cost of your contract. By pre-calculating and using a hardcoded address, you can avoid this additional operation and reduce the overall gas cost of your contract.

Save 100 - 2600 Gas

*There are 12 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
67	        uint256 amount = IERC20(_token).balanceOf(address(this));
```

*GitHub* : [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
129	            uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
...
133	            uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
...
120	            uint256 balanceBefore = address(this).balance;
...
122	            uint256 balanceAfter = address(this).balance;
...
176	        uint256 balanceBefore = _token.balanceOf(address(this));
...
177	        _token.safeTransferFrom(_from, address(this), _amount);
...
178	        uint256 balanceAfter = _token.balanceOf(address(this));
```

*GitHub* : [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129), [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133), [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L122), [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176), [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L177), [178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L178)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
61	        require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
```

*GitHub* : [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L61)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
267	            bytes32(uint256(uint160(address(this)))),
```

*GitHub* : [267](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L267)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L43)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L155)

### [G-21]<a name="g-21"></a> Consider using `bytes32` rather than a `string`

Using the `bytes` types for fixed-length strings is more efficient than having the EVM have to incur the overhead of string processing. Consider whether the value _needs_ to be a `string`. A good reason to keep it as a `string` would be if the variable is defined in an interface that this project does not own.

*There are 12 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol

```solidity
11	    function getName() external view returns (string memory);
```

*GitHub* : [11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L11)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
65	        string memory decodedName;
...
66	        string memory decodedSymbol;
...
77	        try this.decodeString(nameBytes) returns (string memory nameString) {
...
83	        try this.decodeString(symbolBytes) returns (string memory symbolString) {
...
115	        string memory _newName,
...
116	        string memory _newSymbol,
...
161	    function name() public view override returns (string memory) {
...
167	    function symbol() public view override returns (string memory) {
...
180	    function decodeString(bytes memory _input) external pure returns (string memory result) {
```

*GitHub* : [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L65), [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L66), [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L77), [83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L83), [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L115), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L116), [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L161), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167), [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L180)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L8), [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L8)

### [G-22]<a name="g-22"></a> Optimize Zero Checks Using Assembly

The usage of inline assembly to check if variable is the zero can save gas compared to traditional `require` or `if` statement checks. 

The assembly check uses the `extcodesize` operation which is generally cheaper in terms of gas.

[More information can be found here.](https://medium.com/@kalexotsu/solidity-assembly-checking-if-an-address-is-0-efficiently-d2bfe071331)

*There are 99 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
143	        require(_amount != 0, "0T"); // empty deposit
...
188	        require(amount != 0, "2T"); // empty deposit
```

*GitHub* : [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L143), [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L188)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
110	        require(_owner != address(0), "ShB owner 0");
...
131	            require(amount > 0, "ShB: 0 amount to transfer");
...
160	            require(msg.value == 0, "ShB m.v > 0 b d.it");
...
190	        require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
...
204	            require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
...
202	            require(_depositAmount == 0, "ShB wrong withdraw amount");
...
210	        require(amount != 0, "6T"); // empty deposit amount
...
329	        require(_amount > 0, "y1");
```

*GitHub* : [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L110), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131), [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L160), [190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L190), [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L204), [202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202), [210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L210), [329](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L329), [565](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L565), [580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L580)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L124), [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134), [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L227), [328](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L328), [331](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L331)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L44), [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L109), [242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L242)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L84), [248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L248)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L28), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol


*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L27), [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L32)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [193](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L193), [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L239), [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L239), [286](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L286), [293](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L293), [363](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L363), [431](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L431), [593](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L593), [631](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631), [633](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L633), [639](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L639), [663](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L663), [669](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L669), [669](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L669), [670](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670), [670](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L171), [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L185)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L160), [277](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L277), [279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L279)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L95), [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L112), [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L133), [150](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L150), [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L151), [152](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L152), [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L188), [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L251), [253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L253)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L35), [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L37)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25), [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L109), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L134), [143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L143), [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L157), [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L163), [177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L177), [183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L183), [196](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L196), [215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L215), [252](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L252), [281](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L281), [282](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L282)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L26), [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L32)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L52), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L53), [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L54), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55), [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L56), [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L58), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L59), [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L60), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L61), [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L62)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L60)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L57), [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L58), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L59), [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L60), [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L70), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L94), [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L98), [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L126), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L131)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L53)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L61)

### [G-23]<a name="g-23"></a> Consider using `assembly` to write address storage values if the address variable is mutable

Writing address storage values using `assembly` can be more gas efficient when the address variable is mutable.
The following instances show mutable address storage variables that could be optimized using `assembly`.

*There are 35 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
510	            l1Token = bridgehub.baseToken(_chainId);
...
581	                refundRecipient = _prevMsgSender != tx.origin
582	                    ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
583	                    : _prevMsgSender;
```

*GitHub* : [510](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L510), [581..583](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L581-L583)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
57	        pendingAdmin = _newPendingAdmin;
...
67	        admin = currentPendingAdmin;
...
335	            _recipient = _refundRecipient;
...
333	            _recipient = AddressAliasHelper.applyL1ToL2Alias(_refundRecipient);
...
330	            _recipient = msg.sender == tx.origin ? msg.sender : AddressAliasHelper.applyL1ToL2Alias(msg.sender);
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L57), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L67), [335](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L335), [333](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L333), [330](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L330)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
48	        securityCouncil = _securityCouncil;
...
260	        securityCouncil = _newSecurityCouncil;
```

*GitHub* : [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L48), [260](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L260)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
87	        genesisUpgrade = _initializeData.genesisUpgrade;
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L87), [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L89), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L116), [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L126), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L135)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


*GitHub* : [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L33), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L34), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L35), [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L36), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L40), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L49)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L29), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L39)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L237), [250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L250), [252](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L252), [255](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L255), [280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L280), [282](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L282)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L32), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L42)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L62)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L54), [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L56)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L32), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L42)

### [G-24]<a name="g-24"></a> Consider Caching Multiple Accesses to Mappings/Arrays

Leveraging a local variable to cache these values when accessed more than once can yield a gas saving of approximately 42 units per access. This reduction is attributed to eliminating the need for recalculating the key's keccak256 hash (which costs Gkeccak256 - 30 gas) and the associated stack operations. For arrays, this also prevents the overhead of re-computing offsets in memory or calldata.

*There are 29 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
135	    function deposit(
136	        address _l2Receiver,
137	        address _l1Token,
138	        uint256 _amount,
139	        uint256 _l2TxGasLimit,
140	        uint256 _l2TxGasPerPubdataByte,
141	        address _refundRecipient
142	    ) public payable nonReentrant returns (bytes32 l2TxHash) {
...
178	    function claimFailedDeposit(
179	        address _depositSender,
180	        address _l1Token,
181	        bytes32 _l2TxHash,
182	        uint256 _l2BatchNumber,
183	        uint256 _l2MessageIndex,
184	        uint16 _l2TxNumberInBatch,
185	        bytes32[] calldata _merkleProof
186	    ) external nonReentrant {
```

*GitHub* : [135..142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L135-L142), [178..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L178-L186)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
118	    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
...
184	    function bridgehubDeposit(
185	        uint256 _chainId,
186	        address _prevMsgSender,
187	        uint256, // l2Value, needed for Weth deposits in the future
188	        bytes calldata _data
189	    ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
...
234	    function bridgehubConfirmL2Transaction(
235	        uint256 _chainId,
236	        bytes32 _txDataHash,
237	        bytes32 _txHash
238	    ) external override onlyBridgehub {
...
305	    function _claimFailedDeposit(
306	        bool _checkedInLegacyBridge,
307	        uint256 _chainId,
308	        address _depositSender,
309	        address _l1Token,
310	        uint256 _amount,
311	        bytes32 _l2TxHash,
312	        uint256 _l2BatchNumber,
313	        uint256 _l2MessageIndex,
314	        uint16 _l2TxNumberInBatch,
315	        bytes32[] calldata _merkleProof
316	    ) internal nonReentrant {
...
411	    function _finalizeWithdrawal(
412	        uint256 _chainId,
413	        uint256 _l2BatchNumber,
414	        uint256 _l2MessageIndex,
415	        uint16 _l2TxNumberInBatch,
416	        bytes calldata _message,
417	        bytes32[] calldata _merkleProof
418	    ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
...
556	    function depositLegacyErc20Bridge(
557	        address _prevMsgSender,
558	        address _l2Receiver,
559	        address _l1Token,
560	        uint256 _amount,
561	        uint256 _l2TxGasLimit,
562	        uint256 _l2TxGasPerPubdataByte,
563	        address _refundRecipient
564	    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
```

*GitHub* : [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118), [184..189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L184-L189), [234..238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L234-L238), [305..316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L305-L316), [411..418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L411-L418), [556..564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L556-L564)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
84	    function addStateTransitionManager(address _stateTransitionManager) external onlyOwner {
...
94	    function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner {
```

*GitHub* : [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L84), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L94), [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L103), [116..123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L116-L123)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L179), [241..247](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L241-L247)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L80), [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L89)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [34..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L34-L38), [388..392](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L388-L392)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L165), [183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183), [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L204)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L98), [191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L191), [207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L207), [230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L230), [259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L259)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


*GitHub* : [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L40)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L74)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [81..87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L81-L87)

### [G-25]<a name="g-25"></a> Optimize Gas by Using Do-While Loops

Using `do-while` loops instead of `for` loops can be more gas-efficient. 
Even if you add an `if` condition to account for the case where the loop doesn't execute at all, a `do-while` loop can still be cheaper in terms of gas.

*There are 22 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
227	        for (uint256 i = 0; i < _calls.length; ++i) {
228	            (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
229	            if (!success) {
230	                // Propagate an error if the call fails.
231	                assembly {
232	                    revert(add(returnData, 0x20), mload(returnData))
233	                }
234	            }
235	        }
```

*GitHub* : [227..235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L227-L235)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
118	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
119	                committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);
120	            }
...
137	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
138	                committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);
139	            }
...
187	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
188	                uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
189	                    _newBatchesData[i].batchNumber
190	                );
191	
192	                // Note: if the `commitBatchTimestamp` is zero, that means either:
193	                // * The batch was committed, but not through this contract.
194	                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
195	                // We allow executing such batches.
196	
197	                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
198	            }
...
211	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
212	                uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
213	
214	                // Note: if the `commitBatchTimestamp` is zero, that means either:
215	                // * The batch was committed, but not through this contract.
216	                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
217	                // We allow executing such batches.
218	
219	                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
220	            }
```

*GitHub* : [118..120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L118-L120), [137..139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L137-L139), [187..198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L187-L198), [211..220](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L211-L220)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
144	        for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
145	            // Extract the values to be compared to/used such as the log sender, key, and value
146	            (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
147	            (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
148	            (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);
149	
150	            // Ensure that the log hasn't been processed already
151	            require(!_checkBit(processedLogs, uint8(logKey)), "kp");
152	            processedLogs = _setBit(processedLogs, uint8(logKey));
153	
154	            // Need to check that each log was sent by the correct address.
155	            if (logKey == uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)) {
156	                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");
157	                logOutput.l2LogsTreeRoot = logValue;
158	            } else if (logKey == uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)) {
159	                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");
160	                logOutput.pubdataHash = logValue;
161	            } else if (logKey == uint256(SystemLogKey.STATE_DIFF_HASH_KEY)) {
162	                require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");
163	                logOutput.stateDiffHash = logValue;
164	            } else if (logKey == uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)) {
165	                require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");
166	                logOutput.packedBatchAndL2BlockTimestamp = uint256(logValue);
167	            } else if (logKey == uint256(SystemLogKey.PREV_BATCH_HASH_KEY)) {
168	                require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");
169	                logOutput.previousBatchHash = logValue;
170	            } else if (logKey == uint256(SystemLogKey.CHAINED_PRIORITY_TXN_HASH_KEY)) {
171	                require(logSender == L2_BOOTLOADER_ADDRESS, "bl");
172	                logOutput.chainedPriorityTxsHash = logValue;
173	            } else if (logKey == uint256(SystemLogKey.NUMBER_OF_LAYER_1_TXS_KEY)) {
174	                require(logSender == L2_BOOTLOADER_ADDRESS, "bk");
175	                logOutput.numberOfLayer1Txs = uint256(logValue);
176	            } else if (logKey == uint256(SystemLogKey.BLOB_ONE_HASH_KEY)) {
177	                require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");
178	                logOutput.blob1Hash = logValue;
179	            } else if (logKey == uint256(SystemLogKey.BLOB_TWO_HASH_KEY)) {
180	                require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");
181	                logOutput.blob2Hash = logValue;
182	            } else if (logKey == uint256(SystemLogKey.EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY)) {
183	                require(logSender == L2_BOOTLOADER_ADDRESS, "bu");
184	                require(_expectedSystemContractUpgradeTxHash == logValue, "ut");
185	            } else {
186	                revert("ul");
187	            }
188	        }
...
259	        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
260	            _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));
261	
262	            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
263	            emit BlockCommit(
264	                _lastCommittedBatchData.batchNumber,
265	                _lastCommittedBatchData.batchHash,
266	                _lastCommittedBatchData.commitment
267	            );
268	        }
...
291	        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
292	            // The upgrade transaction must only be included in the first batch.
293	            bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
294	            _lastCommittedBatchData = _commitOneBatch(
295	                _lastCommittedBatchData,
296	                _newBatchesData[i],
297	                expectedUpgradeTxHash
298	            );
299	
300	            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
301	            emit BlockCommit(
302	                _lastCommittedBatchData.batchNumber,
303	                _lastCommittedBatchData.batchHash,
304	                _lastCommittedBatchData.commitment
305	            );
306	        }
...
313	        for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {
314	            PriorityOperation memory priorityOp = s.priorityQueue.popFront();
315	            concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));
316	        }
...
353	        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
354	            _executeOneBatch(_batchesData[i], i);
355	            emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
356	        }
```

*GitHub* : [144..188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L144-L188), [259..268](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L259-L268), [291..306](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L291-L306), [313..316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313-L316), [353..356](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353-L356), [407..422](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L407-L422), [580..583](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580-L583), [636..658](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636-L658), [667..673](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667-L673)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [210..215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L210-L215)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [358..365](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L358-L365)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [228..233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L228-L233)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [103..120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L103-L120), [140..146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L140-L146), [160..169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L160-L169), [180..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L180-L186)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [31..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L31-L36)

### [G-26]<a name="g-26"></a> Use Assembly for Efficient Event Emission

To efficiently emit events, consider utilizing assembly by making use of scratch space and the free memory pointer.
This approach can potentially avoid the costs associated with memory expansion.

However, it's crucial to cache and restore the free memory pointer for safe optimization.
Good examples of such practices can be found in well-optimized [Solady's codebases](https://github.com/Vectorized/solady/blob/main/src/tokens/ERC1155.sol#L167).
Please review your code and consider the potential gas savings of this approach.

*There are 65 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
157	        emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);
...
201	        emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);
...
227	        emit WithdrawalFinalized(l1Receiver, l1Token, amount);
```

*GitHub* : [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L157), [201](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L201), [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L227)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
170	        emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);
...
229	        emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);
...
241	        emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);
...
369	        emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);
...
456	        emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);
...
604	        emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
```

*GitHub* : [170](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L170), [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L229), [241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L241), [369](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L369), [456](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L456), [604](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L604)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
58	        emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
```

*GitHub* : [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L58), [70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L70), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L71), [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L147)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L49), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L52), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L134), [146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L146), [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L159), [182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L182), [201](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L201), [252](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L252), [259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L259)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L117), [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L129), [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L130), [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L229), [237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L237), [289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L289)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L85), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L94), [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L100)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L30), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L42), [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L43), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L49), [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L56), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L65), [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L77), [88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L88), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L94), [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L117), [127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L127), [141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L141), [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L151)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [263..267](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L263-L267), [301..305](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L301-L305), [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L355), [436](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436), [496](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [345..351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L345-L351)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L89), [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L106), [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L123), [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L139), [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L159), [258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L258)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L42), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L69)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L123)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L107), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L136)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L103), [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L128), [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L149), [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L158)

### [G-27]<a name="g-27"></a> Optimize External Calls with Assembly for Memory Efficiency

Using interfaces to make external contract calls in Solidity is convenient but can be inefficient in terms of memory utilization.
Each such call involves creating a new memory location to store the data being passed, thus incurring memory expansion costs. 

Inline assembly allows for optimized memory usage by re-using already allocated memory spaces or using the scratch space for smaller datasets.
This can result in notable gas savings, especially for contracts that make frequent external calls.

Additionally, using inline assembly enables important safety checks like verifying if the target address has code deployed to it using `extcodesize(addr)` before making the call, mitigating risks associated with contract interactions.

*There are 65 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
67	        uint256 amount = IERC20(_token).balanceOf(address(this));
...
147	        l2TxHash = sharedBridge.depositLegacyErc20Bridge{value: msg.value}(
...
147	        l2TxHash = sharedBridge.depositLegacyErc20Bridge{value: msg.value}(
...
163	        uint256 balanceBefore = _token.balanceOf(address(sharedBridge));
...
165	        uint256 balanceAfter = _token.balanceOf(address(sharedBridge));
...
191	        sharedBridge.claimFailedDepositLegacyErc20Bridge(
...
220	        (address l1Receiver, address l1Token, uint256 amount) = sharedBridge.finalizeWithdrawalLegacyErc20Bridge(
```

*GitHub* : [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67), [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L147), [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L147), [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L163), [165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L165), [191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L191), [220](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L220)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
129	            uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
...
130	            uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
...
132	            IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);
```

*GitHub* : [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129), [130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L130), [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132), [133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133), [121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L121), [140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L140), [176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176), [178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L178), [197](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L197), [318](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L318), [398](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L398), [425](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L425), [469](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L469), [479](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L479), [510](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L510), [597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L597), [597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L597)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L78), [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L139), [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L162), [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L174), [189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L189), [208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L208), [230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L230), [230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L230), [240](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L240), [280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L280), [280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L280), [290..291](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L290-L291), [290..291](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L290-L291), [306](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L306), [320](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L320)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L77), [163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L163), [168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L168), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L173), [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L228)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L64), [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L228)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L108)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L229), [444](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L444)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L45), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L45), [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L188), [222](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L222), [222](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L222)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L68), [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L106), [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L115), [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L128)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L77), [83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L83), [95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L95), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L122)


---

	 - code/contracts/zksync/contracts/ForceDeployUpgrader.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L16), [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L16)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L93)

### [G-28]<a name="g-28"></a> Use Assembly for Hash Calculations

In certain cases, using inline assembly to calculate hashes can lead to significant gas savings. Solidity's built-in keccak256 function is convenient but costs more gas than the equivalent assembly code. However, it's important to note that using assembly should be done with care as it's less readable and could increase the risk of introducing errors.

*There are 29 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
78	        bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
```

*GitHub* : [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L78)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
212	        bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));
...
343	                bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));
...
600	        bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
```

*GitHub* : [212](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L212), [343](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L343), [600](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L600)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
207	        return keccak256(abi.encode(_operation));
```

*GitHub* : [207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L207)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
102	        storedBatchZero = keccak256(abi.encode(batchZero));
...
104	        initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));
...
140	        initialCutHash = keccak256(abi.encode(_diamondCut));
...
149	        upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
...
158	        upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
```

*GitHub* : [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102), [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L104), [140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L140), [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L149), [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L158), [257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L257)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L106)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L65), [315](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L315), [460](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L460), [506](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L506), [507](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L507), [508](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L508), [512](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L512), [545](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L545), [588](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L588), [654](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L654)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L114), [140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L140), [334](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L334)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [214](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L214)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L69)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [152](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L152)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L110)

### [G-29]<a name="g-29"></a> Consider Using Solady's Gas Optimized Lib for Math

Utilizing gas-optimized math functions from libraries like [Solady](https://github.com/Vectorized/solady/blob/main/src/utils/FixedPointMathLib.sol) can lead to more efficient smart contracts.
This is particularly beneficial in contracts where these operations are frequently used.

*There are 29 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
108	        assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
```

*GitHub* : [108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L108)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

```solidity
53	        assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
```

*GitHub* : [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L53)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
578	        blobAuxOutputWords = new bytes32[](2 * TOTAL_BLOBS_IN_COMMITMENT);
...
581	            blobAuxOutputWords[i * 2] = _blobHashes[i];
...
582	            blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
...
632	        require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");
```

*GitHub* : [578](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L578), [581](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L581), [582](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L582), [632](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L632)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
151	        return l2GasPrice * _l2GasLimit;
...
161	        uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
162	            s.baseTokenGasPriceMultiplierDenominator;
...
161	        uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
...
165	            pubdataPriceBaseToken = L1_GAS_PER_PUBDATA_BYTE * l1GasPriceConverted;
```

*GitHub* : [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L151), [161..162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L161-L162), [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L161), [165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L165), [168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L168), [170..171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L170-L171), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L173), [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L174), [273](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L273)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L27), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L52)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


*GitHub* : [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L25), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L29), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L45), [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L50)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L32), [85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L85), [88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L88), [97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L97), [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L100), [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L100), [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L137)


---

	 - code/contracts/ethereum/contracts/common/Config.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L16)

### [G-30]<a name="g-30"></a> Trade-offs Between Modifiers and Internal Functions

In Solidity, both internal functions and modifiers are used to refactor and manage code, but they come with their own trade-offs, especially in terms of gas cost and flexibility.

#### Modifiers:
- Less runtime gas cost (saves around 24 gas per function call).
- Increases deployment gas cost due to repetitive code.
- Can only be executed at the start or end of a function.

#### Internal Functions:
- Lower deployment cost.
- Can be executed at any point in a function.
- Slightly higher runtime gas cost (24 gas) due to the need to jump to the function's location in bytecode.

#### Recommendations:
- Use modifiers for high-frequency functions where runtime gas cost matters the most.
- Use internal functions where the priority is reducing deployment gas cost or when you need more flexibility in the function's logic.

Example analysis shows that using modifiers can increase deployment costs by over 35k gas but save 24 gas per function call during runtime. Choose wisely based on your specific use case.

*There are 122 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
57	    constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
...
62	    function initialize() external reentrancyGuardInitializer {}
...
142	    ) public payable nonReentrant returns (bytes32 l2TxHash) {
...
186	    ) external nonReentrant {
...
216	    ) external nonReentrant {
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L57), [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L62), [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L142), [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186), [216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L216)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
70	    modifier onlyBridgehub() {
71	        require(msg.sender == address(bridgehub), "ShB not BH");
72	        _;
73	    }
...
76	    modifier onlyBridgehubOrEra(uint256 _chainId) {
77	        require(
78	            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
79	            "L1SharedBridge: not bridgehub or era chain"
80	        );
81	        _;
82	    }
...
85	    modifier onlyLegacyBridge() {
86	        require(msg.sender == address(legacyBridge), "ShB not legacy bridge");
87	        _;
88	    }
...
96	    ) reentrancyGuardInitializer {
...
109	    ) external reentrancyGuardInitializer initializer {
```

*GitHub* : [70..73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L70-L73), [76..82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L76-L82), [85..88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L85-L88), [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L96), [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L109), [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L109), [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L144), [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L155), [189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L189), [238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L238), [316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L316), [418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L418), [564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564), [564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564), [623](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L623), [655](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L655)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L40), [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L43), [47..50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L47-L50), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L53), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L84), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L94), [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L103), [110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L110), [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123), [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123), [221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L221), [266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L266)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [60..63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L60-L63), [66..69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L66-L69), [72..78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L72-L78), [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L131), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L144), [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L156), [169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L169), [188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L188), [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L251), [258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L258)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L60), [65..68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L65-L68), [71..74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L71-L74), [83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L83), [112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L112), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L134), [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L139), [148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L148), [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L157), [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L162), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L167), [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L172), [235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L235), [247](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L247)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [63..66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L63-L66), [69..72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L69-L72), [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L75), [80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L80), [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L89), [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98), [113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L113), [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L132), [148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L148), [155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L155), [166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L166), [178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L178), [184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L184), [208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L208)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L21), [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L26)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L25), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L47), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L53), [60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L60), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L69), [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L81), [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L91), [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L105), [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L125), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L135), [145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L145)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L204), [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L204), [213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L213), [213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L213), [342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L342), [342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L342), [347](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L347), [347](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L347), [374](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L374), [374](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L374), [384](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L384), [384](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L384), [472](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L472), [472](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L472), [477](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L477), [477](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L477)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L40), [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L51), [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L186), [232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L232)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol


*GitHub* : [17..20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L17-L20), [23..26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L23-L26), [28..31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L28-L31), [33..36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L33-L36), [38..44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L38-L44), [46..52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L46-L52), [54..57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L54-L57)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [43..46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L43-L46), [70..91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L70-L91)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L56)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L52), [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L118), [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L118), [131..134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L131-L134), [136..141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L136-L141), [147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L147), [156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L156)

### [G-31]<a name="g-31"></a> Consider Packing Small `uint` When it's Possible

Packing `uint` variables into the same storage slot can help in reducing gas costs.
This is particularly useful when storing or reading multiple smaller uints (e.g., uint80) in a single transaction.
Consider using bit manipulation to pack these variables.

If you pack two `uint` variables into a single `uint` storage slot, you'd perform only one SLOAD operation (800 gas) instead of two (1,600 gas) when you read them.
This saves 800 gas for each read operation involving the two variables.

Similarly, when you need to update both variables, a single SSTORE operation would cost you 20,000 gas instead of 40,000 gas, saving you another 20,000 gas. 

Example:
```Solidity
uint160 packedVariables;

function packVariables(uint80 x, uint80 y) external {
  packedVariables = uint160(x) << 80 | uint160(y);
}
```

*There are 4 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
55	    uint32 public executionDelay;
```

*GitHub* : [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

```solidity
24	    uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L24)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
33	    uint8 private decimals_;
```

*GitHub* : [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L33)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol

```solidity
24	    uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L24)

### [G-32]<a name="g-32"></a> Avoid Unnecessary Public Variables

Public storage variables increase the contract's size due to the implicit generation of public getter functions. 
This makes the contract larger and could increase deployment and interaction costs.

If you do not require other contracts to read these variables, consider making them `private` or `internal`. 

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

*There are 43 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
25	    IL1SharedBridge public immutable override sharedBridge;
...
29	    mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
30	        public isWithdrawalFinalized;
...
34	    mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
35	        public depositAmount;
...
38	    address public l2Bridge;
...
41	    address public l2TokenBeacon;
...
44	    bytes32 public l2TokenProxyBytecodeHash;
```

*GitHub* : [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L25), [29..30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L29-L30), [34..35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L34-L35), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L38), [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L41), [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L44)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
36	    address public immutable override l1WethAddress;
...
39	    IBridgehub public immutable override bridgehub;
...
42	    IL1ERC20Bridge public immutable override legacyBridge;
...
50	    mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;
```

*GitHub* : [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L36), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L39), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L42), [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L50), [54..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L54-L56), [59..60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L59-L60)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L20), [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L23), [25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L25), [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L28), [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L31), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L34)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L28), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L34), [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L37)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L29), [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L32), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L35), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L38), [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L41), [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L44), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L47), [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L50), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L53)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L28), [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L46), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L52), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L22)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L27)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L37)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L27), [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L31), [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L37)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L36), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L39)

### [G-33]<a name="g-33"></a> Optimize by Using Assembly for Low-Level Calls' Return Data

Even second return value from a low-level call is not assigned, it is still copied to memory, leading to additional gas costs.
By employing assembly, you can bypass this memory copying, achieving a 159 gas saving.

*There are 1 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
228	            (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```

*GitHub* : [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L228)

### [G-34]<a name="g-34"></a> Avoid Zero Transfers to Save Gas

Performing token or Ether transfers with a zero amount may result in unnecessary gas consumption. 
The absence of a zero-amount check before a transfer or send operation can lead to wasted gas, as the state of the contract remains the same even if the amount is zero. 
Adding a conditional check for zero amounts can prevent these costly, unnecessary operations, thereby optimizing the contract's gas usage.

*There are 4 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
65	    function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
...
162	    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```

*GitHub* : [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65), [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L162)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
175	    function _depositFunds(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
...
411	    function _finalizeWithdrawal(
412	        uint256 _chainId,
413	        uint256 _l2BatchNumber,
414	        uint256 _l2MessageIndex,
415	        uint16 _l2TxNumberInBatch,
416	        bytes calldata _message,
417	        bytes32[] calldata _merkleProof
418	    ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
```

*GitHub* : [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175), [411..418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L411-L418)

### [G-35]<a name="g-35"></a> Optimize Unsigned Integer Comparison With Zero

For unsigned integers, checking whether the integer is not equal to zero (`!= 0`) is less gas-intensive than checking whether it is greater than zero (`> 0`). 

This is because the Ethereum Virtual Machine (EVM) can perform a simple bitwise operation to check if any bit is set (which directly translates to `!= 0`), while checking for `> 0` requires additional logic.

As such, when dealing with unsigned integers in Solidity, it is recommended to use the `!= 0` comparison for gas optimization.

*There are 13 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
131	            require(amount > 0, "ShB: 0 amount to transfer");
...
329	        require(_amount > 0, "y1");
```

*GitHub* : [131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131), [329](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L329)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
331	        } else if (_refundRecipient.code.length > 0) {
```

*GitHub* : [331](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L331)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
431	        if (_proof.serializedProof.length > 0) {
...
593	        return (_bitMap & (1 << _index)) > 0;
...
631	        require(_pubdataCommitments.length > 0, "pl");
```

*GitHub* : [431](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L431), [593](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L593), [631](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

```solidity
160	        require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");
...
279	        if (refundRecipient.code.length > 0) {
```

*GitHub* : [160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L160), [279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L279)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
109	            require(selectors.length > 0, "B"); // no functions for diamond cut
...
134	        require(_facet.code.length > 0, "G");
```

*GitHub* : [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L109), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L134), [157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L157)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L26)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L126)

### [G-36]<a name="g-36"></a> Delete Unused State Variables

State variables that aren't used in the contract not only clutter the codebase but also consume unnecessary gas during deployment.
Specifically, setting non-zero initial values for state variables costs significant gas.
By removing these unused state variables, you can save on both deployment gas and potential future storage gas costs.
This optimization not only reduces gas expenditures but also enhances code clarity and maintainability.
Always ensure a thorough review to confirm that these variables are indeed redundant before removal.

*There are 18 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
47	    mapping(address => uint256) private __DEPRECATED_lastWithdrawalLimitReset;
...
50	    mapping(address => uint256) private __DEPRECATED_withdrawnAmountInWindow;
...
53	    mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L47), [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L50), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L53)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
123	    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
```

*GitHub* : [123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
228	            (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
```

*GitHub* : [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L228)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
28	    string public constant override getName = "ValidatorTimelock";
...
40	    error AddressAlreadyValidator(uint256 _chainId);
...
43	    error ValidatorDoesNotExist(uint256 _chainId);
...
228	        address contractAddress = stateTransitionManager.stateTransition(_chainId);
```

*GitHub* : [28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L28), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L40), [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L43), [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L228)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

```solidity
22	    string public constant override getName = "AdminFacet";
```

*GitHub* : [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L22)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L27)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L37), [359](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L359)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L265), [271](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L271)


---

	 - code/contracts/ethereum/contracts/common/ReentrancyGuard.sol


*GitHub* : [31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L31), [41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L41)

### [G-37]<a name="g-37"></a> Optimize Gas by Using Only Named Returns

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

*There are 187 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
77	    function l2TokenAddress(address _l1Token) external view returns (address) {
...
162	    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
```

*GitHub* : [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L77), [162](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L162)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
175	    function _depositFunds(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
...
245	    function _getDepositL2Calldata(
246	        address _l1Sender,
247	        address _l2Receiver,
248	        address _l1Token,
249	        uint256 _amount
250	    ) internal view returns (bytes memory) {
...
256	    function _getERC20Getters(address _token) internal view returns (bytes memory) {
...
376	    function _isEraLegacyWithdrawal(uint256 _chainId, uint256 _l2BatchNumber) internal view returns (bool) {
```

*GitHub* : [175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175), [245..250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L245-L250), [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L256), [376](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L376)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
77	    function getStateTransition(uint256 _chainId) public view returns (address) {
...
154	    function proveL2MessageInclusion(
155	        uint256 _chainId,
156	        uint256 _batchNumber,
157	        uint256 _index,
158	        L2Message calldata _message,
159	        bytes32[] calldata _proof
160	    ) external view override returns (bool) {
...
166	    function proveL2LogInclusion(
167	        uint256 _chainId,
168	        uint256 _batchNumber,
169	        uint256 _index,
170	        L2Log memory _log,
171	        bytes32[] calldata _proof
172	    ) external view override returns (bool) {
...
178	    function proveL1ToL2TransactionStatus(
179	        uint256 _chainId,
180	        bytes32 _l2TxHash,
181	        uint256 _l2BatchNumber,
182	        uint256 _l2MessageIndex,
183	        uint16 _l2TxNumberInBatch,
184	        bytes32[] calldata _merkleProof,
185	        TxStatus _status
186	    ) external view override returns (bool) {
```

*GitHub* : [77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L77), [154..160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L154-L160), [166..172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L166-L172), [178..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L178-L186), [200..205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L200-L205)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L86), [91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L91), [97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L97), [102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L102), [107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L107), [206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L206)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L76)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L104)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L26)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [34..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L34-L38), [453..457](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L453-L457), [500..505](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L500-L505), [515](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515), [525](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525), [537..542](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L542), [587](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L587), [592](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L592), [597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L34), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L39), [44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L44), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L49), [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L54), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L59), [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L64), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L69), [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L74), [79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L79), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L84), [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L89), [94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L94), [99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L99), [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L104), [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L109), [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L114), [119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L119), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L124), [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L129), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L134), [139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L139), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L144), [149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L149), [154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L154), [159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L159), [178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L178), [183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183), [190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L190), [195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L195), [219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L219), [225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L225), [231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L231), [241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L241), [246](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L246), [251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L251), [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L256), [261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L261)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [56..61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L56-L61), [66..71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L66-L71), [76..83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L76-L83), [106..111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L106-L111), [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L132), [145..149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L145-L149), [158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [182..186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L182-L186)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


*GitHub* : [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L49)


---

	 - code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol


*GitHub* : [15](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L15)


---

	 - code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L16)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [62..67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L62-L67)


---

	 - code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol


*GitHub* : [13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L13), [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L19)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [20..24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L20-L24)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L37), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L42), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L47), [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L52), [66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L66)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [71..75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L71-L75)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


*GitHub* : [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L26), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L69)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


*GitHub* : [60..64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L60-L64), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L116), [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L118), [120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L120), [122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L122), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L124)


---

	 - code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol


*GitHub* : [19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L19), [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L21), [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L23)


---

	 - code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol


*GitHub* : [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L65), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L67), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L69), [71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L71), [75..81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L75-L81), [83..89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L83-L89), [91..99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L91-L99), [109..114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L109-L114)


---

	 - code/contracts/ethereum/contracts/governance/IGovernance.sol


*GitHub* : [43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L43), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L45), [47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L47), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L49), [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L51), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L63)


---

	 - code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


*GitHub* : [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L45), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L55), [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L57), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L59), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L61), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L63), [65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L65), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L73)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


*GitHub* : [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L64)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol


*GitHub* : [21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L21), [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L24), [27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L27), [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L30), [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L33), [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L36), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L39), [42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L42), [45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L45), [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L48), [51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L51), [58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L58), [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L61), [64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L64), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L67), [75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L75), [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L78), [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L81), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L84), [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L87), [90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L90), [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L93), [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L100), [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L103), [108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L108), [111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L111), [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L114), [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L117), [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L132), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L135), [144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L144)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol


*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L16), [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L20), [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L24), [30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L30), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L38)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


*GitHub* : [20..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L20-L25), [33..38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L33-L38), [49..56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L49-L56), [109..113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L109-L113)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol


*GitHub* : [21..25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L21-L25), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L29)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol


*GitHub* : [11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L11)


---

	 - code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol


*GitHub* : [10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L10)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L111), [140..144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L140-L144), [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L151)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L161), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167), [173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L173)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol


*GitHub* : [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L36), [38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L38), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L40)


---

	 - code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol


*GitHub* : [18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L18), [20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L20)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L24), [55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L55), [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L92), [103..108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L103-L108)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L29)

### [G-38]<a name="g-38"></a> Use assembly in place of `abi.decode` to extract `calldata` values more efficiently

Instead of using abi.decode, we can use assembly to decode our desired calldata values directly. This will allow us to avoid decoding calldata values that we will not use.
For more details on how to implement this, check the following [report](https://code4rena.com/reports/2023-05-juicebox#g-04-use-assembly-in-place-of-abidecode-to-extract-calldata-values-more-efficiently)

*There are 9 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
192	        (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
```

*GitHub* : [192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L192)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
254	        Diamond.DiamondCutData memory diamondCut = abi.decode(_diamondCut, (Diamond.DiamondCutData));
```

*GitHub* : [254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L254)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
617	        (, uint256 result) = abi.decode(data, (uint256, uint256));
...
682	        versionedHash = abi.decode(data, (bytes32));
```

*GitHub* : [617](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L617), [682](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L682)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

```solidity
300	            require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1");
```

*GitHub* : [300](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L300)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

```solidity
179	        proxy = BeaconProxy(abi.decode(returndata, (address)));
```

*GitHub* : [179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L179)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

```solidity
59	        (bytes memory nameBytes, bytes memory symbolBytes, bytes memory decimalsBytes) = abi.decode(
...
181	        (result) = abi.decode(_input, (string));
...
186	        (result) = abi.decode(_input, (uint8));
```

*GitHub* : [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L59), [181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L181), [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L186)

### [G-39]<a name="g-39"></a> Optimize Address Storage Value Management with `assembly`



*There are 29 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
98	        l1WethAddress = _l1WethAddress;
...
114	        l2BridgeAddress[ERA_CHAIN_ID] = ERA_ERC20_BRIDGE_ADDRESS;
...
145	        l2BridgeAddress[_chainId] = _l2BridgeAddress;
```

*GitHub* : [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L98), [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L114), [145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L145)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
57	        pendingAdmin = _newPendingAdmin;
...
67	        admin = currentPendingAdmin;
...
136	        stateTransitionManager[_chainId] = _stateTransitionManager;
...
137	        baseToken[_chainId] = _baseToken;
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L57), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L67), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L136), [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L137)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
48	        securityCouncil = _securityCouncil;
...
260	        securityCouncil = _newSecurityCouncil;
```

*GitHub* : [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L48), [260](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L260)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
61	        bridgehub = _bridgehub;
```

*GitHub* : [61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L61), [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L87), [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L89), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L116), [126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L126), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L135), [236](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L236), [284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L284)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


*GitHub* : [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L33), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L34), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L35), [36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L36), [40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L40), [49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L49)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L29), [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L39)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L62), [101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L101)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L54), [56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L56)

### [G-40]<a name="g-40"></a> Use calldata instead of memory for function arguments that do not get mutated

Mark data types as `calldata` instead of `memory` where possible. This makes it so that the data is not automatically loaded into memory. If the data passed into the function does not need to be changed (like updating values in an array), it can be passed in as `calldata`. The one exception to this is if the argument must later be passed into another function that takes an argument that specifies `memory` storage.

*There are 54 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
462	        MessageParams memory _messageParams,
...
491	        bytes memory _l2ToL1message
```

*GitHub* : [462](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L462), [491](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L491)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
170	        L2Log memory _log,
```

*GitHub* : [170](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L170)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
35	        StoredBatchInfo memory _previousBatch,
...
202	        StoredBatchInfo memory _lastCommittedBatchData,
...
211	        StoredBatchInfo memory _lastCommittedBatchData,
...
218	        StoredBatchInfo memory _lastCommittedBatchData,
...
256	        StoredBatchInfo memory _lastCommittedBatchData,
...
276	        StoredBatchInfo memory _lastCommittedBatchData,
...
323	    function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {
```

*GitHub* : [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L35), [202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L202), [211](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L211), [218](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L218), [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L256), [276](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L276), [323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L323), [440](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L440), [456](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L456), [503](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L503), [504](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L504), [540](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L540), [541](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L541), [562](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L562), [563](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L563), [587](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L587), [627](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L627)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L50), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L59), [69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L69), [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L109), [132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L132), [231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L231), [262](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L262), [263](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L263), [264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L264), [292](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L292), [293](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L293), [294](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L294), [319](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L319), [320](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L320), [321](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L321), [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L355)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


*GitHub* : [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L98), [128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L128), [151](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L151), [174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L174), [280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L280)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L57)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


*GitHub* : [22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L22), [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L23), [48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L48)


---

	 - code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


*GitHub* : [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L52), [115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L115), [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L116), [180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L180), [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L185)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L92)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L39), [82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L82)

### [G-41]<a name="g-41"></a> Gas savings can be achieved by changing the model for assigning value to the structure

Change this `structName a = structName({item1: val1,item2: val2}); ==> structName a; a.item1 = val1; a.item2 = val2;`

*There are 19 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
221	            request = L2TransactionRequestTwoBridgesInner({
222	                magicValue: TWO_BRIDGES_MAGIC_VALUE,
223	                l2Contract: l2BridgeAddress[_chainId],
224	                l2Calldata: l2TxCalldata,
225	                factoryDeps: new bytes[](0),
226	                txDataHash: txDataHash
227	            });
...
432	        MessageParams memory messageParams = MessageParams({
433	            l2BatchNumber: _l2BatchNumber,
434	            l2MessageIndex: _l2MessageIndex,
435	            l2TxNumberInBatch: _l2TxNumberInBatch
436	        });
...
472	            l2ToL1Message = L2Message({
473	                txNumberInBatch: _messageParams.l2TxNumberInBatch,
474	                sender: l2Sender,
475	                data: _message
476	            });
...
586	            L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
587	                chainId: ERA_CHAIN_ID,
588	                l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
589	                mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
590	                l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
591	                l2Calldata: l2TxCalldata,
592	                l2GasLimit: _l2TxGasLimit,
593	                l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
594	                factoryDeps: new bytes[](0),
595	                refundRecipient: refundRecipient
596	            });
```

*GitHub* : [221..227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L221-L227), [432..436](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L432-L436), [472..476](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L472-L476), [586..596](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L586-L596)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

```solidity
241	            BridgehubL2TransactionRequest({
242	                sender: msg.sender,
243	                contractL2: _request.l2Contract,
244	                mintValue: _request.mintValue,
245	                l2Value: _request.l2Value,
246	                l2Calldata: _request.l2Calldata,
247	                l2GasLimit: _request.l2GasLimit,
248	                l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
249	                factoryDeps: _request.factoryDeps,
250	                refundRecipient: refundRecipient
251	            })
...
307	            BridgehubL2TransactionRequest({
308	                sender: _request.secondBridgeAddress,
309	                contractL2: outputRequest.l2Contract,
310	                mintValue: _request.mintValue,
311	                l2Value: _request.l2Value,
312	                l2Calldata: outputRequest.l2Calldata,
313	                l2GasLimit: _request.l2GasLimit,
314	                l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
315	                factoryDeps: outputRequest.factoryDeps,
316	                refundRecipient: refundRecipient
317	            })
```

*GitHub* : [241..251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L241-L251), [307..317](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L307-L317)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

```solidity
92	        IExecutor.StoredBatchInfo memory batchZero = IExecutor.StoredBatchInfo(
93	            0,
94	            _initializeData.genesisBatchHash,
95	            _initializeData.genesisIndexRepeatedStorageChanges,
96	            0,
97	            EMPTY_STRING_KECCAK,
98	            DEFAULT_L2_LOGS_TREE_ROOT_HASH,
99	            0,
100	            _initializeData.genesisBatchCommitment
101	        );
...
184	        L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
185	            txType: SYSTEM_UPGRADE_L2_TX_TYPE,
186	            from: uint256(uint160(L2_FORCE_DEPLOYER_ADDR)),
187	            to: uint256(uint160(L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR)),
188	            gasLimit: 72000000,
189	            gasPerPubdataByteLimit: REQUIRED_L2_GAS_PRICE_PER_PUBDATA,
190	            maxFeePerGas: uint256(0),
191	            maxPriorityFeePerGas: uint256(0),
192	            paymaster: uint256(0),
193	            // Note, that the priority operation id is used as "nonce" for L1->L2 transactions
194	            nonce: protocolVersion,
195	            value: 0,
196	            reserved: [uint256(0), 0, 0, 0],
197	            data: systemContextCalldata,
198	            signature: new bytes(0),
199	            factoryDeps: uintEmptyArray,
200	            paymasterInput: new bytes(0),
201	            reservedDynamic: new bytes(0)
202	        });
...
204	        ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
205	            l2ProtocolUpgradeTx: l2ProtocolUpgradeTx,
206	            factoryDeps: bytesEmptyArray,
207	            bootloaderHash: bytes32(0),
208	            defaultAccountHash: bytes32(0),
209	            verifier: address(0),
210	            verifierParams: VerifierParams({
211	                recursionNodeLevelVkHash: bytes32(0),
212	                recursionLeafLevelVkHash: bytes32(0),
213	                recursionCircuitsSetVksHash: bytes32(0)
214	            }),
215	            l1ContractsUpgradeCalldata: new bytes(0),
216	            postUpgradeCalldata: new bytes(0),
217	            upgradeTimestamp: 0,
218	            newProtocolVersion: protocolVersion
219	        });
...
210	            verifierParams: VerifierParams({
211	                recursionNodeLevelVkHash: bytes32(0),
212	                recursionLeafLevelVkHash: bytes32(0),
213	                recursionCircuitsSetVksHash: bytes32(0)
214	            }),
```

*GitHub* : [92..101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L92-L101), [184..202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L184-L202), [204..219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L204-L219), [210..214](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L210-L214), [222..226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L222-L226)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [89..98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L89-L98)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [214](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L214)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


*GitHub* : [94..101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L94-L101), [134..141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L134-L141), [210..220](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L210-L220), [296..314](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L296-L314), [337..341](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L337-L341)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [220..224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L220-L224)

### [G-42]<a name="g-42"></a> Use `Array.unsafeAccess` to avoid repeated array length checks

When using storage arrays, solidity adds an internal lookup of the array's length (a **Gcoldsload 2100 gas**) to ensure it doesn't read past the array's end.

It's possible to avoid this lookup by using `Array.unsafeAccess` in cases where the length has already been checked.

*There are 100 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
178	    function claimFailedDeposit(
179	        address _depositSender,
180	        address _l1Token,
181	        bytes32 _l2TxHash,
182	        uint256 _l2BatchNumber,
183	        uint256 _l2MessageIndex,
184	        uint16 _l2TxNumberInBatch,
185	        bytes32[] calldata _merkleProof
186	    ) external nonReentrant {
...
// @audit: array `depositAmount[_depositSender]` is accesed 2 times
187	        uint256 amount = depositAmount[_depositSender][_l1Token][_l2TxHash];
...
// @audit: array `depositAmount[_depositSender]` is accesed 2 times
189	        delete depositAmount[_depositSender][_l1Token][_l2TxHash];
...
// @audit: array `depositAmount[_depositSender][_l1Token]` is accesed 2 times
187	        uint256 amount = depositAmount[_depositSender][_l1Token][_l2TxHash];
...
// @audit: array `depositAmount[_depositSender][_l1Token]` is accesed 2 times
189	        delete depositAmount[_depositSender][_l1Token][_l2TxHash];
...
// @audit: array `depositAmount[_depositSender][_l1Token][_l2TxHash]` is accesed 2 times
187	        uint256 amount = depositAmount[_depositSender][_l1Token][_l2TxHash];
...
// @audit: array `depositAmount[_depositSender][_l1Token][_l2TxHash]` is accesed 2 times
189	        delete depositAmount[_depositSender][_l1Token][_l2TxHash];
```

*GitHub* : [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L187), [189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L189), [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L187), [189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L189), [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L187), [189](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L189)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
118	    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
...
// @audit: array `chainBalance[_targetChainId]` is accesed 4 times
124	            chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
...
// @audit: array `chainBalance[_targetChainId]` is accesed 4 times
125	                chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
```

*GitHub* : [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L124), [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L125), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L135), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L135), [124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L124), [125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L125), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L135), [135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L135), [223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L223), [190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L190), [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L239), [240](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L240), [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L239), [240](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L240), [342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L342), [345](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L345), [342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L342), [345](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L345), [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L351), [352](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L352), [351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L351), [352](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L352), [419](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L419), [420](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L420), [419](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L419), [420](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L420), [419](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L419), [420](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L420), [441](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L441), [442](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L442), [441](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L441), [442](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L442), [565](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L565), [588](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L588)


---

	 - code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


*GitHub* : [86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L86), [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L89), [96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L96), [99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L99), [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L104), [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L105), [134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134), [136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L136)


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol


*GitHub* : [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L228), [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L228), [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L228)


---

	 - code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


*GitHub* : [248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L248), [284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L284)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


*GitHub* : [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L81), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L84), [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L81), [84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L84), [90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L90), [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L93), [90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L90), [93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L93)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [354](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L354), [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L355), [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L355), [355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L355), [404](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L404), [410](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L410), [410](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L410), [414](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L414), [669](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L669), [670](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670), [669](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L669), [670](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


*GitHub* : [170](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L170), [172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L172), [185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L185), [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L186)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


*GitHub* : [104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L104), [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L105), [106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L106), [107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107), [194](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L194), [197](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L197), [210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L210), [216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L216), [225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L225), [234](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L234), [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L249), [235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L235), [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L239), [241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L241), [246](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L246)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


*GitHub* : [46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L46), [63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L63)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


*GitHub* : [33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L33), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L34)


---

	 - code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


*GitHub* : [80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L80), [81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L81)


---

	 - code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


*GitHub* : [97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L97), [101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L101)

### [G-43]<a name="g-43"></a> Consider using OpenZeppelin's `EnumerateSet` instead of nested mappings

Nested mappings and multi-dimensional arrays in Solidity operate through a process of double hashing, wherein the original storage slot and the first key are concatenated and hashed, and then this hash is again concatenated with the second key and hashed. This process can be quite gas expensive due to the double-hashing operation and subsequent storage operation (sstore).

OpenZeppelin's `EnumerableSet` provides a potential solution to this problem. It creates a data structure that combines the benefits of set operations with the ability to enumerate stored elements, which is not natively available in Solidity. EnumerableSet handles the element uniqueness internally and can therefore provide a more gas-efficient and collision-resistant alternative to nested mappings or multi-dimensional arrays in certain scenarios.

*There are 10 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

```solidity
29	    mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))
...
34	    mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
...
34	    mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))
...
53	    mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;
```

*GitHub* : [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L29), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L34), [34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L34), [53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L53)


---

	 - code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

```solidity
54	    mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
...
59	    mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
...
59	    mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
...
67	    mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;
```

*GitHub* : [54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L54), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L59), [59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L59), [67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L67)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
52	    mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```

*GitHub* : [52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L52)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

```solidity
116	    mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;
```

*GitHub* : [116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L116)

### [G-44]<a name="g-44"></a> Counting down in `for` statements is more gas efficient

Counting down is more gas efficient than counting up because neither we are making zero variable to non-zero variable and also we will get gas refund in the last transaction when making non-zero to zero variable. [More info](https://solodit.xyz/issues/g-02-counting-down-in-for-statements-is-more-gas-efficient-code4rena-pooltogether-pooltogether-git)

*There are 8 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
// @audit `i` is counter for the loop
227	        for (uint256 i = 0; i < _calls.length; ++i) {
...
 // @audit increment is used for counter
227	        for (uint256 i = 0; i < _calls.length; ++i) {
```

*GitHub* : [227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L227)


---

	 - code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

```solidity
// @audit `i` is counter for the loop
118	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
...
 // @audit increment is used for counter
118	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
...
// @audit `i` is counter for the loop
137	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
...
 // @audit increment is used for counter
137	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
...
// @audit `i` is counter for the loop
187	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
...
 // @audit increment is used for counter
187	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
...
// @audit `i` is counter for the loop
211	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
...
 // @audit increment is used for counter
211	            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
```

*GitHub* : [118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L118), [137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L137), [187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L187), [211](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L211)


---

	 - code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


*GitHub* : [580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580), [667](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667)


---

	 - code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


*GitHub* : [228](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L228)

### [G-45]<a name="g-45"></a> Do not calculate constants

Due to how constant variables are implemented (replacements at compile-time), an expression assigned to a constant variable is recomputed each time that the variable is used, which wastes some gas.

*There are 1 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/common/Config.sol

```solidity
16	uint256 constant MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES = 4 + L2_TO_L1_LOG_SERIALIZE_SIZE * 512;
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L16)



While it does not save gas for some simple binary expressions because the compiler knows that developers often make this mistake, it's still best to use the right tool for the task at hand. There is a difference between `constant` variables and `immutable` variables, and they should each be used in their appropriate contexts. `constants` should be used for literal values written into the code, and `immutable` variables should be used for expressions, or values calculated in, or passed into the constructor.

*There are 27 instance(s) of this issue:*


---

	 - code/contracts/ethereum/contracts/governance/Governance.sol

```solidity
24	    uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1);
```

*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L24)


---

	 - code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

```solidity
14	    bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");
```

*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L14)


---

	 - code/contracts/ethereum/contracts/common/Config.sol

```solidity
16	uint256 constant MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES = 4 + L2_TO_L1_LOG_SERIALIZE_SIZE * 512;
...
24	bytes32 constant DEFAULT_L2_LOGS_TREE_ROOT_HASH = bytes32(0);
...
87	address constant POINT_EVALUATION_PRECOMPILE_ADDR = address(0x0A);
...
103	address constant ETH_TOKEN_ADDRESS = address(1);
...
109	address constant ERA_ERC20_BRIDGE_ADDRESS = address(1233);
...
114	bytes32 constant TWO_BRIDGES_MAGIC_VALUE = bytes32(uint256(keccak256("TWO_BRIDGES_MAGIC_VALUE")) - 1);
...
117	address constant BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS = address(uint160(type(uint16).max));
```

*GitHub* : [16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L16), [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L24), [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L87), [103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L103), [109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L109), [114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L114), [117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L117)


---

	 - code/contracts/ethereum/contracts/common/L2ContractAddresses.sol

```solidity
8	address constant L2_BOOTLOADER_ADDRESS = address(0x8001);
```

*GitHub* : [8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L8), [11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L11), [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L14), [23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L23), [26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L26), [29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L29), [32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L32), [35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L35)


---

	 - code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L24)


---

	 - code/contracts/zksync/contracts/interfaces/IPaymaster.sol


*GitHub* : [14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L14)


---

	 - code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol


*GitHub* : [24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L24)


---

	 - code/contracts/zksync/contracts/L2ContractHelper.sol


*GitHub* : [72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L72), [73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L73), [74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L74), [76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L76), [78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L78), [87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L87)


---

	 - code/contracts/zksync/contracts/SystemContractsCaller.sol


*GitHub* : [9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L9)