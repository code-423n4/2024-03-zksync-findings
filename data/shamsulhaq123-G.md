## Gas Optimization

## Summary

|No|Issue|Instance|
|--|-----|--------|
|[G-01]|address(this) can be stored in state variable that will ultimately cost less|18|
|[G-02]|Call msg.sender directly instead of caching them|65|
|[G-03]|Use assembly to check for `address(0)`|32|
|[G-04]|+= costs more gas than = + for state variables|5|
|[G-05]|Use assembly to emit events|70|
|[G-06]|Stack variable cost less while used in emiting event|70|
|[G-07]|Use constants instead of type(uintx).max|11|
|[G-08]|Use hardcode address instead address(this)|18|
|[G-09]|Modifiers are redundant if used only once or not used at all. |6|
|[G-10]|Use function instead of modifiers |6|
|[G-11]|Remove or replace unused state variables|20|
|[G-12]|Should use arguments instead of state variable|70|
|[G-13]|Do not calculate constant|6|
|[G-14]|Use assembly in place of abi.decode to extract calldata values more efficiently|11|
|[G-15]|Using mappings instead of arrays to avoid length checks save gas|20|
|[G-16]|Caching global variables is more expensive than using the actual variable (use msg.sender instead of caching it)|65|
|[G-17]|Emitting constants wastes gas|70|
|[G-18]|Use assembly for loops|17|
|[G-19]|Counting down in for statements is more gas efficient|17|
|[G-20]|Consider using OZ EnumerateSet in place of nested mappings|9|
|[G-21]Multiple address/ID mappings can be combined into a single mapping of an address/ID to a struct, where appropriate|20|

## [G-01] address(this) can be stored in state variable that will ultimately cost less
than every time calculating this specifically when it used multiple times in a contract

```solidity

file: bridge/L1ERC20Bridge.sol

65  uint256 amount = IERC20(_token).balanceOf(address(this));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65

```solidity

file: bridge/L1SharedBridge.sol

118             uint256 balanceBefore = address(this).balance;
            
120            uint256 balanceAfter = address(this).balance;

127            uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

131            uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118-L120
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L174-L176

```solidity

file: governance/Governance.sol

59   require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59

```solidity

file: state-transition/StateTransitionManager.sol

265  bytes32(uint256(uint160(address(this)))),
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L265

```solidity

file: state-transition/chain-deps/facets/Mailbox.sol

41  uint256 amount = address(this).balance;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41

```solidity

file: contracts/ContractDeployer.sol

29  require(msg.sender == address(this), "Callable only by self");

333     BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo(address(this), _newAddress, value);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L333

```solidity

file: contracts/DefaultAccount.sol

47  if (codeAddress != address(this)) 

100   require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

188    return recoveredAddress == address(this) && recoveredAddress != address(0);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L47
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L188

```solidity

file: contracts/contracts/L1Messenger.sol#

129   sender: address(this),
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L129

```solidity

file: contracts/contracts/L2BaseToken.sol

106   balance[address(this)] -= amount;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L106

```solidity

file: contracts/MsgValueSimulator.so

60   require(to != address(this), "MsgValueSimulator calls itself");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L60

```solidity

file: contracts/libraries/TransactionHelper.sol

377  uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377

```solidity

file: zksync/contracts/bridge/L2SharedBridge.sol

153   L2ContractHelper.computeCreate2Address(address(this), salt, l2TokenProxyBytecodeHash, constructorInputHash);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L153

## [G-02] Call msg.sender directly instead of caching them

In the instance below, instead of caching `msg.sender` and incurring unnecessary stack manipulation, we can call `msg.sender` directly.

```solidity

file: ethereum/contracts/bridge/L1ERC20Bridge.sol

142 uint256 amount = _depositFundsToSharedBridge(msg.sender, IERC20(_l1Token), _amount);

146   msg.sender,

154    depositAmount[msg.sender][_l1Token][l2TxHash] = _amount;
155     emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L142
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L146
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L154-L155

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

69   require(msg.sender == address(bridgehub), "ShB not BH");

76    msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),

138  require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L76
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138

```solidity

file: ethereum/contracts/bridgehub/Bridgehub.sol

46         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

62  require(msg.sender == currentPendingAdmin, "n42");

230     sender: msg.sender,

280   msg.sender,

291  msg.sender,

328   _recipient = msg.sender == tx.origin ? msg.sender : AddressAliasHelper.applyL1ToL2Alias(msg.sender);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L230
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L280
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L291
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L328

```solidity

file: ethereum/contracts/governance/Governance.sol

59    require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

65      require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

72  msg.sender == owner() || msg.sender == securityCouncil,
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L65
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L72

```solidity

file: /ethereum/contracts/state-transition/StateTransitionManager.sol

64   require(msg.sender == bridgehub, "StateTransition: only bridgehub");

70   require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

121     require(msg.sender == currentPendingAdmin, "n42");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L70
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L121

```solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol#

62     require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

68      require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

34  require(msg.sender == pendingAdmin, "n4"); 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

209          sender: msg.sender,

222    msg.sender,
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L209
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L222

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

16       require(msg.sender == s.admin, "StateTransition Chain: not admin");
        _;
    }

    /// @notice Checks if validator is active
    modifier onlyValidator() {
        require(s.validators[msg.sender], "StateTransition Chain: not validator");
        _;
    }

    modifier onlyStateTransitionManager() {
        require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");
        _;
    }

    modifier onlyBridgehub() {
        require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");
        _;
    }

    modifier onlyAdminOrStateTransitionManager() {
        require(
            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by admin or state transition manager"
        );
        _;
    }

    modifier onlyValidatorOrStateTransitionManager() {
        require(
            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by validator or state transition manager"
        );
        _;
    }

52 modifier onlyBaseTokenBridge() {
        require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22-L52

```solidity

file: contracts/AccountCodeStorage.sol

26  require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L26

```solidity

file: contracts/ComplexUpgrader.sol

22    require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22

```solidity

file: contracts/ContractDeployer.sol

29   require(msg.sender == address(this), "Callable only by self");

66   accountInfo[msg.sender].supportedAAVersion = _version;

68   emit AccountVersionUpdated(msg.sender, _version);

75   AccountInfo memory currentInfo = accountInfo[msg.sender];

84    _storeAccountInfo(msg.sender, currentInfo);

86   emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);

168  NONCE_HOLDER_SYSTEM_CONTRACT.incrementDeploymentNonce(msg.sender);
169  address newAddress = getNewAddressCreate2(msg.sender, _bytecodeHash, _salt, _input);

188  uint256 senderNonce = NONCE_HOLDER_SYSTEM_CONTRACT.incrementDeploymentNonce(msg.sender);
189  address newAddress = getNewAddressCreate(msg.sender, senderNonce);

240    msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),

254   this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);

297  _constructContract(msg.sender, _newAddress, _bytecodeHash, _input, false, true);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L66
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L68
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L75
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L84-L86
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L168
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L188-L189 
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L240
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L254
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L297

```solidity

file: contracts/DefaultAccount.sol

29  if (msg.sender != BOOTLOADER_FORMAL_ADDRESS)

222  assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L29
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L222

```solidity

file: contracts/ImmutableSimulator.sol

35  require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35

```solidity

file: contracts/KnownCodesStorage.sol

20  require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L20


```solidity

file: contracts/L1Messenger.sol

79  sender: msg.sender,

130   key: bytes32(uint256(uint160(msg.sender))),

156  emit L1MessageSent(msg.sender, hash, _message);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L79
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L130
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L156

```solidity

file: contracts/L2BaseToken.sol

34      msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
        msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
36      msg.sender == BOOTLOADER_FORMAL_ADDRESS,

79   emit Withdrawal(msg.sender, _l1Receiver, amount);

89  bytes memory message = _getExtendedWithdrawMessage(_l1Receiver, amount, msg.sender, _additionalData);

92 emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L34-L36 
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L79
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L89
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L92

```solidity

file: contracts/MsgValueSimulator.sol#

64   abi.encodeCall(REAL_BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo, (msg.sender, to, value))

81 return EfficientCall.mimicCall(userGas, to, _data, msg.sender, false, isSystemCall);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L64
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L81

```solidity

file: contracts/NonceHolder.sol

68    uint256 addressAsKey = uint256(uint160(msg.sender));

89  require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");

92  uint256 addressAsKey = uint256(uint160(msg.sender));

96  emit ValueSetUnderNonce(msg.sender, _key, _value);

103   uint256 addressAsKey = uint256(uint160(msg.sender));

111   uint256 addressAsKey = uint256(uint160(msg.sender));

137  msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L68
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L89
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L92
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L96
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L103
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L111
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L137

```solidity

