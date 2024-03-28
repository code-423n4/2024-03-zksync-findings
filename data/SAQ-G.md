## Summary

### Gas Optimization

no | Issue |Instances||
|-|:-|:-:|:-:|
| [G-01] | Use Custom errors rather than `require()`/`revert()` to save gas | 15 | - |
| [G-02] | abi.encode() is less efficient than  abi.encodepacked() | 7 | - |
| [G-03] |  `2**<N>` should be re-written as `type(uint<N>).max` | 4 | - |
| [G-04] | Shorten the array rather than copying to a new one | 1 | - |
| [G-05] | Use assembly to validate `msg.sender` | 2 | - |
| [G-06] | Expression `` is cheaper than `new bytes(0)` | 3 | - |
| [G-07] | USE A MORE RECENT `VERSION `OF SOLIDITY | More file | - |
| [G-08] | Optimize Names to save Gas | 4 | - |
| [G-09] | Using `delete` statement can save gas | 2 | - |
| [G-10] | Use `uint256(1)/uint256(2)` instead for `true` and `false` boolean states | 2 | - |
| [G-11] |  `do-while` is cheaper than `for-loops` when the initial check can be skipped | 2 | - |
| [G-12] | Use nested if and, avoid multiple check combinations | 4 | - |
| [G-13] | Use `constants` instead of `type(uintx).max` | 9 | - |
| [G-14] | Do not calculate `constant` | 9 | - |
| [G-15] | Use assembly to calculate hashes to save gas | 6 | - |
| [G-16] | Avoid fetching a low-level call's return data by using assembly | 2 | - |
| [G-17] | Internal functions only called once can be inlined to save gas | 15 | - |
| [G-18] | `>=` costs less gas than `>` | 4 | - |
| [G-19] | Using assembly to check for zero can save gas | 2 | - |
| [G-20] | Use assembly to emit events | 1 | - |
| [G-21] |  Use `selfbalance()` instead of `address(this).balance` | 3 | - |
| [G-22] | Empty blocks should be removed or emit something | 4 | - |
| [G-23] | Don't initialize variables with default value | 4 | - |

## Gas Optimizations  

## [G-01] Use Custom errors rather than `require()`/`revert()` to save gas



Custom errors are available from solidity version 0.8.4. Custom errors save ~50 gas each time they’re hit by avoiding having to allocate and store the revert string. Not defining the strings also save deployment gas.


#### The Bellow files have multiple instances

[L1ERC20Bridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol
)


[L1SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
)


[Bridgehub.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol
)


[https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol
](Governance.sol)


[StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
)


[DiamondInit.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol
)


[ZkSyncStateTransitionBase.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol
)


[Diamond.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol
)


[BaseZkSyncUpgrade.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol
)


[L2SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol
)


[Compressor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol
)


[ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol
)


[DefaultAccount.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol
)


[L1Messenger.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol
)


[SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol
)



## [G-02] abi.encode() is less efficient than  abi.encodepacked()

In terms of efficiency, abi.encodePacked() is generally considered to be more gas-efficient than abi.encode(), because it skips the step of adding function signatures and other metadata to the encoded data. However, this comes at the cost of reduced safety, as abi.encodePacked() does not perform any type checking or padding of data.

Refference: https://github.com/ConnorBlockchain/Solidity-Encode-Gas-Comparison

```solidity
file: /contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

76        bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


```solidity
file: /contracts/ethereum/contracts/bridge/L1SharedBridge.sol

259            return abi.encode(name, symbol, decimals); // when depositing eth to a non-eth based chain it is an ERC20


265        return abi.encode(data1, data2, data3);


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol


```solidity
file: /contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

102        initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


```solidity
file: /contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

138        initialCutHash = keccak256(abi.encode(_diamondCut));

147        upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


```solidity
file: /system-contracts/contracts/L1Messenger.sol

106        chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol



## [G-03] `2**<N>` should be re-written as `type(uint<N>).max`

Earlier versions of solidity can use uint<n>(-1) instead. Expressions not including the - 1 can often be re-written to accomodate the change (e.g. by using a > rather than a >=, which will also save some gas)

https://code4rena.com/reports/2023-04-frankencoin#g-05-2n-should-be-re-written-as-typeuintnmax


```solidity
file: /contracts/zksync/contracts/L2ContractHelper.sol

26        require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol


```solidity
file: /system-contracts/contracts/Constants.sol

94uint256 constant MAX_MSG_VALUE = 2 ** 128 - 1;


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol


```solidity
file: /system-contracts/contracts/NonceHolder.sol

