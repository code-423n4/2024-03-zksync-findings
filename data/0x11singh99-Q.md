### Low Risk Issues

- [L-01] [Check for the maximum difference between protocol versions may be redundant given the existing checks implemented in the `BaseZkSyncUpgradeGenesis::_setNewProtocolVersion`](#l-01-check-for-the-maximum-difference-between-protocol-versions-may-be-redundant-given-the-existing-checks-implemented-in-the-basezksyncupgradegenesis_setnewprotocolversion)
- [L-02] [Checking the success status of each low-level call and reverting if any call fails](#l-02-checking-the-success-status-of-each-low-level-call-and-reverting-if-any-call-fails)
- [L-03] [Emit events before external call](#l-03-emit-events-before-external-call)
- [L-04] [Remove `unchecked` block](#l-04-remove-unchecked-block)
- [L-05] [Mispleading event](#l-05-mispleading-event)
- [L-06] [Override the `renounceOwnership` function](#l-06-override-the-renounceownership-function)
- [L-07] [Missing checks for `address(0x0)` in the `constructor`](#l-07-missing-checks-for-address0x0-in-the-constructor)
- [L-08] [Missing zero address check in functions with address parameters](#l-08-missing-zero-address-check-in-functions-with-address-parameters)
- [L-09] [State variables `l2Bridge`, `l2TokenBeacon`, and `l2TokenProxyBytecodeHash` are not explicitly initialized](#l-09-state-variables-l2bridge-l2tokenbeacon-and-l2tokenproxybytecodehash-are-not-explicitly-initialized)

| Total Low Risk Issues | 9   |
| --------------------- | --- |

### Non-Critical Issues

- [N-01] [NatSpec: `Event` missing NatSpec `@dev` tag](#n-01-natspec-event-missing-natspec-dev-tag)
- [N-02] [The `upgrade` function declares a `return` type but does not explicitly `return` any value](#n-02-the-upgrade-function-declares-a-return-type-but-does-not-explicitly-return-any-value)
- [N-03] [NatSpec: Functions missing NatSpec `@return` tag](#n-03-natspec-functions-missing-natspec-return-tag)
- [N-04] [NatSpec: Contract declarations should have `@author` tags](#n-04-natspec-contract-declarations-should-have-author-tags)
- [N-05] [NatSpec: Contract declarations should have `@dev` tags](#n-05-natspec-contract-declarations-should-have-dev-tags)
- [N-06] [NatSpec: Modifier missing NatSpec `@dev` tag](#n-06-natspec-modifier-missing-natspec-dev-tag)
- [N-07] [NatSpec: Modifier missing NatSpec `@param` tag](#n-07-natspec-modifier-missing-natspec-param-tag)
- [N-08] [Not using the named return variables when a function returns](#n-08-not-using-the-named-return-variables-when-a-function-returns)
- [N-09] [Order of functions don't follow solidity style guide](#n-09-order-of-functions-dont-follow-solidity-style-guide)

| Total Non-Critical Issues | 9   |
| ------------------------- | --- |

# Low Risk

## [L-01] Check for the maximum difference between protocol versions may be redundant given the existing checks implemented in the `BaseZkSyncUpgradeGenesis::_setNewProtocolVersion`

The `_setNewProtocolVersion` function, which is called internally to change the protocol version, already includes a requirement that the new protocol version must be greater than or equal to the previous one.
Additionally, it checks if the difference between the new and previous protocol versions does not exceed a certain threshold (`MAX_ALLOWED_PROTOCOL_VERSION_DELTA`). The existing checks in `_setNewProtocolVersion` already ensure that the upgrade process adheres to sensible constraints, preventing sudden jumps in protocol versions that could potentially disrupt the system.

```solidity
File : contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

20:    function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
            uint256 previousProtocolVersion = s.protocolVersion;
            require(
                // Genesis Upgrade difference: Note this is the only thing change > to >=
                _newProtocolVersion >= previousProtocolVersion,
                "New protocol version is not greater than the current one"
            );
            require(
28:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
                "Too big protocol version difference"
            );


File : contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

142:    function setNewVersionUpgrade(
            Diamond.DiamondCutData calldata _cutData,
            uint256 _oldProtocolVersion,
            uint256 _newProtocolVersion
        ) external onlyOwner {
            upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
148:        protocolVersion = _newProtocolVersion;
        }

```

[20-30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20C5-L30C11), [142-149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L142C5-L149C6)

## [L-02] Checking the success status of each low-level call and reverting if any call fails

The `_getERC20Getters` function should check the success status of each `staticcall` using the return value and revert the transaction if any call fails. Adding error handling logic to check the success status of `staticcall` operations and revert the transaction if any call fails.

```solidity
File : contracts/ethereum/contracts/bridge/L1SharedBridge.sol

254:    function _getERC20Getters(address _token) internal view returns (bytes memory) {
            if (_token == ETH_TOKEN_ADDRESS) {
                bytes memory name = bytes("Ether");
                bytes memory symbol = bytes("ETH");
                bytes memory decimals = abi.encode(uint8(18));
                return abi.encode(name, symbol, decimals); // when depositing eth to a non-eth based chain it is an ERC20
            }

            (, bytes memory data1) = _token.staticcall(abi.encodeCall(IERC20Metadata.name, ()));
            (, bytes memory data2) = _token.staticcall(abi.encodeCall(IERC20Metadata.symbol, ()));
            (, bytes memory data3) = _token.staticcall(abi.encodeCall(IERC20Metadata.decimals, ()));
            return abi.encode(data1, data2, data3);

```

[254-265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L254C1-L265C48)

## [L-03] Emit events before external call

Emitting events before external calls in Solidity enhances transaction atomicity, provides comprehensive event logging, helps protect against front-running attacks, improves user experience, and enables better gas optimization. It's a best practice that contributes to the security, transparency, and efficiency of smart contract development.

```solidity
File : contracts/ethereum/contracts/bridgehub/Bridgehub.sol

114:  function createNewChain(
...
137:    IStateTransitionManager(_stateTransitionManager).createNewChain(
138:            _chainId,
139:            _baseToken,
140:            address(sharedBridge),
141:            _admin,
142:            _initData
143:        );
144:
145:        emit NewChain(_chainId, _stateTransitionManager, _admin);

```

[137-145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L137C8-L145C66)

## [L-04] Remove `unchecked` block

It mentions that the offset value used in the addition operation is significant, implying that it might be large enough to potentially cause overflow issues. Removing the unchecked block ensures that arithmetic operations are checked for overflow and underflow, reducing the likelihood of vulnerabilities and promoting code safety and reliability.

Remove `unchecked` block from `applyL1ToL2Alias` and `undoL1ToL2Alias` functions

### Unsafe `unchecked` `addition` may cause unwanted `overflow` since offsets also a big value

```solidity
File : contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

28:     function applyL1ToL2Alias(address l1Address) internal pure returns (address l2Address) {
29:           unchecked {
30:              l2Address = address(uint160(l1Address) + offset);
31:           }

```

[28-31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L28C5-L31C10)

### Unsafe `unchecked` `subtraction` may cause unwanted `underflow` since offsets also a big value

```solidity
File : contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

38:     function undoL1ToL2Alias(address l2Address) internal pure returns (address l1Address) {
39:           unchecked {
40:              l1Address = address(uint160(l2Address) - offset);
41:           }

```

[38-41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L38C5-L41C10)

## [L-05] Mispleading event

The event `NewAdmin` emits the address(0) as the `pendingAdmin`, which might be misleading since the `pendingAdmin` is deleted. Instead of emitting address(0) as the `pendingAdmin`, it would be clearer to emit the `currentPendingAdmin` address, as it represents the `newAdmin` address after the `pendingAdmin` is set as the `newAdmin`.

```solidity
File : contracts/ethereum/contracts/bridgehub/Bridgehub.sol

65:        admin = currentPendingAdmin;
66:        delete pendingAdmin;
67:
68:        emit NewPendingAdmin(currentPendingAdmin, address(0));
69:        emit NewAdmin(previousAdmin, pendingAdmin);

```

[65-69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L65C1-L69C52)

## [L-06] Override the `renounceOwnership` function

The override of the `renounceOwnership` function inherited from the `OpenZeppelin` `Ownable` contract. It recommends overriding the `renounceOwnership` function to revert if called, preventing accidental ownership renunciation. The rationale behind this is to add an extra layer of protection against accidental or malicious removal of ownership.

```solidity
File : contracts/ethereum/contracts/governance/Governance.sol

129:    function scheduleTransparent(Operation calldata _operation, uint256 _delay) external onlyOwner {
130:        bytes32 id = hashOperation(_operation);
131:        _schedule(id, _delay);
132:        emit TransparentOperationScheduled(id, _delay, _operation);
133:    }

```

[129-133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L129C1-L133C6)

## [L-07] Missing checks for `address(0x0)` in the `constructor`

### Check `_admin` and `_securityCouncil`

```solidity
File : contracts/ethereum/contracts/governance/Governance.sol

41:    constructor(address _admin, address _securityCouncil, uint256 _minDelay) {
            require(_admin != address(0), "Admin should be non zero address");

            _transferOwnership(_admin);

46:        securityCouncil = _securityCouncil;
           emit ChangeSecurityCouncil(address(0), _securityCouncil);

49:        minDelay = _minDelay;
           emit ChangeMinDelay(0, _minDelay);
        }

```

[41-51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L41C1-L51C6)

### Check `_l1WethAddress`, `_bridgehub` and `_legacyBridge`

```solidity
File : contracts/ethereum/contracts/bridge/L1SharedBridge.sol

90:    constructor(
91:       address _l1WethAddress,
92:       IBridgehub _bridgehub,
93:       IL1ERC20Bridge _legacyBridge
          ) reentrancyGuardInitializer {
              _disableInitializers();
96:           l1WethAddress = _l1WethAddress;
97:           bridgehub = _bridgehub;
98:           legacyBridge = _legacyBridge;
        }

```

[90-99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90C4-L99C6)

## [L-08] Missing zero address check in functions with address parameters

Adding a zero address check for each address type parameter can prevent errors.

### Check `_owner` for address zero

Since `_transferOwnership` don't have address zero check

```solidity
File : contracts/ethereum/contracts/bridgehub/Bridgehub.sol

41:    function initialize(address _owner) external reentrancyGuardInitializer {
42:        _transferOwnership(_owner);
43:    }

```

[41-43](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L41C1-L43C6)

### Check `_stateTransitionManager` for address zero

```solidity
File : contracts/ethereum/contracts/bridgehub/Bridgehub.sol

92:    function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner {
93:        require(
94:            stateTransitionManagerIsRegistered[_stateTransitionManager],
95:            "Bridgehub: state transition not registered yet"
96:        );
97:        stateTransitionManagerIsRegistered[_stateTransitionManager] = false;

```

[92-97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L92C1-L97C77)

### Check `_sharedBridge` for address zero

```solidity
File : contracts/ethereum/contracts/bridgehub/Bridgehub.sol

108:    function setSharedBridge(address _sharedBridge) external onlyOwner {
109:        sharedBridge = IL1SharedBridge(_sharedBridge);

```

[108-109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108C1-L109C55)

## [L-09] State variables `l2Bridge`, `l2TokenBeacon`, and `l2TokenProxyBytecodeHash` are not explicitly initialized

In `L1ERC20Bridge` contract , If these variables are not initialized explicitly, they will indeed take on the default values for their respective types. You may want to initialize these variables in the constructor or at some point during the contract execution to ensure they hold meaningful values.
Otherwise they will always gives 0 value.

```solidity
File : contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

36:    address public l2Bridge;

       /// @dev The address that is used as a beacon for L2 tokens in zkSync Era.
39:    address public l2TokenBeacon;

       /// @dev Stores the hash of the L2 token proxy contract's bytecode on zkSync Era.
42:    bytes32 public l2TokenProxyBytecodeHash;

```

[36-42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L36C5-L42C45)

# Non-Critical

## [N-01] NatSpec: `Event` missing NatSpec `@dev` tag

```solidity
File : contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

       /// @notice Changes the protocol version
46:    event NewProtocolVersion(uint256 indexed previousProtocolVersion, uint256 indexed newProtocolVersion);

       /// @notice Сhanges to the bytecode that is used in L2 as a bootloader (start program)
49:    event NewL2BootloaderBytecodeHash(bytes32 indexed previousBytecodeHash, bytes32 indexed newBytecodeHash);

       /// @notice Сhanges to the bytecode that is used in L2 as a default account
52:    event NewL2DefaultAccountBytecodeHash(bytes32 indexed previousBytecodeHash, bytes32 indexed newBytecodeHash);

       /// @notice Verifier address changed
55:    event NewVerifier(address indexed oldVerifier, address indexed newVerifier);

       /// @notice Verifier parameters changed
58:    event NewVerifierParams(VerifierParams oldVerifierParams, VerifierParams newVerifierParams);

       /// @notice Notifies about complete upgrade
61:    event UpgradeComplete(uint256 indexed newProtocolVersion, bytes32 indexed l2UpgradeTxHash, ProposedUpgrade upgrade);

```

[45-61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L45C1-L61C121)

## [N-02] The `upgrade` function declares a `return` type but does not explicitly `return` any value

Within the `upgrade` function implementation, there is no explicit return statement that provides a bytes32 value. The function executes several upgrade steps and emits an event `UpgradeComplete` but does not explicitly return any value.

```solidity
File : contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

47:    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public virtual override returns (bytes32) {
            // Note that due to commitment delay, the timestamp of the L2 upgrade batch may be earlier than the timestamp
            // of the L1 block at which the upgrade occurred. This means that using timestamp as a signifier of "upgraded"
            // on the L2 side would be inaccurate. The effects of this "back-dating" of L2 upgrade batches will be reduced
            // as the permitted delay window is reduced in the future.
            require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

            _setNewProtocolVersion(_proposedUpgrade.newProtocolVersion);
            _upgradeL1Contract(_proposedUpgrade.l1ContractsUpgradeCalldata);
            _upgradeVerifier(_proposedUpgrade.verifier, _proposedUpgrade.verifierParams);
            _setBaseSystemContracts(_proposedUpgrade.bootloaderHash, _proposedUpgrade.defaultAccountHash);

            bytes32 txHash = _setL2SystemContractUpgrade(
                _proposedUpgrade.l2ProtocolUpgradeTx,
                _proposedUpgrade.factoryDeps,
                _proposedUpgrade.newProtocolVersion
            );

            _postUpgrade(_proposedUpgrade.postUpgradeCalldata);

67:         emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);
        }

```

[47-68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L47C5-L68C6)

## [N-03] NatSpec: Functions missing NatSpec `@return` tag

```solidity
File : contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

11:      /// @notice The main function that will be called by the upgrade proxy.
12:      /// @param _proposedUpgrade The upgrade to be executed.
13:      function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {

```

[11-13](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L11C5-L13C100)

```solidity
File : contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

12:     /// @notice The main function that will be called by the upgrade proxy.
13:     /// @param _proposedUpgrade The upgrade to be executed.
14:     function upgrade(ProposedUpgrade calldata _proposedUpgrade) public override returns (bytes32) {

```

[12-14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L12C4-L14C100)

```solidity
File : contracts/ethereum/contracts/bridgehub/Bridgehub.sol

111:
112:    /// @notice register new chain
113:    /// @notice for Eth the baseToken address is 1
114:    function createNewChain(


150:
151:    /// @notice forwards function call to Mailbox based on ChainId
152:    function proveL2MessageInclusion(


162:
163:    /// @notice forwards function call to Mailbox based on ChainId
164:    function proveL2LogInclusion(

```

[111-114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L111C1-L114C29), [150-152](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L150C1-L152C38), [162-164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L162C1-L164C34)

## [N-04] NatSpec: Contract declarations should have `@author` tags

```solidity
File : contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

20:
21:     library AddressAliasHelper {

```

[20-21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L20C1-L21C29)

## [N-05] NatSpec: Contract declarations should have `@dev` tags

```solidity
File : contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

20:
21:     library AddressAliasHelper {

```

[20-21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L20C1-L21C29)

## [N-06] NatSpec: Modifier missing NatSpec `@dev` tag

```solidity
File : contracts/ethereum/contracts/bridgehub/Bridgehub.sol

44:
45:     modifier onlyOwnerOrAdmin() {

```

[44-45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L44C1-L45C34)

```solidity
File : contracts/ethereum/contracts/governance/Governance.sol

56:
57:    /// @notice Checks that the message sender is contract itself.
58:    modifier onlySelf() {


62:
63:    /// @notice Checks that the message sender is an active security council.
64:    modifier onlySecurityCouncil() {


68:
69:    /// @notice Checks that the message sender is an active owner or an active security council.
70:    modifier onlyOwnerOrSecurityCouncil() {

```

[56-58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L56C1-L58C26), [62-64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L62C1-L64C37), [68-70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L68C1-L70C44)

## [N-07] NatSpec: Modifier missing NatSpec `@param` tag

```solidity
File : contracts/ethereum/contracts/bridgehub/Bridgehub.sol

44:
45:     modifier onlyOwnerOrAdmin() {

```

[44-45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L44C1-L45C34)

## [N-08] Not using the named return variables when a function returns

```solidity
File : contracts/ethereum/contracts/bridgehub/Bridgehub.sol

114:    function createNewChain(
            uint256 _chainId,
            address _stateTransitionManager,
            address _baseToken,
            uint256, //_salt
            address _admin,
            bytes calldata _initData
121:    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
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
146:        return _chainId;
       }

```

[114-147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114C1-L147C6)

## [N-09] Order of functions don't follow solidity style guide

See the [order of functions](https://docs.soliditylang.org/en/latest/style-guide.html#order-of-functions) section of the Solidity Style Guide

```solidity
File :

84:    function isOperation(bytes32 _id) public view returns (bool) {
89:    function isOperationPending(bytes32 _id) public view returns (bool) {
95:    function isOperationReady(bytes32 _id) public view returns (bool) {
100:   function isOperationDone(bytes32 _id) public view returns (bool) {
105:   function getOperationState(bytes32 _id) public view returns (OperationState) {
129:   function scheduleTransparent(Operation calldata _operation, uint256 _delay) external onlyOwner {
142:   function scheduleShadow(bytes32 _id, uint256 _delay) external onlyOwner {
154:   function cancel(bytes32 _id) external onlyOwner {
167:   function execute(Operation calldata _operation) external payable onlyOwnerOrSecurityCouncil {
186    function executeInstant(Operation calldata _operation) external payable onlySecurityCouncil {
204:   function hashOperation(Operation calldata _operation) public pure returns (bytes32) {
215:   function _schedule(bytes32 _id, uint256 _delay) internal {
224:   function _execute(Call[] calldata _calls) internal {
239:   function _checkPredecessorDone(bytes32 _predecessorId) internal view {
249:   function updateDelay(uint256 _newDelay) external onlySelf {
256:   function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
262:   receive() external payable {}


```

[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L84C5-L84C67), [89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L89C5-L89C74), [95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L95C5-L95C72), [100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L100C4-L100C71), [105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L105C5-L105C83), [129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L129C4-L129C101), [142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L142C4-L142C78), [154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L154C5-L154C54), [167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L167C5-L167C98), [186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L186C5-L186C98), [204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L204C5-L204C90), [215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L215C5-L215C63), [224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L224C5-L224C57), [239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L239C4-L239C75), [249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L249C5-L249C64), [256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L256C5-L256C84), [262](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L262C5-L262C34)
