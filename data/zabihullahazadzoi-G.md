### Gas Optimizations Report


## [GAS-1] Increments can be unchecked to save gas
Using unchecked increments can save gas by bypassing the built-in overflow checks. This can save 30-40 gas per iteration. So it is recommended to use unchecked increments when overflow is not possible.

**Total Instances:** 18

**Gas per instance:** 60
**Total Gas saved:** 1080

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 225:         for (uint256 i = 0; i < _calls.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 116:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

 135:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

 185:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

 209:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

 667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 248:         for (uint256 i = 0; i < deploymentsLength; ++i) {

 253:         for (uint256 i = 0; i < deploymentsLength; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L248

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

 38:             for (uint256 i = 0; i < immutablesLength; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L38

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

 30:             for (uint256 i = 0; i < hashesLen; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L30

```solidity
File: system-contracts/contracts/L1Messenger.sol

 206:         for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

 218:         for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

 224:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

 236:         for (uint256 i = 0; i < numberOfMessages; ++i) {

 254:         for (uint256 i = 0; i < numberOfBytecodes; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L206

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol

 36:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36


## [GAS-2] `array[index] += amount` is cheaper than `array[index] = array[index] + amount` (or related variants)
When updating a value in an array with arithmetic, using `array[index] += amount` is cheaper than `array[index] = array[index] + amount`.
This is because you avoid an additonal `mload` when the array is stored in memory, and an `sload` when the array is stored in storage.
This can be applied for any arithmetic operation including `+=`, `-=`,`/=`,`*=`,`^=`,`&=`, `%=`, `<<=`,`>>=`, and `>>>=`.
This optimization can be particularly significant if the pattern occurs during a loop.

*Saves 28 gas for a storage array, 38 for a memory array*

**Total Instances:** 1

**Gas per instance:** 38
**Total Gas saved:** 38

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 133:             chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133


## [GAS-3] Avoid emitting storage values
Caching of a state variable replaces each Gwarmaccess (100 gas) with a much cheaper stack read. We can avoid unecessary SLOADs by caching storage values that were previously accessed and emitting those cached values.

**Total Instances:** 7

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 /// @audit  cache pendingAdmin
 69:         emit NewAdmin(previousAdmin, pendingAdmin);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 /// @audit  cache minDelay
 250:         emit ChangeMinDelay(minDelay, _newDelay);

 /// @audit  cache securityCouncil
 257:         emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L250

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 /// @audit  cache pendingAdmin
 128:         emit NewAdmin(previousAdmin, pendingAdmin);

 /// @audit  cache protocolVersion
 227:         emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L128

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 /// @audit  cache decimals_
 101:         emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);

 /// @audit  cache l1Address, decimals_
 126:         emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126


## [GAS-4]  Avoid updating storage when the value hasn’t changed
If the old value is equal to the new value, not re-storing the value will avoid a Gsreset (2900 gas), potentially at the expense of a Gcoldsload (2100 gas) or a Gwarmaccess (100 gas)

**Total Instances:** 76

**Gas per instance:** 800
**Total Gas saved:** 60800

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 111:         eraFirstPostUpgradeBatch = _eraFirstPostUpgradeBatch;

 112:         l2BridgeAddress[ERA_CHAIN_ID] = ERA_ERC20_BRIDGE_ADDRESS;

 143:         l2BridgeAddress[_chainId] = _l2BridgeAddress;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L111

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 55:         pendingAdmin = _newPendingAdmin;

 65:         admin = currentPendingAdmin;

 87:         stateTransitionManagerIsRegistered[_stateTransitionManager] = true;

 97:         stateTransitionManagerIsRegistered[_stateTransitionManager] = false;

 103:         tokenIsRegistered[_token] = true;

 109:         sharedBridge = IL1SharedBridge(_sharedBridge);

 135:         baseToken[_chainId] = _baseToken;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 179:         timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP;

 198:         timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP;

 219:         timestamps[_id] = block.timestamp + _delay;

 251:         minDelay = _newDelay;

 258:         securityCouncil = _newSecurityCouncil;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L179

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 85:         genesisUpgrade = _initializeData.genesisUpgrade;

 86:         protocolVersion = _initializeData.protocolVersion;

 87:         validatorTimelock = _initializeData.validatorTimelock;

 100:         storedBatchZero = keccak256(abi.encode(batchZero));

 102:         initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

 114:         pendingAdmin = _newPendingAdmin;

 124:         admin = currentPendingAdmin;

 133:         validatorTimelock = _validatorTimelock;

 138:         initialCutHash = keccak256(abi.encode(_diamondCut));

 147:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

 148:         protocolVersion = _newProtocolVersion;

 156:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

 234:         stateTransition[_chainId] = _stateTransitionContract;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L85

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 74:         stateTransitionManager = _stateTransitionManager;

 97:         executionDelay = _executionDelay;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L74

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 60:         l1Bridge = _l1Bridge;

 61:         l2TokenProxyBytecodeHash = _l2TokenProxyBytecodeHash;

 65:             l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(l2StandardToken);

 99:             l1TokenAddress[expectedL2Token] = _l1Token;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L60

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 52:         l1Address = _l1Address;

 54:         l2Bridge = msg.sender;

 95:             decimals_ = decimalsUint8;

 100:         availableGetters = getters;

 124:         availableGetters = _availableGetters;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L52

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 59:         accountInfo[_address] = _newInfo;

 66:         accountInfo[msg.sender].supportedAAVersion = _version;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L59

```solidity
File: system-contracts/contracts/L1Messenger.sol

 106:         chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

 122:         chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

 164:         chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

 329:         chainedLogsHash = bytes32(0);

 330:         numberOfLogsToProcess = 0;

 331:         chainedMessagesHash = bytes32(0);

 332:         chainedL1BytecodesRevealDataHash = bytes32(0);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L106

```solidity
File: system-contracts/contracts/L2BaseToken.sol

 43:             balance[_from] = fromBalance - _amount;

 46:             balance[_to] += _amount;

 65:         totalSupply += _amount;

 66:         balance[_account] += _amount;

 106:             balance[address(this)] -= amount;

 107:             totalSupply -= amount;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L43

```solidity
File: system-contracts/contracts/NonceHolder.sol

 72:             rawNonces[addressAsKey] = (oldRawNonce + _value);

 118:             rawNonces[addressAsKey] = oldRawNonce + 1;

 144:             rawNonces[addressAsKey] = (oldRawNonce + DEPLOY_NONCE_MULTIPLIER);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L72

```solidity
File: system-contracts/contracts/SystemContext.sol

 85:         chainId = _newChainId;

 100:         origin = _newOrigin;

 106:         gasPrice = _gasPrice;

 113:         basePubdataSpent = _basePubdataSpent;

 114:         gasPerPubdataByte = _gasPerPubdataByte;

 213:         l2BlockHash[_block % MINIBLOCK_HASHES_TO_STORE] = _hash;

 271:             currentVirtualL2BlockInfo = currentL2BlockInfo;

 285:             virtualBlockUpgradeInfo.virtualBlockStartBatch = currentBatchNumber;

 307:         currentVirtualL2BlockInfo = virtualBlockInfo;

 316:         currentL2BlockInfo = BlockInfo({number: _l2BlockNumber, timestamp: _l2BlockTimestamp});

 322:         currentL2BlockTxsRollingHash = bytes32(0);

 403:         currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));

 456:         batchHashes[previousBatchNumber] = _prevBatchHash;

 461:         currentBatchInfo = newBlockInfo;

 463:         baseFee = _baseFee;

 477:         currentBatchInfo = newBlockInfo;

 479:         baseFee = _baseFee;

 483:         txNumberInBlock += 1;

 487:         txNumberInBlock = 0;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L487



## [GAS-5] bytes constants are more efficient than string constants
If the data can fit in 32 bytes, the bytes32 data type can be used instead of bytes or strings, as it is more gas efficient and less robust in terms of robustness.

**Total Instances:** 4

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 26:     string public constant override getName = "ValidatorTimelock";

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 20:     string public constant override getName = "AdminFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 27:     string public constant override getName = "ExecutorFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

 25:     string public constant override getName = "GettersFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25



## [GAS-6] Multiple accesses of the same mapping/array key/index should be cached
The instances below point to the second+ access of a value inside a mapping/array, within a function. Caching a mapping’s value in a local storage or calldata variable when the value is accessed multiple times, saves ~42 gas per access due to not having to recalculate the key’s keccak256 hash (Gkeccak256 - 30 gas) and that calculation’s associated stack operations. Caching an array’s struct avoids recalculating the array offsets into memory/calldata

**Total Instances:** 27

**Gas per instance:** 42
**Total Gas saved:** 1134

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 187:         delete depositAmount[_depositSender][_l1Token][_l2TxHash];

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L187

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 122:             chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =

 221:                 l2Contract: l2BridgeAddress[_chainId],

 237:         require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");

 343:                 delete depositHappened[_chainId][_l2TxHash];

 349:             require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");

 417:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");

 439:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds

 586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L122

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 84:             !stateTransitionManagerIsRegistered[_stateTransitionManager],

 102:         require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L84

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 82:         validators[_chainId][_newValidator] = true;

 91:         validators[_chainId][_validator] = false;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L82

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 66:             blobHashes[0] = logOutput.blob1Hash;

 353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

 408:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],

 670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),

 670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L66

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 103:             address facet = facetCuts[i].facet;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L103

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

 31:                 ? _efficientHash(currentHash, _path[i])

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L31

```solidity
File: system-contracts/contracts/Compressor.sol

 174:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L174

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 249:             sumOfValues += _deployments[i].value;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L249

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

 40:                 bytes32 value = _immutables[i].value;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L40

```solidity
File: system-contracts/contracts/L1Messenger.sol

 219:             l2ToL1LogsTreeArray[i] = L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L219

```solidity
File: system-contracts/contracts/libraries/RLPEncoder.sol

 29:                 encoded[0] = (_val == 0) ? bytes1(uint8(128)) : bytes1(uint8(_val));

 64:                 encoded[0] = bytes1(uint8(_len + _offset));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L64


## [GAS-7] The result of a function call should be cached rather than re-calling the function
The function calls in solidity are expensive. If the same result of the same function calls are to be used several times, the result should be cached to reduce the gas consumption of repeated calls.

**Total Instances:** 13

**Gas per instance:** 100
**Total Gas saved:** 1300

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 67:         IERC20(_token).safeTransfer(address(sharedBridge), amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 128:             uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L128

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 288:         L2TransactionRequestTwoBridgesInner memory outputRequest = IL1SharedBridge(_request.secondBridgeAddress)

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L288

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 177:         require(isOperationReady(id), "Operation must be ready after execution");

 196:         require(isOperationPending(id), "Operation must be pending after execution");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L177

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 430:             _verifyProof(proofPublicInput, _proof);

 637:             bytes32 blobVersionedHash = _getBlobVersionedHash(versionedHashIndex);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L430

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

 55:         require(_transaction.reserved[1] <= type(uint160).max, "uf");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55

```solidity
File: system-contracts/contracts/Compressor.sol

 178:             _verifyValueCompression(

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L178

```solidity
File: system-contracts/contracts/GasBoundCaller.sol

 57:         bytes memory returnData = EfficientCall.call(gasleft(), _to, msg.value, _data, false);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L57

```solidity
File: system-contracts/contracts/L1Messenger.sol

 119:         uint256 gasSpentOnMessageHashing = gasBeforeMessageHashing - gasleft();

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L119

```solidity
File: system-contracts/contracts/SystemContext.sol

 392:             _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L392

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 382:                 IERC20(token).safeApprove(paymaster, 0);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L382


## [GAS-8] State variables that are used multiple times in a function should be cached in stack variables
When performing multiple operations on a state variable in a function, it is recommended to cache it first. Either multiple reads or multiple writes to a state variable can save gas by caching it on the stack. Caching of a state variable replaces each Gwarmaccess (100 gas) with a much cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses. Saves 100 gas per instance.

**Total Instances:** 29

**Gas per instance:** 100
**Total Gas saved:** 2900

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 64:         require(msg.sender == address(sharedBridge), "Not shared bridge");

 163:         uint256 balanceAfter = _token.balanceOf(address(sharedBridge));

 187:         delete depositAmount[_depositSender][_l1Token][_l2TxHash];

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 123:                 chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +

 221:                 l2Contract: l2BridgeAddress[_chainId],

 237:         require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");

 343:                 delete depositHappened[_chainId][_l2TxHash];

 349:             require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");

 417:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");

 439:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds

 467:             bool baseTokenWithdrawal = (l1Token == bridgehub.baseToken(_chainId));

 586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L123

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 84:             !stateTransitionManagerIsRegistered[_stateTransitionManager],

 102:         require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L84

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 82:         validators[_chainId][_newValidator] = true;

 91:         validators[_chainId][_validator] = false;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L82

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 66:             l2TokenBeacon.transferOwnership(_aliasedOwner);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L66

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol

 108:             codeHash = EMPTY_STRING_KECCAK;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L108

```solidity
File: system-contracts/contracts/L1Messenger.sol

 106:         chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

 109:         numberOfLogsToProcess++;

 122:         chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

 164:         chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

 215:             reconstructedChainedLogsHash == chainedLogsHash,

 246:             reconstructedChainedMessagesHash == chainedMessagesHash,

 270:             reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L106

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol

 54:             ? gasInContext - MSG_VALUE_SIMULATOR_STIPEND_GAS

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L54

```solidity
File: system-contracts/contracts/NonceHolder.sol

 181:         minNonce = _rawMinNonce % DEPLOY_NONCE_MULTIPLIER;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L181

```solidity
File: system-contracts/contracts/SystemContext.sol

 119:         return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;

 403:         currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L403


## [GAS-9] Use calldata instead of memory for function arguments that do not get mutated
Mark data types as `calldata` instead of `memory` where possible. This makes it so that the data is not automatically loaded into memory. If the data passed into the function does not need to be changed (like updating values in an array), it can be passed in as `calldata`. The one exception to this is if the argument must later be passed into another function that takes an argument that specifies `memory` storage.

**Total Instances:** 14

**Gas per instance:** 300
**Total Gas saved:** 4200

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 /// @audit  _log
 164:     function proveL2LogInclusion(
             uint256 _chainId,
             uint256 _batchNumber,
             uint256 _index,
             L2Log memory _log,
             bytes32[] calldata _proof
         ) external view override returns (bool) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L164

```solidity
File: contracts/ethereum/contracts/bridgehub/IBridgehub.sol

 /// @audit  _log
 81:     function proveL2LogInclusion(

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L81

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

 /// @audit  _diamondCut
 11:     constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 /// @audit  _lastCommittedBatchData
 199:     function commitBatches(
             StoredBatchInfo memory _lastCommittedBatchData,
             CommitBatchInfo[] calldata _newBatchesData
         ) external nonReentrant onlyValidator {

 /// @audit  _lastCommittedBatchData
 207:     function commitBatchesSharedBridge(
             uint256, // _chainId
             StoredBatchInfo memory _lastCommittedBatchData,
             CommitBatchInfo[] calldata _newBatchesData
         ) external nonReentrant onlyValidator {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L199

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

 /// @audit  _log
 31:     function proveL2LogInclusion(

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L31

```solidity
File: contracts/zksync/contracts/L2ContractHelper.sol

 /// @audit  _message
 22:     function sendToL1(bytes memory _message) external returns (bytes32);

 /// @audit  _additionalData
 65:     function withdrawWithMessage(address _l1Receiver, bytes memory _additionalData) external payable;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L22

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 /// @audit  _data
 50:     function bridgeInitialize(address _l1Address, bytes memory _data) external initializer {

 /// @audit  _newName, _newSymbol
 111:     function reinitializeToken(
             ERC20Getters calldata _availableGetters,
             string memory _newName,
             string memory _newSymbol,
             uint8 _version
         ) external onlyNextVersion(_version) reinitializer(_version) {

 /// @audit  _input
 178:     function decodeString(bytes memory _input) external pure returns (string memory result) {

 /// @audit  _input
 183:     function decodeUint8(bytes memory _input) external pure returns (uint8 result) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L50

```solidity
File: system-contracts/contracts/L2BaseToken.sol

 /// @audit  _additionalData
 85:     function withdrawWithMessage(address _l1Receiver, bytes memory _additionalData) external payable override {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L85

```solidity
File: system-contracts/contracts/interfaces/IL1Messenger.sol

 /// @audit  _message
 49:     function sendToL1(bytes memory _message) external returns (bytes32);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IL1Messenger.sol#L49


## [GAS-10] Multiple address/ID mappings can be combined into a single mapping of an address/ID to a struct, where appropriate
Saves a storage slot for the mapping. Depending on the circumstances and sizes of types, can avoid a Gsset (20000 gas) per mapping combined. Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Finally, if both fields are accessed in the same function, can save ~42 gas per access due to not having to recalculate the key keccak256 hash (Gkeccak256 - 30 gas) and that calculations associated stack operations.

**Total Instances:** 19

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 32:     mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))

 45:     mapping(address => uint256) private __DEPRECATED_lastWithdrawalLimitReset;

 48:     mapping(address => uint256) private __DEPRECATED_withdrawnAmountInWindow;

 51:     mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L32

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 48:     mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;

 52:     mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))

 57:     mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))

 61:     mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;

 65:     mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L48

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 21:     mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;

 23:     mapping(address _token => bool) public tokenIsRegistered;

 26:     mapping(uint256 _chainId => address) public stateTransitionManager;

 29:     mapping(uint256 _chainId => address) public baseToken;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 30:     mapping(uint256 => address) public stateTransition;

 48:     mapping(uint256 => bytes32) public upgradeCutHash;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L30

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 47:     mapping(uint256 => LibMap.Uint32Map) internal committedBatchTimestamp;

 50:     mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L47

```solidity
File: system-contracts/contracts/NonceHolder.sol

 36:     mapping(uint256 account => uint256 packedMinAndDeploymentNonce) internal rawNonces;

 41:     mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L41


## [GAS-11] Consider activating via-ir for deploying
By using --via-ir or {"viaIR": true}, the compiler is able to use more advanced multi-function optimizations, for extra gas savings.

**Total Instances:** 103

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 19: contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L19

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 30: contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L30

```solidity
File: contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

 11: interface IL1ERC20Bridge {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11

```solidity
File: contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

 12: interface IL1SharedBridge {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L12

```solidity
File: contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol

 6: interface IL2Bridge {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L6

```solidity
File: contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol

 4: interface IWETH9 {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L4

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 16: contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L16

```solidity
File: contracts/ethereum/contracts/bridgehub/IBridgehub.sol

 42: interface IBridgehub {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L42

```solidity
File: contracts/ethereum/contracts/common/ReentrancyGuard.sol

 25: abstract contract ReentrancyGuard {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L25

```solidity
File: contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol

 9: interface IL2ContractDeployer {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L9

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

 10: library L2ContractHelper {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L10

```solidity
File: contracts/ethereum/contracts/common/libraries/UncheckedMath.sol

 10: library UncheckedMath {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L10

```solidity
File: contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol

 18: library UnsafeBytes {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L18

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 20: contract Governance is IGovernance, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L20

```solidity
File: contracts/ethereum/contracts/governance/IGovernance.sol

 8: interface IGovernance {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/IGovernance.sol#L8

```solidity
File: contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

 26: interface IStateTransitionManager {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L26

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 25: contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L25

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 22: contract ValidatorTimelock is IExecutor, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L22

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

 17: contract DiamondInit is ZkSyncStateTransitionBase, IDiamondInit {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L17

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

 10: contract DiamondProxy {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L10

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 18: contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L18

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 22: contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L22

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

 20: contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L20

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

 11: contract ZkSyncStateTransitionBase is ReentrancyGuard {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L11

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol

 13: interface IAdmin is IZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L13

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol

 61: interface IDiamondInit {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L61

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

 73: interface IExecutor is IZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L73

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol

 13: interface IGetters is IZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L13

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol

 11: interface ILegacyGetters is IZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L11

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

 11: interface IMailbox is IZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L11

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol

 15: interface IVerifier {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L15

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol

 15: interface IZkSyncStateTransition is IAdmin, IExecutor, IGetters, IMailbox {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L15

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol

 7: interface IZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L7

```solidity
File: contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol

 4: interface ISystemContext {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L4

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 11: library Diamond {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L11

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

 8: library LibMap {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L8

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

 9: library Merkle {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L9

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

 20: library PriorityQueue {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L20

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

 13: library TransactionValidator {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L13

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 44: abstract contract BaseZkSyncUpgrade is ZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L44

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

 17: abstract contract BaseZkSyncUpgradeGenesis is BaseZkSyncUpgrade {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L17

```solidity
File: contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

 10: contract DefaultUpgrade is BaseZkSyncUpgrade {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L10

```solidity
File: contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

 11: contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L11

```solidity
File: contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol

 7: interface IDefaultUpgrade {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L7

```solidity
File: contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

 21: library AddressAliasHelper {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L21

```solidity
File: contracts/zksync/contracts/ForceDeployUpgrader.sol

 10: contract ForceDeployUpgrader {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L10

```solidity
File: contracts/zksync/contracts/L2ContractHelper.sol

 18: interface IL2Messenger {

 30: interface IContractDeployer {

 61: interface IBaseToken {

 83: library L2ContractHelper {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L18

```solidity
File: contracts/zksync/contracts/SystemContractsCaller.sol

 26: library Utils {

 36: library SystemContractsCaller {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L26

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 23: contract L2SharedBridge is IL2SharedBridge, Initializable {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L23

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 15: contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L15

```solidity
File: contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol

 8: interface IL1ERC20Bridge {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L8

```solidity
File: contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol

 8: interface IL1SharedBridge {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L8

```solidity
File: contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol

 6: interface IL2SharedBridge {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L6

```solidity
File: contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol

 5: interface IL2StandardToken {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L5

```solidity
File: contracts/zksync/contracts/interfaces/IPaymaster.sol

 14: interface IPaymaster {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L14

```solidity
File: contracts/zksync/contracts/interfaces/IPaymasterFlow.sol

 13: interface IPaymasterFlow {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L13

```solidity
File: contracts/zksync/contracts/vendor/AddressAliasHelper.sol

 21: library AddressAliasHelper {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L21

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol

 22: contract AccountCodeStorage is IAccountCodeStorage {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L22

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol

 16: contract BootloaderUtilities is IBootloaderUtilities {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L16

```solidity
File: system-contracts/contracts/ComplexUpgrader.sol

 14: contract ComplexUpgrader is IComplexUpgrader {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L14

```solidity
File: system-contracts/contracts/Compressor.sol

 22: contract Compressor is ICompressor, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L22

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 23: contract ContractDeployer is IContractDeployer, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L23

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 19: contract DefaultAccount is IAccount {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L19

```solidity
File: system-contracts/contracts/EmptyContract.sol

 10: contract EmptyContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/EmptyContract.sol#L10

```solidity
File: system-contracts/contracts/GasBoundCaller.sol

 15: contract GasBoundCaller {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L15

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

 18: contract ImmutableSimulator is IImmutableSimulator {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L18

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

 18: contract KnownCodesStorage is IKnownCodesStorage, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L18

```solidity
File: system-contracts/contracts/L1Messenger.sol

 25: contract L1Messenger is IL1Messenger, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L25

```solidity
File: system-contracts/contracts/L2BaseToken.sol

 18: contract L2BaseToken is IBaseToken, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L18

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol

 19: contract MsgValueSimulator is ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L19

```solidity
File: system-contracts/contracts/NonceHolder.sol

 27: contract NonceHolder is INonceHolder, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L27

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol

 16: contract PubdataChunkPublisher is IPubdataChunkPublisher, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L16

```solidity
File: system-contracts/contracts/SystemContext.sol

 17: contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L17

```solidity
File: system-contracts/contracts/interfaces/IAccount.sol

 9: interface IAccount {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IAccount.sol#L9

```solidity
File: system-contracts/contracts/interfaces/IAccountCodeStorage.sol

 5: interface IAccountCodeStorage {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IAccountCodeStorage.sol#L5

```solidity
File: system-contracts/contracts/interfaces/IBaseToken.sol

 5: interface IBaseToken {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IBaseToken.sol#L5

```solidity
File: system-contracts/contracts/interfaces/IBootloaderUtilities.sol

 7: interface IBootloaderUtilities {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IBootloaderUtilities.sol#L7

```solidity
File: system-contracts/contracts/interfaces/IComplexUpgrader.sol

 10: interface IComplexUpgrader {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IComplexUpgrader.sol#L10

```solidity
File: system-contracts/contracts/interfaces/ICompressor.sol

 18: interface ICompressor {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ICompressor.sol#L18

```solidity
File: system-contracts/contracts/interfaces/IContractDeployer.sol

 5: interface IContractDeployer {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IContractDeployer.sol#L5

```solidity
File: system-contracts/contracts/interfaces/IImmutableSimulator.sol

 10: interface IImmutableSimulator {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IImmutableSimulator.sol#L10

```solidity
File: system-contracts/contracts/interfaces/IKnownCodesStorage.sol

 11: interface IKnownCodesStorage {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IKnownCodesStorage.sol#L11

```solidity
File: system-contracts/contracts/interfaces/IL1Messenger.sol

 40: interface IL1Messenger {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IL1Messenger.sol#L40

```solidity
File: system-contracts/contracts/interfaces/IL2StandardToken.sol

 5: interface IL2StandardToken {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IL2StandardToken.sol#L5

```solidity
File: system-contracts/contracts/interfaces/IMailbox.sol

 5: interface IMailbox {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IMailbox.sol#L5

```solidity
File: system-contracts/contracts/interfaces/INonceHolder.sol

 13: interface INonceHolder {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/INonceHolder.sol#L13

```solidity
File: system-contracts/contracts/interfaces/IPaymaster.sol

 14: interface IPaymaster {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPaymaster.sol#L14

```solidity
File: system-contracts/contracts/interfaces/IPaymasterFlow.sol

 12: interface IPaymasterFlow {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPaymasterFlow.sol#L12

```solidity
File: system-contracts/contracts/interfaces/IPubdataChunkPublisher.sol

 9: interface IPubdataChunkPublisher {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPubdataChunkPublisher.sol#L9

```solidity
File: system-contracts/contracts/interfaces/ISystemContext.sol

 11: interface ISystemContext {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L11

```solidity
File: system-contracts/contracts/interfaces/ISystemContextDeprecated.sol

 10: interface ISystemContextDeprecated {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContextDeprecated.sol#L10

```solidity
File: system-contracts/contracts/interfaces/ISystemContract.sol

 17: abstract contract ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L17

```solidity
File: system-contracts/contracts/libraries/EfficientCall.sol

 32: library EfficientCall {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L32

```solidity
File: system-contracts/contracts/libraries/RLPEncoder.sol

 10: library RLPEncoder {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L10

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol

 41: library SystemContractHelper {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L41

```solidity
File: system-contracts/contracts/libraries/SystemContractsCaller.sol

 68: library SystemContractsCaller {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L68

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 78: library TransactionHelper {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L78

```solidity
File: system-contracts/contracts/libraries/UnsafeBytesCalldata.sol

 18: library UnsafeBytesCalldata {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L18

```solidity
File: system-contracts/contracts/libraries/Utils.sol

 11: library Utils {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L11


## [GAS-12] Consider pre-calculating the address of `address(this)` to save gas
'Use `foundry's` [script.sol](https://book.getfoundry.sh/reference/forge-std/compute-create-address) or `solady's` [LibRlp.sol](https://github.com/Vectorized/solady/blob/main/src/utils/LibRLP.sol) to save the value in a constant, which will avoid having to spend gas to push the value on the stack every time it's used.'

**Total Instances:** 19

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 65:         uint256 amount = IERC20(_token).balanceOf(address(this));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 118:             uint256 balanceBefore = address(this).balance;

 120:             uint256 balanceAfter = address(this).balance;

 127:             uint256 balanceBefore = IERC20(_token).balanceOf(address(this));

 131:             uint256 balanceAfter = IERC20(_token).balanceOf(address(this));

 174:         uint256 balanceBefore = _token.balanceOf(address(this));

 175:         _token.safeTransferFrom(_from, address(this), _amount);

 176:         uint256 balanceAfter = _token.balanceOf(address(this));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L59

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 265:             bytes32(uint256(uint160(address(this)))),

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L265

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 153:             L2ContractHelper.computeCreate2Address(address(this), salt, l2TokenProxyBytecodeHash, constructorInputHash);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L153

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 29:         require(msg.sender == address(this), "Callable only by self");

 333:                 BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo(address(this), _newAddress, value);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L29

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 47:         if (codeAddress != address(this)) {

 100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

 188:         return recoveredAddress == address(this) && recoveredAddress != address(0);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L47

```solidity
File: system-contracts/contracts/L1Messenger.sol

 129:             sender: address(this),

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L129

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol

 60:         require(to != address(this), "MsgValueSimulator calls itself");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L60

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 377:             uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377


## [GAS-13] 'Consider using Solady's `FixedPointMathLib`'
Saves gas, and works to avoid unnecessary [overflows](https://github.com/Vectorized/solady/blob/6cce088e69d6e46671f2f622318102bd5db77a65/src/utils/FixedPointMathLib.sol#L267).

**Total Instances:** 1

```solidity
File: system-contracts/contracts/L1Messenger.sol

 62:         return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L62


## [GAS-14] 'Consider using `solady's` token contracts to save gas'
They're written using heavily-optimized assembly, and will your users a lot of gas

**Total Instances:** 1

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 /// @audit  ERC20PermitUpgradeable, ERC1967Upgrade
 15: contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L15


## [GAS-15] Expressions for constant values such as a call to keccak256(), should use immutable rather than constant
The reason for this is that constant variables are evaluated at runtime and their value is included in the bytecode of the contract. This means that any expensive operations performed as part of the constant expression, such as a call to keccak256(), will be executed every time the contract is deployed, even if the result is always the same. This can result in higher gas costs. In contrast, immutable variables are evaluated at compilation time, and their values are included in the bytecode of the contract as constants. This means that any expensive operations performed as part of the immutable expression are only executed once, when the contract is compiled, and the result is reused every time the contract is deployed. This can result in lower gas costs compared to using constant variables.

**Total Instances:** 82

```solidity
File: contracts/ethereum/contracts/common/Config.sol

 14: uint256 constant MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES = 4 + L2_TO_L1_LOG_SERIALIZE_SIZE * 512;

 22: bytes32 constant DEFAULT_L2_LOGS_TREE_ROOT_HASH = bytes32(0);

 50: uint256 constant MAX_GAS_PER_TRANSACTION = $(MAX_GAS_PER_TRANSACTION);

 54: uint256 constant L1_GAS_PER_PUBDATA_BYTE = $(L1_GAS_PER_PUBDATA_BYTE);

 57: uint256 constant L1_TX_INTRINSIC_L2_GAS = $(L1_TX_INTRINSIC_L2_GAS);

 60: uint256 constant L1_TX_INTRINSIC_PUBDATA = $(L1_TX_INTRINSIC_PUBDATA);

 63: uint256 constant L1_TX_MIN_L2_GAS_BASE = $(L1_TX_MIN_L2_GAS_BASE);

 66: uint256 constant L1_TX_DELTA_544_ENCODING_BYTES = $(L1_TX_DELTA_544_ENCODING_BYTES);

 69: uint256 constant L1_TX_DELTA_FACTORY_DEPS_L2_GAS = $(L1_TX_DELTA_FACTORY_DEPS_L2_GAS);

 72: uint256 constant L1_TX_DELTA_FACTORY_DEPS_PUBDATA = $(L1_TX_DELTA_FACTORY_DEPS_PUBDATA);

 75: uint256 constant MAX_NEW_FACTORY_DEPS = $(MAX_NEW_FACTORY_DEPS);

 78: uint256 constant REQUIRED_L2_GAS_PRICE_PER_PUBDATA = $(REQUIRED_L2_GAS_PRICE_PER_PUBDATA);

 85: address constant POINT_EVALUATION_PRECOMPILE_ADDR = address(0x0A);

 101: address constant ETH_TOKEN_ADDRESS = address(1);

 104: uint256 constant ERA_CHAIN_ID = $(ERA_CHAIN_ID);

 107: address constant ERA_ERC20_BRIDGE_ADDRESS = $(ERA_ERC20_BRIDGE_ADDRESS);

 110: address constant ERA_DIAMOND_PROXY = $(ERA_DIAMOND_PROXY);

 112: bytes32 constant TWO_BRIDGES_MAGIC_VALUE = bytes32(uint256(keccak256("TWO_BRIDGES_MAGIC_VALUE")) - 1);

 115: address constant BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS = address(uint160(type(uint16).max));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L14

```solidity
File: contracts/ethereum/contracts/common/L2ContractAddresses.sol

 6: address constant L2_BOOTLOADER_ADDRESS = address(0x8001);

 9: address constant L2_KNOWN_CODE_STORAGE_SYSTEM_CONTRACT_ADDR = address(0x8004);

 12: address constant L2_DEPLOYER_SYSTEM_CONTRACT_ADDR = address(0x8006);

 21: address constant L2_FORCE_DEPLOYER_ADDR = address(0x8007);

 24: address constant L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR = address(0x8008);

 27: address constant L2_BASE_TOKEN_SYSTEM_CONTRACT_ADDR = address(0x800a);

 30: address constant L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR = address(0x800b);

 33: address constant L2_PUBDATA_CHUNK_PUBLISHER_ADDR = address(0x8011);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/L2ContractAddresses.sol#L6

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

 12:     bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L12

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 22:     uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L22

```solidity
File: contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

 22:     uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L22

```solidity
File: contracts/zksync/contracts/L2ContractHelper.sol

 70: address constant BOOTLOADER_ADDRESS = address(SYSTEM_CONTRACTS_OFFSET + 0x01);

 71: address constant MSG_VALUE_SYSTEM_CONTRACT = address(SYSTEM_CONTRACTS_OFFSET + 0x09);

 72: address constant DEPLOYER_SYSTEM_CONTRACT = address(SYSTEM_CONTRACTS_OFFSET + 0x06);

 74: IL2Messenger constant L2_MESSENGER = IL2Messenger(address(SYSTEM_CONTRACTS_OFFSET + 0x08));

 76: IBaseToken constant L2_BASE_TOKEN_ADDRESS = IBaseToken(address(SYSTEM_CONTRACTS_OFFSET + 0x0a));

 85:     bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L70

```solidity
File: contracts/zksync/contracts/SystemContractsCaller.sol

 7: address constant SYSTEM_CALL_CALL_ADDRESS = address((1 << 16) - 11);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L7

```solidity
File: contracts/zksync/contracts/interfaces/IPaymaster.sol

 12: bytes4 constant PAYMASTER_VALIDATION_SUCCESS_MAGIC = IPaymaster.validateAndPayForPaymasterTransaction.selector;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L12

```solidity
File: contracts/zksync/contracts/vendor/AddressAliasHelper.sol

 22:     uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L22

```solidity
File: system-contracts/contracts/NonceHolder.sol

 28:     uint256 private constant DEPLOY_NONCE_MULTIPLIER = 2 ** 128;

 31:     uint256 private constant MAXIMAL_MIN_NONCE_INCREMENT = 2 ** 32;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L28

```solidity
File: system-contracts/contracts/interfaces/IAccount.sol

 7: bytes4 constant ACCOUNT_VALIDATION_SUCCESS_MAGIC = IAccount.validateTransaction.selector;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IAccount.sol#L7

```solidity
File: system-contracts/contracts/interfaces/IPaymaster.sol

 12: bytes4 constant PAYMASTER_VALIDATION_SUCCESS_MAGIC = IPaymaster.validateAndPayForPaymasterTransaction.selector;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPaymaster.sol#L12

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol

 9: uint256 constant UINT32_MASK = type(uint32).max;

 10: uint256 constant UINT64_MASK = type(uint64).max;

 11: uint256 constant UINT128_MASK = type(uint128).max;

 12: uint256 constant ADDRESS_MASK = type(uint160).max;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L9

```solidity
File: system-contracts/contracts/libraries/SystemContractsCaller.sol

 12: address constant TO_L1_CALL_ADDRESS = address((1 << 16) - 1);

 13: address constant CODE_ADDRESS_CALL_ADDRESS = address((1 << 16) - 2);

 14: address constant PRECOMPILE_CALL_ADDRESS = address((1 << 16) - 3);

 15: address constant META_CALL_ADDRESS = address((1 << 16) - 4);

 16: address constant MIMIC_CALL_CALL_ADDRESS = address((1 << 16) - 5);

 17: address constant SYSTEM_MIMIC_CALL_CALL_ADDRESS = address((1 << 16) - 6);

 18: address constant MIMIC_CALL_BY_REF_CALL_ADDRESS = address((1 << 16) - 7);

 19: address constant SYSTEM_MIMIC_CALL_BY_REF_CALL_ADDRESS = address((1 << 16) - 8);

 20: address constant RAW_FAR_CALL_CALL_ADDRESS = address((1 << 16) - 9);

 21: address constant RAW_FAR_CALL_BY_REF_CALL_ADDRESS = address((1 << 16) - 10);

 22: address constant SYSTEM_CALL_CALL_ADDRESS = address((1 << 16) - 11);

 23: address constant SYSTEM_CALL_BY_REF_CALL_ADDRESS = address((1 << 16) - 12);

 24: address constant SET_CONTEXT_VALUE_CALL_ADDRESS = address((1 << 16) - 13);

 25: address constant SET_PUBDATA_PRICE_CALL_ADDRESS = address((1 << 16) - 14);

 26: address constant INCREMENT_TX_COUNTER_CALL_ADDRESS = address((1 << 16) - 15);

 27: address constant PTR_CALLDATA_CALL_ADDRESS = address((1 << 16) - 16);

 28: address constant CALLFLAGS_CALL_ADDRESS = address((1 << 16) - 17);

 29: address constant PTR_RETURNDATA_CALL_ADDRESS = address((1 << 16) - 18);

 30: address constant EVENT_INITIALIZE_ADDRESS = address((1 << 16) - 19);

 31: address constant EVENT_WRITE_ADDRESS = address((1 << 16) - 20);

 32: address constant LOAD_CALLDATA_INTO_ACTIVE_PTR_CALL_ADDRESS = address((1 << 16) - 21);

 33: address constant LOAD_LATEST_RETURNDATA_INTO_ACTIVE_PTR_CALL_ADDRESS = address((1 << 16) - 22);

 34: address constant PTR_ADD_INTO_ACTIVE_CALL_ADDRESS = address((1 << 16) - 23);

 35: address constant PTR_SHRINK_INTO_ACTIVE_CALL_ADDRESS = address((1 << 16) - 24);

 36: address constant PTR_PACK_INTO_ACTIVE_CALL_ADDRESS = address((1 << 16) - 25);

 37: address constant MULTIPLICATION_HIGH_ADDRESS = address((1 << 16) - 26);

 38: address constant GET_EXTRA_ABI_DATA_ADDRESS = address((1 << 16) - 27);

 41: uint256 constant META_GAS_PER_PUBDATA_BYTE_OFFSET = 0 * 8;

 42: uint256 constant META_HEAP_SIZE_OFFSET = 8 * 8;

 43: uint256 constant META_AUX_HEAP_SIZE_OFFSET = 12 * 8;

 44: uint256 constant META_SHARD_ID_OFFSET = 28 * 8;

 45: uint256 constant META_CALLER_SHARD_ID_OFFSET = 29 * 8;

 46: uint256 constant META_CODE_SHARD_ID_OFFSET = 30 * 8;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L12

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 82:     bytes32 constant EIP712_DOMAIN_TYPEHASH = keccak256("EIP712Domain(string name,string version,uint256 chainId)");

 84:     bytes32 constant EIP712_TRANSACTION_TYPE_HASH =

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L84


## [GAS-16] Constructors can be marked as payable to save deployment gas
Payable functions cost less gas to execute, because the compiler does not have to add extra checks to ensure that no payment is provided. A constructor can be safely marked as payable, because only the deployer would be able to pass funds, and the project itself would not pass any funds.

**Total Instances:** 10

**Gas per instance:** 21
**Total Gas saved:** 210

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 55:     constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 90:     constructor(

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 38:     constructor() reentrancyGuardInitializer {}

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 41:     constructor(address _admin, address _securityCouncil, uint256 _minDelay) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L41

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 58:     constructor(address _bridgehub) reentrancyGuardInitializer {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 55:     constructor(address _initialOwner, uint32 _executionDelay) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

 19:     constructor() reentrancyGuardInitializer {}

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

 11:     constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 41:     constructor() {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L41

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 40:     constructor() {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L40


## [GAS-17] Counting down when iterating, saves gas
Counting down saves 6 gas per loop, since checks for zero are more efficient than checks against any other value

**Total Instances:** 3

**Gas per instance:** 12
**Total Gas saved:** 36

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

 667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol

 36:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36



## [GAS-18] Division by powers of two should use bit shifting
<x> / 2 is the same as <x> >> 1. While the compiler uses the SHR opcode to accomplish both, the version that uses division incurs an overhead of 20 gas due to JUMPs to and from a compiler utility function that introduces checks which can be avoided by using unchecked {} around the division by two.

**Total Instances:** 6

**Gas per instance:** 20
**Total Gas saved:** 120

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

 25:         uint256 bytecodeLenInWords = _bytecode.length / 32;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

 23:             uint256 mapValue = _map.map[_index / 8];

 43:             uint256 mapIndex = _index / 8;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L23

```solidity
File: system-contracts/contracts/Compressor.sol

 57:                 dictionary.length / 8 <= encodedData.length / 2,

 57:                 dictionary.length / 8 <= encodedData.length / 2,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L57

```solidity
File: system-contracts/contracts/libraries/Utils.sol

 86:         uint256 lengthInWords = _bytecode.length / 32;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L86


## [GAS-19] Emitting constants wastes gas
'Every event parameter costs `Glogdata` (8 gas) per byte. You can avoid this extra cost, in cases where you're emitting a constant, by creating a second version of the event, which doesn't have the parameter (and have users look to the contract's variables for its value instead), and using the new event in the cases shown below.'

**Total Instances:** 1

**Gas per instance:** 8
**Total Gas saved:** 8

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 /// @audit  0
 50:         emit ChangeMinDelay(0, _minDelay);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L50


## [GAS-20] `""` has the same value as `new bytes(0)` but costs less gas
Optimize gas costs by using an empty string ("") instead of new bytes(0) for the same value.

**Total Instances:** 5

**Gas per instance:** 259
**Total Gas saved:** 1295

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 196:             signature: new bytes(0),

 198:             paymasterInput: new bytes(0),

 199:             reservedDynamic: new bytes(0)

 213:             l1ContractsUpgradeCalldata: new bytes(0),

 214:             postUpgradeCalldata: new bytes(0),

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L214


## [GAS-21] Empty blocks should be removed or emit something
 Removing empty blocks help conserve computational resources on the blockchain network, reducing transaction costs and improving overall efficiency.

**Total Instances:** 6

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 60:     function initialize() external reentrancyGuardInitializer {}

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L60

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 262:     receive() external payable {}

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L262

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 125:     function executeTransactionFromOutside(Transaction calldata _transaction) external payable override {

 227:     receive() external payable {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L125

```solidity
File: system-contracts/contracts/EmptyContract.sol

 11:     fallback() external payable {}

 13:     receive() external payable {}

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/EmptyContract.sol#L13


## [GAS-22] Events should be emitted outside of loops
Emitting an event has an overhead of 375 gas, which will be incurred on every iteration of the loop. It is cheaper to emit only once after the loop has finished.

**Total Instances:** 3

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 261:             emit BlockCommit(

 299:             emit BlockCommit(

 353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353


## [GAS-23] >= costs less gas than >
The compiler uses opcodes GT and ISZERO for solidity code that uses `>`, but only requires LT for `>=`, which saves 3 gas. If `<` is being used, the condition can be inverted. In cases where a for-loop is being used, one can count down rather than up, in order to use the optimal operator

**Total Instances:** 94

**Gas per instance:** 3
**Total Gas saved:** 282

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 121:             require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");

 129:             require(amount > 0, "ShB: 0 amount to transfer");

 327:         require(_amount > 0, "y1");

 375:         return (_chainId == ERA_CHAIN_ID) && (_l2BatchNumber < eraFirstPostUpgradeBatch);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L121

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 301:             _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,

 329:         } else if (_refundRecipient.code.length > 0) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L301

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

 26:         require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L26

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 111:         } else if (timestamp > block.timestamp) {

 225:         for (uint256 i = 0; i < _calls.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L111

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 116:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

 135:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

 185:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

 209:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 117:             s.protocolVersion > _oldProtocolVersion,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L117

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 114:         require(_previousBatchTimestamp < batchTimestamp, "h3");

 142:         for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

 257:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

 289:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

 311:         for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {

 351:         for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {

 405:         for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {

 429:         if (_proof.serializedProof.length > 0) {

 482:         require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch

 485:         if (_newLastBatch < s.totalBatchesVerified) {

 492:         if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) {

 580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

 593:         return (_bitMap & (1 << _index)) > 0;

 631:         require(_pubdataCommitments.length > 0, "pl");

 636:         for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {

 667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L114

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

 208:         for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 101:         for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {

 107:             require(selectors.length > 0, "B"); // no functions for diamond cut

 132:         require(_facet.code.length > 0, "G");

 138:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

 155:         require(_facet.code.length > 0, "K");

 158:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

 178:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

 24:         require(pathLength > 0, "xc");

 25:         require(pathLength < 256, "bt");

 26:         require(_index < (1 << pathLength), "px");

 29:         for (uint256 i; i < pathLength; i = i.uncheckedInc()) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {

 239:             _newProtocolVersion > previousProtocolVersion,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 124:         require(_amount > 0, "Amount cannot be zero");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L124

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol

 102:         if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) {

 132:             uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS &&

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L102

```solidity
File: system-contracts/contracts/ComplexUpgrader.sol

 24:         require(_delegateTo.code.length > 0, "Delegatee is an EOA");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L24

```solidity
File: system-contracts/contracts/Compressor.sol

 61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {

 63:                 require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

 127:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

 159:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L61

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 48:             _address > address(MAX_SYSTEM_CONTRACT_ADDRESS) &&

 248:         for (uint256 i = 0; i < deploymentsLength; ++i) {

 253:         for (uint256 i = 0; i < deploymentsLength; ++i) {

 265:         require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

 303:         require(knownCodeMarker > 0, "The code hash is not known");

 332:             if (value > 0) {

 339:             if (value > 0) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L48

```solidity
File: system-contracts/contracts/GasBoundCaller.sol

 49:         uint256 pubdataAllowance = _maxTotalGas > expectedForCompute ? _maxTotalGas - expectedForCompute : 0;

 63:         uint256 pubdataSpent = pubdataPublishedAfter > pubdataPublishedBefore

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L49

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

 38:             for (uint256 i = 0; i < immutablesLength; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L38

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

 30:             for (uint256 i = 0; i < hashesLen; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L30

```solidity
File: system-contracts/contracts/L1Messenger.sol

 206:         for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

 218:         for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

 222:         while (nodesOnCurrentLevel > 1) {

 224:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

 236:         for (uint256 i = 0; i < numberOfMessages; ++i) {

 254:         for (uint256 i = 0; i < numberOfBytecodes; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L206

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol

 53:         uint256 userGas = gasInContext > MSG_VALUE_SIMULATOR_STIPEND_GAS

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L53

```solidity
File: system-contracts/contracts/NonceHolder.sol

 156:         return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);

 156:         return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L156

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol

 36:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36

```solidity
File: system-contracts/contracts/SystemContext.sol

 119:         return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;

 144:         if (blockNumber <= _block || blockNumber - _block > 256) {

 146:         } else if (_block < currentVirtualBlockUpgradeInfo.virtualBlockStartBatch) {

 152:             currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0

 245:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

 287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

 355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

 387:                 _l2BlockTimestamp > currentL2BlockTimestamp,

 413:         require(currentBatchNumber > 0, "The current batch number must be greater than 0");

 430:             _newTimestamp > currentBlockTimestamp,

 451:         require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L119

```solidity
File: system-contracts/contracts/libraries/RLPEncoder.sol

 26:             if (_val < 128) {

 62:             if (_len < 56) {

 86:             if (_number > type(uint128).max) {

 90:             if (_number > type(uint64).max) {

 94:             if (_number > type(uint32).max) {

 98:             if (_number > type(uint16).max) {

 102:             if (_number > type(uint8).max) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L26

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol

 319:         require(index < 10, "There are only 10 accessible registers");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 378:             if (currentAllowance < minAllowance) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L378

```solidity
File: system-contracts/contracts/libraries/Utils.sol

 87:         require(lengthInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L87


## [GAS-24] keccak256() hash of literals should only be computed once
The result of the hash should be stored in an immutable variable, and the variable should be used instead. If the hash is being used as a part of a function selector, the cast to bytes4 should also only be done once. 

**Total Instances:** 8

**Gas per instance:** 42
**Total Gas saved:** 336

```solidity
File: contracts/ethereum/contracts/common/Config.sol

 112: bytes32 constant TWO_BRIDGES_MAGIC_VALUE = bytes32(uint256(keccak256("TWO_BRIDGES_MAGIC_VALUE")) - 1);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L112

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

 12:     bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L12

```solidity
File: contracts/zksync/contracts/L2ContractHelper.sol

 85:     bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L85

```solidity
File: system-contracts/contracts/L1Messenger.sol

 89:         uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) + 2 * keccakGasCost(64);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L89

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 82:     bytes32 constant EIP712_DOMAIN_TYPEHASH = keccak256("EIP712Domain(string name,string version,uint256 chainId)");

 85:         keccak256(

 139:             abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

 139:             abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139


## [GAS-25] Initializers can be marked as payable to save deployment gas
Payable functions cost less gas to execute, because the compiler does not have to add extra checks to ensure that no payment is provided. Initializers can be safely marked as payable, because only the deployer or the factory contract would call the function without carrying any funds.

**Total Instances:** 2

**Gas per instance:** 21
**Total Gas saved:** 42

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 104:     function initialize(
             address _owner,
             uint256 _eraFirstPostUpgradeBatch
         ) external reentrancyGuardInitializer initializer {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L104

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 50:     function bridgeInitialize(address _l1Address, bytes memory _data) external initializer {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L50


## [GAS-26] internal functions only called once can be inlined to save gas
If an internal function is only used once, there is no need to modularize it, unless the function calling it would otherwise be too long and complex. Not inlining costs 20 to 40 gas because of two extra JUMP instructions and additional stack operations needed for function calls.

**Total Instances:** 76

**Gas per instance:** 20
**Total Gas saved:** 1520

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 160:     function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 254:     function _getERC20Getters(address _token) internal view returns (bytes memory) {

 458:     function _checkWithdrawal(
             uint256 _chainId,
             MessageParams memory _messageParams,
             bytes calldata _message,
             bytes32[] calldata _merkleProof
         ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {

 487:     function _parseL2WithdrawalMessage(
             uint256 _chainId,
             bytes memory _l2ToL1message
         ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L254

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

 49:     function bytecodeLen(bytes32 _bytecodeHash) internal pure returns (uint256 codeLengthInWords) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L49

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 177:     function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 103:     function _verifyBatchTimestamp(
             uint256 _packedBatchAndL2BlockTimestamp,
             uint256 _expectedBatchTimestamp,
             uint256 _previousBatchTimestamp
         ) internal view {

 130:     function _processL2Logs(
             CommitBatchInfo calldata _newBatch,
             bytes32 _expectedSystemContractUpgradeTxHash
         ) internal pure returns (LogProcessingOutput memory logOutput) {

 253:     function _commitBatchesWithoutSystemContractsUpgrade(
             StoredBatchInfo memory _lastCommittedBatchData,
             CommitBatchInfo[] calldata _newBatchesData
         ) internal {

 273:     function _commitBatchesWithSystemContractsUpgrade(
             StoredBatchInfo memory _lastCommittedBatchData,
             CommitBatchInfo[] calldata _newBatchesData,
             bytes32 _systemContractUpgradeTxHash
         ) internal {

 308:     function _collectOperationsFromPriorityQueue(uint256 _nPriorityOps) internal returns (bytes32 concatHash) {

 321:     function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {

 453:     function _getBatchProofPublicInput(
             bytes32 _prevBatchCommitment,
             bytes32 _currentBatchCommitment,
             VerifierParams memory _verifierParams
         ) internal pure returns (uint256) {

 500:     function _createBatchCommitment(
             CommitBatchInfo calldata _newBatchData,
             bytes32 _stateDiffHash,
             bytes32[] memory _blobCommitments,
             bytes32[] memory _blobHashes
         ) internal view returns (bytes32) {

 515:     function _batchPassThroughData(CommitBatchInfo calldata _batch) internal pure returns (bytes memory) {

 525:     function _batchMetaParameters() internal view returns (bytes memory) {

 537:     function _batchAuxiliaryOutput(
             CommitBatchInfo calldata _batch,
             bytes32 _stateDiffHash,
             bytes32[] memory _blobCommitments,
             bytes32[] memory _blobHashes
         ) internal pure returns (bytes memory) {

 561:     function _encodeBlobAuxilaryOutput(
             bytes32[] memory _blobCommitments,
             bytes32[] memory _blobHashes
         ) internal pure returns (bytes32[] memory blobAuxOutputWords) {

 592:     function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

 597:     function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {

 605:     function _pointEvaluationPrecompile(
             bytes32 _versionedHash,
             bytes32 _openingPoint,
             bytes calldata _openingValueCommitmentProof
         ) internal view {

 625:     function _verifyBlobInformation(
             bytes calldata _pubdataCommitments,
             bytes32[] memory _blobHashes
         ) internal view returns (bytes32[] memory blobCommitments) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L103

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

 69:     function getMinimalPriorityTransactionGasLimit(
            uint256 _encodingLength,
            uint256 _numberOfFactoryDependencies,
            uint256 _l2GasPricePerPubdata
        ) internal pure returns (uint256) {

 109:     function getTransactionBodyGasLimit(
             uint256 _totalGasLimit,
             uint256 _encodingLength
         ) internal pure returns (uint256 txBodyGasLimit) {

 128:     function getOverheadForTransaction(
             uint256 _encodingLength
         ) internal pure returns (uint256 batchOverheadForTransaction) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L69

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 163:     function _upgradeVerifier(address _newVerifier, VerifierParams calldata _verifierParams) internal {

 171:     function _setBaseSystemContracts(bytes32 _bootloaderHash, bytes32 _defaultAccountHash) internal {

 180:     function _setL2SystemContractUpgrade(
             L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
             bytes[] calldata _factoryDeps,
             uint256 _newProtocolVersion
         ) internal returns (bytes32) {

 236:     function _setNewProtocolVersion(uint256 _newProtocolVersion) internal virtual {

 263:     function _upgradeL1Contract(bytes calldata _customCallDataForUpgrade) internal virtual {}

 269:     function _postUpgrade(bytes calldata _customCallDataForUpgrade) internal virtual {}

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L163

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

 20:     function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20

```solidity
File: contracts/zksync/contracts/SystemContractsCaller.sol

 37:     function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

 95:     function getFarCallABI(
            uint32 dataOffset,
            uint32 memoryPage,
            uint32 dataStart,
            uint32 dataLength,
            uint32 gasPassed,
            uint8 shardId,
            CalldataForwardingMode forwardingMode,
            bool isConstructorCall,
            bool isSystemCall
        ) internal pure returns (uint256 farCallAbi) {

 121:     function getFarCallABIWithEmptyFatPointer(
             uint32 gasPassed,
             uint8 shardId,
             CalldataForwardingMode forwardingMode,
             bool isConstructorCall,
             bool isSystemCall
         ) internal pure returns (uint256 farCallAbiWithEmptyFatPtr) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L37

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 109:     function _deployL2Token(address _l1Token, bytes calldata _data) internal returns (address) {

 138:     function _getL1WithdrawMessage(
             address _to,
             address _l1Token,
             uint256 _amount
         ) internal pure returns (bytes memory) {

 164:     function _deployBeaconProxy(bytes32 salt) internal returns (BeaconProxy proxy) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L109

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol

 44:     function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {

 139:     function encodeEIP2930TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {

 229:     function encodeEIP1559TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L44

```solidity
File: system-contracts/contracts/Compressor.sol

 197:     function _decodeRawBytecode(
             bytes calldata _rawCompressedData
         ) internal pure returns (bytes calldata dictionary, bytes calldata encodedData) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L197

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 283:     function _performDeployOnAddress(
             bytes32 _bytecodeHash,
             address _newAddress,
             AccountAbstractionVersion _aaVersion,
             bytes calldata _input
         ) internal {

 309:     function _storeConstructingByteCodeHashOnAddress(address _newAddress, bytes32 _bytecodeHash) internal {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L283

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 78:     function _validateTransaction(
            bytes32 _suggestedSignedHash,
            Transaction calldata _transaction
        ) internal returns (bytes4 magic) {

 131:     function _execute(Transaction calldata _transaction) internal {

 159:     function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L78

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

 74:     function _validateBytecode(bytes32 _bytecodeHash) internal pure {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L74

```solidity
File: system-contracts/contracts/L1Messenger.sol

 61:     function sha256GasCost(uint256 _length) internal pure returns (uint256) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L61

```solidity
File: system-contracts/contracts/L2BaseToken.sol

 112:     function _getL1WithdrawMessage(address _to, uint256 _amount) internal pure returns (bytes memory) {

 117:     function _getExtendedWithdrawMessage(
             address _to,
             uint256 _amount,
             address _sender,
             bytes memory _additionalData
         ) internal pure returns (bytes memory) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L112

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol

 25:     function _getAbiParams() internal view returns (uint256 value, bool isSystemCall, address to) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L25

```solidity
File: system-contracts/contracts/SystemContext.sol

 221:     function _calculateL2BlockHash(
             uint128 _blockNumber,
             uint128 _blockTimestamp,
             bytes32 _prevL2BlockHash,
             bytes32 _blockTxsRollingHash
         ) internal pure returns (bytes32) {

 233:     function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {

 241:     function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {

 263:     function _setVirtualBlock(
             uint128 _l2BlockNumber,
             uint128 _maxVirtualBlocksToCreate,
             uint128 _newTimestamp
         ) internal {

 427:     function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L221

```solidity
File: system-contracts/contracts/libraries/EfficientCall.sol

 124:     function rawCall(
             uint256 _gas,
             address _address,
             uint256 _value,
             bytes calldata _data,
             bool _isSystem
         ) internal returns (bool success) {

 159:     function rawStaticCall(uint256 _gas, address _address, bytes calldata _data) internal view returns (bool success) {

 173:     function rawDelegateCall(uint256 _gas, address _address, bytes calldata _data) internal returns (bool success) {

 191:     function rawMimicCall(
             uint256 _gas,
             address _address,
             bytes calldata _data,
             address _whoToMimic,
             bool _isConstructor,
             bool _isSystem
         ) internal returns (bool success) {

 232:     function propagateRevert() internal pure {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L124

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol

 148:     function unsafePrecompileCall(
             uint256 _rawParams,
             uint32 _gasToBurn,
             uint32 _pubdataToSpend
         ) internal view returns (bool success) {

 203:     function getZkSyncMetaBytes() internal view returns (uint256 meta) {

 227:     function getPubdataPublishedFromMeta(uint256 meta) internal pure returns (uint32 pubdataPublished) {

 237:     function getHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 heapSize) {

 246:     function getAuxHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 auxHeapSize) {

 254:     function getShardIdFromMeta(uint256 meta) internal pure returns (uint8 shardId) {

 263:     function getCallerShardIdFromMeta(uint256 meta) internal pure returns (uint8 callerShardId) {

 272:     function getCodeShardIdFromMeta(uint256 meta) internal pure returns (uint8 codeShardId) {

 296:     function getCallFlags() internal view returns (uint256 callFlags) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L148

```solidity
File: system-contracts/contracts/libraries/SystemContractsCaller.sol

 76:     function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

 123:     function systemCallWithReturndata(
             uint32 gasLimit,
             address to,
             uint128 value,
             bytes memory data
         ) internal returns (bool success, bytes memory returnData) {

 250:     function getFarCallABIWithEmptyFatPointer(
             uint32 gasPassed,
             uint8 shardId,
             CalldataForwardingMode forwardingMode,
             bool isConstructorCall,
             bool isSystemCall
         ) internal pure returns (uint256 farCallAbiWithEmptyFatPtr) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L76

```solidity
File: system-contracts/contracts/libraries/Utils.sol

 44:     function bytecodeLenInWords(bytes32 _bytecodeHash) internal pure returns (uint256 codeLengthInWords) {

 71:     function constructedBytecodeHash(bytes32 _bytecodeHash) internal pure returns (bytes32) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L71


## [GAS-27] A modifier used only once and not being inherited should be inlined to save gas
When you use a modifier in Solidity, Solidity generates code to check the conditions of the modifier and execute the modified function if the conditions are met. This generated code can consume gas, especially if the modifier is used frequently or if the modified function is called multiple times. By inlining a modifier that is used only once and not being inherited, you can eliminate the overhead of the generated code and reduce the gas cost of your contract.

**Total Instances:** 7

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 74:     modifier onlyBridgehubOrEra(uint256 _chainId) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L74

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 64:     modifier onlySecurityCouncil() {

 70:     modifier onlyOwnerOrSecurityCouncil() {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L64

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 63:     modifier onlyBridgehub() {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L63

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 134:     modifier onlyNextVersion(uint8 _version) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L134

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 28:     modifier onlySelf() {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L28

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

 19:     modifier onlyCompressor() {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L19


## [GAS-28] Private functions only used once can be inlined to save gas
If a private function is only used once, there is no need to modularize it, unless the function calling it would otherwise be too long and complex.

**Total Instances:** 15

**Gas per instance:** 30
**Total Gas saved:** 450

```solidity
File: contracts/ethereum/contracts/common/ReentrancyGuard.sol

 46:     function _initializeReentrancyGuard() private {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L46

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 126:     function _addFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {

 149:     function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {

 172:     function _removeFunctions(address _facet, bytes4[] memory _selectors) private {

 257:     function _removeFacet(address _facet) private {

 278:     function _initializeDiamondCut(address _init, bytes memory _calldata) private {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L126

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 92:     function _setL2DefaultAccountBytecodeHash(bytes32 _l2DefaultAccountBytecodeHash) private {

 109:     function _setL2BootloaderBytecodeHash(bytes32 _l2BootloaderBytecodeHash) private {

 126:     function _setVerifier(IVerifier _newVerifier) private {

 142:     function _setVerifierParams(VerifierParams calldata _newVerifierParams) private {

 222:     function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L92

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 118:     function _encodeHashEIP712Transaction(Transaction calldata _transaction) private view returns (bytes32) {

 147:     function _encodeHashLegacyTransaction(Transaction calldata _transaction) private view returns (bytes32) {

 219:     function _encodeHashEIP2930Transaction(Transaction calldata _transaction) private view returns (bytes32) {

 289:     function _encodeHashEIP1559Transaction(Transaction calldata _transaction) private view returns (bytes32) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L289


## [GAS-29] Usage of ints/uints smaller than 32 bytes incurs overhead
Using ints/uints smaller than 32 bytes may cost more gas. This is because the EVM operates on 32 bytes at a time, so if an element is smaller than 32 bytes, the EVM must perform more operations to reduce the size of the element from 32 bytes to the desired size.

**Total Instances:** 256

**Gas per instance:** 55
**Total Gas saved:** 14080

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 182:         uint16 _l2TxNumberInBatch,

 211:         uint16 _l2TxNumberInBatch,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L182

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 285:         uint16 _l2TxNumberInBatch,

 312:         uint16 _l2TxNumberInBatch,

 389:         uint16 _l2TxNumberInBatch,

 404:         uint16 l2TxNumberInBatch;

 413:         uint16 _l2TxNumberInBatch,

 503:         (uint32 functionSignature, uint256 offset) = UnsafeBytes.readUint32(_l2ToL1message, 0);

 618:         uint16 _l2TxNumberInBatch,

 651:         uint16 _l2TxNumberInBatch,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L285

```solidity
File: contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

 49:         uint16 _l2TxNumberInBatch,

 56:         uint16 _l2TxNumberInBatch,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L49

```solidity
File: contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

 81:         uint16 _l2TxNumberInBatch,

 93:         uint16 _l2TxNumberInBatch,

 100:         uint16 _l2TxNumberInBatch,

 109:         uint16 _l2TxNumberInBatch,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L81

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 123:         require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");

 181:         uint16 _l2TxNumberInBatch,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123

```solidity
File: contracts/ethereum/contracts/bridgehub/IBridgehub.sol

 94:         uint16 _l2TxNumberInBatch,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L94

```solidity
File: contracts/ethereum/contracts/common/Config.sol

 115: address constant BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS = address(uint160(type(uint16).max));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L115

```solidity
File: contracts/ethereum/contracts/common/Messaging.sol

 24:     uint8 l2ShardId;

 26:     uint16 txNumberInBatch;

 38:     uint16 txNumberInBatch;

 60:     uint64 expirationTimestamp;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L24

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

 40:         uint8 version = uint8(_bytecodeHash[0]);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L40

```solidity
File: contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol

 19:     function readUint32(bytes memory _bytes, uint256 _start) internal pure returns (uint32 result, uint256 offset) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L19

```solidity
File: contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

 20:     uint64 genesisIndexRepeatedStorageChanges;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L20

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 53:     uint32 public executionDelay;

 55:     constructor(address _initialOwner, uint32 _executionDelay) {

 96:     function setExecutionDelay(uint32 _executionDelay) external onlyOwner {

 115:             uint32 timestamp = uint32(block.timestamp);

 134:             uint32 timestamp = uint32(block.timestamp);

 183:         uint256 delay = executionDelay; // uint32

 207:         uint256 delay = executionDelay; // uint32

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L53

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

 32:     uint40 proposedUpgradeTimestamp;

 33:     uint40 currentProposalId;

 54:     uint32 batchOverheadL1Gas;

 55:     uint32 maxPubdataPerBatch;

 56:     uint32 maxL2GasPerBatch;

 57:     uint32 priorityTxMaxPubdata;

 58:     uint64 minimalL2GasPrice;

 151:     uint128 baseTokenGasPriceMultiplierNominator;

 152:     uint128 baseTokenGasPriceMultiplierDenominator;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L32

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 79:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {

 79:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {

 80:         uint128 oldNominator = s.baseTokenGasPriceMultiplierNominator;

 81:         uint128 oldDenominator = s.baseTokenGasPriceMultiplierDenominator;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 39:         uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));

 592:     function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {

 597:     function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L39

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

 67:     function baseTokenGasPriceMultiplierNominator() external view returns (uint128) {

 72:     function baseTokenGasPriceMultiplierDenominator() external view returns (uint128) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L67

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol

 40:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external;

 40:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external;

 84:         uint128 oldNominator,

 85:         uint128 oldDenominator,

 86:         uint128 newNominator,

 87:         uint128 newDenominator

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L40

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

 84:         uint64 batchNumber;

 86:         uint64 indexRepeatedStorageChanges;

 113:         uint64 batchNumber;

 114:         uint64 timestamp;

 115:         uint64 indexRepeatedStorageChanges;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L84

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol

 112:     function baseTokenGasPriceMultiplierNominator() external view returns (uint128);

 115:     function baseTokenGasPriceMultiplierDenominator() external view returns (uint128);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L112

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

 51:         uint16 _l2TxNumberInBatch,

 65:         uint16 _l2TxNumberInBatch,

 126:         uint64 expirationTimestamp,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L51

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 32:         uint16 selectorPosition;

 41:         uint16 facetPosition;

 208:         uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16();

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L32

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

 18:     function get(Uint32Map storage _map, uint256 _index) internal view returns (uint32 result) {

 38:     function set(Uint32Map storage _map, uint256 _index, uint32 _value) internal {

 54:             uint32 oldValue = uint32(mapValue >> bitOffset);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L18

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

 12:     uint64 expirationTimestamp;

 13:     uint192 layer2Tip;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L12

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

 48:         require(_transaction.from <= type(uint16).max, "ua");

 49:         require(_transaction.to <= type(uint160).max, "ub");

 55:         require(_transaction.reserved[1] <= type(uint160).max, "uf");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L48

```solidity
File: contracts/ethereum/contracts/vendor/AddressAliasHelper.sol

 22:     uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/vendor/AddressAliasHelper.sol#L22

```solidity
File: contracts/zksync/contracts/L2ContractHelper.sol

 68: uint160 constant SYSTEM_CONTRACTS_OFFSET = 0x8000; // 2^15

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L68

```solidity
File: contracts/zksync/contracts/SystemContractsCaller.sol

 27:     function safeCastToU32(uint256 _x) internal pure returns (uint32) {

 28:         require(_x <= type(uint32).max, "Overflow");

 37:     function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

 40:         uint32 dataStart;

 44:         uint32 dataLength = uint32(Utils.safeCastToU32(data.length));

 77:         uint32 gasLimit,

 79:         uint128 value,

 96:         uint32 dataOffset,

 97:         uint32 memoryPage,

 98:         uint32 dataStart,

 99:         uint32 dataLength,

 100:         uint32 gasPassed,

 101:         uint8 shardId,

 122:         uint32 gasPassed,

 123:         uint8 shardId,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L27

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 31:     uint8 private decimals_;

 93:         try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {

 115:         uint8 _version

 134:     modifier onlyNextVersion(uint8 _version) {

 171:     function decimals() public view override returns (uint8) {

 183:     function decodeUint8(bytes memory _input) external pure returns (uint8 result) {

 184:         (result) = abi.decode(_input, (uint8));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L31

```solidity
File: contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol

 12:         uint16 _l2TxNumberInBatch,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L12

```solidity
File: contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol

 13:         uint16 _l2TxNumberInBatch,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L13

```solidity
File: contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol

 6:     event BridgeInitialize(address indexed l1Token, string name, string symbol, uint8 decimals);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L6

```solidity
File: contracts/zksync/contracts/vendor/AddressAliasHelper.sol

 22:     uint160 constant offset = uint160(0x1111000000000000000000000000000000001111);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/vendor/AddressAliasHelper.sol#L22

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol

 68:             uint64 txDataLen = uint64(_transaction.data.length);

 164:             uint64 txDataLen = uint64(_transaction.data.length);

 259:             uint64 txDataLen = uint64(_transaction.data.length);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L68

```solidity
File: system-contracts/contracts/Compressor.sol

 65:                 uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);

 66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);

 129:             uint64 enumIndex = stateDiff.readUint64(84);

 143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

 145:             uint8 operation = metadata & OPERATION_BITMASK;

 146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

 161:             uint64 enumIndex = stateDiff.readUint64(84);

 174:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

 176:             uint8 operation = metadata & OPERATION_BITMASK;

 177:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L65

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 133:         uint128 value = Utils.safeCastToU128(_transaction.value);

 135:         uint32 gas = Utils.safeCastToU32(gasleft());

 161:         uint8 v;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L133

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

 75:         uint8 version = uint8(_bytecodeHash[0]);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L75

```solidity
File: system-contracts/contracts/L1Messenger.sol

 200:         uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

 233:         uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

 237:             uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

 251:         uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

 255:             uint32 currentBytecodeLength = uint32(

 286:         uint24 compressedStateDiffSize = uint24(bytes3(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 3]));

 289:         uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));

 300:         uint32 numberOfStateDiffs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L200

```solidity
File: system-contracts/contracts/L2BaseToken.sol

 140:     function decimals() external pure override returns (uint8) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L140

```solidity
File: system-contracts/contracts/SystemContext.sol

 37:     uint256 public blockGasLimit = type(uint32).max;

 89:     uint16 public txNumberInBlock;

 133:         uint128 blockNumber = currentVirtualL2BlockInfo.number;

 172:     function getBatchNumberAndTimestamp() public view returns (uint128 batchNumber, uint128 batchTimestamp) {

 172:     function getBatchNumberAndTimestamp() public view returns (uint128 batchNumber, uint128 batchTimestamp) {

 180:     function getL2BlockNumberAndTimestamp() public view returns (uint128 blockNumber, uint128 blockTimestamp) {

 180:     function getL2BlockNumberAndTimestamp() public view returns (uint128 blockNumber, uint128 blockTimestamp) {

 190:     function getBlockNumber() public view returns (uint128) {

 198:     function getBlockTimestamp() public view returns (uint128) {

 222:         uint128 _blockNumber,

 223:         uint128 _blockTimestamp,

 233:     function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {

 241:     function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {

 264:         uint128 _l2BlockNumber,

 265:         uint128 _maxVirtualBlocksToCreate,

 266:         uint128 _newTimestamp

 278:             uint128 currentBatchNumber = currentBatchInfo.number;

 314:     function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal {

 314:     function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal {

 342:         uint128 _l2BlockNumber,

 343:         uint128 _l2BlockTimestamp,

 346:         uint128 _maxVirtualBlocksToCreate

 350:             uint128 currentBatchTimestamp = currentBatchInfo.timestamp;

 358:         (uint128 currentL2BlockNumber, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();

 358:         (uint128 currentL2BlockNumber, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();

 409:         (uint128 currentBatchNumber, uint128 currentBatchTimestamp) = getBatchNumberAndTimestamp();

 409:         (uint128 currentBatchNumber, uint128 currentBatchTimestamp) = getBatchNumberAndTimestamp();

 410:         (, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();

 427:     function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {

 428:         uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp;

 446:         uint128 _newTimestamp,

 447:         uint128 _expectedNewNumber,

 450:         (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();

 450:         (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();

 497:         (uint128 blockNumber, uint128 blockTimestamp) = getBatchNumberAndTimestamp();

 497:         (uint128 blockNumber, uint128 blockTimestamp) = getBatchNumberAndTimestamp();

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L37

```solidity
File: system-contracts/contracts/interfaces/IBaseToken.sol

 16:     function decimals() external pure returns (uint8);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IBaseToken.sol#L16

```solidity
File: system-contracts/contracts/interfaces/ICompressor.sol

 6: uint8 constant OPERATION_BITMASK = 7;

 8: uint8 constant LENGTH_BITS_OFFSET = 3;

 10: uint8 constant MAX_ENUMERATION_INDEX_SIZE = 8;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ICompressor.sol#L6

```solidity
File: system-contracts/contracts/interfaces/IL1Messenger.sol

 15:     uint8 l2ShardId;

 17:     uint16 txNumberInBlock;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IL1Messenger.sol#L15

```solidity
File: system-contracts/contracts/interfaces/IMailbox.sol

 9:         uint16 _l2TxNumberInBlock,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IMailbox.sol#L9

```solidity
File: system-contracts/contracts/interfaces/ISystemContext.sol

 13:         uint128 timestamp;

 14:         uint128 number;

 23:         uint128 virtualBlockStartBatch;

 27:         uint128 virtualBlockFinishL2Block;

 44:     function txNumberInBlock() external view returns (uint16);

 50:     function getBlockNumber() external view returns (uint128);

 52:     function getBlockTimestamp() external view returns (uint128);

 54:     function getBatchNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);

 54:     function getBatchNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);

 56:     function getL2BlockNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);

 56:     function getL2BlockNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L13

```solidity
File: system-contracts/contracts/libraries/EfficientCall.sol

 261:         uint32 shrinkTo = uint32(msg.data.length - (_data.length + dataOffset));

 264:         uint32 gas = Utils.safeCastToU32(_gas);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L261

```solidity
File: system-contracts/contracts/libraries/RLPEncoder.sol

 49:     function encodeNonSingleBytesLen(uint64 _len) internal pure returns (bytes memory) {

 56:     function encodeListLen(uint64 _len) internal pure returns (bytes memory) {

 60:     function _encodeLength(uint64 _len, uint256 _offset) private pure returns (bytes memory encoded) {

 86:             if (_number > type(uint128).max) {

 90:             if (_number > type(uint64).max) {

 94:             if (_number > type(uint32).max) {

 98:             if (_number > type(uint16).max) {

 102:             if (_number > type(uint8).max) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L49

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol

 9: uint256 constant UINT32_MASK = type(uint32).max;

 10: uint256 constant UINT64_MASK = type(uint64).max;

 11: uint256 constant UINT128_MASK = type(uint128).max;

 12: uint256 constant ADDRESS_MASK = type(uint160).max;

 16:     uint32 pubdataPublished;

 17:     uint32 heapSize;

 18:     uint32 auxHeapSize;

 19:     uint8 shardId;

 20:     uint8 callerShardId;

 21:     uint8 codeShardId;

 94:     function ptrAddIntoActive(uint32 _value) internal view {

 106:     function ptrShrinkIntoActive(uint32 _shrink) internal view {

 125:         uint32 _inputMemoryOffset,

 126:         uint32 _inputMemoryLength,

 127:         uint32 _outputMemoryOffset,

 128:         uint32 _outputMemoryLength,

 129:         uint64 _perPrecompileInterpreted

 150:         uint32 _gasToBurn,

 151:         uint32 _pubdataToSpend

 168:     function setValueForNextFarCall(uint128 _value) internal returns (bool success) {

 227:     function getPubdataPublishedFromMeta(uint256 meta) internal pure returns (uint32 pubdataPublished) {

 237:     function getHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 heapSize) {

 246:     function getAuxHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 auxHeapSize) {

 254:     function getShardIdFromMeta(uint256 meta) internal pure returns (uint8 shardId) {

 263:     function getCallerShardIdFromMeta(uint256 meta) internal pure returns (uint8 callerShardId) {

 272:     function getCodeShardIdFromMeta(uint256 meta) internal pure returns (uint8 codeShardId) {

 344:     function burnGas(uint32 _gasToPay, uint32 _pubdataToSpend) internal view {

 344:     function burnGas(uint32 _gasToPay, uint32 _pubdataToSpend) internal view {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L9

```solidity
File: system-contracts/contracts/libraries/SystemContractsCaller.sol

 76:     function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

 79:         uint32 dataStart;

 83:         uint32 dataLength = uint32(Utils.safeCastToU32(data.length));

 124:         uint32 gasLimit,

 126:         uint128 value,

 151:         uint32 gasLimit,

 153:         uint128 value,

 215:         uint32 dataOffset,

 216:         uint32 memoryPage,

 217:         uint32 dataStart,

 218:         uint32 dataLength,

 219:         uint32 gasPassed,

 220:         uint8 shardId,

 251:         uint32 gasPassed,

 252:         uint8 shardId,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L76

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 15: uint8 constant EIP_712_TX_TYPE = 0x71;

 18: uint8 constant LEGACY_TX_TYPE = 0x0;

 20: uint8 constant EIP_2930_TX_TYPE = 0x01;

 22: uint8 constant EIP_1559_TX_TYPE = 0x02;

 171:             uint64 txDataLen = uint64(_transaction.data.length);

 249:             uint64 txDataLen = uint64(_transaction.data.length);

 321:             uint64 txDataLen = uint64(_transaction.data.length);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L15

```solidity
File: system-contracts/contracts/libraries/UnsafeBytesCalldata.sol

 19:     function readUint16(bytes calldata _bytes, uint256 _start) internal pure returns (uint16 result) {

 26:     function readUint32(bytes calldata _bytes, uint256 _start) internal pure returns (uint32 result) {

 33:     function readUint64(bytes calldata _bytes, uint256 _start) internal pure returns (uint64 result) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L19

```solidity
File: system-contracts/contracts/libraries/Utils.sol

 20:     function safeCastToU128(uint256 _x) internal pure returns (uint128) {

 21:         require(_x <= type(uint128).max, "Overflow");

 26:     function safeCastToU32(uint256 _x) internal pure returns (uint32) {

 27:         require(_x <= type(uint32).max, "Overflow");

 32:     function safeCastToU24(uint256 _x) internal pure returns (uint24) {

 33:         require(_x <= type(uint24).max, "Overflow");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L33


## [GAS-30] Long require/revert strings
require()/revert() strings longer than 32 bytes cost extra gas

**Total Instances:** 100

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 75:         require(
                msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
                "L1SharedBridge: not bridgehub or era chain"

 155:             require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");

 195:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

 427:             require(!alreadyFinalized, "Withdrawal is already finalized 2");

 564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 83:         require(
                !stateTransitionManagerIsRegistered[_stateTransitionManager],
                "Bridgehub: state transition already registered"

 93:         require(
                stateTransitionManagerIsRegistered[_stateTransitionManager],
                "Bridgehub: state transition not registered yet"

 102:         require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

 125:         require(
                 stateTransitionManagerIsRegistered[_stateTransitionManager],
                 "Bridgehub: state transition not registered"

 132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

 225:                 require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");

 300:         require(
                 _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
                 "Bridgehub: second bridge address too low"

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

 65:         require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

 71:         require(
                msg.sender == owner() || msg.sender == securityCouncil,
                "Only the owner and security council are allowed to call this function"

 172:         require(isOperationReady(id), "Operation must be ready before execution");

 177:         require(isOperationReady(id), "Operation must be ready after execution");

 191:         require(isOperationPending(id), "Operation must be pending before execution");

 196:         require(isOperationPending(id), "Operation must be pending after execution");

 216:         require(!isOperation(_id), "Operation with this proposal id already exists");

 217:         require(_delay >= minDelay, "Proposed delay is less than minimum delay");

 240:         require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L59

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 256:         require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L256

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 62:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

 68:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 90:         require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed

 105:         require(
                 cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
                 "StateTransition: cutHash mismatch"

 110:         require(
                 s.protocolVersion == _oldProtocolVersion,
                 "StateTransition: protocolVersion mismatch in STC when upgrading"

 116:         require(
                 s.protocolVersion > _oldProtocolVersion,
                 "StateTransition: protocolVersion mismatch in STC after upgrading"

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 226:         require(
                 IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
                 "Executor facet: wrong protocol version"

 616:         require(success, "failed to call point evaluation precompile");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L226

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

 22:         require(s.validators[msg.sender], "StateTransition Chain: not validator");

 27:         require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

 32:         require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

 37:         require(
                msg.sender == s.admin || msg.sender == s.stateTransitionManager,
                "StateTransition Chain: Only by admin or state transition manager"

 45:         require(
                s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
                "StateTransition Chain: Only by validator or state transition manager"

 53:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 190:         require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");

 205:         require(
                 _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
                 "The new protocol version should be included in the L2 system upgrade tx"

 238:         require(
                 _newProtocolVersion > previousProtocolVersion,
                 "New protocol version is not greater than the current one"

 242:         require(
                 _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
                 "Too big protocol version difference"

 249:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

 250:         require(
                 s.l2SystemContractsUpgradeBatchNumber == 0,
                 "The batch number of the previous upgrade has not been cleaned"

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L190

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

 22:         require(
                // Genesis Upgrade difference: Note this is the only thing change > to >=
                _newProtocolVersion >= previousProtocolVersion,
                "New protocol version is not greater than the current one"

 27:         require(
                _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
                "Too big protocol version difference"

 33:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

 34:         require(
                s.l2SystemContractsUpgradeBatchNumber == 0,
                "The batch number of the previous upgrade has not been cleaned"

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 92:         require(msg.value == 0, "Value should be 0 for ERC20 bridge");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol

 26:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

 37:         require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");

 48:         require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");

 57:         require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L26

```solidity
File: system-contracts/contracts/ComplexUpgrader.sol

 22:         require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L22

```solidity
File: system-contracts/contracts/Compressor.sol

 51:             require(
                    encodedData.length * 4 == _bytecode.length,
                    "Encoded data length should be 4 times shorter than the original bytecode"

 56:             require(
                    dictionary.length / 8 <= encodedData.length / 2,
                    "Dictionary should have at most the same number of entries as the encoded data"

 63:                 require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

 68:                 require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");

 119:         require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");

 156:         require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");

 187:         require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");

 230:                 require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");

 232:                 require(
                         _initialValue + convertedValue == _finalValue,
                         "add: initial plus converted not equal to final"

 237:                 require(
                         _initialValue - convertedValue == _finalValue,
                         "sub: initial minus converted not equal to final"

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L51

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 77:         require(
                _nonceOrdering == AccountNonceOrdering.Arbitrary &&
                    currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
                "It is only possible to change from sequential to arbitrary ordering"

 239:         require(
                 msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
                 "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"

 251:         require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");

 265:         require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

 350:             require(value == 0, "The value must be zero if we do not call the constructor");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L77

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

 202:         require(success, "Failed to pay the fee to the operator");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L100

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

 35:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L35

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

 76:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L76

```solidity
File: system-contracts/contracts/L1Messenger.sol

 214:         require(
                 reconstructedChainedLogsHash == chainedLogsHash,
                 "reconstructedChainedLogsHash is not equal to chainedLogsHash"

 245:         require(
                 reconstructedChainedMessagesHash == chainedMessagesHash,
                 "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"

 269:         require(
                 reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
                 "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"

 279:         require(
                 uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
                     STATE_DIFF_COMPRESSION_VERSION_NUMBER,
                 "state diff compression version mismatch"

 315:         require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L214

```solidity
File: system-contracts/contracts/L2BaseToken.sol

 33:         require(
                msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
                    msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
                    msg.sender == BOOTLOADER_FORMAL_ADDRESS,
                "Only system contracts with special access can call this method"

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L33

```solidity
File: system-contracts/contracts/NonceHolder.sol

 66:         require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");

 136:         require(
                 msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
                 "Only the contract deployer can increment the deployment nonce"

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L66

```solidity
File: system-contracts/contracts/SystemContext.sol

 242:         require(_isFirstInBatch, "Upgrade transaction must be first");

 245:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

 249:             require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");

 287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

 351:             require(
                     _l2BlockTimestamp >= currentBatchTimestamp,
                     "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"

 355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

 367:             require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");

 368:             require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");

 369:             require(
                     _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
                     "The previous hash of the same L2 block must be same"

 373:             require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");

 385:             require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");

 386:             require(
                     _l2BlockTimestamp > currentL2BlockTimestamp,
                     "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"

 413:         require(currentBatchNumber > 0, "The current batch number must be greater than 0");

 429:         require(
                 _newTimestamp > currentBlockTimestamp,
                 "The timestamp of the batch must be greater than the timestamp of the previous block"

 452:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L242

```solidity
File: system-contracts/contracts/interfaces/ISystemContract.sol

 21:         require(
                SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
                "This method require system call flag"

 31:         require(
                SystemContractHelper.isSystemContract(msg.sender),
                "This method require the caller to be system contract"

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L21

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol

 319:         require(index < 10, "There are only 10 accessible registers");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 363:         require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");

 367:             require(
                     _transaction.paymasterInput.length >= 68,
                     "The approvalBased paymaster input must be at least 68 bytes long"

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L367


## [GAS-31] Low level call can be optimized with assembly
When using low-level calls, the returnData is copied to memory even if the variable is not utilized. The proper way to handle this is through a low level assembly call. 
```solidity 
 (bool success,) = payable(receiver).call{gas: gas, value: value}("");
 ```
 can be optimized to 
```solidity 
 bool success; 
 assembly { 
  success := call(gas, receiver, value, 0, 0, 0, 0) 
 } 
 ```


**Total Instances:** 1

**Gas per instance:** 248
**Total Gas saved:** 248

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226


## [GAS-32] Reduce gas usage by moving to Solidity 0.8.19 or later
Solidity version 0.8.19 introduced a number of gas optimizations, refer to the Solidity 0.8.19 Release Announcement for details.

**Total Instances:** 1

**Gas per instance:** 1000
**Total Gas saved:** 1000

```solidity
File: contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol

 2: pragma solidity ^0.8.0;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L2


## [GAS-33] Using a nesting if statement instead of a logical AND(&&)
Using a nesting if statement instead of a logical AND (&&) can provide similar short-circuiting behavior whereas double if is slightly more gas efficient.

**Total Instances:** 7

**Gas per instance:** 6
**Total Gas saved:** 42

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 361:         if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L361

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 147:         if (

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L147

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol

 131:         if (

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L131

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 47:         if (

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L47

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 139:         if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L139

```solidity
File: system-contracts/contracts/NonceHolder.sol

 88:         if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {

 171:         } else if (!isUsed && _shouldBeUsed) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L171


## [GAS-34] Optimize names to save gas
public/external function names and public member variable names can be optimized to save gas. Below are the interfaces/abstract contracts that can be optimized so that the most frequently-called functions use the least amount of gas possible during method lookup. Method IDs that have two leading zero bytes can save 128 gas each during deployment, and renaming functions to have lower method IDs will save 22 gas per call, per sorted position shifted.

**Total Instances:** 79

**Gas per instance:** 22
**Total Gas saved:** 1738

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 /// @audit  (), initialize(), tranferTokenToSharedBridge(), l2TokenAddress(), deposit(), deposit(), claimFailedDeposit(), finalizeWithdrawal(), sharedBridge, isWithdrawalFinalized, depositAmount, l2Bridge, l2TokenBeacon, l2TokenProxyBytecodeHash, 
 19: contract L1ERC20Bridge is IL1ERC20Bridge, ReentrancyGuard {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L19

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 /// @audit  (), initialize(), transferFundsFromLegacy(), receiveEth(), initializeChainGovernance(), bridgehubDepositBaseToken(), bridgehubDeposit(), bridgehubConfirmL2Transaction(), claimFailedDeposit(), finalizeWithdrawal(), depositLegacyErc20Bridge(), finalizeWithdrawalLegacyErc20Bridge(), claimFailedDepositLegacyErc20Bridge(), l1WethAddress, bridgehub, legacyBridge, l2BridgeAddress, depositHappened, isWithdrawalFinalized, 
 30: contract L1SharedBridge is IL1SharedBridge, ReentrancyGuard, Initializable, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L30

```solidity
File: contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

 /// @audit  isWithdrawalFinalized(), deposit(), deposit(), claimFailedDeposit(), finalizeWithdrawal(), l2TokenAddress(), sharedBridge(), l2TokenBeacon(), l2Bridge(), depositAmount(), tranferTokenToSharedBridge(), 
 11: interface IL1ERC20Bridge {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L11

```solidity
File: contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

 /// @audit  isWithdrawalFinalized(), depositLegacyErc20Bridge(), claimFailedDepositLegacyErc20Bridge(), claimFailedDeposit(), finalizeWithdrawalLegacyErc20Bridge(), finalizeWithdrawal(), l1WethAddress(), bridgehub(), legacyBridge(), l2BridgeAddress(), depositHappened(), bridgehubDeposit(), bridgehubDepositBaseToken(), bridgehubConfirmL2Transaction(), receiveEth(), 
 12: interface IL1SharedBridge {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L12

```solidity
File: contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol

 /// @audit  finalizeDeposit(), withdraw(), l1TokenAddress(), l2TokenAddress(), l1Bridge(), 
 6: interface IL2Bridge {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL2Bridge.sol#L6

```solidity
File: contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol

 /// @audit  deposit(), withdraw(), 
 4: interface IWETH9 {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L4

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 /// @audit  (), initialize(), setPendingAdmin(), acceptAdmin(), getStateTransition(), addStateTransitionManager(), removeStateTransitionManager(), addToken(), setSharedBridge(), createNewChain(), proveL2MessageInclusion(), proveL2LogInclusion(), proveL1ToL2TransactionStatus(), l2TransactionBaseCost(), requestL2TransactionDirect(), requestL2TransactionTwoBridges(), sharedBridge, stateTransitionManagerIsRegistered, tokenIsRegistered, stateTransitionManager, baseToken, admin, 
 16: contract Bridgehub is IBridgehub, ReentrancyGuard, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L16

```solidity
File: contracts/ethereum/contracts/bridgehub/IBridgehub.sol

 /// @audit  setPendingAdmin(), acceptAdmin(), stateTransitionManagerIsRegistered(), stateTransitionManager(), tokenIsRegistered(), baseToken(), sharedBridge(), getStateTransition(), proveL2MessageInclusion(), proveL2LogInclusion(), proveL1ToL2TransactionStatus(), requestL2TransactionDirect(), requestL2TransactionTwoBridges(), l2TransactionBaseCost(), createNewChain(), addStateTransitionManager(), removeStateTransitionManager(), addToken(), setSharedBridge(), 
 42: interface IBridgehub {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L42

```solidity
File: contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol

 /// @audit  forceDeployOnAddresses(), create2(), 
 9: interface IL2ContractDeployer {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L9

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 /// @audit  (), isOperation(), isOperationPending(), isOperationReady(), isOperationDone(), getOperationState(), scheduleTransparent(), scheduleShadow(), cancel(), execute(), executeInstant(), hashOperation(), updateDelay(), updateSecurityCouncil(), (), securityCouncil, timestamps, minDelay, 
 20: contract Governance is IGovernance, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L20

```solidity
File: contracts/ethereum/contracts/governance/IGovernance.sol

 /// @audit  isOperation(), isOperationPending(), isOperationReady(), isOperationDone(), getOperationState(), scheduleTransparent(), scheduleShadow(), cancel(), execute(), executeInstant(), hashOperation(), updateDelay(), updateSecurityCouncil(), 
 8: interface IGovernance {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/IGovernance.sol#L8

```solidity
File: contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol

 /// @audit  bridgehub(), setPendingAdmin(), acceptAdmin(), stateTransition(), storedBatchZero(), initialCutHash(), genesisUpgrade(), upgradeCutHash(), protocolVersion(), initialize(), setInitialCutHash(), setValidatorTimelock(), getChainAdmin(), createNewChain(), registerAlreadyDeployedStateTransition(), setNewVersionUpgrade(), setUpgradeDiamondCut(), freezeChain(), unfreezeChain(), 
 26: interface IStateTransitionManager {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L26

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 /// @audit  (), getChainAdmin(), initialize(), setPendingAdmin(), acceptAdmin(), setValidatorTimelock(), setInitialCutHash(), setNewVersionUpgrade(), setUpgradeDiamondCut(), freezeChain(), unfreezeChain(), revertBatches(), registerAlreadyDeployedStateTransition(), createNewChain(), bridgehub, stateTransition, storedBatchZero, initialCutHash, genesisUpgrade, protocolVersion, validatorTimelock, upgradeCutHash, admin, 
 25: contract StateTransitionManager is IStateTransitionManager, ReentrancyGuard, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L25

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 /// @audit  (), setStateTransitionManager(), addValidator(), removeValidator(), setExecutionDelay(), getCommittedBatchTimestamp(), commitBatches(), commitBatchesSharedBridge(), revertBatches(), revertBatchesSharedBridge(), proveBatches(), proveBatchesSharedBridge(), executeBatches(), executeBatchesSharedBridge(), getName, stateTransitionManager, validators, executionDelay, 
 22: contract ValidatorTimelock is IExecutor, Ownable2Step {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L22

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

 /// @audit  (), initialize(), 
 17: contract DiamondInit is ZkSyncStateTransitionBase, IDiamondInit {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L17

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

 /// @audit  (), (), 
 10: contract DiamondProxy {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L10

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 /// @audit  setPendingAdmin(), acceptAdmin(), setValidator(), setPorterAvailability(), setPriorityTxMaxGasLimit(), changeFeeParams(), setTokenMultiplier(), setValidiumMode(), upgradeChainFromVersion(), executeUpgrade(), freezeDiamond(), unfreezeDiamond(), getName, 
 18: contract AdminFacet is ZkSyncStateTransitionBase, IAdmin {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L18

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 /// @audit  commitBatches(), commitBatchesSharedBridge(), executeBatchesSharedBridge(), executeBatches(), proveBatches(), proveBatchesSharedBridge(), revertBatches(), revertBatchesSharedBridge(), getName, 
 22: contract ExecutorFacet is ZkSyncStateTransitionBase, IExecutor {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L22

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

 /// @audit  getVerifier(), getAdmin(), getPendingAdmin(), getBridgehub(), getStateTransitionManager(), getBaseToken(), getBaseTokenBridge(), baseTokenGasPriceMultiplierNominator(), baseTokenGasPriceMultiplierDenominator(), getTotalBatchesCommitted(), getTotalBatchesVerified(), getTotalBatchesExecuted(), getTotalPriorityTxs(), getFirstUnprocessedPriorityTx(), getPriorityQueueSize(), priorityQueueFrontOperation(), isValidator(), l2LogsRootHash(), storedBatchHash(), getL2BootloaderBytecodeHash(), getL2DefaultAccountBytecodeHash(), getVerifierParams(), getProtocolVersion(), getL2SystemContractsUpgradeTxHash(), getL2SystemContractsUpgradeBatchNumber(), isDiamondStorageFrozen(), isFacetFreezable(), getPriorityTxMaxGasLimit(), isFunctionFreezable(), isEthWithdrawalFinalized(), getPubdataPricingMode(), facets(), facetFunctionSelectors(), facetAddresses(), facetAddress(), getTotalBlocksCommitted(), getTotalBlocksVerified(), getTotalBlocksExecuted(), storedBlockHash(), getL2SystemContractsUpgradeBlockNumber(), getName, 
 20: contract GettersFacet is ZkSyncStateTransitionBase, IGetters, ILegacyGetters {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L20

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol

 /// @audit  setPendingAdmin(), acceptAdmin(), setValidator(), setPorterAvailability(), setPriorityTxMaxGasLimit(), changeFeeParams(), setTokenMultiplier(), setValidiumMode(), upgradeChainFromVersion(), executeUpgrade(), freezeDiamond(), unfreezeDiamond(), 
 13: interface IAdmin is IZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L13

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol

 /// @audit  initialize(), 
 61: interface IDiamondInit {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L61

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol

 /// @audit  commitBatches(), commitBatchesSharedBridge(), proveBatches(), proveBatchesSharedBridge(), executeBatches(), executeBatchesSharedBridge(), revertBatches(), revertBatchesSharedBridge(), 
 73: interface IExecutor is IZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L73

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol

 /// @audit  getVerifier(), getAdmin(), getPendingAdmin(), getBridgehub(), getStateTransitionManager(), getBaseToken(), getBaseTokenBridge(), getTotalBatchesCommitted(), getTotalBatchesVerified(), getTotalBatchesExecuted(), getTotalPriorityTxs(), getFirstUnprocessedPriorityTx(), getPriorityQueueSize(), priorityQueueFrontOperation(), isValidator(), l2LogsRootHash(), storedBatchHash(), getL2BootloaderBytecodeHash(), getL2DefaultAccountBytecodeHash(), getVerifierParams(), isDiamondStorageFrozen(), getProtocolVersion(), getL2SystemContractsUpgradeTxHash(), getL2SystemContractsUpgradeBatchNumber(), getPriorityTxMaxGasLimit(), isEthWithdrawalFinalized(), getPubdataPricingMode(), baseTokenGasPriceMultiplierNominator(), baseTokenGasPriceMultiplierDenominator(), facets(), facetFunctionSelectors(), facetAddresses(), facetAddress(), isFunctionFreezable(), isFacetFreezable(), 
 13: interface IGetters is IZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L13

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol

 /// @audit  getTotalBlocksCommitted(), getTotalBlocksVerified(), getTotalBlocksExecuted(), storedBlockHash(), getL2SystemContractsUpgradeBlockNumber(), 
 11: interface ILegacyGetters is IZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/ILegacyGetters.sol#L11

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

 /// @audit  proveL2MessageInclusion(), proveL2LogInclusion(), proveL1ToL2TransactionStatus(), finalizeEthWithdrawal(), requestL2Transaction(), bridgehubRequestL2Transaction(), l2TransactionBaseCost(), transferEthToSharedBridge(), 
 11: interface IMailbox is IZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L11

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol

 /// @audit  verify(), verificationKeyHash(), 
 15: interface IVerifier {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IVerifier.sol#L15

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol

 /// @audit  getName(), 
 7: interface IZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransitionBase.sol#L7

```solidity
File: contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol

 /// @audit  setChainId(), 
 4: interface ISystemContext {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L4

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 /// @audit  upgrade(), 
 44: abstract contract BaseZkSyncUpgrade is ZkSyncStateTransitionBase {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L44

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

 /// @audit  upgrade(), 
 17: abstract contract BaseZkSyncUpgradeGenesis is BaseZkSyncUpgrade {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L17

```solidity
File: contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol

 /// @audit  upgrade(), 
 10: contract DefaultUpgrade is BaseZkSyncUpgrade {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/DefaultUpgrade.sol#L10

```solidity
File: contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol

 /// @audit  upgrade(), 
 11: contract GenesisUpgrade is BaseZkSyncUpgradeGenesis {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/GenesisUpgrade.sol#L11

```solidity
File: contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol

 /// @audit  upgrade(), 
 7: interface IDefaultUpgrade {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/IDefaultUpgrade.sol#L7

```solidity
File: contracts/zksync/contracts/ForceDeployUpgrader.sol

 /// @audit  forceDeploy(), 
 10: contract ForceDeployUpgrader {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/ForceDeployUpgrader.sol#L10

```solidity
File: contracts/zksync/contracts/L2ContractHelper.sol

 /// @audit  sendToL1(), 
 18: interface IL2Messenger {

 /// @audit  forceDeployOnAddresses(), create2(), 
 30: interface IContractDeployer {

 /// @audit  withdrawWithMessage(), 
 61: interface IBaseToken {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L18

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 /// @audit  (), initialize(), finalizeDeposit(), withdraw(), l2TokenAddress(), l1Bridge, l2TokenBeacon, l1TokenAddress, 
 23: contract L2SharedBridge is IL2SharedBridge, Initializable {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L23

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 /// @audit  (), bridgeInitialize(), reinitializeToken(), bridgeMint(), bridgeBurn(), name(), symbol(), decimals(), decodeString(), decodeUint8(), l2Bridge, l1Address, 
 15: contract L2StandardERC20 is ERC20PermitUpgradeable, IL2StandardToken, ERC1967Upgrade {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L15

```solidity
File: contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol

 /// @audit  finalizeWithdrawal(), 
 8: interface IL1ERC20Bridge {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L8

```solidity
File: contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol

 /// @audit  finalizeWithdrawal(), 
 8: interface IL1SharedBridge {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL1SharedBridge.sol#L8

```solidity
File: contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol

 /// @audit  finalizeDeposit(), withdraw(), l1TokenAddress(), l2TokenAddress(), l1Bridge(), 
 6: interface IL2SharedBridge {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L6

```solidity
File: contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol

 /// @audit  bridgeMint(), bridgeBurn(), l1Address(), l2Bridge(), 
 5: interface IL2StandardToken {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/interfaces/IL2StandardToken.sol#L5

```solidity
File: contracts/zksync/contracts/interfaces/IPaymaster.sol

 /// @audit  validateAndPayForPaymasterTransaction(), postTransaction(), 
 14: interface IPaymaster {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L14

```solidity
File: contracts/zksync/contracts/interfaces/IPaymasterFlow.sol

 /// @audit  general(), approvalBased(), 
 13: interface IPaymasterFlow {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/interfaces/IPaymasterFlow.sol#L13

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol

 /// @audit  storeAccountConstructingCodeHash(), storeAccountConstructedCodeHash(), markAccountCodeHashAsConstructed(), getRawCodeHash(), getCodeHash(), getCodeSize(), 
 22: contract AccountCodeStorage is IAccountCodeStorage {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L22

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol

 /// @audit  getTransactionHashes(), 
 16: contract BootloaderUtilities is IBootloaderUtilities {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L16

```solidity
File: system-contracts/contracts/ComplexUpgrader.sol

 /// @audit  upgrade(), 
 14: contract ComplexUpgrader is IComplexUpgrader {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L14

```solidity
File: system-contracts/contracts/Compressor.sol

 /// @audit  publishCompressedBytecode(), verifyCompressedStateDiffs(), 
 22: contract Compressor is ICompressor, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L22

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 /// @audit  getAccountInfo(), extendedAccountVersion(), updateAccountVersion(), updateNonceOrdering(), getNewAddressCreate2(), getNewAddressCreate(), create2(), create(), create2Account(), createAccount(), forceDeployOnAddress(), forceDeployOnAddresses(), 
 23: contract ContractDeployer is IContractDeployer, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L23

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 /// @audit  validateTransaction(), executeTransaction(), executeTransactionFromOutside(), payForTransaction(), prepareForPaymaster(), (), (), 
 19: contract DefaultAccount is IAccount {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L19

```solidity
File: system-contracts/contracts/EmptyContract.sol

 /// @audit  (), (), 
 10: contract EmptyContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/EmptyContract.sol#L10

```solidity
File: system-contracts/contracts/GasBoundCaller.sol

 /// @audit  gasBoundCall(), 
 15: contract GasBoundCaller {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L15

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

 /// @audit  getImmutable(), setImmutables(), 
 18: contract ImmutableSimulator is IImmutableSimulator {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L18

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

 /// @audit  markFactoryDeps(), markBytecodeAsPublished(), getMarker(), 
 18: contract KnownCodesStorage is IKnownCodesStorage, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L18

```solidity
File: system-contracts/contracts/L1Messenger.sol

 /// @audit  sendL2ToL1Log(), sendToL1(), requestBytecodeL1Publication(), publishPubdataAndClearState(), 
 25: contract L1Messenger is IL1Messenger, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L25

```solidity
File: system-contracts/contracts/L2BaseToken.sol

 /// @audit  transferFromTo(), balanceOf(), mint(), withdraw(), withdrawWithMessage(), name(), symbol(), decimals(), totalSupply, 
 18: contract L2BaseToken is IBaseToken, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L18

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol

 /// @audit  (), 
 19: contract MsgValueSimulator is ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L19

```solidity
File: system-contracts/contracts/NonceHolder.sol

 /// @audit  getMinNonce(), getRawNonce(), increaseMinNonce(), setValueUnderNonce(), getValueUnderNonce(), incrementMinNonceIfEquals(), getDeploymentNonce(), incrementDeploymentNonce(), isNonceUsed(), validateNonceUsage(), 
 27: contract NonceHolder is INonceHolder, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L27

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol

 /// @audit  chunkAndPublishPubdata(), 
 16: contract PubdataChunkPublisher is IPubdataChunkPublisher, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L16

```solidity
File: system-contracts/contracts/SystemContext.sol

 /// @audit  setChainId(), setTxOrigin(), setGasPrice(), setPubdataInfo(), getCurrentPubdataSpent(), getCurrentPubdataCost(), getBlockHashEVM(), getBatchHash(), getBatchNumberAndTimestamp(), getL2BlockNumberAndTimestamp(), getBlockNumber(), getBlockTimestamp(), setL2Block(), appendTransactionToCurrentL2Block(), publishTimestampDataToL1(), setNewBatch(), unsafeOverrideBatch(), incrementTxNumberInBatch(), resetTxNumberInBatch(), currentBlockInfo(), getBlockNumberAndTimestamp(), blockHash(), chainId, origin, gasPrice, blockGasLimit, coinbase, difficulty, baseFee, txNumberInBlock, gasPerPubdataByte, 
 17: contract SystemContext is ISystemContext, ISystemContextDeprecated, ISystemContract {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L17

```solidity
File: system-contracts/contracts/interfaces/IAccount.sol

 /// @audit  validateTransaction(), executeTransaction(), executeTransactionFromOutside(), payForTransaction(), prepareForPaymaster(), 
 9: interface IAccount {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IAccount.sol#L9

```solidity
File: system-contracts/contracts/interfaces/IAccountCodeStorage.sol

 /// @audit  storeAccountConstructingCodeHash(), storeAccountConstructedCodeHash(), markAccountCodeHashAsConstructed(), getRawCodeHash(), getCodeHash(), getCodeSize(), 
 5: interface IAccountCodeStorage {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IAccountCodeStorage.sol#L5

```solidity
File: system-contracts/contracts/interfaces/IBaseToken.sol

 /// @audit  balanceOf(), transferFromTo(), totalSupply(), name(), symbol(), decimals(), mint(), withdraw(), withdrawWithMessage(), 
 5: interface IBaseToken {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IBaseToken.sol#L5

```solidity
File: system-contracts/contracts/interfaces/IBootloaderUtilities.sol

 /// @audit  getTransactionHashes(), 
 7: interface IBootloaderUtilities {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IBootloaderUtilities.sol#L7

```solidity
File: system-contracts/contracts/interfaces/IComplexUpgrader.sol

 /// @audit  upgrade(), 
 10: interface IComplexUpgrader {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IComplexUpgrader.sol#L10

```solidity
File: system-contracts/contracts/interfaces/ICompressor.sol

 /// @audit  publishCompressedBytecode(), verifyCompressedStateDiffs(), 
 18: interface ICompressor {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ICompressor.sol#L18

```solidity
File: system-contracts/contracts/interfaces/IContractDeployer.sol

 /// @audit  getNewAddressCreate2(), getNewAddressCreate(), create2(), create2Account(), create(), createAccount(), getAccountInfo(), updateAccountVersion(), updateNonceOrdering(), 
 5: interface IContractDeployer {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IContractDeployer.sol#L5

```solidity
File: system-contracts/contracts/interfaces/IImmutableSimulator.sol

 /// @audit  getImmutable(), setImmutables(), 
 10: interface IImmutableSimulator {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IImmutableSimulator.sol#L10

```solidity
File: system-contracts/contracts/interfaces/IKnownCodesStorage.sol

 /// @audit  markFactoryDeps(), markBytecodeAsPublished(), getMarker(), 
 11: interface IKnownCodesStorage {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IKnownCodesStorage.sol#L11

```solidity
File: system-contracts/contracts/interfaces/IL1Messenger.sol

 /// @audit  sendToL1(), sendL2ToL1Log(), requestBytecodeL1Publication(), 
 40: interface IL1Messenger {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IL1Messenger.sol#L40

```solidity
File: system-contracts/contracts/interfaces/IL2StandardToken.sol

 /// @audit  bridgeMint(), bridgeBurn(), l1Address(), l2Bridge(), 
 5: interface IL2StandardToken {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IL2StandardToken.sol#L5

```solidity
File: system-contracts/contracts/interfaces/IMailbox.sol

 /// @audit  finalizeEthWithdrawal(), 
 5: interface IMailbox {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IMailbox.sol#L5

```solidity
File: system-contracts/contracts/interfaces/INonceHolder.sol

 /// @audit  getMinNonce(), getRawNonce(), increaseMinNonce(), setValueUnderNonce(), getValueUnderNonce(), incrementMinNonceIfEquals(), getDeploymentNonce(), incrementDeploymentNonce(), validateNonceUsage(), isNonceUsed(), 
 13: interface INonceHolder {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/INonceHolder.sol#L13

```solidity
File: system-contracts/contracts/interfaces/IPaymaster.sol

 /// @audit  validateAndPayForPaymasterTransaction(), postTransaction(), 
 14: interface IPaymaster {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPaymaster.sol#L14

```solidity
File: system-contracts/contracts/interfaces/IPaymasterFlow.sol

 /// @audit  general(), approvalBased(), 
 12: interface IPaymasterFlow {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPaymasterFlow.sol#L12

```solidity
File: system-contracts/contracts/interfaces/IPubdataChunkPublisher.sol

 /// @audit  chunkAndPublishPubdata(), 
 9: interface IPubdataChunkPublisher {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPubdataChunkPublisher.sol#L9

```solidity
File: system-contracts/contracts/interfaces/ISystemContext.sol

 /// @audit  chainId(), origin(), gasPrice(), blockGasLimit(), coinbase(), difficulty(), baseFee(), txNumberInBlock(), getBlockHashEVM(), getBatchHash(), getBlockNumber(), getBlockTimestamp(), getBatchNumberAndTimestamp(), getL2BlockNumberAndTimestamp(), gasPerPubdataByte(), getCurrentPubdataSpent(), 
 11: interface ISystemContext {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L11

```solidity
File: system-contracts/contracts/interfaces/ISystemContextDeprecated.sol

 /// @audit  currentBlockInfo(), getBlockNumberAndTimestamp(), blockHash(), 
 10: interface ISystemContextDeprecated {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContextDeprecated.sol#L10



## [GAS-35] Change public state variable visibility to private
its generally a good practice to limit the visibility of state variables to the minimum necessary level. This means that you should use the private visibility modifier for state variables whenever possible, and avoid using the public modifier unless it is absolutely necessary. Public state variables can be more expensive to read and write than private state variables, since Solidity generates additional getter and setter functions for public variables. By using private state variables, you can reduce the gas cost of your contract and improve its efficiency. Public state variables can be more expensive to read and write than private state variables, since Solidity generates additional getter and setter functions for public variables. By using private state variables, you can reduce the gas cost of your contract and improve its efficiency.

**Total Instances:** 43

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 23:     IL1SharedBridge public immutable override sharedBridge;

 27:     mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))

 32:     mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))

 36:     address public l2Bridge;

 39:     address public l2TokenBeacon;

 42:     bytes32 public l2TokenProxyBytecodeHash;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L23

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 34:     address public immutable override l1WethAddress;

 37:     IBridgehub public immutable override bridgehub;

 40:     IL1ERC20Bridge public immutable override legacyBridge;

 48:     mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;

 52:     mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))

 57:     mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L34

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 18:     IL1SharedBridge public sharedBridge;

 21:     mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;

 23:     mapping(address _token => bool) public tokenIsRegistered;

 26:     mapping(uint256 _chainId => address) public stateTransitionManager;

 29:     mapping(uint256 _chainId => address) public baseToken;

 32:     address public admin;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L18

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 26:     address public securityCouncil;

 32:     mapping(bytes32 operationId => uint256 executionTimestamp) public timestamps;

 35:     uint256 public minDelay;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L26

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 27:     address public immutable bridgehub;

 33:     bytes32 public storedBatchZero;

 36:     bytes32 public initialCutHash;

 39:     address public genesisUpgrade;

 42:     uint256 public protocolVersion;

 45:     address public validatorTimelock;

 48:     mapping(uint256 => bytes32) public upgradeCutHash;

 51:     address public admin;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L27

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 44:     IStateTransitionManager public stateTransitionManager;

 50:     mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;

 53:     uint32 public executionDelay;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L44

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 25:     address public override l1Bridge;

 29:     UpgradeableBeacon public l2TokenBeacon;

 35:     mapping(address l2TokenAddress => address l1TokenAddress) public override l1TokenAddress;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L25

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 34:     address public override l2Bridge;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L34

```solidity
File: system-contracts/contracts/L2BaseToken.sol

 23:     uint256 public override totalSupply;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L23

```solidity
File: system-contracts/contracts/SystemContext.sol

 26:     uint256 public chainId;

 30:     address public origin;

 34:     uint256 public gasPrice;

 48:     uint256 public baseFee;

 89:     uint16 public txNumberInBlock;

 92:     uint256 public gasPerPubdataByte;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L92


## [GAS-36] Duplicated require()/revert() checks should be refactored to a modifier Or function to save gas
Saves deployment costs.

**Total Instances:** 4

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 217:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L217

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 58:         require(_l2TokenProxyBytecodeHash != bytes32(0), "df");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L58

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 167:         if (availableGetters.ignoreSymbol) revert();

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L167

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol

 191:             require(vInt == 27 || vInt == 28, "Invalid v value");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L191


## [GAS-37] require() or revert() statements that check input arguments should be at the top of the function
Checks that involve constants should come before checks that involve state variables, function calls, and calculations. By doing these checks first, the function is able to revert before wasting a Gcoldsload (2100 gas*) in a function that may ultimately revert in the unhappy case.

**Total Instances:** 31

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 /// @audit  could be moved to line 64
 66:         require(amount == _amount, "Incorrect amount");

 /// @audit  could be moved to line 141
 143:         require(amount == _amount, "3T"); // The token has non-standard transfer logic

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L66

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 /// @audit  could be moved to line 315
 327:         require(_amount > 0, "y1");

 /// @audit  could be moved to line 563
 564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 /// @audit  could be moved to line 122
 123:         require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 /// @audit  could be moved to line 216
 217:         require(_delay >= minDelay, "Proposed delay is less than minimum delay");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L217

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 /// @audit  could be moved to line 104
 110:         require(
                 s.protocolVersion == _oldProtocolVersion,
                 "StateTransition: protocolVersion mismatch in STC when upgrading"

 /// @audit  could be moved to line 104
 116:         require(
                 s.protocolVersion > _oldProtocolVersion,
                 "StateTransition: protocolVersion mismatch in STC after upgrading"

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L110

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 /// @audit  could be moved to line 109
 110:         require(batchTimestamp == _expectedBatchTimestamp, "tb");

 /// @audit  could be moved to line 109
 114:         require(_previousBatchTimestamp < batchTimestamp, "h3");

 /// @audit  could be moved to line 482
 483:         require(_newLastBatch >= s.totalBatchesExecuted, "v2"); // Already executed batches cannot be reverted

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L110

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 /// @audit  could be moved to line 173
 175:         require(_facet == address(0), "a1"); // facet address must be zero

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

 /// @audit  could be moved to line 23
 26:         require(_index < (1 << pathLength), "px");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L26

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

 /// @audit  could be moved to line 25
 28:         require(l2GasForTxBody <= _priorityTxMaxGasLimit, "ui");

 /// @audit  could be moved to line 25
 30:         require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");

 /// @audit  could be moved to line 113
 115:         require(_totalGasLimit >= overhead, "my"); // provided gas limit doesn't cover transaction overhead

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L28

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 /// @audit  could be moved to line 186
 205:         require(
                 _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
                 "The new protocol version should be included in the L2 system upgrade tx"

 /// @audit  could be moved to line 237
 238:         require(
                 _newProtocolVersion > previousProtocolVersion,
                 "New protocol version is not greater than the current one"

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L205

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

 /// @audit  could be moved to line 21
 22:         require(
                // Genesis Upgrade difference: Note this is the only thing change > to >=
                _newProtocolVersion >= previousProtocolVersion,
                "New protocol version is not greater than the current one"

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 /// @audit  could be moved to line 55
 56:         require(_l2TokenProxyBytecodeHash != bytes32(0), "df");

 /// @audit  could be moved to line 55
 57:         require(_aliasedOwner != address(0), "sf");

 /// @audit  could be moved to line 55
 58:         require(_l2TokenProxyBytecodeHash != bytes32(0), "df");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L56

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 /// @audit  could be moved to line 75
 77:         require(
                _nonceOrdering == AccountNonceOrdering.Arbitrary &&
                    currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
                "It is only possible to change from sequential to arbitrary ordering"

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L77

```solidity
File: system-contracts/contracts/GasBoundCaller.sol

 /// @audit  could be moved to line 40
 46:         require(_maxTotalGas >= gasleft(), "Gas limit is too low");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L46

```solidity
File: system-contracts/contracts/L2BaseToken.sol

 /// @audit  could be moved to line 33
 41:         require(fromBalance >= _amount, "Transfer amount exceeds balance");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L41

```solidity
File: system-contracts/contracts/NonceHolder.sol

 /// @audit  could be moved to line 83
 85:         require(_value != 0, "Nonce value cannot be set to 0");

 /// @audit  could be moved to line 111
 115:         require(oldMinNonce == _expectedNonce, "Incorrect nonce");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L85

```solidity
File: system-contracts/contracts/SystemContext.sol

 /// @audit  could be moved to line 242
 245:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

 /// @audit  could be moved to line 428
 429:         require(
                 _newTimestamp > currentBlockTimestamp,
                 "The timestamp of the batch must be greater than the timestamp of the previous block"

 /// @audit  could be moved to line 450
 451:         require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");

 /// @audit  could be moved to line 450
 452:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L452



## [GAS-38] State variable read in a loop
The state variable should be cached in a local variable rather than reading it on every iteration of the for-loop, which will replace each Gwarmaccess (100 gas) with a much cheaper stack read.

**Total Instances:** 5

**Gas per instance:** 97
**Total Gas saved:** 485

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 /// @audit  committedBatchTimestamp
 117:                 committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);

 /// @audit  committedBatchTimestamp
 136:                 committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);

 /// @audit  committedBatchTimestamp
 186:                 uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(

 /// @audit  committedBatchTimestamp
 210:                 uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L117

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

 /// @audit  immutableDataStorage
 41:                 immutableDataStorage[uint256(uint160(_dest))][index] = value;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L41


## [GAS-39] State variables only set in their definitions should be declared constant
Avoids a Gsset (20000 gas) at deployment, and replaces the first access in each transaction (Gcoldsload - 2100 gas) and each access thereafter (Gwarmacces - 100 gas) with a PUSH32 (3 gas).

**Total Instances:** 3

**Gas per instance:** 2097
**Total Gas saved:** 6291

```solidity
File: system-contracts/contracts/SystemContext.sol

 37:     uint256 public blockGasLimit = type(uint32).max;

 41:     address public coinbase = BOOTLOADER_FORMAL_ADDRESS;

 44:     uint256 public difficulty = 2.5e15;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L44


## [GAS-40] Use uint256(1)/uint256(2) instead of true/false to save gas for changes (Missed by 4naly3er)
Avoids a Gsset (20000 gas) when changing from false to true, after having been true in the past

**Total Instances:** 1

**Gas per instance:** 8550
**Total Gas saved:** 8550

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

 74:     mapping(address validatorAddress => bool isValidator) validators;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#74


## [GAS-41] Unlimited gas consumption risk due to external call recipients
When calling an external function without specifying a gas limit , the called contract may consume all the remaining gas, causing the tx to be reverted. To mitigate this, it is recommended to explicitly set a gas limit when making low level external calls.

**Total Instances:** 1

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226


## [GAS-42] Unused named return variables without optimizer waste gas
Consider changing the variable to be an unnamed one, since the variable is never assigned, nor is it returned by name. If the optimizer is not turned on, leaving the code as it is will also waste gas for the stack variable.

**Total Instances:** 43

**Gas per instance:** 9
**Total Gas saved:** 387

```solidity
File: contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

 /// @audit  txHash
 33:     ) external payable returns (bytes32 txHash);

 /// @audit  txHash
 41:     ) external payable returns (bytes32 txHash);

 /// @audit  amount
 73:     ) external returns (uint256 amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L33

```solidity
File: contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol

 /// @audit  txHash
 72:     ) external payable returns (bytes32 txHash);

 /// @audit  l1Receiver, l1Token, amount
 103:     ) external returns (address l1Receiver, address l1Token, uint256 amount);

 /// @audit  request
 133:     ) external payable returns (L2TransactionRequestTwoBridgesInner memory request);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L72

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 /// @audit  chainId
 121:     ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L121

```solidity
File: contracts/ethereum/contracts/bridgehub/IBridgehub.sol

 /// @audit  canonicalTxHash
 101:     ) external payable returns (bytes32 canonicalTxHash);

 /// @audit  canonicalTxHash
 105:     ) external payable returns (bytes32 canonicalTxHash);

 /// @audit  chainId
 123:     ) external returns (uint256 chainId);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L101

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol

 /// @audit  merkleRoot
 68:     function l2LogsRootHash(uint256 _batchNumber) external view returns (bytes32 merkleRoot);

 /// @audit  facets
 136:     function facetAddresses() external view returns (address[] memory facets);

 /// @audit  facet
 139:     function facetAddress(bytes4 _selector) external view returns (address facet);

 /// @audit  isFreezable
 145:     function isFacetFreezable(address _facet) external view returns (bool isFreezable);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L68

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

 /// @audit  canonicalTxHash
 96:     ) external payable returns (bytes32 canonicalTxHash);

 /// @audit  canonicalTxHash
 100:     ) external payable returns (bytes32 canonicalTxHash);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L96

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 /// @audit  diamondStorage
 87:     function getDiamondStorage() internal pure returns (DiamondStorage storage diamondStorage) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L87

```solidity
File: contracts/zksync/contracts/interfaces/IPaymaster.sol

 /// @audit  magic, context
 32:     ) external payable returns (bytes4 magic, bytes memory context);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L32

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol

 /// @audit  txHash
 44:     function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L44

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 /// @audit  info
 34:     function getAccountInfo(address _address) external view returns (AccountInfo memory info) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L34

```solidity
File: system-contracts/contracts/interfaces/IAccount.sol

 /// @audit  magic
 24:     ) external payable returns (bytes4 magic);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IAccount.sol#L24

```solidity
File: system-contracts/contracts/interfaces/IAccountCodeStorage.sol

 /// @audit  codeHash
 12:     function getRawCodeHash(address _address) external view returns (bytes32 codeHash);

 /// @audit  codeHash
 14:     function getCodeHash(uint256 _input) external view returns (bytes32 codeHash);

 /// @audit  codeSize
 16:     function getCodeSize(uint256 _input) external view returns (uint256 codeSize);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IAccountCodeStorage.sol#L12

```solidity
File: system-contracts/contracts/interfaces/IBootloaderUtilities.sol

 /// @audit  txHash, signedTxHash
 10:     ) external view returns (bytes32 txHash, bytes32 signedTxHash);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IBootloaderUtilities.sol#L10

```solidity
File: system-contracts/contracts/interfaces/ICompressor.sol

 /// @audit  bytecodeHash
 22:     ) external payable returns (bytes32 bytecodeHash);

 /// @audit  stateDiffHash
 29:     ) external payable returns (bytes32 stateDiffHash);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ICompressor.sol#L22

```solidity
File: system-contracts/contracts/interfaces/IContractDeployer.sol

 /// @audit  newAddress
 48:     ) external view returns (address newAddress);

 /// @audit  newAddress
 50:     function getNewAddressCreate(address _sender, uint256 _senderNonce) external pure returns (address newAddress);

 /// @audit  newAddress
 56:     ) external payable returns (address newAddress);

 /// @audit  newAddress
 63:     ) external payable returns (address newAddress);

 /// @audit  newAddress
 72:     ) external payable returns (address newAddress);

 /// @audit  newAddress
 81:     ) external payable returns (address newAddress);

 /// @audit  info
 84:     function getAccountInfo(address _address) external view returns (AccountInfo memory info);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IContractDeployer.sol#L48

```solidity
File: system-contracts/contracts/interfaces/IL1Messenger.sol

 /// @audit  logIdInMerkleTree
 51:     function sendL2ToL1Log(bool _isService, bytes32 _key, bytes32 _value) external returns (uint256 logIdInMerkleTree);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IL1Messenger.sol#L51

```solidity
File: system-contracts/contracts/interfaces/IPaymaster.sol

 /// @audit  magic, context
 32:     ) external payable returns (bytes4 magic, bytes memory context);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/IPaymaster.sol#L32

```solidity
File: system-contracts/contracts/interfaces/ISystemContext.sol

 /// @audit  hash
 48:     function getBatchHash(uint256 _batchNumber) external view returns (bytes32 hash);

 /// @audit  blockNumber, blockTimestamp
 54:     function getBatchNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);

 /// @audit  blockNumber, blockTimestamp
 56:     function getL2BlockNumberAndTimestamp() external view returns (uint128 blockNumber, uint128 blockTimestamp);

 /// @audit  gasPerPubdataByte
 58:     function gasPerPubdataByte() external view returns (uint256 gasPerPubdataByte);

 /// @audit  currentPubdataSpent
 60:     function getCurrentPubdataSpent() external view returns (uint256 currentPubdataSpent);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContext.sol#L48

```solidity
File: system-contracts/contracts/interfaces/ISystemContextDeprecated.sol

 /// @audit  blockNumber, blockTimestamp
 13:     function getBlockNumberAndTimestamp() external view returns (uint256 blockNumber, uint256 blockTimestamp);

 /// @audit  hash
 15:     function blockHash(uint256 _blockNumber) external view returns (bytes32 hash);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContextDeprecated.sol#L15


## [GAS-43] Remove or replace unused state variables
Saves a storage slot. If the variable is assigned a non-zero value, saves Gsset (20000 gas). If it’s assigned a zero value, saves Gsreset (2900 gas). If the variable remains unassigned, there is no gas savings unless the variable is public, in which case the compiler-generated non-payable getter deployment cost is saved. If the state variable is overriding an interface’s public function, mark the variable as constant or immutable so that it does not use a storage slot. Note that there may be cases where a variable superficially appears to be used, but this is only because there are multiple definitions of the variable in different files. In such cases, the variable definition should be moved into a separate file. The instances below are the unused variables.

**Total Instances:** 10

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 45:     mapping(address => uint256) private __DEPRECATED_lastWithdrawalLimitReset;

 48:     mapping(address => uint256) private __DEPRECATED_withdrawnAmountInWindow;

 51:     mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L45

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 26:     string public constant override getName = "ValidatorTimelock";

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 20:     string public constant override getName = "AdminFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 27:     string public constant override getName = "ExecutorFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

 25:     string public constant override getName = "GettersFacet";

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25

```solidity
File: system-contracts/contracts/SystemContext.sol

 37:     uint256 public blockGasLimit = type(uint32).max;

 41:     address public coinbase = BOOTLOADER_FORMAL_ADDRESS;

 44:     uint256 public difficulty = 2.5e15;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L44


## [GAS-44] Use `Array.unsafeAccess` to avoid repeated array length checks
When using storage arrays, solidity adds an internal lookup of the array's length (a Gcoldsload 2100 gas) to ensure it doesn't read past the array's end. It's possible to avoid this lookup by using `Array.unsafeAccess `in cases where the length has already been checked.

**Total Instances:** 55

**Gas per instance:** 2100
**Total Gas saved:** 115500

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

 226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

 226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L226

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 117:                 committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);

 117:                 committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);

 136:                 committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);

 136:                 committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);

 186:                 uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(

 187:                     _newBatchesData[i].batchNumber

 210:                 uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);

 210:                 uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L117

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 258:             _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));

 294:                 _newBatchesData[i],

 352:             _executeOneBatch(_batchesData[i], i);

 408:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],

 408:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],

 412:             bytes32 currentBatchCommitment = _committedBatches[i].commitment;

 413:             proofPublicInput[i] = _getBatchProofPublicInput(

 581:             blobAuxOutputWords[i * 2] = _blobHashes[i];

 582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];

 654:             blobCommitments[versionedHashIndex] = keccak256(

 669:                 (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||

 669:                 (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||

 670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),

 670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L258

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

 209:             address facetAddr = ds.facets[i];

 210:             Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];

 212:             result[i] = Facet(facetAddr, facetToSelectors.selectors);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L209

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 102:             Action action = facetCuts[i].action;

 103:             address facet = facetCuts[i].facet;

 104:             bool isFacetFreezable = facetCuts[i].isFreezable;

 105:             bytes4[] memory selectors = facetCuts[i].selectors;

 139:             bytes4 selector = _selectors[i];

 140:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

 159:             bytes4 selector = _selectors[i];

 160:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

 179:             bytes4 selector = _selectors[i];

 180:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L102

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

 31:                 ? _efficientHash(currentHash, _path[i])

 32:                 : _efficientHash(_path[i], currentHash);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L31

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 228:                 L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),

 228:                 L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L228

```solidity
File: system-contracts/contracts/Compressor.sol

 143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

 174:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L143

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 249:             sumOfValues += _deployments[i].value;

 254:             this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);

 254:             this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L249

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

 39:                 uint256 index = _immutables[i].index;

 40:                 bytes32 value = _immutables[i].value;

 41:                 immutableDataStorage[uint256(uint160(_dest))][index] = value;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L39

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

 31:                 _markBytecodeAsPublished(_hashes[i], _shouldSendToL1);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L31

```solidity
File: system-contracts/contracts/L1Messenger.sol

 211:             l2ToL1LogsTreeArray[i] = hashedLog;

 219:             l2ToL1LogsTreeArray[i] = L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH;

 225:                 l2ToL1LogsTreeArray[i] = keccak256(

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L211

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol

 52:             blobHashes[i] = blobHash;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L52


## [GAS-45] Use assembly in place of `abi.decode` to save gas
Instead of using `abi.decode`, we can use assembly to decode our desired calldata values directly. This will allow us to avoid decoding calldata values that we will not use.

**Total Instances:** 11

**Gas per instance:** 18
**Total Gas saved:** 198

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 190:         (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L190

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 252:         Diamond.DiamondCutData memory diamondCut = abi.decode(_diamondCut, (Diamond.DiamondCutData));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L252

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 617:         (, uint256 result) = abi.decode(data, (uint256, uint256));

 682:         versionedHash = abi.decode(data, (bytes32));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L617

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 298:             require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L298

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 177:         proxy = BeaconProxy(abi.decode(returndata, (address)));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L177

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 57:         (bytes memory nameBytes, bytes memory symbolBytes, bytes memory decimalsBytes) = abi.decode(

 179:         (result) = abi.decode(_input, (string));

 184:         (result) = abi.decode(_input, (uint8));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L57

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 347:             ImmutableData[] memory immutables = abi.decode(returnData, (ImmutableData[]));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L347

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 374:             (address token, uint256 minAllowance) = abi.decode(_transaction.paymasterInput[4:68], (address, uint256));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L374


## [GAS-46] Use assembly to validate `msg.sender`
We can use assembly to efficiently validate msg.sender with the least amount of opcodes necessary. For more details check the following report [Here](https://code4rena.com/reports/2023-05-juicebox#g-06-use-assembly-to-validate-msgsender).

**Total Instances:** 42

**Gas per instance:** 12
**Total Gas saved:** 504

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 64:         require(msg.sender == address(sharedBridge), "Not shared bridge");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 69:         require(msg.sender == address(bridgehub), "ShB not BH");

 76:             msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),

 76:             msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),

 84:         require(msg.sender == address(legacyBridge), "ShB not legacy bridge");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 46:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

 46:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

 62:         require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

 328:             _recipient = msg.sender == tx.origin ? msg.sender : AddressAliasHelper.applyL1ToL2Alias(msg.sender);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

 65:         require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

 72:             msg.sender == owner() || msg.sender == securityCouncil,

 72:             msg.sender == owner() || msg.sender == securityCouncil,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L59

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 64:         require(msg.sender == bridgehub, "StateTransition: only bridgehub");

 70:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

 70:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");

 121:         require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 62:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 34:         require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

 16:         require(msg.sender == s.admin, "StateTransition Chain: not admin");

 27:         require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

 32:         require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

 38:             msg.sender == s.admin || msg.sender == s.stateTransitionManager,

 38:             msg.sender == s.admin || msg.sender == s.stateTransitionManager,

 46:             s.validators[msg.sender] || msg.sender == s.stateTransitionManager,

 53:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 120:         require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");

 130:         require(msg.sender == l2Bridge, "xnt"); // Only L2 bridge can call this method

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol

 26:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/AccountCodeStorage.sol#L26

```solidity
File: system-contracts/contracts/ComplexUpgrader.sol

 22:         require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ComplexUpgrader.sol#L22

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 29:         require(msg.sender == address(this), "Callable only by self");

 240:             msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),

 240:             msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L29

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 29:         if (msg.sender != BOOTLOADER_FORMAL_ADDRESS) {

 222:         assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L29

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

 35:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L35

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

 20:         require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L20

```solidity
File: system-contracts/contracts/L2BaseToken.sol

 36:                 msg.sender == BOOTLOADER_FORMAL_ADDRESS,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L36

```solidity
File: system-contracts/contracts/NonceHolder.sol

 137:             msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L137

```solidity
File: system-contracts/contracts/interfaces/ISystemContract.sol

 41:         require(msg.sender == caller, "Inappropriate caller");

 48:         require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader");

 55:         require(msg.sender == FORCE_DEPLOYER);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/interfaces/ISystemContract.sol#L55


## [GAS-47] Using bitmap to store bool states can save gas
Using a bitmap instead of a bool array or a bool mapping to store boolean states can save gas fees. This is because the bitmap can store 256 boolean values in a single slot instead of 256 slots, which can save gas when writing bool values or when reading multiple bool values from the same slot.

**Total Instances:** 8

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 27:     mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 57:     mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))

 61:     mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 21:     mapping(address _stateTransitionManager => bool) public stateTransitionManagerIsRegistered;

 23:     mapping(address _token => bool) public tokenIsRegistered;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L21

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 50:     mapping(uint256 _chainId => mapping(address _validator => bool)) public validators;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol

 74:     mapping(address validatorAddress => bool isValidator) validators;

 114:     mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) isEthWithdrawalFinalized;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L114


## [GAS-48] Use constants instead of type(uintx).max
'it's generally more gas-efficient to use constants instead of type(uintX).max when you need to set the maximum value of an unsigned integer type.'

**Total Instances:** 19

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 123:         require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123

```solidity
File: contracts/ethereum/contracts/common/Config.sol

 115: address constant BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS = address(uint160(type(uint16).max));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L115

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

 48:         require(_transaction.from <= type(uint16).max, "ua");

 49:         require(_transaction.to <= type(uint160).max, "ub");

 55:         require(_transaction.reserved[1] <= type(uint160).max, "uf");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L48

```solidity
File: contracts/zksync/contracts/SystemContractsCaller.sol

 28:         require(_x <= type(uint32).max, "Overflow");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L28

```solidity
File: system-contracts/contracts/SystemContext.sol

 37:     uint256 public blockGasLimit = type(uint32).max;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L37

```solidity
File: system-contracts/contracts/libraries/RLPEncoder.sol

 86:             if (_number > type(uint128).max) {

 90:             if (_number > type(uint64).max) {

 94:             if (_number > type(uint32).max) {

 98:             if (_number > type(uint16).max) {

 102:             if (_number > type(uint8).max) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L86

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol

 9: uint256 constant UINT32_MASK = type(uint32).max;

 10: uint256 constant UINT64_MASK = type(uint64).max;

 11: uint256 constant UINT128_MASK = type(uint128).max;

 12: uint256 constant ADDRESS_MASK = type(uint160).max;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L9

```solidity
File: system-contracts/contracts/libraries/Utils.sol

 21:         require(_x <= type(uint128).max, "Overflow");

 27:         require(_x <= type(uint32).max, "Overflow");

 33:         require(_x <= type(uint24).max, "Overflow");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L33


## [GAS-49] Use do while loops instead of for loops
A do while loop will cost less gas since the condition is not being checked for the first iteration.

**Total Instances:** 34

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 225:         for (uint256 i = 0; i < _calls.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 116:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

 135:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

 185:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

 209:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 142:         for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

 257:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

 289:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

 311:         for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {

 351:         for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {

 405:         for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {

 580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

 636:         for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {

 667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

 208:         for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 101:         for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {

 138:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

 158:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

 178:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

 29:         for (uint256 i; i < pathLength; i = i.uncheckedInc()) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L29

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226

```solidity
File: system-contracts/contracts/Compressor.sol

 61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {

 127:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

 159:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L61

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 248:         for (uint256 i = 0; i < deploymentsLength; ++i) {

 253:         for (uint256 i = 0; i < deploymentsLength; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L248

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol

 38:             for (uint256 i = 0; i < immutablesLength; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L38

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

 30:             for (uint256 i = 0; i < hashesLen; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L30

```solidity
File: system-contracts/contracts/L1Messenger.sol

 206:         for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

 218:         for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {

 224:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

 236:         for (uint256 i = 0; i < numberOfMessages; ++i) {

 254:         for (uint256 i = 0; i < numberOfBytecodes; ++i) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L206

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol

 36:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36


## [GAS-50] Using globals directly is cheaper than assigning them to variables
Using the global directly saves 5 gas

**Total Instances:** 1

**Gas per instance:** 5
**Total Gas saved:** 5

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 329:         uint256 value = msg.value;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L329


## [GAS-51] Newer versions of solidity are more gas efficient
The solidity language continues to pursue more efficient gas optimization schemes. Adopting a newer version of solidity can be more gas efficient. 

**Total Instances:** 1

```solidity
File: contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol

 2: pragma solidity ^0.8.0;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L2


## [GAS-52] Use a more recent version of solidity
- Use a solidity version of at least 0.8.2 to get compiler automatic inlining \n - Use a solidity version of at least 0.8.3 to get better struct packing and cheaper multiple storage reads. \n - Use a solidity version of at least 0.8.4 to get custom errors, which are cheaper at deployment than `revert()/require()` strings. \n - Use a solidity version of at least 0.8.10 to have external calls skip contract existence checks if the external call has a return value.

**Total Instances:** 1

```solidity
File: contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol

 2: pragma solidity ^0.8.0;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/l2-deps/ISystemContext.sol#L2


## [GAS-53] Use storage instead of memory for structs/arrays
When fetching data from a storage location, assigning the data to a memory variable causes all fields of the struct/array to be read from storage, which incurs a Gcoldsload (2100 gas) for each field of the struct/array. If the fields are read from the new memory variable, they incur an additional MLOAD rather than a cheap stack read. Instead of declaring the variable with the memory keyword, declaring the variable with the storage keyword and caching any fields that need to be re-read in stack variables, will be much cheaper, only incurring the Gcoldsload for the fields actually read. The only time it makes sense to read the whole struct/array into a memory variable, is if the full struct/array is being returned by the function, is being passed to a function that requires memory, or if the array/struct is being read from another memory array/struct.

**Total Instances:** 2

**Gas per instance:** 4200
**Total Gas saved:** 8400

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 41:         AccountInfo memory info = accountInfo[_address];

 75:         AccountInfo memory currentInfo = accountInfo[msg.sender];

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L75


## [GAS-54] Use unchecked block for safe subtractions
If it can be confirmed that the subtraction operation will not overflow, using an unchecked block can save gas. For example, require(x <= y); z = y - x; can be optimized to require(x <= y); unchecked { z = y - x; }.

**Total Instances:** 15

**Gas per instance:** 85
**Total Gas saved:** 1275

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 /// @audit  checked on line 121
 132:             require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");

 /// @audit  checked on line 121
 178:         return balanceAfter - balanceBefore;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

 /// @audit  checked on line 115
 118:             txBodyGasLimit = _totalGasLimit - overhead;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L118

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 /// @audit  checked on line 239
 243:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L243

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

 /// @audit  checked on line 24
 28:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L28

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol

 /// @audit  checked on line 92
 193:             vEncoded = RLPEncoder.encodeUint256(vInt - 27);

 /// @audit  checked on line 191
 193:             vEncoded = RLPEncoder.encodeUint256(vInt - 27);

 /// @audit  checked on line 92
 288:             vEncoded = RLPEncoder.encodeUint256(vInt - 27);

 /// @audit  checked on line 191
 288:             vEncoded = RLPEncoder.encodeUint256(vInt - 27);

 /// @audit  checked on line 286
 288:             vEncoded = RLPEncoder.encodeUint256(vInt - 27);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L193

```solidity
File: system-contracts/contracts/GasBoundCaller.sol

 /// @audit  checked on line 49
 49:         uint256 pubdataAllowance = _maxTotalGas > expectedForCompute ? _maxTotalGas - expectedForCompute : 0;

 /// @audit  checked on line 63
 64:             ? pubdataPublishedAfter - pubdataPublishedBefore

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L49

```solidity
File: system-contracts/contracts/L2BaseToken.sol

 /// @audit  checked on line 41
 43:             balance[_from] = fromBalance - _amount;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L43

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol

 /// @audit  checked on line 53
 54:             ? gasInContext - MSG_VALUE_SIMULATOR_STIPEND_GAS

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L54

```solidity
File: system-contracts/contracts/SystemContext.sol

 /// @audit  checked on line 119
 119:         return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L119


## [GAS-55] `internal` functions not called by the contract should be removed
If the functions are required by an interface, the contract should inherit from that interface and use the `override` keyword

**Total Instances:** 28

```solidity
File: contracts/ethereum/contracts/common/libraries/UncheckedMath.sol

 11:     function uncheckedInc(uint256 _number) internal pure returns (uint256) {

 17:     function uncheckedAdd(uint256 _lhs, uint256 _rhs) internal pure returns (uint256) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L11

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/LibMap.sol

 18:     function get(Uint32Map storage _map, uint256 _index) internal view returns (uint32 result) {

 38:     function set(Uint32Map storage _map, uint256 _index, uint32 _value) internal {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L18

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

 18:     function calculateRoot(

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L18

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol

 35:     function getFirstUnprocessedPriorityTx(Queue storage _queue) internal view returns (uint256) {

 40:     function getTotalPriorityTxs(Queue storage _queue) internal view returns (uint256) {

 45:     function getSize(Queue storage _queue) internal view returns (uint256) {

 50:     function isEmpty(Queue storage _queue) internal view returns (bool) {

 55:     function pushBack(Queue storage _queue, PriorityOperation memory _operation) internal {

 64:     function front(Queue storage _queue) internal view returns (PriorityOperation memory) {

 72:     function popFront(Queue storage _queue) internal returns (PriorityOperation memory priorityOperation) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L35

```solidity
File: system-contracts/contracts/libraries/EfficientCall.sol

 88:     function delegateCall(

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L88

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol

 124:     function packPrecompileParams(

 181:     function eventInitialize(uint256 initializer, uint256 value1) internal {

 191:     function eventWrite(uint256 value1, uint256 value2) internal {

 307:     function getCalldataPtr() internal view returns (uint256 ptr) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L124

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 94:     function isEthToken(uint256 _addr) internal pure returns (bool) {

 100:     function encodeHash(Transaction calldata _transaction) internal view returns (bytes32 resultHash) {

 362:     function processPaymasterInput(Transaction calldata _transaction) internal {

 395:     function payToTheBootloader(Transaction calldata _transaction) internal returns (bool success) {

 405:     function totalRequiredBalance(Transaction calldata _transaction) internal pure returns (uint256 requiredBalance) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L94

```solidity
File: system-contracts/contracts/libraries/UnsafeBytesCalldata.sol

 19:     function readUint16(bytes calldata _bytes, uint256 _start) internal pure returns (uint16 result) {

 26:     function readUint32(bytes calldata _bytes, uint256 _start) internal pure returns (uint32 result) {

 33:     function readUint64(bytes calldata _bytes, uint256 _start) internal pure returns (uint64 result) {

 40:     function readBytes32(bytes calldata _bytes, uint256 _start) internal pure returns (bytes32 result) {

 46:     function readUint256(bytes calldata _bytes, uint256 _start) internal pure returns (uint256 result) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L19

```solidity
File: system-contracts/contracts/libraries/Utils.sol

 32:     function safeCastToU24(uint256 _x) internal pure returns (uint24) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L32


## [GAS-56] Use assembly to write address/contract type storage values
Using `assembly { sstore(state.slot, addr) instead of state = addr` can save gas.

**Total Instances:** 15

**Gas per instance:** 50
**Total Gas saved:** 750

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 96:         l1WethAddress = _l1WethAddress;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L96

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 55:         pendingAdmin = _newPendingAdmin;

 65:         admin = currentPendingAdmin;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 46:         securityCouncil = _securityCouncil;

 258:         securityCouncil = _newSecurityCouncil;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L46

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 59:         bridgehub = _bridgehub;

 85:         genesisUpgrade = _initializeData.genesisUpgrade;

 87:         validatorTimelock = _initializeData.validatorTimelock;

 114:         pendingAdmin = _newPendingAdmin;

 124:         admin = currentPendingAdmin;

 133:         validatorTimelock = _validatorTimelock;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L59

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 60:         l1Bridge = _l1Bridge;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L60

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 52:         l1Address = _l1Address;

 54:         l2Bridge = msg.sender;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L52

```solidity
File: system-contracts/contracts/SystemContext.sol

 100:         origin = _newOrigin;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L100


## [GAS-57] Use assembly to emit events
To efficiently emit events, it’s possible to utilize assembly by making use of [scratch space](https://github.com/Vectorized/solady/blob/30558f5402f02351b96eeb6eaf32bcea29773841/src/tokens/ERC1155.sol#L501-L504) in order to save gas. This approach has the advantage of potentially avoiding the costs associated with memory expansion. However, it’s important to note that in order to safely optimize this process, it is preferable to cache and restore the free memory pointer.

**Total Instances:** 46

**Gas per instance:** 38
**Total Gas saved:** 1748

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 56:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

 68:         emit NewPendingAdmin(currentPendingAdmin, address(0));

 69:         emit NewAdmin(previousAdmin, pendingAdmin);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L56

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 47:         emit ChangeSecurityCouncil(address(0), _securityCouncil);

 50:         emit ChangeMinDelay(0, _minDelay);

 144:         emit ShadowOperationScheduled(_id, _delay);

 157:         emit OperationCancelled(_id);

 180:         emit OperationExecuted(id);

 199:         emit OperationExecuted(id);

 250:         emit ChangeMinDelay(minDelay, _newDelay);

 257:         emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L47

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 115:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

 127:         emit NewPendingAdmin(currentPendingAdmin, address(0));

 128:         emit NewAdmin(previousAdmin, pendingAdmin);

 235:         emit StateTransitionNewChain(_chainId, _stateTransitionContract);

 287:         emit StateTransitionNewChain(_chainId, stateTransitionAddress);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L115

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

 83:         emit ValidatorAdded(_chainId, _newValidator);

 92:         emit ValidatorRemoved(_chainId, _validator);

 98:         emit NewExecutionDelay(_executionDelay);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L83

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 28:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);

 40:         emit NewPendingAdmin(pendingAdmin, address(0));

 41:         emit NewAdmin(previousAdmin, pendingAdmin);

 47:         emit ValidatorStatusUpdate(_validator, _active);

 54:         emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);

 63:         emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);

 75:         emit NewFeeParams(oldFeeParams, _newFeeParams);

 92:         emit ValidiumModeStatusUpdate(_validiumMode);

 115:         emit ExecuteUpgrade(_diamondCut);

 125:         emit ExecuteUpgrade(_diamondCut);

 139:         emit Freeze();

 149:         emit Unfreeze();

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L28

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 436:         emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L436

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 104:         emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);

 121:         emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);

 137:         emit NewVerifier(address(oldVerifier), address(_newVerifier));

 157:         emit NewVerifierParams(oldVerifierParams, _newVerifierParams);

 256:         emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L104

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

 40:         emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L40

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 147:         emit BridgeMint(_to, _amount);

 156:         emit BridgeBurn(_from, _amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L147

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 68:         emit AccountVersionUpdated(msg.sender, _version);

 86:         emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L68

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

 59:             emit MarkedAsKnown(_bytecodeHash, _shouldSendToL1);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L59

```solidity
File: system-contracts/contracts/L1Messenger.sol

 111:         emit L2ToL1LogSent(_l2ToL1Log);

 181:         emit BytecodeL1PublicationRequested(_bytecodeHash);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L111

```solidity
File: system-contracts/contracts/L2BaseToken.sol

 67:         emit Mint(_account, _amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L67


## [GAS-58] Use assembly to compute hashes to save gas
If the arguments to the encode call can fit into the scratch space (two words or fewer), then it’s more efficient to use assembly to generate the hash (80 gas): keccak256(abi.encodePacked(x, y)) -> assembly {mstore(0x00, a); mstore(0x20, b); let hash := keccak256(0x00, 0x40); }

**Total Instances:** 38

**Gas per instance:** 80
**Total Gas saved:** 3040

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 76:         bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76

```solidity
File: contracts/ethereum/contracts/common/Config.sol

 112: bytes32 constant TWO_BRIDGES_MAGIC_VALUE = bytes32(uint256(keccak256("TWO_BRIDGES_MAGIC_VALUE")) - 1);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L112

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

 12:     bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L12

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 205:         return keccak256(abi.encode(_operation));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L205

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 100:         storedBatchZero = keccak256(abi.encode(batchZero));

 102:         initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));

 138:         initialCutHash = keccak256(abi.encode(_diamondCut));

 147:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

 156:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));

 255:         bytes32 cutHashInput = keccak256(_diamondCut);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 104:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 63:                     keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),

 313:             concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));

 506:         bytes32 passThroughDataHash = keccak256(_batchPassThroughData(_newBatchData));

 507:         bytes32 metadataHash = keccak256(_batchMetaParameters());

 545:         bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs);

 588:         return keccak256(abi.encode(_storedBatchInfo));

 654:             blobCommitments[versionedHashIndex] = keccak256(
                     abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L63

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 212:         bytes32 l2ProtocolUpgradeTxHash = keccak256(encodedTransaction);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L212

```solidity
File: contracts/zksync/contracts/L2ContractHelper.sol

 85:     bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/L2ContractHelper.sol#L85

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 150:         bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol

 29:             txHash = keccak256(bytes.concat(signedTxHash, EfficientCall.keccak(_transaction.signature)));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L29

```solidity
File: system-contracts/contracts/L1Messenger.sol

 89:         uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) + 2 * keccakGasCost(64);

 106:         chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));

 122:         chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));

 164:         chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));

 212:             reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));

 225:                 l2ToL1LogsTreeArray[i] = keccak256(
                         abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])

 243:             reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));

 259:             reconstructedChainedL1BytecodesRevealDataHash = keccak256(
                     abi.encode(

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L1Messenger.sol#L89

```solidity
File: system-contracts/contracts/SystemContext.sol

 159:             hash = keccak256(abi.encode(_block));

 234:         return keccak256(abi.encodePacked(uint32(_blockNumber)));

 403:         currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L159

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 82:     bytes32 constant EIP712_DOMAIN_TYPEHASH = keccak256("EIP712Domain(string name,string version,uint256 chainId)");

 85:         keccak256(
                "Transaction(uint256 txType,uint256 from,uint256 to,uint256 gasLimit,uint256 gasPerPubdataByteLimit,uint256 maxFeePerGas,uint256 maxPriorityFeePerGas,uint256 paymaster,uint256 nonce,uint256 value,bytes data,bytes32[] factoryDeps,bytes paymasterInput)"

 133:                 keccak256(abi.encodePacked(_transaction.factoryDeps)),

 139:             abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

 139:             abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139


## [GAS-59] Using assembly to check for zero can save gas
Using assembly to check for zero can save gas by allowing more direct access to the evm and reducing some of the overhead associated with high-level operations in solidity.

**Total Instances:** 89

**Gas per instance:** 6
**Total Gas saved:** 534

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 141:         require(_amount != 0, "0T"); // empty deposit

 186:         require(amount != 0, "2T"); // empty deposit

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 108:         require(_owner != address(0), "ShB owner 0");

 158:             require(msg.value == 0, "ShB m.v > 0 b d.it");

 188:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");

 200:             require(_depositAmount == 0, "ShB wrong withdraw amount");

 202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");

 208:         require(amount != 0, "6T"); // empty deposit amount

 563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");

 578:             if (_refundRecipient == address(0)) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L108

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol

 122:         require(_chainId != 0, "Bridgehub: chainId cannot be 0");

 130:         require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");

 132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

 225:                 require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");

 326:         if (_refundRecipient == address(0)) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L122

```solidity
File: contracts/ethereum/contracts/common/ReentrancyGuard.sol

 58:         require(lockSlotOldValue == 0, "1B");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L58

```solidity
File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol

 23:         require(_bytecode.length % 32 == 0, "pq");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol

 42:         require(_admin != address(0), "Admin should be non zero address");

 107:         if (timestamp == 0) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L42

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

 82:         require(_initializeData.governor != address(0), "StateTransition: governor zero");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L82

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

 25:         require(address(_initializeData.verifier) != address(0), "vt");

 26:         require(_initializeData.admin != address(0), "vy");

 27:         require(_initializeData.validatorTimelock != address(0), "hc");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

 25:         require(msg.data.length >= 4 || msg.data.length == 0, "Ut");

 30:         require(facetAddress != address(0), "F"); // Proxy has no facet for this selector

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

 90:         require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

 237:         if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {

 284:         require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");

 291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);

 361:         if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {

 633:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L237

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

 169:         if (selectorsArrayLen != 0) {

 183:         require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L169

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

 141:             require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists

 161:             require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

 175:         require(_facet == address(0), "a1"); // facet address must be zero

 181:             require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet

 194:         if (selectorsLength == 0) {

 213:         if (selectorPosition != 0) {

 250:         if (lastSelectorPosition == 0) {

 279:         if (_init == address(0)) {

 280:             require(_calldata.length == 0, "H"); // Non-empty calldata for zero address

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L141

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol

 30:             currentHash = (_index % 2 == 0)

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L30

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

 50:         require(_transaction.paymaster == 0, "uc");

 51:         require(_transaction.value == 0, "ud");

 52:         require(_transaction.maxFeePerGas == 0, "uq");

 53:         require(_transaction.maxPriorityFeePerGas == 0, "ux");

 54:         require(_transaction.reserved[0] == 0, "ue");

 56:         require(_transaction.reserved[2] == 0, "ug");

 57:         require(_transaction.reserved[3] == 0, "uo");

 58:         require(_transaction.signature.length == 0, "uh");

 59:         require(_transaction.paymasterInput.length == 0, "ul1");

 60:         require(_transaction.reservedDynamic.length == 0, "um");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L50

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

 186:         if (_l2ProtocolUpgradeTx.txType == 0) {

 251:             s.l2SystemContractsUpgradeBatchNumber == 0,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L186

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

 35:             s.l2SystemContractsUpgradeBatchNumber == 0,

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L35

```solidity
File: contracts/zksync/contracts/SystemContractsCaller.sol

 59:         if (value == 0) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/SystemContractsCaller.sol#L59

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol

 55:         require(_l1Bridge != address(0), "bf");

 57:         require(_aliasedOwner != address(0), "sf");

 68:             require(_l1LegecyBridge != address(0), "bf2");

 92:         require(msg.value == 0, "Value should be 0 for ERC20 bridge");

 129:         require(l1Token != address(0), "yh");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L55

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol

 51:         require(_l1Address != address(0), "in6"); // Should be non-zero address

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol

 96:             if (_transaction.reserved[0] != 0) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/BootloaderUtilities.sol#L96

```solidity
File: system-contracts/contracts/Compressor.sol

 130:             if (enumIndex != 0) {

 146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

 162:             if (enumIndex == 0) {

 177:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;

 229:             if (_operation == 0 || _operation == 3) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L130

```solidity
File: system-contracts/contracts/ContractDeployer.sol

 49:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getRawCodeHash(_address) == 0

 350:             require(value == 0, "The value must be zero if we do not call the constructor");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L49

```solidity
File: system-contracts/contracts/DefaultAccount.sol

 188:         return recoveredAddress == address(this) && recoveredAddress != address(0);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L188

```solidity
File: system-contracts/contracts/GasBoundCaller.sol

 73:         if (pubdataCost != 0) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/GasBoundCaller.sol#L73

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol

 47:         if (getMarker(_bytecodeHash) == 0) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L47

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol

 30:         isSystemCall = (mask & MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT) != 0;

 62:         if (value != 0) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/MsgValueSimulator.sol#L30

```solidity
File: system-contracts/contracts/NonceHolder.sol

 85:         require(_value != 0, "Nonce value cannot be set to 0");

 88:         if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L85

```solidity
File: system-contracts/contracts/SystemContext.sol

 360:         if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {

 360:         if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {

 373:             require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L360

```solidity
File: system-contracts/contracts/libraries/EfficientCall.sol

 131:         if (_value == 0) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L131

```solidity
File: system-contracts/contracts/libraries/RLPEncoder.sol

 29:                 encoded[0] = (_val == 0) ? bytes1(uint8(128)) : bytes1(uint8(_val));

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/RLPEncoder.sol#L29

```solidity
File: system-contracts/contracts/libraries/SystemContractHelper.sol

 332:         return (callFlags & 2) != 0;

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L332

```solidity
File: system-contracts/contracts/libraries/SystemContractsCaller.sol

 98:         if (value == 0) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L98

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol

 95:         return _addr == uint256(uint160(address(BASE_TOKEN_SYSTEM_CONTRACT))) || _addr == 0;

 184:         if (_transaction.reserved[0] != 0) {

 406:         if (address(uint160(_transaction.paymaster)) != address(0)) {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L95

```solidity
File: system-contracts/contracts/libraries/Utils.sol

 84:         require(_bytecode.length % 32 == 0, "po");

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/Utils.sol#L84


## [GAS-60] Amounts should be checked for 0 before calling a transfer
It is generally a good practice to check for zero values before making any transfers in smart contract functions. This can help to avoid unnecessary external calls and can save gas costs. Checking for zero values is especially important when transferring tokens or ether, as sending these assets to an address with a zero value will result in the loss of those assets.

**Total Instances:** 5

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

 67:         IERC20(_token).safeTransfer(address(sharedBridge), amount);

 162:         _token.safeTransferFrom(_from, address(sharedBridge), _amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L67

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

 175:         _token.safeTransferFrom(_from, address(this), _amount);

 362:             IERC20(_l1Token).safeTransfer(_depositSender, _amount);

 452:             IERC20(l1Token).safeTransfer(l1Receiver, amount);

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L452