28    uint256 private constant DEPLOY_NONCE_MULTIPLIER = 2 ** 128;

31    uint256 private constant MAXIMAL_MIN_NONCE_INCREMENT = 2 ** 32;


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol


## [G-04] Shorten the array rather than copying to a new one

Inline-assembly can be used to shorten the array by changing the length slot, so that the entries don't have to be copied to a new, shorter array

```solidity
file: /system-contracts/contracts/L1Messenger.sol
 
204        bytes32[] memory l2ToL1LogsTreeArray = new bytes32[](L2_TO_L1_LOGS_MERKLE_TREE_LEAVES);


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol


## [G-05] Use assembly to validate `msg.sender`

We can use assembly to efficiently validate msg.sender for the didPay and uniswapV3SwapCallback functions with the least amount of opcodes necessary. Additionally, we can use xor() instead of iszero(eq()), saving 3 gas. We can also potentially save gas on the unhappy path by using scratch space to store the error selector, potentially avoiding memory expansion costs.

```solidity
file: /contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

64        require(msg.sender == address(sharedBridge), "Not shared bridge");


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


```solidity
file: /contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62        require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol



## [G-06] Expression `` is cheaper than `new bytes(0)`

```solidity
file: /contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

196            signature: new bytes(0),

198            paymasterInput: new bytes(0),

199            reservedDynamic: new bytes(0)

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol



## [G-07] USE A MORE RECENT `VERSION `OF SOLIDITY

  change  -> Version 0.8.25
```solidity
file: All file

More file have 0.8.20 version
```


## [G-08]  Optimize Names to save Gas


```solidity
file: /contracts/ethereum/contracts/bridge/L1SharedBridge.sol

30  contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol


```solidity
file: /contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

19 contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


```solidity
file: /contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

30  contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


```solidity
file: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol
 
16  contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol



## [G-09] Using `delete` statement can save gas

```solidity
file: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

276                baseTokenMsgValue = 0;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


```solidity 
file: /system-contracts/contracts/SystemContext.sol

487        txNumberInBlock = 0;


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol



## [G-10]  Use `uint256(1)/uint256(2)` instead for `true` and `false` boolean states


If you don't use boolean for storage you will avoid Gwarmaccess 100 gas. In addition, state changes of boolean from true to false can cost up to ~20000 gas rather than uint256(2) to uint256(1) that would cost significantly less.

```solidity
file: /contracts/ethereum/contracts/bridgehub/Bridgehub.sol

23    mapping(address _token => bool) public tokenIsRegistered;

103        tokenIsRegistered[_token] = true;


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


```solidity
file: /contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

50    mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;

68        require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol



## [G-11] `do-while` is cheaper than `for-loops` when the initial check can be skipped


`for (uint256 i; i < len; ++i){ ... }` -> `do { ...; ++i } while (i < len);`


```solidity
file: /contracts/ethereum/contracts/governance/Governance.sol

225        for (uint256 i = 0; i < _calls.length; ++i) {


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol


```solidity
file: /contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

