## [G-01] CONSTANT STATE VARIABLES

The contract has defined state variables whose values are never modified throughout the contract.

The variables whose values never change should be marked as `constant` to save gas.

**INSTANCES:** 2

> ZkSyncStateTransitionStorage internal s

https://github.com//code-423n4/2024-03zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L12-L12

> VirtualBlockUpgradeInfo internal virtualBlockUpgradeInfo;

https://github.com//code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L80-L80

## [G-02] UNUSED NAMED RETURNS

Using both `named returns` and a return statement isn't necessary. Removing unused `named return` variables can reduce gas usage and improve code clarity.

**INSTANCES:** 1

> function getDeploymentNonce(address _address) external view returns (uint256 deploymentNonce) {
uint256 addressAsKey = uint256(uint160(_address));
(deploymentNonce, ) = _splitRawNonce(rawNonces[addressAsKey]);
return deploymentNonce;
}

https://github.com//code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L125-L130

## [G-03] BYTES CONSTANT MORE EFFICIENT THAN STRING LITERAL

The contract was found to be using `getName` string constant. This can be optimized by using `bytes32` constant to save gas.

Unless explicitly required, if the string is lesser than `32 bytes`, it is recommended to use `bytes32` constant instead of a string constant as it’ll save some gas.

**INSTANCES:** 5

> string public constant override getName = "GettersFacet";

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25-L25

> string public constant override getName = "ValidatorTimelock";

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26-L26

>  string public constant override getName = "AdminFacet";

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20-L20

> string public constant override getName = "ExecutorFacet";

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27-L27

> string public constant override getName = "MailboxFacet";

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35-L35

## [G-04] CODE OPTIMIZATION BY USING MAX AND MIN

The contract was using the expression `2**N` to calculate the maximum storage capacity of the data type. This both lacks readability and costs more gas.

`2**N` can be replaced by `type(uintN).max` or `type(uintN).min`, which is more readable and will also save some gas.

**INSTANCES:** 3

The contract is using the expression `2**16` to calculate the maximum storage capacity of the data type.

replaced by `type(uint16).max`, or `type(uint16).min`.

> require(bytecodeLenInWords < 2 ** 16, "pp");

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L26-L26

> uint256 private constant DEPLOY_NONCE_MULTIPLIER = 2 ** 128;

The contract is using the expression `2**128` to calculate the maximum storage capacity of the data type.

`2**128` can be replaced by `type(uint128).max` or `type(uint128).min`.

https://github.com//code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L28-L28

> uint256 private constant MAXIMAL_MIN_NONCE_INCREMENT = 2 ** 32;

The contract was using the expression `2**32` to calculate the maximum storage capacity of the data type. 

`2**32` can be replaced by `type(uint32).max` or type(uint32).min.

https://github.com//code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L31-L31

## [G-05] DEFINE CONSTRUCTOR AS PAYABLE

Developers can save around 10 opcodes and some gas if the constructors are defined as `payable`.

However, it should be noted that it comes with risks because payable constructors can accept ETH during deployment.

**INSTANCES:** 10

> constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11-L16