file: contracts/interfaces/ISystemContract.sol

22 SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),

32  SystemContractHelper.isSystemContract(msg.sender),

41      require(msg.sender == caller, "Inappropriate caller");

    
48     require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");
  
55     require(msg.sender == FORCE_DEPLOYER);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L22
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L32
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L41_55

```solidity

file: zksync/contracts/bridge/L2SharedBridge.sol

88     AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
89     AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,

126   IL2StandardToken(_l2Token).bridgeBurn(msg.sender, _amount);

134   emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L88-L89
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L126
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L134

```solidity

file: zksync/contracts/bridge/L2StandardERC20.sol

54 l2Bridge = msg.sender;

120    require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");

130  require(msg.sender == l2Bridge, "xnt");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L54
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L130

## [G-03]  Use assembly to check for `address(0)`

```solidity

file: ethereum/contracts/bridge/L1ERC20Bridge.sol

105   l2TxHash = deposit(_l2Receiver, _l1Token, _amount, _l2TxGasLimit, _l2TxGasPerPubdataByte, address(0));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L105

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

108  require(_owner != address(0), "ShB owner 0");

188  require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

563  require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

578  if (_refundRecipient == address(0)) 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L108
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L578

```solidity

file: ethereum/contracts/bridgehub/Bridgehub.sol

68 emit NewPendingAdmin(currentPendingAdmin, address(0));

130         require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

132         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered")
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130-L132

```solidity

file: ethereum/contracts/governance/Governance.sol

42   require(_admin != address(0), "Admin should be non zero address");

47  emit ChangeSecurityCouncil(address(0), _securityCouncil);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L42
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L47

```solidity

file: ethereum/contracts/state-transition/StateTransitionManager.sol

82   require(_initializeData.governor != address(0), "StateTransition: governor zero");

127   emit NewPendingAdmin(currentPendingAdmin, address(0));

207   verifier: address(0),

246   if (stateTransition[_chainId] != address(0)) 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L82
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L127
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L207
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L246

```solidity

file: ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

225 require(address(_initializeData.verifier) != address(0), "vt");
    require(_initializeData.admin != address(0), "vy");
227 require(_initializeData.validatorTimelock != address(0), "hc");

30 require(facetAddress != address(0), "F");

40   emit NewPendingAdmin(pendingAdmin, address(0));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L225-L227
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

183   require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

275   address refundRecipient = _params.refundRecipient == address(0) ? _params.sender : _params.refundRecipient;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L275

```solidity

file: ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

131  if (_newVerifier == IVerifier(address(0))) 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L131

```solidity

file: ethereum/contracts/state-transition/libraries/Diamond.sol

141   require(oldFacet.facetAddress == address(0), "J");

161 require(oldFacet.facetAddress != address(0), "L");

175  require(_facet == address(0), "a1");

181  require(oldFacet.facetAddress != address(0), "a2");

279   if (_init == address(0)) 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L141
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L161
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L181
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L279

```solidity

file: contracts/DefaultAccount.sol

188  return recoveredAddress == address(this) && recoveredAddress != address(0);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L188

```solidity

file: contracts/libraries/TransactionHelper.sol

406 if (address(uint160(_transaction.paymaster)) != address(0)) 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L406

```solidity

file: zksync/contracts/bridge/L2SharedBridge.sol

55 require(_l1Bridge != address(0), "bf");

57  require(_aliasedOwner != address(0), "sf");

68  require(_l1LegecyBridge != address(0), "bf2");

96  if (currentL1Token == address(0)) 

129  require(l1Token != address(0), "yh");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L55
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L57
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L68
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L96
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L129

```solidity

file: zksync/contracts/bridge/L2StandardERC20.sol#

51  require(_l1Address != address(0), "in6"); 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51

## [G-04] += costs more gas than = + for state variables
use = + or = - instead to save gas

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

165  chainBalance[_chainId][_l1Token] += _amount;

212 chainBalance[_chainId][_l1Token] += amount;

568  chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L165
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L212
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L568

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

636   for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) 

657   versionedHashIndex += 1;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L657

```solidity

file: contracts/libraries/RLPEncoder.sol

88            hbs += 16;
            }
            if (_number > type(uint64).max) {
                _number >>= 64;
                hbs += 8;
            }
            if (_number > type(uint32).max) {
                _number >>= 32;
                hbs += 4;
            }
            if (_number > type(uint16).max) {
                _number >>= 16;
                hbs += 2;
            }
            if (_number > type(uint8).max) {
103            hbs += 1;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L88-L103

## [G-05] Use assembly to emit events
We can use assembly to emit events efficiently by utilizing `scratch space` and the `free memory pointer`. This will allow us to potentially avoid memory expansion costs. Note: In order to do this optimization safely, we will need to cache and restore the free memory pointer.

```solidity

file: ethereum/contracts/bridge/L1ERC20Bridge.sol

155  emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);

199  emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);

225  emit WithdrawalFinalized(l1Receiver, l1Token, amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L155
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L199
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L225

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

168  emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);

227  emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);

239  emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);

367  emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);

454   emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);

602   emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L168
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L227
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L239
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L367
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L454
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L602

```solidity

file: ethereum/contracts/bridgehub/Bridgehub.sol

56   emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

68    emit NewPendingAdmin(currentPendingAdmin, address(0));
69    emit NewAdmin(previousAdmin, pendingAdmin);

145   emit NewChain(_chainId, _stateTransitionManager, _admin);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L56
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68-L69 
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L145


```solidity

file: ethereum/contracts/governance/Governance.sol

47         emit ChangeSecurityCouncil(address(0), _securityCouncil);

50        emit ChangeMinDelay(0, _minDelay);

132  emit TransparentOperationScheduled(id, _delay, _operation);

144    emit ShadowOperationScheduled(_id, _delay);

157   emit OperationCancelled(_id);

180    emit OperationExecuted(id);

199  emit OperationExecuted(id);

250   emit ChangeMinDelay(minDelay, _newDelay);

257 emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L47-L50
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L132
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L144
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L157
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L180
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L199
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L250
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L257

```solidity

file: ethereum/contracts/state-transition/StateTransitionManager.sol

127         emit NewPendingAdmin(currentPendingAdmin, address(0));
128        emit NewAdmin(previousAdmin, pendingAdmin);

227   emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);

235  emit StateTransitionNewChain(_chainId, _stateTransitionContract);

287   emit StateTransitionNewChain(_chainId, stateTransitionAddress);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L127-L128 
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L235
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L287

```solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol

83   emit ValidatorAdded(_chainId, _newValidator);

92   emit ValidatorRemoved(_chainId, _validator);

98   emit NewExecutionDelay(_executionDelay);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L83
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L92
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

28   emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

40   emit NewPendingAdmin(pendingAdmin, address(0));
41   emit NewAdmin(previousAdmin, pendingAdmin);

47   emit ValidatorStatusUpdate(_validator, _active);

54  emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);

63  emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);

75  emit NewFeeParams(oldFeeParams, _newFeeParams);

86  emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator);

92  emit ValidiumModeStatusUpdate(_validiumMode);

115 emit ExecuteUpgrade(_diamondCut);

125 emit ExecuteUpgrade(_diamondCut);

139  emit Freeze();

149  emit Unfreeze();
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L28
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40-L41
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L47
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L54
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L63
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L75
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L86
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L115
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L125
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L139
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L149

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

135   bytes memory emittedL2Logs = _newBatch.systemLogs;

142    for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
      (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
      (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
146   (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);

261   emit BlockCommit

299  emit BlockCommit

353  emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);   

436 emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

496 emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L135
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142-L146
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L299
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

343  emit NewPriorityRequest
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L343

```solidity

file: ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

87  emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);

104  emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);

121  emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);

137  emit NewVerifier(address(oldVerifier), address(_newVerifier));

157   emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

256   emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L87
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L104
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L121
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L137
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L157
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L256

```solidity

file: contracts/ContractDeployer.sol

68   emit AccountVersionUpdated(msg.sender, _version);

86   emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);

355   emit ContractDeployed(_sender, _bytecodeHash, _newAddress);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L68
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L86
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L355

```solidity

file: contracts/L1Messenger.sol

111 emit L2ToL1LogSent(_l2ToL1Log);

56  emit L1MessageSent(msg.sender, hash, _message);

181 emit BytecodeL1PublicationRequested(_bytecodeHash);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L111
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L156
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L181

```solidity

file: contracts/L2BaseToken.sol

49  emit Transfer(_from, _to, _amount);

67  emit Mint(_account, _amount);

79  emit Withdrawal(msg.sender, _l1Receiver, amount);

92  emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L49
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L67
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L79
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L92

```solidity