185            for (uint256 i = 0; i < _newBatchesData.length; ++i) {


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


## [G-12] Use nested if and, avoid multiple check combinations

Using nested if is cheaper than using && multiple check combinations. There are more advantages, such as easier to read code and better coverage reports.

```solidity
file: /system-contracts/contracts/AccountCodeStorage.sol

78            _nonceOrdering == AccountNonceOrdering.Arbitrary &&


131        if (
            uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS &&
            codeHash != 0x00 &&
            !Utils.isContractConstructing(codeHash)
        ) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol


```solidity
file: /system-contracts/contracts/NonceHolder.sol

169        if (isUsed && !_shouldBeUsed) {
            revert("Reusing the same nonce twice");
171        } else if (!isUsed && _shouldBeUsed) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol



## [G-13] Use `constants` instead of `type(uintx).max`

type(uint120).max or type(uint128).max, etc. it uses more gas in the distribution process and also for each transaction than constant usage.

```solidity
file: /contracts/ethereum/contracts/bridgehub/Bridgehub.sol

123       require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol


```solidity
file: /contracts/ethereum/contracts/common/Config.sol

115address constant BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS = address(uint160(type(uint16).max));


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol


```solidity
file: /contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

48        require(_transaction.from <= type(uint16).max, "ua");

49        require(_transaction.to <= type(uint160).max, "ub");

55        require(_transaction.reserved[1] <= type(uint160).max, "uf");



```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


```solidity
file: /system-contracts/contracts/libraries/Utils.sol

21        require(_x <= type(uint128).max, "Overflow");

27        require(_x <= type(uint32).max, "Overflow");

33        require(_x <= type(uint24).max, "Overflow");


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol



## [G-14] Do not calculate `constant`


```solidity
file: /system-contracts/contracts/Constants.sol

94    uint256 constant MAX_MSG_VALUE = 2 ** 128 - 1;


135     uint256 constant COMPRESSED_INITIAL_WRITE_SIZE = DERIVED_KEY_LENGTH + VALUE_LENGTH;
  
137     uint256 constant COMPRESSED_REPEATED_WRITE_SIZE = ENUM_INDEX_LENGTH + VALUE_LENGTH;


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol


```solidity
file: system-contracts/contracts/libraries/SystemContractsCaller.sol

41   uint256 constant META_GAS_PER_PUBDATA_BYTE_OFFSET = 0 * 8;

42   uint256 constant META_HEAP_SIZE_OFFSET = 8 * 8;

43   uint256 constant META_AUX_HEAP_SIZE_OFFSET = 12 * 8;

44   uint256 constant META_SHARD_ID_OFFSET = 28 * 8;

45   uint256 constant META_CALLER_SHARD_ID_OFFSET = 29 * 8;

46   uint256 constant META_CODE_SHARD_ID_OFFSET = 30 * 8;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol



## [G-15] Use assembly to calculate hashes to save gas

Using assembly to calculate hashes can save 80 gas per instance

```solidity
file: /contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

76        bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


```solidity
file: /contracts/ethereum/contracts/bridge/L1SharedBridge.sol

341                bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol


```solidity
file: /contracts/zksync/contracts/bridge/L2SharedBridge.sol

150        bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""));


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

```solidity
file: /system-contracts/contracts/BootloaderUtilities.sol

360           keccak256(
                bytes.concat(
                    "\x02",
                    encodedListLength,
                    encodedFixedLengthParams,
                    encodedDataLength,
                    _transaction.data,
                    encodedAccessListLength,
                    vEncoded,
                    rEncoded,
                    sEncoded
                )

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol


```solidity
file: /system-contracts/contracts/ContractDeployer.sol

105      bytes32 hash = keccak256(
            bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, constructorInputHash)
        );


121     bytes32 hash = keccak256(
            bytes.concat(CREATE_PREFIX, bytes32(uint256(uint160(_sender))), bytes32(_senderNonce))
        );        

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol



## [G-16] Avoid fetching a low-level call's return data by using assembly

Even if you don't assign the call's second return value, it still gets copied to memory. Use assembly instead to prevent this and save 159 gas:
`(bool success,) = payable(receiver).call{gas: gas, value: value}("");` -> `bool success; assembly { success := call(gas, receiver, value, 0, 0, 0, 0) }`

```solidity
file: /system-contracts/contracts/libraries/SystemContractHelper.sol

285        meta.callerShardId = getCallerShardIdFromMeta(metaPacked);


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol


```solidity
file: /contracts/zksync/contracts/vendor/AddressAliasHelper.sol

66        (bool success, ) = recipient.call{value: amount}("");


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol




## [G-17]   Internal functions only called once can be inlined to save gas


```solidity
file: /contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

160     function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


```solidity
file: /contracts/ethereum/contracts/bridge/L1SharedBridge.sol