>  constructor(address _admin, address _securityCouncil, uint256 _minDelay) {

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L41-L51

> constructor() reentrancyGuardInitializer {}

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19-L19

> constructor() {

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L40-L43

>  constructor() {

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L41-L43

> constructor(address _initialOwner, uint32 _executionDelay) {

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55-L58

> constructor(address _bridgehub) reentrancyGuardInitializer {

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58-L60

> constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55-L57

> constructor() reentrancyGuardInitializer {}

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38-L38

>  constructor(address _l1WethAddress,IBridgehub _bridgehub,IL1ERC20Bridge _legacyBridge) reentrancyGuardInitializer {

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90-L99

## [G-06] ABI ENCODE IS LESS EFFICIENT THAN ABI ENCODEPACKED

Unless explicitly needed , it is recommended to use `abi.encodePacked()` instead of `abi.encode()` to save Gas.

**INSTANCES:** 10

The contract is using `abi.encode()` in the function `_deployBeaconProxy`. In `abi.encode()`, all elementary types are padded to `32 bytes` and dynamic arrays include their length, whereas `abi.encodePacked()` will only use the minimal required memory to encode the data.

> (salt, l2TokenProxyBytecodeHash, abi.encode(address(l2TokenBeacon), ""))

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L171-L171

The contract is using `abi.encode()` in the function `initialize`. In `abi.encode()`, all elementary types are padded to `32 bytes` and dynamic arrays include their length, whereas `abi.encodePacked()` will only use the minimal required memory to encode the data.

> storedBatchZero = keccak256(abi.encode(batchZero));

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100-L100

The contract is using `abi.encode()` in the function `initialize`. In `abi.encode()`, all elementary types are padded to `32 bytes` and dynamic arrays include their length, whereas `abi.encodePacked()` will only use the minimal required memory to encode the data.

> initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102-L102

The contract is using `abi.encode()` in the function `setInitialCutHash`. In `abi.encode()`, all elementary types are padded to `32 bytes` and dynamic arrays include their length, whereas `abi.encodePacked()` will only use the minimal required memory to encode the data.

> initialCutHash = keccak256(abi.encode(_diamondCut));

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138-L138

The contract is using `abi.encode()` in the function `setNewVersionUpgrade`. In `abi.encode()`, all elementary types are padded to `32 bytes` and dynamic arrays include their length, whereas `abi.encodePacked()` will only use the minimal required memory to encode the data.

> upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L147-L147

The contract is using `abi.encode()` in the function `setUpgradeDiamondCut`. In `abi.encode()`, all elementary types are padded to `32 bytes` and dynamic arrays include their length, whereas `abi.encodePacked()` will only use the minimal required memory to encode the data.

> upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L156-L156

The contract is using `abi.encode()` in the function `_setL2SystemContractUpgrade`. In `abi.encode()`, all elementary types are padded to `32 bytes` and dynamic arrays include their length, whereas `abi.encodePacked()` will only use the minimal required memory to encode the data.

> bytes memory encodedTransaction = abi.encode(_l2ProtocolUpgradeTx);

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L192-L192

The contract is using `abi.encode()` in the function `_processL2ToL1Log`. In `abi.encode()`, all elementary types are padded to `32 bytes` and dynamic arrays include their length, whereas `abi.encodePacked()` will only use the minimal required memory to encode the data.

> chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

https://github.com//code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L106-L106

The contract is using `abi.encode()` in the function `sendToL1`. In `abi.encode()`, all elementary types are padded to `32 bytes` and dynamic arrays include their length, whereas `abi.encodePacked()` will only use the minimal required memory to encode the data.

> chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

https://github.com//code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L122-L122

The contract is using `abi.encode()` in the function `requestBytecodeL1Publication`. In `abi.encode()`, all elementary types are padded to `32 bytes` and dynamic arrays include their length, whereas `abi.encodePacked()` will only use the minimal required memory to encode the data.

> chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

https://github.com//code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L164-L164

## [G-07] EMIT USED IN LOOP

In Solidity, when a code emits an event inside of a loop, internally it performs a `LOG` operation `N` times, where `N` represents the number of iterations in the loop. This can lead to inflated gas costs and potentially impact the efficiency of the code.

To optimize your code and reduce gas consumption, it is recommended to refactor the code to emit the event only once at the end of the loop.

**INSTANCES:** 3

> emit BlockCommit

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261-L265

> emit BlockCommit

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L299-L303

> emit BlockExecution

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353-L353

## [G-08] GAS OPTIMIZATION FOR THIS KEYWORD

Calling an external function internally, through the use of this keyword wastes gas overhead of calling an external function `100 gas`.

It is recommended to update the function's visibility from external to public and remove the this keyword if gas optimization is needed here.

**INSTANCES:** 4

> try this.decodeString(nameBytes) returns (string memory nameString) {

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L75-L75

> try this.decodeString(symbolBytes) returns (string memory symbolString) {

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L81-L81

> try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L93-L93

> this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);

https://github.com//code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L254-L254

## [G-09] USE SELFBALANCE() INSTEAD OF ADDRESS(THIS).BALANCE

In Solidity, efficient use of gas is paramount to ensure cost-effective execution on the Ethereum blockchain. Gas can be optimized when obtaining contract balance by using `selfbalance()` rather than `address(this).balance` because it bypasses gas costs and refunds, which are not required for obtaining the contract's balance.

**INSTANCES:** 4

> uint256 balanceBefore = address(this).balance;

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118-L118

> uint256 balanceAfter = address(this).balance;

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120-L120

> uint256 amount = address(this).balance;

https://github.com//code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41-L41

> require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

https://github.com//code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100-L100

## [G-10] GAS OPTIMIZATION FOR STATE VARIABLES

Plus equals `+=` costs more gas than addition operator. The same thing happens with minus equals `-=`. Therefore, `x +=y` costs more gas than `x = x + y`.

**INSTANCES**: 2

> totalSupply += _amount;

https://github.com//code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L65-L65

> txNumberInBlock += 1;

https://github.com//code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L483-L483 


 

 



