file: contracts/NonceHolder.sol

96  emit ValueSetUnderNonce(msg.sender, _key, _value);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L96

```solidity

file: zksync/contracts/bridge/L2SharedBridge.sol

105  emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);

134   emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L105
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L134

```solidity

file: zksync/contracts/bridge/L2StandardERC20.sol

101  emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);

126  emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);

147  emit BridgeMint(_to, _amount);

156  emit BridgeBurn(_from, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L101
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L147
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L156

## [G-06] Stack variable cost less while used in emiting event
Even if the variable is going to be used only one time, caching a state variable and use its cache in an emit would help you reduce the cost by at least

```solidity

file: ethereum/contracts/bridge/L1ERC20Bridge.sol

155  emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);

199  emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);

225  emit WithdrawalFinalized(l1Receiver, l1Token, amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L155
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L199
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L225

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

168  emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);

227  emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);

239  emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);

367  emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);

454   emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);

602   emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L168
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L227
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L239
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L367
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L454
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L602

```solidity

file: ethereum/contracts/bridgehub/Bridgehub.sol

56   emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

68    emit NewPendingAdmin(currentPendingAdmin, address(0));
69    emit NewAdmin(previousAdmin, pendingAdmin);

145   emit NewChain(_chainId, _stateTransitionManager, _admin);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L56
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68-L69 
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L145


```solidity

file: ethereum/contracts/governance/Governance.sol

47         emit ChangeSecurityCouncil(address(0), _securityCouncil);

50        emit ChangeMinDelay(0, _minDelay);

132  emit TransparentOperationScheduled(id, _delay, _operation);

144    emit ShadowOperationScheduled(_id, _delay);

157   emit OperationCancelled(_id);

180    emit OperationExecuted(id);

199  emit OperationExecuted(id);

250   emit ChangeMinDelay(minDelay, _newDelay);

257 emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L47-L50
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L132
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L144
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L157
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L180
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L199
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L250
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L257

```solidity

file: ethereum/contracts/state-transition/StateTransitionManager.sol

127         emit NewPendingAdmin(currentPendingAdmin, address(0));
128        emit NewAdmin(previousAdmin, pendingAdmin);

227   emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);

235  emit StateTransitionNewChain(_chainId, _stateTransitionContract);

287   emit StateTransitionNewChain(_chainId, stateTransitionAddress);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L127-L128 
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L235
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L287

```solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol

83   emit ValidatorAdded(_chainId, _newValidator);

92   emit ValidatorRemoved(_chainId, _validator);

98   emit NewExecutionDelay(_executionDelay);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L83
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L92
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

28   emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

40   emit NewPendingAdmin(pendingAdmin, address(0));
41   emit NewAdmin(previousAdmin, pendingAdmin);

47   emit ValidatorStatusUpdate(_validator, _active);

54  emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);

63  emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);

75  emit NewFeeParams(oldFeeParams, _newFeeParams);

86  emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator);

92  emit ValidiumModeStatusUpdate(_validiumMode);

115 emit ExecuteUpgrade(_diamondCut);

125 emit ExecuteUpgrade(_diamondCut);

139  emit Freeze();

149  emit Unfreeze();
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L28
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40-L41
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L47
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L54
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L63
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L75
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L86
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L115
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L125
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L139
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L149

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

135   bytes memory emittedL2Logs = _newBatch.systemLogs;

142    for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
      (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
      (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
146   (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);

261   emit BlockCommit

299  emit BlockCommit

353  emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);   

436 emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

496 emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L135
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142-L146
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L299
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

343  emit NewPriorityRequest
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L343

```solidity

file: ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

87  emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);

104  emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);

121  emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);

137  emit NewVerifier(address(oldVerifier), address(_newVerifier));

157   emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

256   emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L87
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L104
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L121
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L137
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L157
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L256

```solidity

file: contracts/ContractDeployer.sol

68   emit AccountVersionUpdated(msg.sender, _version);

86   emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);

355   emit ContractDeployed(_sender, _bytecodeHash, _newAddress);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L68
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L86
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L355

```solidity

file: contracts/L1Messenger.sol

111 emit L2ToL1LogSent(_l2ToL1Log);

56  emit L1MessageSent(msg.sender, hash, _message);

181 emit BytecodeL1PublicationRequested(_bytecodeHash);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L111
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L156
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L181

```solidity

file: contracts/L2BaseToken.sol

49  emit Transfer(_from, _to, _amount);

67  emit Mint(_account, _amount);

79  emit Withdrawal(msg.sender, _l1Receiver, amount);

92  emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L49
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L67
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L79
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L92

```solidity

file: contracts/NonceHolder.sol

96  emit ValueSetUnderNonce(msg.sender, _key, _value);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L96

```solidity

file: zksync/contracts/bridge/L2SharedBridge.sol

105  emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);

134   emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L105
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L134

```solidity

file: zksync/contracts/bridge/L2StandardERC20.sol

101  emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);

126  emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);

147  emit BridgeMint(_to, _amount);

156  emit BridgeBurn(_from, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L101
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L147
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L156

## [G-07] Use constants instead of type(uintx).max

type(uint120).max or type(uint128).max, etc. it uses more gas in the distribution process and also for each transaction than constant usage.

```solidity

file: ethereum/contracts/bridgehub/Bridgehub.sol

123   require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123

```solidity

file: ethereum/contracts/state-transition/libraries/TransactionValidator.sol

48  require(_transaction.from <= type(uint16).max, "ua");
49  require(_transaction.to <= type(uint160).max, "ub");

55  require(_transaction.reserved[1] <= type(uint160).max, "uf");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L48-L49
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55

```solidity

file: ethereum/contracts/common/Config.sol#

115 address constant BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS = address(uint160(type(uint16).max));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L115

```solidity

file: contracts/SystemContext.sol

37  uint256 public blockGasLimit = type(uint32).max;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L37

```solidity

file: contracts/libraries/RLPEncoder.sol

88             if (_number > type(uint128).max) {
                _number >>= 128;
                hbs += 16;
            }
            if (_number > type(uint64).max) {
                _number >>= 64;
                hbs += 8;
            }
            if (_number > type(uint32).max) {
                _number >>= 32;
                hbs += 4;
            }
            if (_number > type(uint16).max) {
                _number >>= 16;
                hbs += 2;
            }
103            if (_number > type(uint8).max) {
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L88-L103

```solidity

file: contracts/libraries/SystemContractHelper.sol

9  uint256 constant UINT32_MASK = type(uint32).max;
   uint256 constant UINT64_MASK = type(uint64).max;
   uint256 constant UINT128_MASK = type(uint128).max;
12 uint256 constant ADDRESS_MASK = type(uint160).max;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L9-L12

```solidity

file: contracts/libraries/Utils.sol

21  require(_x <= type(uint128).max, "Overflow");

27   require(_x <= type(uint32).max, "Overflow");

33 require(_x <= type(uint24).max, "Overflow");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L21
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L27
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L33

```solidity

file: zksync/contracts/SystemContractsCaller.sol

28  require(_x <= type(uint32).max, "Overflow");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L28

## [G-08] Use hardcode address instead address(this)
Instead of using address(this), it is more gas-efficient to pre-calculate and use the hardcoded address.

```solidity

file: bridge/L1ERC20Bridge.sol

65  uint256 amount = IERC20(_token).balanceOf(address(this));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65

```solidity

file: bridge/L1SharedBridge.sol

118             uint256 balanceBefore = address(this).balance;
            
120            uint256 balanceAfter = address(this).balance;

127            uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

131            uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118-L120
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L174-L176

```solidity

file: governance/Governance.sol

59   require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59

```solidity

file: state-transition/StateTransitionManager.sol

265  bytes32(uint256(uint160(address(this)))),
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L265

```solidity

file: state-transition/chain-deps/facets/Mailbox.sol

41  uint256 amount = address(this).balance;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41

```solidity

file: contracts/ContractDeployer.sol

29  require(msg.sender == address(this), "Callable only by self");

333     BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo(address(this), _newAddress, value);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L333

```solidity

file: contracts/DefaultAccount.sol

47  if (codeAddress != address(this)) 

100   require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

188    return recoveredAddress == address(this) && recoveredAddress != address(0);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L47
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L188

```solidity

file: contracts/contracts/L1Messenger.sol#

129   sender: address(this),
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L129

```solidity

file: contracts/contracts/L2BaseToken.sol

106   balance[address(this)] -= amount;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L106

```solidity

file: contracts/MsgValueSimulator.so

60   require(to != address(this), "MsgValueSimulator calls itself");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L60

```solidity

file: contracts/libraries/TransactionHelper.sol

377  uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377

```solidity

file: zksync/contracts/bridge/L2SharedBridge.sol

153   L2ContractHelper.computeCreate2Address(address(this), salt, l2TokenProxyBytecodeHash, constructorInputHash);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L153

## [G-09] Modifiers are redundant if used only once or not used at all. 

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

68     modifier onlyBridgehub() {
        require(msg.sender == address(bridgehub), "ShB not BH");
        _;
    }

    /// @notice Checks that the message sender is the bridgehub or zkSync Era Diamond Proxy.
    modifier onlyBridgehubOrEra(uint256 _chainId) {
        require(
            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
            "L1SharedBridge: not bridgehub or era chain"
        );
        _;
    }

    /// @notice Checks that the message sender is the legacy bridge.
83    modifier onlyLegacyBridge() {
        require(msg.sender == address(legacyBridge), "ShB not legacy bridge");
        _;
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L68-L83

```solidity

file: ethereum/contracts/governance/Governance.sol

58     modifier onlySelf() {
        require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
        _;
    }

    /// @notice Checks that the message sender is an active security council.
    modifier onlySecurityCouncil() {
        require(msg.sender == securityCouncil, "Only security council is allowed to call this function");
        _;
    }

    /// @notice Checks that the message sender is an active owner or an active security council.
70  modifier onlyOwnerOrSecurityCouncil() 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L58-L70

```solidity

file: ethereum/contracts/state-transition/StateTransitionManager.sol

63     modifier onlyBridgehub() {
        require(msg.sender == bridgehub, "StateTransition: only bridgehub");
        _;
    }

    /// @notice the admin can call, for non-critical updates
69    modifier onlyOwnerOrAdmin() 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L63-L69

```solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol

61     modifier onlyChainAdmin(uint256 _chainId) {
        require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");
        _;
    }

    /// @notice Checks if the caller is a validator.
67  modifier onlyValidator(uint256 _chainId)
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L61-L67

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

15     modifier onlyAdmin() {
        require(msg.sender == s.admin, "StateTransition Chain: not admin");
        _;
    }

    /// @notice Checks if validator is active
    modifier onlyValidator() {
        require(s.validators[msg.sender], "StateTransition Chain: not validator");
        _;
    }

    modifier onlyStateTransitionManager() {
        require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");
        _;
    }

    modifier onlyBridgehub() {
        require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");
        _;
    }

    modifier onlyAdminOrStateTransitionManager() {
        require(
            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by admin or state transition manager"
        );
        _;
    }

52    modifier onlyValidatorOrStateTransitionManager() {
        require(
            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by validator or state transition manager"
        );
        _;
    }

52    modifier onlyBaseTokenBridge() 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L15-L52
```solidity

file: contracts/interfaces/ISystemContract.sol

20     modifier onlySystemCall() {
        require(
            SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
            "This method require system call flag"
        );
        _;
    }

    /// @notice Modifier that makes sure that the method
    /// can only be called from a system contract.
    modifier onlyCallFromSystemContract() {
        require(
            SystemContractHelper.isSystemContract(msg.sender),
            "This method require the caller to be system contract"
        );
        _;
    }

    /// @notice Modifier that makes sure that the method
    /// can only be called from a special given address.
    modifier onlyCallFrom(address caller) {
        require(msg.sender == caller, "Inappropriate caller");
        _;
    }

    /// @notice Modifier that makes sure that the method
    /// can only be called from the bootloader.
    modifier onlyCallFromBootloader() {
        require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");
        _;
    }

    /// @notice Modifier that makes sure that the method
    /// can only be called from the L1 force deployer.
54    modifier onlyCallFromForceDeployer()
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L20-L52

## [G-10] Use function instead of modifiers 

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

68     modifier onlyBridgehub() {
        require(msg.sender == address(bridgehub), "ShB not BH");
        _;
    }

    /// @notice Checks that the message sender is the bridgehub or zkSync Era Diamond Proxy.
    modifier onlyBridgehubOrEra(uint256 _chainId) {
        require(
            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
            "L1SharedBridge: not bridgehub or era chain"
        );
        _;
    }

    /// @notice Checks that the message sender is the legacy bridge.
83    modifier onlyLegacyBridge() {
        require(msg.sender == address(legacyBridge), "ShB not legacy bridge");
        _;
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L68-L83

```solidity

file: ethereum/contracts/governance/Governance.sol

58     modifier onlySelf() {
        require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");
        _;
    }

    /// @notice Checks that the message sender is an active security council.
    modifier onlySecurityCouncil() {
        require(msg.sender == securityCouncil, "Only security council is allowed to call this function");
        _;
    }

    /// @notice Checks that the message sender is an active owner or an active security council.
70  modifier onlyOwnerOrSecurityCouncil() 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L58-L70

```solidity

file: ethereum/contracts/state-transition/StateTransitionManager.sol

63     modifier onlyBridgehub() {
        require(msg.sender == bridgehub, "StateTransition: only bridgehub");
        _;
    }

    /// @notice the admin can call, for non-critical updates
69    modifier onlyOwnerOrAdmin() 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L63-L69

```solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol

61     modifier onlyChainAdmin(uint256 _chainId) {
        require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");
        _;
    }

    /// @notice Checks if the caller is a validator.
67  modifier onlyValidator(uint256 _chainId)
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L61-L67

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

15     modifier onlyAdmin() {
        require(msg.sender == s.admin, "StateTransition Chain: not admin");
        _;
    }

    /// @notice Checks if validator is active
    modifier onlyValidator() {
        require(s.validators[msg.sender], "StateTransition Chain: not validator");
        _;
    }

    modifier onlyStateTransitionManager() {
        require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");
        _;
    }

    modifier onlyBridgehub() {
        require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");
        _;
    }

    modifier onlyAdminOrStateTransitionManager() {
        require(
            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by admin or state transition manager"
        );
        _;
    }

52    modifier onlyValidatorOrStateTransitionManager() {
        require(
            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by validator or state transition manager"
        );
        _;
    }

52    modifier onlyBaseTokenBridge() 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L15-L52
```solidity

file: contracts/interfaces/ISystemContract.sol

20     modifier onlySystemCall() {
        require(
            SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
            "This method require system call flag"
        );
        _;
    }

    /// @notice Modifier that makes sure that the method
    /// can only be called from a system contract.
    modifier onlyCallFromSystemContract() {
        require(
            SystemContractHelper.isSystemContract(msg.sender),
            "This method require the caller to be system contract"
        );
        _;
    }

    /// @notice Modifier that makes sure that the method
    /// can only be called from a special given address.
    modifier onlyCallFrom(address caller) {
        require(msg.sender == caller, "Inappropriate caller");
        _;
    }

    /// @notice Modifier that makes sure that the method
    /// can only be called from the bootloader.
    modifier onlyCallFromBootloader() {
        require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");
        _;
    }

    /// @notice Modifier that makes sure that the method
    /// can only be called from the L1 force deployer.
54    modifier onlyCallFromForceDeployer()
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L20-L52

## [G-11] Remove or replace unused state variables

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

48  mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;

    /// @dev A mapping chainId => L2 deposit transaction hash => keccak256(abi.encode(account, tokenAddress, amount))
    /// @dev Tracks deposit transactions from L2 to enable users to claim their funds if a deposit fails.
    mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
        public
        override depositHappened;

    /// @dev Tracks the processing status of L2 to L1 messages, indicating whether a message has already been finalized.
    mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
        public isWithdrawalFinalized;

    /// @dev Indicates whether the hyperbridging is enabled for a given chain.
    mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;

    /// @dev Maps token balances for each chain to prevent unauthorized spending across hyperchains.
    /// This serves as a security measure until hyperbridging is implemented.
65    mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L48-L65

```solidity

file: ethereum/contracts/bridgehub/Bridgehub.sol#

21     mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;
    /// @notice we store registered tokens (for arbitrary base token)
    mapping(address _token => bool) public tokenIsRegistered;

    /// @notice chainID => StateTransitionManager contract address, storing StateTransitionManager
    mapping(uint256 _chainId => address) public stateTransitionManager;

    /// @notice chainID => baseToken contract address, storing baseToken
29    mapping(uint256 _chainId => address) public baseToken;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21-L29

```solidity

file: ethereum/contracts/governance/Governance.sol

32  mapping(bytes32 operationId => uint256 executionTimestamp) public timestamps;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L32

```solidity

file: ethereum/contracts/state-transition/StateTransitionManager.sol

30   mapping(uint256 => address) public stateTransition;

48   mapping(uint256 => bytes32) public upgradeCutHash;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L30
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L48

```solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol

47     mapping(uint256 => LibMap.Uint32Map) internal committedBatchTimestamp;

50    mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L47

```solidity

file: ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

74  mapping(address validatorAddress => bool isValidator) validators;

86     mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
    
88    mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;

114   mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;

120  mapping(address => uint256) __DEPRECATED_totalDepositedAmountPerUser;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L74
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L86-L88
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L114
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L120

```solidity

file: ethereum/contracts/state-transition/libraries/Diamond.sol

51   mapping(bytes4 selector => SelectorToFacet selectorInfo) selectorToFacet;
52   mapping(address facetAddress => FacetToSelectors facetInfo) facetToSelectors;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L51-L52

```solidity

file: ethereum/contracts/state-transition/libraries/LibMap.sol

11  mapping(uint256 packedIndex => uint256 eightPackedValues) map;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L11

```solidity

file: ethereum/contracts/state-transition/libraries/PriorityQueue.sol

28   mapping(uint256 priorityOpId => PriorityOperation priorityOp) data;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L28

```solidity

file: contracts/ContractDeployer.sol

26  mapping(address => AccountInfo) internal accountInfo;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L26

```solidity

file: contracts/ImmutableSimulator.sol

21   mapping(uint256 contractAddress => mapping(uint256 index => bytes32 value)) internal immutableDataStorage;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L21

```solidity

file: contracts/L2BaseToken.sol

20  mapping(address account => uint256 balance) internal balance;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L20

```solidity

file: contracts/NonceHolder.sol

36   mapping(uint256 account => uint256 packedMinAndDeploymentNonce) internal rawNonces;

41   mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L36
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L41

```solidity

file: contracts/SystemContext.sol

55   mapping(uint256 batchNumber => bytes32 batchHash) internal batchHashes;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L55

```solidity

file: zksync/contracts/bridge/L2SharedBridge.sol

35  mapping(address l2TokenAddress => address l1TokenAddress) public override l1TokenAddress;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L35

## [G-12] Should use arguments instead of state variable 

state variables should not used in emit  ,  This will save near 97 gas  

```solidity

file: ethereum/contracts/bridge/L1ERC20Bridge.sol

155  emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);

199  emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);

225  emit WithdrawalFinalized(l1Receiver, l1Token, amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L155
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L199
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L225

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

168  emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);

227  emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);

239  emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);

367  emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);

454   emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);

602   emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L168
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L227
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L239
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L367
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L454
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L602

```solidity

file: ethereum/contracts/bridgehub/Bridgehub.sol

56   emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

68    emit NewPendingAdmin(currentPendingAdmin, address(0));
69    emit NewAdmin(previousAdmin, pendingAdmin);

145   emit NewChain(_chainId, _stateTransitionManager, _admin);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L56
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68-L69 
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L145


```solidity

file: ethereum/contracts/governance/Governance.sol

47         emit ChangeSecurityCouncil(address(0), _securityCouncil);

50        emit ChangeMinDelay(0, _minDelay);

132  emit TransparentOperationScheduled(id, _delay, _operation);

144    emit ShadowOperationScheduled(_id, _delay);

157   emit OperationCancelled(_id);

180    emit OperationExecuted(id);

199  emit OperationExecuted(id);

250   emit ChangeMinDelay(minDelay, _newDelay);

257 emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L47-L50
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L132
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L144
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L157
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L180
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L199
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L250
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L257

```solidity

file: ethereum/contracts/state-transition/StateTransitionManager.sol

127         emit NewPendingAdmin(currentPendingAdmin, address(0));
128        emit NewAdmin(previousAdmin, pendingAdmin);

227   emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);

235  emit StateTransitionNewChain(_chainId, _stateTransitionContract);

287   emit StateTransitionNewChain(_chainId, stateTransitionAddress);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L127-L128 
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L235
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L287

```solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol

83   emit ValidatorAdded(_chainId, _newValidator);

92   emit ValidatorRemoved(_chainId, _validator);

98   emit NewExecutionDelay(_executionDelay);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L83
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L92
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

28   emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

40   emit NewPendingAdmin(pendingAdmin, address(0));
41   emit NewAdmin(previousAdmin, pendingAdmin);

47   emit ValidatorStatusUpdate(_validator, _active);

54  emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);

63  emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);

75  emit NewFeeParams(oldFeeParams, _newFeeParams);

86  emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator);

92  emit ValidiumModeStatusUpdate(_validiumMode);

115 emit ExecuteUpgrade(_diamondCut);

125 emit ExecuteUpgrade(_diamondCut);

139  emit Freeze();

149  emit Unfreeze();
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L28
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40-L41
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L47
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L54
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L63
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L75
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L86
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L115
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L125
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L139
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L149

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

135   bytes memory emittedL2Logs = _newBatch.systemLogs;

142    for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
      (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
      (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
146   (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);

261   emit BlockCommit

299  emit BlockCommit

353  emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);   

436 emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

496 emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L135
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142-L146
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L299
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

343  emit NewPriorityRequest
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L343

```solidity

file: ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

87  emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);

104  emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);

121  emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);

137  emit NewVerifier(address(oldVerifier), address(_newVerifier));

157   emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

256   emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L87
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L104
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L121
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L137
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L157
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L256

```solidity

file: contracts/ContractDeployer.sol

68   emit AccountVersionUpdated(msg.sender, _version);

86   emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);

355   emit ContractDeployed(_sender, _bytecodeHash, _newAddress);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L68
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L86
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L355

```solidity

file: contracts/L1Messenger.sol

111 emit L2ToL1LogSent(_l2ToL1Log);

56  emit L1MessageSent(msg.sender, hash, _message);

181 emit BytecodeL1PublicationRequested(_bytecodeHash);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L111
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L156
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L181

```solidity

file: contracts/L2BaseToken.sol

49  emit Transfer(_from, _to, _amount);

67  emit Mint(_account, _amount);

79  emit Withdrawal(msg.sender, _l1Receiver, amount);

92  emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L49
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L67
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L79
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L92

```solidity

file: contracts/NonceHolder.sol

96  emit ValueSetUnderNonce(msg.sender, _key, _value);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L96

```solidity

file: zksync/contracts/bridge/L2SharedBridge.sol

105  emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);

134   emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L105
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L134

```solidity

file: zksync/contracts/bridge/L2StandardERC20.sol

101  emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);

126  emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);

147  emit BridgeMint(_to, _amount);

156  emit BridgeBurn(_from, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L101
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L147
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L156

## [G-13] Do not calculate constant
When you define a constant in Solidity, the compiler can calculate its value at compile-time and replace all references to the constant with its computed value. This can be helpful for readability and reducing the size of the compiled code, but it can also increase gas usage at runtime.

```solidity

file: ethereum/contracts/common/Config.sol

14 uint256 constant MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES = 4 + L2_TO_L1_LOG_SERIALIZE_SIZE * 512;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L14

```solidity

file: contracts/Constants.sol

48 address payable constant BOOTLOADER_FORMAL_ADDRESS = payable(address(SYSTEM_CONTRACTS_OFFSET + 0x01));

52 INonceHolder constant NONCE_HOLDER_SYSTEM_CONTRACT = INonceHolder(address(SYSTEM_CONTRACTS_OFFSET + 0x03));
    IKnownCodesStorage constant KNOWN_CODE_STORAGE_CONTRACT = IKnownCodesStorage(address(SYSTEM_CONTRACTS_OFFSET + 0x04));
    IImmutableSimulator constant IMMUTABLE_SIMULATOR_SYSTEM_CONTRACT = IImmutableSimulator(
54  address(SYSTEM_CONTRACTS_OFFSET + 0x05)

57 IContractDeployer constant DEPLOYER_SYSTEM_CONTRACT = IContractDeployer(address(SYSTEM_CONTRACTS_OFFSET + 0x06));

 address constant FORCE_DEPLOYER = address(SYSTEM_CONTRACTS_OFFSET + 0x07);
 IL1Messenger constant L1_MESSENGER_CONTRACT = IL1Messenger(address(SYSTEM_CONTRACTS_OFFSET + 0x08));
 address constant MSG_VALUE_SYSTEM_CONTRACT = address(SYSTEM_CONTRACTS_OFFSET + 0x09);

 IBaseToken constant BASE_TOKEN_SYSTEM_CONTRACT = IBaseToken(address(SYSTEM_CONTRACTS_OFFSET + 0x0a));
 IBaseToken constant REAL_BASE_TOKEN_SYSTEM_CONTRACT = IBaseToken(address(REAL_SYSTEM_CONTRACTS_OFFSET + 0x0a));

 address constant KECCAK256_SYSTEM_CONTRACT = address(0x8010);

 ISystemContext constant SYSTEM_CONTEXT_CONTRACT = ISystemContext(payable(address(SYSTEM_CONTRACTS_OFFSET + 0x0b)));
 ISystemContext constant REAL_SYSTEM_CONTEXT_CONTRACT = ISystemContext(payable(address(REAL_SYSTEM_CONTRACTS_OFFSET + 0x0b)));

 IBootloaderUtilities constant BOOTLOADER_UTILITIES = IBootloaderUtilities(address(SYSTEM_CONTRACTS_OFFSET + 0x0c));

 address constant EVENT_WRITER_CONTRACT = address(SYSTEM_CONTRACTS_OFFSET + 0x0d);

 ICompressor constant COMPRESSOR_CONTRACT = ICompressor(address(SYSTEM_CONTRACTS_OFFSET + 0x0e));

 IComplexUpgrader constant COMPLEX_UPGRADER_CONTRACT = IComplexUpgrader(address(SYSTEM_CONTRACTS_OFFSET + 0x0f));

86 IPubdataChunkPublisher constant PUBDATA_CHUNK_PUBLISHER = IPubdataChunkPublisher(
    address(SYSTEM_CONTRACTS_OFFSET + 0x11)

94 uint256 constant MAX_MSG_VALUE = 2 ** 128 - 1;    

135 uint256 constant COMPRESSED_INITIAL_WRITE_SIZE = DERIVED_KEY_LENGTH + VALUE_LENGTH;

137 uint256 constant COMPRESSED_REPEATED_WRITE_SIZE = ENUM_INDEX_LENGTH + VALUE_LENGTH;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L48
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L52-L54
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L57-L86
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L94
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L135-L137

## [G-14] Use assembly in place of abi.decode to extract calldata values more efficiently
Instead of using abi.decode we can use assembly to decode our desired calldata values directly. This will allow us to avoid decoding calldata values that we will not use. we can use assembly to decode our desired calldata values directly. This will allow us to avoid decoding calldata values that we will not use

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

190  (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L190

```solidity

file: ethereum/contracts/state-transition/StateTransitionManager.sol

252   Diamond.DiamondCutData memory diamondCut = abi.decode(_diamondCut, (Diamond.DiamondCutData));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L252

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

617   (, uint256 result) = abi.decode(data, (uint256, uint256));

682  versionedHash = abi.decode(data, (bytes32));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L617
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L682

```solidity

file: ethereum/contracts/state-transition/libraries/Diamond.sol

298    require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L298

```solidity

file: contracts/ContractDeployer.sol

347  ImmutableData[] memory immutables = abi.decode(returnData, (ImmutableData[]));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L347

```solidity

file: contracts/libraries/TransactionHelper.sol

374  (address token, uint256 minAllowance) = abi.decode(_transaction.paymasterInput[4:68], (address, uint256));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L374

```solidity

file: zksync/contracts/bridge/L2SharedBridge.sol

177  proxy = BeaconProxy(abi.decode(returndata, (address)));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L177

```solidity

file: zksync/contracts/bridge/L2StandardERC20.sol

57   (bytes memory nameBytes, bytes memory symbolBytes, bytes memory decimalsBytes) = abi.decode(

179  (result) = abi.decode(_input, (string));

184   (result) = abi.decode(_input, (uint8));
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L57
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L179
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L184

## [G-15] Using mappings instead of arrays to avoid length checks save gas
Just by using a mapping, we get a gas saving of 2102 gas. When you read the value of an index of an array, solidity adds bytecode that checks that you are reading from a valid index 

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

48  mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;

    /// @dev A mapping chainId => L2 deposit transaction hash => keccak256(abi.encode(account, tokenAddress, amount))
    /// @dev Tracks deposit transactions from L2 to enable users to claim their funds if a deposit fails.
    mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
        public
        override depositHappened;

    /// @dev Tracks the processing status of L2 to L1 messages, indicating whether a message has already been finalized.
    mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
        public isWithdrawalFinalized;

    /// @dev Indicates whether the hyperbridging is enabled for a given chain.
    mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;

    /// @dev Maps token balances for each chain to prevent unauthorized spending across hyperchains.
    /// This serves as a security measure until hyperbridging is implemented.
65    mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L48-L65

```solidity

file: ethereum/contracts/bridgehub/Bridgehub.sol#

21     mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;
    /// @notice we store registered tokens (for arbitrary base token)
    mapping(address _token => bool) public tokenIsRegistered;

    /// @notice chainID => StateTransitionManager contract address, storing StateTransitionManager
    mapping(uint256 _chainId => address) public stateTransitionManager;

    /// @notice chainID => baseToken contract address, storing baseToken
29    mapping(uint256 _chainId => address) public baseToken;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21-L29

```solidity

file: ethereum/contracts/governance/Governance.sol

32  mapping(bytes32 operationId => uint256 executionTimestamp) public timestamps;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L32

```solidity

file: ethereum/contracts/state-transition/StateTransitionManager.sol

30   mapping(uint256 => address) public stateTransition;

48   mapping(uint256 => bytes32) public upgradeCutHash;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L30
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L48

```solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol

47     mapping(uint256 => LibMap.Uint32Map) internal committedBatchTimestamp;

50    mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L47

```solidity

file: ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

74  mapping(address validatorAddress => bool isValidator) validators;

86     mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
    
88    mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;

114   mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;

120  mapping(address => uint256) __DEPRECATED_totalDepositedAmountPerUser;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L74
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L86-L88
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L114
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L120

```solidity

file: ethereum/contracts/state-transition/libraries/Diamond.sol

51   mapping(bytes4 selector => SelectorToFacet selectorInfo) selectorToFacet;
52   mapping(address facetAddress => FacetToSelectors facetInfo) facetToSelectors;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L51-L52

```solidity

file: ethereum/contracts/state-transition/libraries/LibMap.sol

11  mapping(uint256 packedIndex => uint256 eightPackedValues) map;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L11

```solidity

file: ethereum/contracts/state-transition/libraries/PriorityQueue.sol

28   mapping(uint256 priorityOpId => PriorityOperation priorityOp) data;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L28

```solidity

file: contracts/ContractDeployer.sol

26  mapping(address => AccountInfo) internal accountInfo;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L26

```solidity

file: contracts/ImmutableSimulator.sol

21   mapping(uint256 contractAddress => mapping(uint256 index => bytes32 value)) internal immutableDataStorage;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L21

```solidity

file: contracts/L2BaseToken.sol

20  mapping(address account => uint256 balance) internal balance;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L20

```solidity

file: contracts/NonceHolder.sol

36   mapping(uint256 account => uint256 packedMinAndDeploymentNonce) internal rawNonces;

41   mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L36
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L41

```solidity

file: contracts/SystemContext.sol

55   mapping(uint256 batchNumber => bytes32 batchHash) internal batchHashes;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L55

```solidity

file: zksync/contracts/bridge/L2SharedBridge.sol

35  mapping(address l2TokenAddress => address l1TokenAddress) public override l1TokenAddress;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L35


## [G‑16] Caching global variables is more expensive than using the actual variable (use msg.sender instead of caching it)

```solidity

file: ethereum/contracts/bridge/L1ERC20Bridge.sol

142 uint256 amount = _depositFundsToSharedBridge(msg.sender, IERC20(_l1Token), _amount);

146   msg.sender,

154    depositAmount[msg.sender][_l1Token][l2TxHash] = _amount;
155     emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L142
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L146
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L154-L155

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

69   require(msg.sender == address(bridgehub), "ShB not BH");

76    msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),

138  require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L76
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138

```solidity

file: ethereum/contracts/bridgehub/Bridgehub.sol

46         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

62  require(msg.sender == currentPendingAdmin, "n42");

230     sender: msg.sender,

280   msg.sender,

291  msg.sender,

328   _recipient = msg.sender == tx.origin ? msg.sender : AddressAliasHelper.applyL1ToL2Alias(msg.sender);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L230
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L280
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L291
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L328

```solidity

file: ethereum/contracts/governance/Governance.sol

59    require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

65      require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

72  msg.sender == owner() || msg.sender == securityCouncil,
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L65
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L72

```solidity

file: /ethereum/contracts/state-transition/StateTransitionManager.sol

64   require(msg.sender == bridgehub, "StateTransition: only bridgehub");

70   require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

121     require(msg.sender == currentPendingAdmin, "n42");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L70
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L121

```solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol#

62     require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

68      require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

34  require(msg.sender == pendingAdmin, "n4"); 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

209          sender: msg.sender,

222    msg.sender,
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L209
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L222

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

16       require(msg.sender == s.admin, "StateTransition Chain: not admin");
        _;
    }

    /// @notice Checks if validator is active
    modifier onlyValidator() {
        require(s.validators[msg.sender], "StateTransition Chain: not validator");
        _;
    }

    modifier onlyStateTransitionManager() {
        require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");
        _;
    }

    modifier onlyBridgehub() {
        require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");
        _;
    }

    modifier onlyAdminOrStateTransitionManager() {
        require(
            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by admin or state transition manager"
        );
        _;
    }

    modifier onlyValidatorOrStateTransitionManager() {
        require(
            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
            "StateTransition Chain: Only by validator or state transition manager"
        );
        _;
    }

52 modifier onlyBaseTokenBridge() {
        require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22-L52

```solidity

file: contracts/AccountCodeStorage.sol

26  require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L26

```solidity

file: contracts/ComplexUpgrader.sol

22    require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22

```solidity

file: contracts/ContractDeployer.sol

29   require(msg.sender == address(this), "Callable only by self");

66   accountInfo[msg.sender].supportedAAVersion = _version;

68   emit AccountVersionUpdated(msg.sender, _version);

75   AccountInfo memory currentInfo = accountInfo[msg.sender];

84    _storeAccountInfo(msg.sender, currentInfo);

86   emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);

168  NONCE_HOLDER_SYSTEM_CONTRACT.incrementDeploymentNonce(msg.sender);
169  address newAddress = getNewAddressCreate2(msg.sender, _bytecodeHash, _salt, _input);

188  uint256 senderNonce = NONCE_HOLDER_SYSTEM_CONTRACT.incrementDeploymentNonce(msg.sender);
189  address newAddress = getNewAddressCreate(msg.sender, senderNonce);

240    msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),

254   this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);

297  _constructContract(msg.sender, _newAddress, _bytecodeHash, _input, false, true);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L66
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L68
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L75
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L84-L86
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L168
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L188-L189 
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L240
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L254
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L297

```solidity

file: contracts/DefaultAccount.sol

29  if (msg.sender != BOOTLOADER_FORMAL_ADDRESS)

222  assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L29
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L222

```solidity

file: contracts/ImmutableSimulator.sol

35  require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35

```solidity

file: contracts/KnownCodesStorage.sol

20  require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L20


```solidity

file: contracts/L1Messenger.sol

79  sender: msg.sender,

130   key: bytes32(uint256(uint160(msg.sender))),

156  emit L1MessageSent(msg.sender, hash, _message);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L79
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L130
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L156

```solidity

file: contracts/L2BaseToken.sol

34      msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
        msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
36      msg.sender == BOOTLOADER_FORMAL_ADDRESS,

79   emit Withdrawal(msg.sender, _l1Receiver, amount);

89  bytes memory message = _getExtendedWithdrawMessage(_l1Receiver, amount, msg.sender, _additionalData);

92 emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L34-L36 
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L79
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L89
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L92

```solidity

file: contracts/MsgValueSimulator.sol#

64   abi.encodeCall(REAL_BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo, (msg.sender, to, value))

81 return EfficientCall.mimicCall(userGas, to, _data, msg.sender, false, isSystemCall);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L64
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L81

```solidity

file: contracts/NonceHolder.sol

68    uint256 addressAsKey = uint256(uint160(msg.sender));

89  require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");

92  uint256 addressAsKey = uint256(uint160(msg.sender));

96  emit ValueSetUnderNonce(msg.sender, _key, _value);

103   uint256 addressAsKey = uint256(uint160(msg.sender));

111   uint256 addressAsKey = uint256(uint160(msg.sender));

137  msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L68
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L89
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L92
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L96
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L103
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L111
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L137

```solidity

file: contracts/interfaces/ISystemContract.sol

22 SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),

32  SystemContractHelper.isSystemContract(msg.sender),

41      require(msg.sender == caller, "Inappropriate caller");

    
48     require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");
  
55     require(msg.sender == FORCE_DEPLOYER);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L22
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L32
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L41_55

```solidity

file: zksync/contracts/bridge/L2SharedBridge.sol

88     AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
89     AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,

126   IL2StandardToken(_l2Token).bridgeBurn(msg.sender, _amount);

134   emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L88-L89
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L126
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L134

```solidity

file: zksync/contracts/bridge/L2StandardERC20.sol

54 l2Bridge = msg.sender;

120    require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");

130  require(msg.sender == l2Bridge, "xnt");
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L54
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L130

## [G-17] Emitting constants wastes gas
Every event parameter costs Glogdata (8 gas) per byte. You can avoid this extra cost, in cases where you're emitting a constant, by creating a new version of the event which doesn't have the parameter (and have users look to the contract's variables for its value instead). Alternatively, in the case of boolean constants, two events can be created - one representing the true case and one representing the false case.

```solidity

file: ethereum/contracts/bridge/L1ERC20Bridge.sol

155  emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);

199  emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);

225  emit WithdrawalFinalized(l1Receiver, l1Token, amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L155
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L199
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L225

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

168  emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);

227  emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);

239  emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);

367  emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);

454   emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);

602   emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L168
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L227
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L239
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L367
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L454
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L602

```solidity

file: ethereum/contracts/bridgehub/Bridgehub.sol

56   emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

68    emit NewPendingAdmin(currentPendingAdmin, address(0));
69    emit NewAdmin(previousAdmin, pendingAdmin);

145   emit NewChain(_chainId, _stateTransitionManager, _admin);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L56
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68-L69 
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L145


```solidity

file: ethereum/contracts/governance/Governance.sol

47         emit ChangeSecurityCouncil(address(0), _securityCouncil);

50        emit ChangeMinDelay(0, _minDelay);

132  emit TransparentOperationScheduled(id, _delay, _operation);

144    emit ShadowOperationScheduled(_id, _delay);

157   emit OperationCancelled(_id);

180    emit OperationExecuted(id);

199  emit OperationExecuted(id);

250   emit ChangeMinDelay(minDelay, _newDelay);

257 emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L47-L50
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L132
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L144
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L157
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L180
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L199
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L250
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L257

```solidity

file: ethereum/contracts/state-transition/StateTransitionManager.sol

127         emit NewPendingAdmin(currentPendingAdmin, address(0));
128        emit NewAdmin(previousAdmin, pendingAdmin);

227   emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);

235  emit StateTransitionNewChain(_chainId, _stateTransitionContract);

287   emit StateTransitionNewChain(_chainId, stateTransitionAddress);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L127-L128 
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L235
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L287

```solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol

83   emit ValidatorAdded(_chainId, _newValidator);

92   emit ValidatorRemoved(_chainId, _validator);

98   emit NewExecutionDelay(_executionDelay);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L83
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L92
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

28   emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

40   emit NewPendingAdmin(pendingAdmin, address(0));
41   emit NewAdmin(previousAdmin, pendingAdmin);

47   emit ValidatorStatusUpdate(_validator, _active);

54  emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);

63  emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);

75  emit NewFeeParams(oldFeeParams, _newFeeParams);

86  emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator);

92  emit ValidiumModeStatusUpdate(_validiumMode);

115 emit ExecuteUpgrade(_diamondCut);

125 emit ExecuteUpgrade(_diamondCut);

139  emit Freeze();

149  emit Unfreeze();
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L28
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40-L41
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L47
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L54
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L63
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L75
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L86
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L115
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L125
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L139
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L149

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

135   bytes memory emittedL2Logs = _newBatch.systemLogs;

142    for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
      (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
      (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
146   (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);

261   emit BlockCommit

299  emit BlockCommit

353  emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);   

436 emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

496 emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L135
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142-L146
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L299
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

343  emit NewPriorityRequest
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L343

```solidity

file: ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

87  emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);

104  emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);

121  emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);

137  emit NewVerifier(address(oldVerifier), address(_newVerifier));

157   emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

256   emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L87
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L104
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L121
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L137
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L157
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L256

```solidity

file: contracts/ContractDeployer.sol

68   emit AccountVersionUpdated(msg.sender, _version);

86   emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);

355   emit ContractDeployed(_sender, _bytecodeHash, _newAddress);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L68
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L86
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L355

```solidity

file: contracts/L1Messenger.sol

111 emit L2ToL1LogSent(_l2ToL1Log);

56  emit L1MessageSent(msg.sender, hash, _message);

181 emit BytecodeL1PublicationRequested(_bytecodeHash);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L111
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L156
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L181

```solidity

file: contracts/L2BaseToken.sol

49  emit Transfer(_from, _to, _amount);

67  emit Mint(_account, _amount);

79  emit Withdrawal(msg.sender, _l1Receiver, amount);

92  emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L49
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L67
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L79
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L92

```solidity

file: contracts/NonceHolder.sol

96  emit ValueSetUnderNonce(msg.sender, _key, _value);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L96

```solidity

file: zksync/contracts/bridge/L2SharedBridge.sol

105  emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);

134   emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L105
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L134

```solidity

file: zksync/contracts/bridge/L2StandardERC20.sol

101  emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);

126  emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);

147  emit BridgeMint(_to, _amount);

156  emit BridgeBurn(_from, _amount);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L101
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L147
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L156

## [G-18]  Use assembly for loops
In the following instances, assembly is used for more gas efficient loops.

```solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol

116   for (uint256 i = 0; i < _newBatchesData.length; ++i) 

135   for (uint256 i = 0; i < _newBatchesData.length; ++i) 

185   for (uint256 i = 0; i < _newBatchesData.length; ++i) 

209   for (uint256 i = 0; i < _newBatchesData.length; ++i)
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

208   for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc())
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#

356  for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356

```solidity

file: ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226  for (uint256 i = 0; i < _factoryDeps.length; ++i)
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226

```solidity

file: ethereum/contracts/state-transition/libraries/Diamond.sol#

101    for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc())

138  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc())

158  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) 

178  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L138
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L178

```solidity

file: contracts/KnownCodesStorage.sol

30   for (uint256 i = 0; i < hashesLen; ++i) 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L30

```solidity

file: ystem-contracts/contracts/L1Messenger.sol

206  for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i)

218  for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) 

224 for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) 

236   for (uint256 i = 0; i < numberOfMessages; ++i) 

254    for (uint256 i = 0; i < numberOfBytecodes; ++i) 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L218
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L224
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L236
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L254

## [G‑19] Counting down in for statements is more gas efficient
Counting down is more gas efficient than counting up because neither we are making zero variable to non-zero variable and also we will get gas refund in the last transaction when making non-zero to zero variable.

``solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol

116   for (uint256 i = 0; i < _newBatchesData.length; ++i) 

135   for (uint256 i = 0; i < _newBatchesData.length; ++i) 

185   for (uint256 i = 0; i < _newBatchesData.length; ++i) 

209   for (uint256 i = 0; i < _newBatchesData.length; ++i)
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

208   for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc())
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208

```solidity

file: ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#

356  for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356

```solidity

file: ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226  for (uint256 i = 0; i < _factoryDeps.length; ++i)
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226

```solidity

file: ethereum/contracts/state-transition/libraries/Diamond.sol#

101    for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc())

138  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc())

158  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) 

178  for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L138
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L178

```solidity

file: contracts/KnownCodesStorage.sol

30   for (uint256 i = 0; i < hashesLen; ++i) 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L30

```solidity

file: ystem-contracts/contracts/L1Messenger.sol

206  for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i)

218  for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) 

224 for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) 

236   for (uint256 i = 0; i < numberOfMessages; ++i) 

254    for (uint256 i = 0; i < numberOfBytecodes; ++i) 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L218
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L224
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L236
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L254

## [G-20] Consider using OZ EnumerateSet in place of nested mappings
Nested mappings and multi-dimensional arrays in Solidity operate through a process of double hashing, wherein the original storage slot and the first key are concatenated and hashed, and then this hash is again concatenated with the second key and hashed. This process can be quite gas expensive due to the double-hashing operation and subsequent storage operation (sstore).
A possible optimization involves manually concatenating the keys followed by a single hash operation and an sstore. However, this technique introduces the risk of storage collision, especially when there are other nested hash maps in the contract that use the same key types. Because Solidity is unaware of the number and structure of nested hash maps in a contract, it follows a conservative approach in computing the storage slot to avoid possible collisions.
OpenZeppelin's EnumerableSet provides a potential solution to this problem. It creates a data structure that combines the benefits of set operations with the ability to enumerate stored elements, which is not natively available in Solidity. EnumerableSet handles the element uniqueness internally and can therefore provide a more gas-efficient and collision-resistant alternative to nested mappings or multi-dimensional arrays in certain scenarios.

```solidity

file: ethereum/contracts/bridge/L1ERC20Bridge.sol

32   mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))

51   mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L32
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L51

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

52  mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))

57  mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))

65  mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L52
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L65

```solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol

50  mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50

```solidity

file: ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

114  mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L114

```solidity

file: contracts/ImmutableSimulator.sol

21   mapping(uint256 contractAddress => mapping(uint256 index => bytes32 value)) internal immutableDataStorage;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L21

```solidity

file: contracts/NonceHolder.sol

41  mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L41

## [G-21] Multiple address/ID mappings can be combined into a single mapping of an address/ID to a struct, where appropriate
Saves a storage slot for the mapping. Depending on the circumstances and sizes of types, can avoid a Gsset (20000 gas) per mapping combined. Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Finally, if both fields are accessed in the same function, can save ~42 gas per access due to not having to recalculate the key’s keccak256 hash (Gkeccak256 - 30 gas) and that calculation’s associated stack operations.

```solidity

file: ethereum/contracts/bridge/L1SharedBridge.sol

48  mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;

    /// @dev A mapping chainId => L2 deposit transaction hash => keccak256(abi.encode(account, tokenAddress, amount))
    /// @dev Tracks deposit transactions from L2 to enable users to claim their funds if a deposit fails.
    mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))
        public
        override depositHappened;

    /// @dev Tracks the processing status of L2 to L1 messages, indicating whether a message has already been finalized.
    mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))
        public isWithdrawalFinalized;

    /// @dev Indicates whether the hyperbridging is enabled for a given chain.
    mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;

    /// @dev Maps token balances for each chain to prevent unauthorized spending across hyperchains.
    /// This serves as a security measure until hyperbridging is implemented.
65    mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L48-L65

```solidity

file: ethereum/contracts/bridgehub/Bridgehub.sol#

21     mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;
    /// @notice we store registered tokens (for arbitrary base token)
    mapping(address _token => bool) public tokenIsRegistered;

    /// @notice chainID => StateTransitionManager contract address, storing StateTransitionManager
    mapping(uint256 _chainId => address) public stateTransitionManager;

    /// @notice chainID => baseToken contract address, storing baseToken
29    mapping(uint256 _chainId => address) public baseToken;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21-L29

```solidity

file: ethereum/contracts/governance/Governance.sol

32  mapping(bytes32 operationId => uint256 executionTimestamp) public timestamps;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L32

```solidity

file: ethereum/contracts/state-transition/StateTransitionManager.sol

30   mapping(uint256 => address) public stateTransition;

48   mapping(uint256 => bytes32) public upgradeCutHash;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L30
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L48

```solidity

file: ethereum/contracts/state-transition/ValidatorTimelock.sol

47     mapping(uint256 => LibMap.Uint32Map) internal committedBatchTimestamp;

50    mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L47

```solidity

file: ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

74  mapping(address validatorAddress => bool isValidator) validators;

86     mapping(uint256 batchNumber => bytes32 batchHash) storedBatchHashes;
    
88    mapping(uint256 batchNumber => bytes32 l2LogsRootHash) l2LogsRootHashes;

114   mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;

120  mapping(address => uint256) __DEPRECATED_totalDepositedAmountPerUser;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L74
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L86-L88
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L114
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L120

```solidity

file: ethereum/contracts/state-transition/libraries/Diamond.sol

51   mapping(bytes4 selector => SelectorToFacet selectorInfo) selectorToFacet;
52   mapping(address facetAddress => FacetToSelectors facetInfo) facetToSelectors;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L51-L52

```solidity

file: ethereum/contracts/state-transition/libraries/LibMap.sol

11  mapping(uint256 packedIndex => uint256 eightPackedValues) map;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L11

```solidity

file: ethereum/contracts/state-transition/libraries/PriorityQueue.sol

28   mapping(uint256 priorityOpId => PriorityOperation priorityOp) data;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L28

```solidity

file: contracts/ContractDeployer.sol

26  mapping(address => AccountInfo) internal accountInfo;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L26

```solidity

file: contracts/ImmutableSimulator.sol

21   mapping(uint256 contractAddress => mapping(uint256 index => bytes32 value)) internal immutableDataStorage;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L21

```solidity

file: contracts/L2BaseToken.sol

20  mapping(address account => uint256 balance) internal balance;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L20

```solidity

file: contracts/NonceHolder.sol

36   mapping(uint256 account => uint256 packedMinAndDeploymentNonce) internal rawNonces;

41   mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L36
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L41

```solidity

file: contracts/SystemContext.sol

55   mapping(uint256 batchNumber => bytes32 batchHash) internal batchHashes;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L55

```solidity

file: zksync/contracts/bridge/L2SharedBridge.sol

35  mapping(address l2TokenAddress => address l1TokenAddress) public override l1TokenAddress;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L35