458    function _checkWithdrawal(
        uint256 _chainId,
        MessageParams memory _messageParams,
        bytes calldata _message,
        bytes32[] calldata _merkleProof
    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {


487    function _parseL2WithdrawalMessage(
        uint256 _chainId,
        bytes memory _l2ToL1message
    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {     

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol


```solidity
file: /contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

177    function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


```solidity
file: /contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

163    function _upgradeVerifier(address _newVerifier, VerifierParams calldata _verifierParams) internal {


180    function _setL2SystemContractUpgrade(
        L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
        bytes[] calldata _factoryDeps,
        uint256 _newProtocolVersion
    ) internal returns (bytes32) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


```solidity
file: /code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

164    function _deployBeaconProxy(bytes32 salt) internal returns (BeaconProxy proxy) {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol


```solidity
file: system-contracts/contracts/BootloaderUtilities.sol

44    function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {


139    function encodeEIP2930TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {


229    function encodeEIP1559TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol


```solidity
file: /system-contracts/contracts/ContractDeployer.sol

283    function _performDeployOnAddress(
        bytes32 _bytecodeHash,
        address _newAddress,
        AccountAbstractionVersion _aaVersion,
        bytes calldata _input
    ) internal {


309    function _storeConstructingByteCodeHashOnAddress(address _newAddress, bytes32 _bytecodeHash) internal {
  

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol


```solidity
file: /system-contracts/contracts/DefaultAccount.sol

78    function _validateTransaction(
        bytes32 _suggestedSignedHash,
        Transaction calldata _transaction
    ) internal returns (bytes4 magic) {


131    function _execute(Transaction calldata _transaction) internal {     


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol


```solidity
file: /system-contracts/contracts/L1Messenger.sol

61    function sha256GasCost(uint256 _length) internal pure returns (uint256) {


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol


```solidity
file: /system-contracts/contracts/SystemContext.sol

263    function _setVirtualBlock(
        uint128 _l2BlockNumber,
        uint128 _maxVirtualBlocksToCreate,
        uint128 _newTimestamp
    ) internal {

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol



## [G-18] `>=` costs less gas than `>`
 
The compiler uses opcodes GT and ISZERO for solidity code that uses >, but only requires LT for >=, which saves 3 gas 
Reference:  https://gist.github.com/IllIllI000/3dc79d25acccfa16dee4e83ffdc6ffde

```solidity
file: /contracts/ethereum/contracts/bridge/L1SharedBridge.sol

129            require(amount > 0, "ShB: 0 amount to transfer");

327        require(_amount > 0, "y1");


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol


```solidity
file: /system-contracts/contracts/ContractDeployer.sol

332            if (value > 0) {

339            if (value > 0) {


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol



## [G-19] Using assembly to check for zero can save gas

Using assembly to check for zero can save gas by allowing more direct access to the evm and reducing some of the overhead associated with high-level operations in solidity.

```solidity
file: /contracts/ethereum/contracts/bridge/L1SharedBridge.sol

158            require(msg.value == 0, "ShB m.v > 0 b d.it");


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol


```solidity
file: /contracts/ethereum/contracts/governance/Governance.sol

107        if (timestamp == 0) {


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol



## [G-20] Use assembly to emit events

We can use assembly to emit events efficiently by utilizing scratch space and the free memory pointer. This will allow us to potentially avoid memory expansion costs. Note: In order to do this optimization safely, we will need to cache and restore the free memory pointer.

```solidity
file: /contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

87        emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol



## [G-21] Use `selfbalance()` instead of `address(this).balance`

Using selfbalance() instead of address(this).balance can save gas in Solidity because selfbalance() is a built-in function that returns the balance of the current contract directly as a uint256 value, without the need to create a new address object.

```solidity
file: /contracts/ethereum/contracts/bridge/L1SharedBridge.sol
 
118            uint256 balanceBefore = address(this).balance;

120            uint256 balanceAfter = address(this).balance;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol


```solidity
file: /system-contracts/contracts/DefaultAccount.sol

100        require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol



## [G-22] Empty blocks should be removed or emit something

If the block is an empty if-statement block to avoid doing subsequent checks in the else-if/else conditions, the else-if/else conditions should be 
nested under the negation of the if-statement, because they involve different classes of checks, which may lead to the introduction of errors when 
the code is later modified (if( x ) {}else if(y){ . . . }else{ . . . } => if ( !x) {if(y) { . . . }else{ . . .}}) . 
Empty receive()/fallback() payable functions that are not used, can be removed to save deployment gas.

```solidity
file: /contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

60    function initialize() external reentrancyGuardInitializer {}


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


```solidity
file: /contracts/ethereum/contracts/governance/Governance.sol
 
262    receive() external payable {}


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol


```solidity
file: /contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

263    function _upgradeL1Contract(bytes calldata _customCallDataForUpgrade) internal virtual {}

269    function _postUpgrade(bytes calldata _customCallDataForUpgrade) internal virtual {}


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol



## [G-23] Don't initialize variables with default value

Uninitialized variables are assigned with the types default value. Explicitly initializing a variable with it's default value costs unnecesary gas.


```solidity
file: system-contracts/contracts/ContractDeployer.sol

247        uint256 sumOfValues = 0;


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol


```solidity
file: /contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

92        uint256 costForPubdata = 0;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


```solidity
file: /system-contracts/contracts/Compressor.sol

123        uint256 stateDiffPtr = 2;

124        uint256 numInitialWritesProcessed = 0;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol

